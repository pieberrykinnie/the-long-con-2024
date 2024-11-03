# Let's talk IoT: Internet of Terrible

Presented by William

## How IoT works

- IoT: Devices connected to the internet
- Example: Belkin Wemo
    - First real popular consumer IoT device
    - It was terrible, took 2 years later for firmware to update and work
    - One of the first smart plugs to hit the market
    - Had basically a router inside it
- 20 years later: ESP line chips
    - Ability to connect things to the internet with a 25 cents chip
    - General purpose computers being used for IoT, now have specifically designed devices for IoT
- Government of Manitoba had a program for people to buy surveillance camera
- But IoT is kind of a mess on the security side

## The problem

- What happens when companies stop supporting products?
    - Case study: Best Buy pulling the plug on Insignia, Hub6 Safe
    - You have no guarantee from any of these companies that they would keep supporting
    - Bunch of e-waste in people's home
- Managed to reverse engineer Hub6 Safe and make usable firmware in 2 days
- If you're a software engineer, you're probably better than 50% of IoT product makers

## Dissecting an IoT product

- Linda Wang left behind a buncha things on Toshiba IK-WB02A
- Reverse Engineering:
    - Binwalk: Find a firmware update file and just throw it on binwalk and you'll get the file system
    - D-Link VTA Telephone Adapter: subsidized small computer from 10 years ago ($9.99)
    - Chips usually have a serial port you can buy an adapater to connect to and watch its processes run

## The Terrible in IoT

- Shipping hardware without further support: no guarantee that device will stay working
- Prices are shipped with one update at best, security vulnerabilities get worse as time goes by
- Cameras actually scan QR code to set up, if you scan it it's just `json`: this means you can inject malicious scripts into any random camera
- There are backdoors in many things because they come with default passwords
- In short: be careful with what you're doing with these products, if you're looking at no-name products, take the Internet out of it, if you *need* a camera, wire it

## Q&A

- IoT bad?
    - Generalization; Amazon and Google follow best practices, but for budget options you get what you pay for - if you aren't IT savvy stick to named products
- If I want to get into firmware, do I need to be expert in network/security?
    - It's not that hard because many things are templated, depends on the product - just gotta be competent enough to put the Lego together
- Regarding the e-waste problem?
    - When you have these products shipped out, how long will the backend be available? Beneficial if we have devices with standards behind them, but no guarantee; when we buy these, we don't know how long they're gonna work
