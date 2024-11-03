# Introduction to global anycast using OpenBSD (on a budget)

Presented by Rob Keizer

If you take one thing away from this talk...There are many other operating systems besides Linux.

## Anycast primer

- Multiple servers
- Multiple locations
- Multiple ISPs
- The same IP addresses
- Why?
    - Lowering latency
    - Load distribution
    - DoS mitigation (single D)
- No control over inbound traffic

- Why I cared...
    - Single point of failure is administrative in nature
    - Volumetric denial of service attacks should be (relatively) geographically bounded.
    - DDoS mitigations require scaling up the resources, but don't require massive architecture changes.

- Any individual PoP will likely go down
- So have multiple PoPs
    - You own the hardware
    - Full control
    - Generally fixed/known costs
    - You rent the resources
    - Small/no setup time
    - Usage based billing
    - Easy to get started

- Who do I talk to?
    - bgp.services (211 providers listed...)
    - datapacker.com (CDN77)
    - vultr.com
    - openbsd.amsertdam
    - anexia.com
    - neptunenetworks.org
    - coloclue.net

- How can I do it?
    - Advertise BGP (Border Gate Patrol)
    - Do that from multiple places

- Some details not covered in this talk
    - RPKI and IRR
    - Bogons
    - Communities
    - Prefix limits

- External Networking - pf.conf(5)

- Internal Networking - VPN/Routing
    - Do you need it? Comes down to state
    - tailscale / headscale / wg
        - Tailscale proper
        - Headscale
        - Distribute the public keys and IPs yourself

- Internal Networking - pfsync(4)
    - Protocol and daemons to sync firewall state
    - Do you need it?
    - Option to multicast to other nodes
    - Use the defer option to attempt to ensure sync

- External Networking - note about BGP speakers
    - Transit connections will likely hand you a /30 or /29 of ipv4 space
    - Can point traffic at another host on the same network

- Elixir
    - In packages (pkg_add elixir)
    - Functional, concurrent, high-level general-purpose
    - Runs on the BEAM
    - Processes and message passing
    - Known for Phoenix: MVC framework supporting http and websocket
    - Generally used for real-time systems

- Preemptive questions
    - Doesn't anycast not work for TCP? It works fine, within certain bounds
    - What happens to a TCP session when routes change? It resets
    - Why bother to do this? I'm sorry I failed; See previous slide around latency and scale
    - How does this relate to security? See denial of service notes in previous slide
