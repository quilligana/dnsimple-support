---
title: DNSSEC, DS records, and SERVFAIL
excerpt: A common error that occurs with DNSSEC is when a DS record is present in parent DNS servers without a corresponding DNSSEC DNSKEY in the authoritative name servers. This article covers how to address this issue.
catagories:
- DNS
---

# DNSSEC, DS records, and SERVFAIL

DNSSEC works by creating a chain of trust from the DNS root through to the authoritative name server for a domain. This chain is created by linking DS records in parent name servers to DNSKEY records in child name servers. If a DS record is present without a DNSKEY, then a DNS resolver that verifies DNSSEC will fail, typically with a SERVFAIL error.

To remove the SERVFAIL, either add the appropriate DNSKEY to the child name servers, or remove the DS record from the parent name servers.

## Domain Transfers for signed zones

A common pitfall when transferring a domain with DNSSEC enabled, especially when the transfer is accompanied by a DNS delegation change, is that the DS record will remain attached to the domain in the registry name servers, but the DNSKEY will not exist in the new name servers. If you are planning on changing the DNS delegation while transferring a domain, you should handle the change of the zone before executing the transfer. This means that if the zone is currently signed, you will need to sign it in the new DNS system, add the corresponding DS record to the zone at the current domain registrar.
