---
description: >-
  Learn how to resolve Farcaster(s) fname/username/FID to 0x address, ENS, Lens,
  and XMTP and Reverse Resolution.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: true
---

# 🆔 Resolve Farcaster Users

[Airstack](https://airstack.xyz) provides easy-to-use APIs for enriching [Farcaster](https://farcaster.xyz) applications and for integrating onchain and offchain data with Farcaster.

## Table Of Contents

In this guide you will learn how to use Airstack to:

* [Get All 0x addresses of Farcaster user(s)](resolve-farcaster-users.md#get-all-0x-addresses-of-farcaster-user-s)
* [Get All Solana addresses of Farcaster user](resolve-farcaster-users.md#get-all-solana-addresses-of-farcaster-user)
* [Get Farcaster profiles of a given Solana address](resolve-farcaster-users.md#get-farcaster-profiles-of-a-given-solana-address)
* [Get all ENS domains owned by Farcaster user(s)](resolve-farcaster-users.md#get-all-ens-domains-owned-by-farcaster-user-s)
* [Get All Web3 Social Accounts (Farcaster, Lens) owned by 0x address or ENS](resolve-farcaster-users.md#get-all-web3-social-accounts-farcaster-lens-owned-by-0x-address-or-ens)

### Pre-requisites

* An [Airstack](https://airstack.xyz/) account
* Basic knowledge of GraphQL

### Get Started

**JavaScript/TypeScript/Python**

If you are using JavaScript/TypeScript or Python, Install the Airstack SDK:

{% tabs %}
{% tab title="npm" %}
**React**

```sh
npm install @airstack/airstack-react
```

**Node**

```sh
npm install @airstack/node
```
{% endtab %}

{% tab title="yarn" %}
**React**

```sh
yarn add @airstack/airstack-react
```

**Node**

```sh
yarn add @airstack/node
```
{% endtab %}

{% tab title="pnpm" %}
**React**

```sh
pnpm install @airstack/airstack-react
```

**Node**

```sh
pnpm install @airstack/node
```
{% endtab %}

{% tab title="pip" %}
```sh
pip install airstack
```
{% endtab %}
{% endtabs %}

Then, add the following snippets to your code:

{% tabs %}
{% tab title="React" %}
```jsx
import { init, useQuery } from "@airstack/airstack-react";

init("YOUR_AIRSTACK_API_KEY");

const query = `YOUR_QUERY`; // Replace with GraphQL Query

const Component = () => {
  const { data, loading, error } = useQuery(query);

  if (data) {
    return <p>Data: {JSON.stringify(data)}</p>;
  }

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Error: {error.message}</p>;
  }
};
```
{% endtab %}

{% tab title="Node" %}
```javascript
import { init, fetchQuery } from "@airstack/node";

init("YOUR_AIRSTACK_API_KEY");

const query = `YOUR_QUERY`; // Replace with GraphQL Query

const { data, error } = fetchQuery(query);

console.log("data:", data);
console.log("error:", error);
```
{% endtab %}

{% tab title="Python" %}
```python
import asyncio
from airstack.execute_query import AirstackClient

api_client = AirstackClient(api_key="YOUR_AIRSTACK_API_KEY")

query = """YOUR_QUERY""" # Replace with GraphQL Query

async def main():
    execute_query_client = api_client.create_execute_query_object(
        query=query)

    query_response = await execute_query_client.execute_query()
    print(query_response.data)

asyncio.run(main())
```
{% endtab %}
{% endtabs %}

**Other Programming Languages**

To access the Airstack APIs in other languages, you can use [https://api.airstack.xyz/gql](https://api.airstack.xyz/gql) as your GraphQL endpoint.

## Get All 0x addresses of Farcaster user(s)

You can resolve an array of Farcaster user(s) to their 0x addresses:

### Try Demo

{% embed url="https://app.airstack.xyz/query/rQQVTG8laa" %}
Show 0x addresses of Farcaster user name dwr.eth and user ID 1
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query GetAddressesOfFarcasters {
  Socials(
    input: {
      filter: { identity: { _in: ["fc_fname:dwr.eth", "fc_fid:1"] } }
      blockchain: ethereum
    }
  ) {
    Social {
      userAssociatedAddresses
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Socials": {
      "Social": [
        {
          "userAssociatedAddresses": [
            "0x8773442740c17c9d0f0b87022c722f9a136206ed",
            "0x86924c37a93734e8611eb081238928a9d18a63c0"
          ]
        },
        {
          "userAssociatedAddresses": [
            "0xd7029bdea1c17493893aafe29aad69ef892b8ff2"
          ]
        },
        {
          "userAssociatedAddresses": [
            "0xb877f7bb52d28f06e60f557c00a56225124b357f",
            "0xa14b4c95b5247199d74c5578531b4887ca5e4909",
            "0xd7029bdea1c17493893aafe29aad69ef892b8ff2",
            "0x74232bf61e994655592747e20bdf6fa9b9476f79"
          ]
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get All Solana addresses of Farcaster user

You can resolve a Farcaster user to their Solana addresses by using [`Socials`](../../api-references/api-reference/socials-api.md) API:

### Try Demo

{% embed url="https://app.airstack.xyz/query/4oizUq1TtG" %}
Show me the Solana connected address of Farcaster user v
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query MyQuery {
  Socials(
    input: {
      filter: { dappName: { _eq: farcaster }, profileName: { _eq: "v" } }
      blockchain: ethereum
    }
  ) {
    Social {
      connectedAddresses {
        address
        blockchain
        chainId
        timestamp
      }
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Socials": {
      "Social": [
        {
          "connectedAddresses": [
            {
              "address": "9t92xZy9q5SyfKBH4rZwEDFXjaZKgzj5PgviPhKtBjyy",
              "blockchain": "solana",
              "chainId": "900",
              "timestamp": "2024-02-16T22:13:14Z"
            },
            {
              "address": "0x91031dcfdea024b4d51e775486111d2b2a715871",
              "blockchain": "ethereum",
              "chainId": "1",
              "timestamp": "2023-04-28T17:42:20Z"
            },
            {
              "address": "0x182327170fc284caaa5b1bc3e3878233f529d741",
              "blockchain": "ethereum",
              "chainId": "1",
              "timestamp": "2023-07-26T20:46:33Z"
            }
          ]
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get Farcaster profiles of a given Solana address

You can resolve Solana address to get all the Farcaster profiles owned by the given Solana address by using the [`Socials`](../../api-references/api-reference/socials-api.md) API:

### Try Demo

{% embed url="https://app.airstack.xyz/query/ewk0zjfkll" %}
Show me the Farcaster profile of solana address 9t92xZy9q5SyfKBH4rZwEDFXjaZKgzj5PgviPhKtBjyy
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query MyQuery {
  Socials(
    input: {
      filter: {
        identity: { _eq: "9t92xZy9q5SyfKBH4rZwEDFXjaZKgzj5PgviPhKtBjyy" }
        dappName: { _eq: farcaster }
      }
      blockchain: ethereum
    }
  ) {
    Social {
      profileName
      fid: userId
      userAssociatedAddresses
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Socials": {
      "Social": [
        {
          "profileName": "v",
          "fid": "2",
          "userAssociatedAddresses": [
            "0x4114e33eb831858649ea3702e1c9a2db3f626446",
            "0x91031dcfdea024b4d51e775486111d2b2a715871",
            "0x182327170fc284caaa5b1bc3e3878233f529d741",
            "0xf86a7a5b7c703b1fd8d93c500ac4cc75b67477f0",
            "9t92xZy9q5SyfKBH4rZwEDFXjaZKgzj5PgviPhKtBjyy"
          ]
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get all ENS domains owned by Farcaster user(s)

You can resolve an array of Farcaster user(s) to their ENS domains:

### Try Demo

{% embed url="https://app.airstack.xyz/query/6TtsANTcnd" %}
Show all ENS domains owned by Farcaster user name dwr.eth and user id 1
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query GetENSOfFarcasters {
  Domains(
    input: {
      filter: { owner: { _in: ["fc_fname:dwr.eth", "fc_fid:1"] } }
      blockchain: ethereum
    }
  ) {
    Domain {
      name
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Domains": {
      "Domain": [
        {
          "name": "noun124.eth"
        },
        {
          "name": "dwr.mirror.xyz"
        },
        {
          "name": "warpcast.eth"
        },
        {
          "name": "danromero.eth"
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get All Web3 Social Accounts (Farcaster, Lens) owned by 0x address or ENS

You can resolve any 0x address or ENS to their web3 socials, which comprise of Farcaster and Lens:

### Try Demo

{% embed url="https://app.airstack.xyz/query/FHYr4PHYwu" %}
Show web3 social accounts (Farcaster, Lens) owned by dwr.eth and 0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query GetWeb3SocialsOfFarcasters {
  Socials(
    input: {
      filter: {
        identity: {
          _in: ["dwr.eth", "0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045"]
        }
      }
      blockchain: ethereum
    }
  ) {
    Social {
      dappName
      profileName
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Socials": {
      "Social": [
        {
          "dappName": "farcaster",
          "profileName": "vbuterin"
        },
        {
          "dappName": "lens",
          "profileName": "lens/@vitalik"
        },
        {
          "dappName": "lens",
          "profileName": "lens/@danromero"
        },
        {
          "dappName": "farcaster",
          "profileName": "dwr.eth"
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Developer Support

If you have any questions or need help regarding resolving identities for Farcaster user(s), please join our Airstack's [Telegram](https://t.me/+1k3c2FR7z51mNDRh) group.

## More Resources

* [Resolve Identities](../../guides/resolve-identities/)
  * [Farcaster](../../guides/resolve-identities/farcaster.md)
  * [Solana Address](../../guides/resolve-identities/solana-address.md)
* [Socials API Reference](../../api-references/api-reference/socials-api.md)
* [XMTPs API Reference](../../api-references/api-reference/xmtps-api.md)
