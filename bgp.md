# BGP

[BGP Path Attributes - IANA](https://www.iana.org/assignments/bgp-parameters/bgp-parameters.xhtml#bgp-parameters-2)

## RFCs

### BGP Protocol
- [RFC1771](https://www.rfc-editor.org/rfc/rfc1771) - A Border Gateway Protocol 4 - the original!
- [RFC1997](https://www.rfc-editor.org/rfc/rfc1997) - BGP Communities Attribute
- [RFC4271](https://www.rfc-editor.org/rfc/rfc4271) - A Border Gateway Protocol 4 - current - obsoletes RFC1771
- [RFC7196](https://www.rfc-editor.org/rfc/rfc7196) - Making Route Flap Damping Usable
- [RFC7606](https://www.rfc-editor.org/rfc/rfc7606) - Revised Error Handling for BGP UPDATE Messages
- [RFC8642](https://www.rfc-editor.org/rfc/rfc8642) - Policy Behavior for Well-Known BGP Communities
- [RFC8092](https://www.rfc-editor.org/rfc/rfc8092) - BGP Large Communities Attribute
- [RFC8212](https://www.rfc-editor.org/rfc/rfc8212.html) - Default External BGP (EBGP) Route Propagation Behavior without Policies

### BGP Security

- [RFC2385](https://www.rfc-editor.org/rfc/rfc2385) - Protection of BGP Sessions via the TCP MD5 Signature Option
- [RFC3704](https://www.rfc-editor.org/rfc/rfc3704) - Ingress Filtering for Multihomed Networks
- [RFC4272](https://www.rfc-editor.org/rfc/rfc4272) - BGP Security Vulnerabilities Analysis
- [RFC5082](https://www.rfc-editor.org/rfc/rfc5082) - The Generalized TTL Security Mechanism (GTSM)
- [RFC5925](https://www.rfc-editor.org/rfc/rfc5925) - The TCP Authentication Option - obsoletes RFC2385
- [RFC6192](https://www.rfc-editor.org/rfc/rfc6192) - Protecting the Router Control Plane
- [RFC6952](https://www.rfc-editor.org/rfc/rfc6952) - Analysis of BGP, LDP, PCEP, and MSDP Issues...
- [RFC7454](https://www.rfc-editor.org/rfc/rfc7454) - BGP Operations and Security

### BGP Data
- [RFC6396](https://www.rfc-editor.org/rfc/rfc6396) - Multi-Threaded Routing Toolkit (MRT) Routing Information Export Format

## Filtering

### Prefix Filtering
- Not as scalable as AS path filtering
- Scripts/Tools
  - level3 filtergen - change RIR and ASN as appropriate to query:
    - `whois -h filtergen.level3.net -- "RIPE::AS3333"`
    - `whois -h filtergen.level3.net -- "RIPE::AS-RIPENCC -v6"`
    - `whois -h filtergen.level3.net -- "RIPE::AS3333 -v6"`
  - [bgpq3](https://github.com/snar/bgpq3)
    - Generate JunOS: `bgpq3 -S RIPE -Jl PFX_LIST_NAME AS3333`
    - Default Cisco: `bgpq3 -S RIPE -l PFX_LIST_NAME AS3333`
    - IPv6 Aggregated, Routes up to /128 from as-set: `bgpq3 -l PFX_LIST_NAME -6 -A -R 128 AS-RIPENCC`
  - [bgpq4](https://github.com/bgp/bgpq4)
  - [IRR Toolset](https://github.com/irrtoolset/irrtoolset)
  - [IRR Power Tools](https://github.com/6connect/irrpt)
  - peval
- https://www.iana.org/assignments/iana-ipv4-special-registry/iana-ipv4-special-registry.xhtml
- https://www.iana.org/assignments/iana-ipv6-special-registry/iana-ipv6-special-registry.xhtml

### AS Path Filtering
- AS Paths that start with an AS number not belonging to one of your peers should not be accepted (unless originated by IXP’s router server)
- [NLNOG BGP Filter Guide](https://bgpfilterguide.nlnog.net/)

### Resources and Tools
- [Routeviews](https://www.routeviews.org/routeviews/)
- [RIPE RIS](https://ris.ripe.net/docs/25_ris_live.html)
- [BGPStream](https://bgpstream.caida.org/)
- [RIPE RPKI](https://www.ripe.net/manage-ips-and-asns/resource-management/rpki/tools-and-resources)

### BGP RPKI
- General
  - https://isbgpsafeyet.com/
  - https://rpki.readthedocs.io/en/latest/
- RFCs
  - [RFC3779](https://www.rfc-editor.org/rfc/rfc3779) - X.509 Extensions for IP Addresses and AS Identifiers
  - [RFC6482](https://www.rfc-editor.org/rfc/rfc6482) - A Profile for Route Origin Authorizations (ROAs)
  - [RFC6811](https://www.rfc-editor.org/rfc/rfc6811) - BGP Prefix Origin Validation
  - [RFC8210](https://www.rfc-editor.org/rfc/rfc8210) - The Resource Public Key Infrastructure (RPKI) to Router Protocol, Version 1 
  - [RFC8481](https://www.rfc-editor.org/rfc/rfc8481) - Clarifications to BGP Origin Validation Based on RPKI
  - [RFC9319](https://www.rfc-editor.org/rfc/rfc9319) - The Use of maxLength in the RPKI
- Validators
  - [Routinator](https://routinator.docs.nlnetlabs.nl/en/stable/index.html)
  - [OctoRPKI](https://github.com/cloudflare/cfrpki)
  - [Fort](https://fortproject.net/en/validator)
  - [rpki-client](https://fortproject.net/en/validator)

### Other
- Filter prefixes with two Tier 1 ASNs in path
- https://bgpfilterguide.nlnog.net/
- Prefix filtering not as scalable as AS path filtering
- https://github.com/TCP-AO/Configuration-examples/blob/master/JuniperNetworks.md

### IX Peering
- IXPs should announce their LAN prefix to all of their member ASes and members should accept this prefix.
- As an IXP member, you should not accept more specific prefixes for the IXP LAN prefix from any external BGP peers, as this may create a black hole for IXP LAN connectivity. 
- If the IXP-LAN prefix is accepted, then It should only be accepted from the ASes that are authorised to announce by the IXP.

### Reading
- https://labs.ripe.net/author/florian_streibelt/bgp-communities-a-weapon-for-the-internet-part-1/
- https://www.potaroo.net/ispcol/2022-12/securedrouting.html

