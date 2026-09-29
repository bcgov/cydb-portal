```mermaid
flowchart TD
    start([Start])
    user(User)
    portal[CYDB portal]
    middle[Social middleware]
    idBroker[OCIO-SSO]
    portalProxy[OCIO-APS]
    socialProxy[OCIO-APS]
    icm[ICM REST framework]
    forms[Embedded online forms solution]
    email[Bulk email service]

start-->user
user-->portalProxy
portalProxy-->portal

portal-->socialProxy
portal<-->idBroker
portal<-->forms

middle-->email
email-->user

socialProxy<-->idBroker
socialProxy-->middle

middle-->icm

subgraph mcsGold["MCS-Gold"]
    style mcsGold fill:#8B720E
    portalProxy
    socialProxy
    idBroker
    portal
    middle
end

subgraph mcsEmerald["MCS-Emerald"]
    style mcsEmerald fill:#00803C
    icm
end
```