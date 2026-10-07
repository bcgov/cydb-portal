```mermaid
flowchart TD
    email[Bulk email service]
    start([Start])
    user(User)
    portal[CYDB portal]
    middle[Social middleware framework]
    portalProxy[OCIO-APS]
    idBroker[OIDC Provider]
    icm[ICM REST framework]
    forms[Embedded online forms solution]

start-->user

user-->portalProxy
portalProxy-->portal

portal-->middle
portal<-->idBroker
portal<-->forms

middle-->email
middle<-->idBroker
middle-->icm

email-->user

subgraph mcsGold["MCS-Gold"]
    style mcsGold fill:#8B720E
    portalProxy
    idBroker
    portal
    middle
end

subgraph mcsEmerald["MCS-Emerald"]
    style mcsEmerald fill:#00803C
    icm
end
```

Additional information:

- **MCS-Gold**: Managed Container Services - Private Cloud Gold Tier
- **MCS-Emerald**: Managed Container Services - Private Cloud Emerald Tier
- [ICM REST framework](https://dev.azure.com/bc-icm/SiebelCRM%20Lab/_wiki/wikis/SiebelCRM-Lab.wiki/575/Siebel-Application-Client-ID-(Service-Account)-Operation-for-DATA-API)
- [Social middleware framework - GitHub repo](https://github.com/bcgov/social-middleware)