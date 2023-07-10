# Poaps API

{% hint style="info" %}
The Poaps API allows users to query POAPs held by a particular wallet, all POAP tokens from a particular event, or simply fetch details about a particular POAP Token, and also return event-specific metadata, including  <mark style="background-color:green;">**resized images**</mark>.
{% endhint %}

Inputs & Filters

```graphql
input PoapFilter {
  dappName: # POAP Dapp Name
  dappSlug: # POAP Dapp Version
  eventId: #POAP Event ID
  owner: # Identity: blockchain address, domain name, social identity
  tokenId: # POAP Token ID
}
```

Outputs

```graphql
type Poap {
  id: # Airstack unique element identifier
  chainId: # Blockchain ID 
  blockchain: # Blockchain name
  dappName: 
  dappSlug: 
  dappVersion: 
  eventId: #POAP Event ID
  owner: Wallet! # **Nested query** allowing to retrieve address, domain names, and social profiles of the owner
  createdAtBlockTimestamp: 
  createdAtBlockNumber: 
  tokenId: #POAP Token ID
  tokenAddress: #POAP contract address
  tokenUri: # POAP Token URI
  poapEvent:# **Nested query** allowing to return all POAP event-related metadata including images.
}
```