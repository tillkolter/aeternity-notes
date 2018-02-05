# aeternity-notes

## Questions to the core team

### What are the implication of mining for client applications? 

We know that we must wait for a block to be mined before we can progress to the next stage the various operations we make. However it's still possible that a transaction can become invalid due to being on a chain which is orphaned. What do you envisage as the right way to handle for a client application? When can we truly assume that a transaction has succeeded, and what do we do if we discover that something we'd relied upon is no longer valid? If these are corner cases which we think will only occur very infrequently, can we put numbers on that?

### Mining speed 
Related: we have sped up mining speed on our test network to one block on average every 15 seconds, which makes life much easier. Since TTLs are expressed in blocks, speeding up the mining speed on the main net after launch will cause a great many assumptions to become invalid, things to expire before they're anticipated, and so on. What's current thinking in the core team about this?

### How can we make sure an oracle logic is available "forever"?

I understand that it makes sense to give a TTL to oracles, answers and questions. However since Oracles are meant to be reliable information providers which consuming smart contracts rely on, Oracles are usually meant to live forever or at least for a long amount of time. That means, that a reinitialisation would have to be scheduled before an oracle expires to make sure, that the information flow is steady. 

Conceivably an AENS name could help with this, if their lifetimes could be extended, but this doesn't seem part of the current plan. Is there a way of addressing this?

### Can we get rid of the error logging pollution, please?

It seems that every exception that is thrown during transaction processing is reposted to the `epoch.log` over and over again which makes development almost impossible after a couple of bad transactions have been produced. In addition this now seems to affect server stability.

### Could transaction errors be made available via HTTP? 

I wonder if this is a philosophical issue--it seems to me that the current logic is:

- on syntactically invalid request, nothing is returned.
- on a syntactically valid request which is nonetheless not valid, a successful result is returned. Sometimes this is useful--for instance I can register an Oracle, and if it already exists I receive back an identifier for the existing one. However now I have an inaccurate idea of the oracle's ttl, at minimum. Is there a strategy this this?

It would be very helpful to pull a list of errors from the server, if not get them as they occur.


Informative error handling during Dapp development is very important imho and my one of the biggest fails on Ethereum in my opinion, so it would be nice if we could do better here.

### Will it ever be possible to have multiple Oracles per node?

That would be cool.

### Public Websocket port, Webserver configuration, CORS Headers?
If understand the concept right, the websockets are not supposed to be exposed to the web in the future? Anyway, for development purposes it is important to be able to talk to an oracle via the browser in my opinion. Everyone who wants to build web clients for the oracles, has to set up an Nginx/Apache proxy that provides valid CORS headers and expose the Websocket port. It would be nice if we could have a starter setup for our users and the internal developers.


### What are the lower boundary points for the delta TTLs specifications?

Is the mining block time the starting point for the delta or the block time of the broadcasting node? It seemed to me, that sometimes I received almost instantly ttl expirations errors and sometimes the query/response pairs seemed to live even longer than expected.

# The questions below are rewritten above--please check the point is still adequately made.


### How can we get access to the transaction hash for an oracle registration?

Increased mining block height should not be taken as a proof that an oracle has been successfully registered. The transaction could either fail or even not be mined yet due to network congestions. How I understand it, that means, that the registering account needs to keep track of the TX hash or an id to make sure, that the oracle *really* has been registered.

### Should we consider a minimum amount of mined blocks before an oracle answer is accepted to be `true`?

Would it make sense to freeze an answer to make sure, that malicious node dont broadcast false answers?



### How are oracle providers meant to be implemented?

Right now we implemented examples for Python/NodeJS and Browser. Does this even make sense if the input/output formats are later to be specified as types of the smart contract language. Can we cast to these types later or do the oracles themselves have to be ported to the smart contract language?

