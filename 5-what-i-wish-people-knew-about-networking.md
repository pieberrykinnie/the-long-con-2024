# What I Wish People Knew About Networking

Presented by Adam Thompson

## How networking actually works

- Hanlon's Razor
    - "Never attribute to malice that which is adequately explained by stupidity"
    - "Cock-ups, not conspiracies"
- Con't:
    - Stop believing that EVERYTHING is an attack
    - ALMOST everything that COULD be an attack, is actually an accident, a mistake, or a screw-up, of some sort.
    - Assuming there's an attacker hiding behind every door leads to inefficient, needlessly-expensive networking and system design
- It's just Math and Boolean Logic
    - Binary math and binary logic
- Failures/Attacks
    - 99.99% Human error
        - You don't attack math; almost always somebody messed up
        - Failing circuits
    - Exploiting known errors in circuit implementations
        - Pentium DIV bug
        - MMU bugs
        - How does the attacker get to the electrical signals? Insanely hard
    - Mostout out of scope
- Organization: Layering & Encapsulation
    - Very strongly organized into layers
    - "Layering violation": it works, but it's not right
    - The OSI stack is hugely problematic and mostly obsolete
- OSI stack (bottom 4 layers)
    - Physical Layer
    - Data Link Layer
    - Network Layer
    - Transport
- Security relationship: Most firewalls will emncompass layer 2 domains, which encompass L3, which encompass L4

## Layers

- Layering attacks do not exist; network-centric attacks focus on layer boundaries
- Layer 1 - Physical:
    - Copper:
        - Never assume cable or patch cord "must" be OK, even if it's freshly installed
        - Cause: Stretching, folding...
        - Effect: Silent retries
        - Detection: Interface statistics
        - Fix: Only use BICSI- or AMP- certified cables and installers. Use patch cords
        - Faults & Attacks: 100% of every copper problem, ever, was a fault, not an attack; Physical security is the solution
        - Hanlon's Razor: It's always a fault in the copper
    - Fiber
    - Radio (Wi-Fi)
        - Vulnerable to DoS, otherwise eh (and comes with measures for lower layers)
- Layer 2 - Data Link
    - No such thing as an MTU attack, some routers/servers may still be vulnerable to fragmentation attacks
- VLAN hopping attacks don't exist
