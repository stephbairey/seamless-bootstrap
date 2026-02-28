# Operator Note: Gmail Send-As Configuration
**Date:** February 27, 2026

All of these addresses are configured as "Send mail as" identities in the stephbairey@gmail.com Gmail account. Maya sends from all of them depending on context. The stephbairey@gmail.com account is the hub — all sending happens through Gmail regardless of the from-address.

## Send-As Identities

| From Address | Display Name | Mail Server | Notes |
|---|---|---|---|
| stephbairey@gmail.com | Steph Bairey | Gmail (default) | Default sending address. Reply-to: stephbairey@gmail.com |
| arc@tomahawkdestiny.com | ARC | mail.tomahawkdestiny.com (SSL 465) | ARC organizational identity |
| doorknobs@lynnahaller.com | Maya Bairey | mail.lynnahaller.com (SSL 465) | |
| grannynewsletter@gmail.com | PRG Newsletter | Gmail | PRG newsletter distribution |
| info@linguaink.com | Lingua Ink | dfw-s07.nixihost.com (SSL 465) | Business identity |
| maya@bairey.com | Maya Bairey | mail.bairey.com (SSL 465) | Not an alias (separate identity) |
| maya@linguaink.com | Maya Bairey | mail.linguaink.com (SSL 465) | |
| mjbairey@gmail.com | Maya Bairey | Gmail | Reply-to: mjbairey@gmail.com |
| pdxraginggrannies@gmail.com | Portland Raging Grannies | Gmail | PRG organizational identity |
| scb.zombie@gmail.com | Steph Bairey | Gmail | Reply-to: scb.zombie@gmail.com |
| steph.bairey.arc@tomahawkdestiny.com | Steph Bairey (ARC) | mail.tomahawkdestiny.com (SSL 465) | Personal ARC identity (vs. org arc@ address) |
| steph@bairey.com | Steph Bairey | mail.bairey.com (SSL 465) | |
| steph@linguaink.com | Steph Bairey | dfw-s07.nixihost.com (SSL 465) | |
| steph@linguainkmedia.com | Steph Bairey | mail.linguainkmedia.com (SSL 465) | |
| webgranny@bairey.com | Steph Bairey | mail.bairey.com (SSL 465) | |
| webgranny@gmail.com | Steph Bairey | Gmail | |
| webmaster@tomahawkdestiny.com | Webmaster | iah-s01.nixihost.com (TLS 587) | Different mail server than other TDA addresses |

## Observations for Phase 1
- 16 send-as identities through one Gmail account — significantly more complex than the 4-address model in the audit report
- Multiple domains: gmail.com, bairey.com, linguaink.com, linguainkmedia.com, tomahawkdestiny.com, lynnahaller.com
- Three distinct mail servers: nixihost (dfw-s07, iah-s01), plus domain-specific mail servers
- Identity splits within organizations: arc@ (org) vs. steph.bairey.arc@ (personal-within-org)
- "webgranny" appears on both bairey.com and gmail.com
- maya@bairey.com is explicitly marked "Not an alias" — distinct from other send-as addresses
