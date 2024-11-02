# Abuses, Implementations, and Other Malarckey

Presented by David Dyck

## Zeroconf - Quick and "zero-configuration" advertisement and discovery of services

- Three Main Components:
    - Link-Local Addressing
    - Multicast DNS
    - DNS Service Discovery
- Who cares? Used for Spotify Connect, Chromecast, AirPlay, IOT and More

## Technology Overview

- Link-Local Addressing
    - IP Address Acquisition without DHCP or manual configuation
    - Process:
        1. Choose a random address ex. within 169.254.0.0/16
        2. Send an ARP probe (or equivalent) for the chosen address. If another machine repeats, pick different address
        3. Profit
- mDNS
    - DNS, but served over multicast by multiple hosts
    - .local TLD, as well as the reverse lookup zone
- DNS-SD
    - Naming convention and usage protocol for DNS / mDNS to provide standard way of advertising and discovering services
    - This standard isn't always followed, but the concept often is
    - `<instance>.<service>.<domain>`
        - `instance`: name of a particular instance
        - `service`: two parts, service name as defined by IANA and then the protocol, TCP or UDP, prefixed with underscore
        - `domain`: as many parts as needed to define the domain
        - Example: "`Davids Cool Minecraft Server._minecraft._tcp.local`"

## Basic Abuses of these Systems

- Address Acquisition Denial (Link-Local Addressing)
    - When victim tries to acquire IP and sends probe to see if it's taken, respond that we have it, continuously
    - For extra spice, target it at specific MAC
- IP Takeover (Link-Local Addressing)
    - Conflict resolution in link-local addressing
    - Can abuse this to kick someone off an IP
    - MS implementation is not RFC-compliant and is therefore not vulnerable
- Service Cloning (mDNS and DNS-SD)
    - Take someone else's info from mDNS and advertise the same service
- Options for Service Takeover
    1. Combine IP takeover with service cloning
    2. Just do service cloning and hope they hit your service
    3. Do service cloning but change weights and priorities
    4. Do (2) or (3) but MITM instead of full take over

## Mitigations and Detection

- Detection:
    - Link-Local Addressing Abuses - Very loud and easy to detect
    - mDNS monitoring of some form
- Mitigation:
    - ARP Protection or avoiding LL addressing
    - Use regular DNS, and always authenticate services in some way
