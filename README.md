# aeternity-notes

## Questions to the core team

### How can we get access to the transaction hash for an oracle registration?

Increased mining block height should not be taken as a proof that an oracle has been successfully registered. The transaction could either fail or even not be mined yet due to network congestions. How I understand it, that means, that the registering account needs to keep track of the TX hash or an id to make sure, that the oracle *really* has been registered.

### Should we consider a minimum amount of mined blocks before an oracle answer is accepted to be `true`?

Would it make sense to freeze an answer to make sure, that malicious node dont broadcast false answers?

### What are the lower boundary points for the delta TTLs specifications?

Is the mining block time the starting point for the delta or the block time of the broadcasting node? It seemed to me, that sometimes I received almost instantly ttl expirations errors and sometimes the query/response pairs seemed to live even longer than expected.

### How can we make sure an oracle logic is available "forever"?

I understand that it makes sense to give a TTL to oracles, answers and questions. However since Oracles are meant to be reliable information providers which consuming smart contracts rely on, Oracles are usually meant to live forever or at least for a long amount of time. That means, that a reinitialisation would have to be scheduled before an oracle expires to make sure, that the information flow is steady. When testing we constantly received `account_is_already_an_oracle` errors and I was wondering how a zero-downtime would be possible then?

### Can we get rid of the error logging pollution, please?

It seems that every exception that is thrown during transaction processing is reposted to the `epoch.log` over and over again which makes development almost impossible after a couple of bad transactions have been produced. 

### Could transaction errors be made available via HTTP? 

Maybe instead of a file log, the errors could maybe be fetched per user via a dedicated endpoint. Informative error handling during Dapp development is very important imho and my one of the biggest fails on Ethereum in my opinion, so it would be nice if we could do better here.

### How are oracle providers meant to be implemented?

Right now we implemented examples for Python/NodeJS and Browser. Does this even make sense if the input/output formats are later to be specified as types of the smart contract language. Can we cast to these types later or do the oracles themselves have to be ported to the smart contract language?

### Public Websocket port, Webserver configuration, CORS Headers?
If understand the concept right, the websockets are not supposed to be exposed to the web in the future? Anyway, for development purposes it is important to be able to talk to an oracle via the browser in my opinion. Everyone who wants to build web clients for the oracles, has to set up an Nginx/Apache proxy that provides valid CORS headers and expose the Websocket port. It would be nice if we could have a starter setup for our users and the internal developers.
