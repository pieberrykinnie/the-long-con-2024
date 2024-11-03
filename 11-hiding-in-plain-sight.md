# Hiding in Plain Sight: Shell Obfuscation

Presented by Mike - Red Siege Principal Consultant

Slides [here](https://redsiege.com/hiding/)

## Shellcode

- Small piece of code as the payload (basically command shell)
- Common payload now is your C2 or stage 0
- Why hide:
    - Shellcode from any well-known framework is likely signatrued (Metasploit/Cobalt Strike etc.)
    - Including signatured shellcode will likely result in detection
    - Example: 27/72 engines on VirusTotal detected the pattern shellcode
- How to hide:
    - Encode
    - Encrypt
    - Obfuscate
    - Separate shellcode from our loader

## Encryption Methods

- Old School Encryption:
    - Caesar cipher: shift alphabet (or byte values) by X bytes, subtract 0x0D at runtime
        - Only 7 engines detected
- Modern Encrytion:
    - XOR, XOR with multibyte key, AES, RC4, etc.
    - XOR is the most simple (just XOR every byte with `xor_key`)
        - Only 8 engines detected
    - XOR (Multibyte Key)
        - It's Good: 2/72 engines detected
    - AES: More secure, so should be better
        - Not so much: 8/72 (because of entropy)
        - Benefit:
            - Brute-force the last two bytes of the key for a built-in delay => Can introduce several minutes of delay without triggering sleep detection and can't be fast-forwarded
    - RC4 & SystemFunction032/023
        - `Advapi32.dll` has two undocumented functions to decrypt RC4 in memory
        - `SystemFunction032` is for encrypting
        - `SystemFunction033` is for decrypting
        - Not terrible: 7/72
    - Two Arrays: Split shellcode into two arrays - even and odd
        - Based on position in array, not byte value
        - Meh?: 8/72
    - Flip: Reverse the bytes
        - Surprisingly well: 4/72
    - Reverse the entire string?
        - Not very effective: 14/72
    - Shellcode as UUIDs
        - 128-bit label for information
        - First observed being used by Lazarus group in 2021
        - Breaking the pattern:
            - Normal shellcode loader has recognizable pattern
            - Even if shellcode isn't detected, this pattern is well-known
            - `UuidFromStringA` converts shellcode UUID string to binary and copies into memory for us
        - Unfortunately: 13/72
    - Even More Camo: Shellcode as IPv4/IPv6 address and MAC addresses
        - `RtlIpv4StringToAddressA` / `RtlIpv6StringToAddressA` / `RtlEthernetStringToAddressA`
        - 6/72
- Catch-22:
    - We encrypt shellcode so we don't get caught
    - Encryption raises entropy
    - High entropy increases chance of detection
    - How do we decrease entropy?
- Jargon:
    - Translation table array of 256 unique words
    - Position of each word in array represents a byte of shellcode
    - Works quite well: 3/72
- Jigsaw Puzzle:
    - Create new array same length of shellcode of indices
    - Shuffle the array of indices
    - Construct the payload: for each index, append the byte in said index
    - Reconstruct the payload
    - Works relatively well: 4/72
- Delta Encoding:
    - Store first byte of shellcode in a variable
    - Each subsequent byte in delta array is `current_byte - previous_byte` (use unsigned variable to ease it)
    - Much success: 2/72
- Breaking signatures:
    - Sometimes our decoding/decryption/translation routines get signatured
    - Compile as a Windows program vs exe
    - Break up the pattern by throwing in code that does something but doesn't change the result
        - Disable compiler optimization!
        - Inside your decoding/decryption/deobfuscation routine
        - `printf("");`
        - Write to null device
            - `FILE* outfile = fopen("nul", "w");`
            - `fputs("out", outfile);`
            - `fclose(outfile);`
- TL;DR:
    - Best performing methods: XOR Multibyte Key & Offset
    - Some middle techniques may work better than other
- More info
    - [Adventures in Shellcode Obfuscation blog series](https://redsiege.com/adventures-in-shellcode-obfuscation/)
    - [Code examples](https://github.com/RedSiege/Chromatophore)
- Disclosure: Just about hiding shellcode: getting shellcode into memory and executing them is harder to do

## Other Obfuscation Ideas

- Steganography
    - Encoding data in an iamge
- .NET BigInteger (Casey Smith = GOAT)
- Store shellcode in resource file
- Store shellcode in separate file
- Pull shellcode from remotely hosted location

## Q&A

- Weigh results by which engine detected the most?
    - Didn't check in details: would make different decisions depending on which agent is used
- What about combining other methods of obfuscation?
    - Absolutely could and have seen that done, didn't personally test
- Encoding in images?
    - Wouldn't do it straight in each pixel being a byte, it'd probably work because the bar to evade that isn't high, could do something like using only the red channel, generating a whole image from shellcode would be more prone to detection but doing the ghetto way would work
- Trends down the line making it more difficult to load shellcode?
    - I don't see it, it's the execution piece: people are looking at call stack, only vendor that's looking at that is Elastic but not many people use them
