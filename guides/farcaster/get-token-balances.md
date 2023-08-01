---
description: >-
  Learn how to get ERC20, 721, 1155, and POAPs Of Farcaster User(s), including
  images and metadata, on Ethereum, Polygon, and Gnosis (POAPs).
---

# 💰 Get Token Balances

## Topics

* [Get All ERC20s Owned By Farcaster user(s)](get-token-balances.md#get-all-erc20s-owned-by-farcaster-user-s)
* [Get All NFTs Owned By Farcaster user(s)](get-token-balances.md#get-all-nfts-owned-by-farcaster-user-s)
* [Get All POAPs Owned By Farcaster user(s)](get-token-balances.md#get-all-poaps-owned-by-farcaster-user-s)

## Get All ERC20s Owned By Farcaster user(s)

You can fetch all ERC20 tokens on Ethereum and Polygon owned by any Farcaster user(s) using either their Farcaster names or IDs:

### Try Demo

{% embed url="https://app.airstack.xyz/DTyOZg/FxdfrqG3WS" %}
Show ERC20 tokens on Ethereum and Polygon owned by Farcaster user name dwr.eth and user id 1
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query ERC20sOwnedByFarcasterUser {
  Ethereum: TokenBalances(
    input: {filter: {owner: {_in: ["fc_fname:dwr.eth", "fc_fid:1"]}, tokenType: {_eq: ERC20}}, blockchain: ethereum, limit: 50}
  ) {
    TokenBalance {
      owner {
        socials(input: {filter: {dappName: {_eq: farcaster}}}) {
          profileName
          userId
          userAssociatedAddresses
        }
      }
      amount
      tokenAddress
      token {
        name
        symbol
      }
    }
    pageInfo {
      nextCursor
      prevCursor
    }
  }
  Polygon: TokenBalances(
    input: {filter: {owner: {_in: ["fc_fname:dwr.eth", "fc_fid:1"]}, tokenType: {_eq: ERC20}}, blockchain: polygon, limit: 50}
  ) {
    TokenBalance {
      owner {
        socials(input: {filter: {dappName: {_eq: farcaster}}}) {
          profileName
          userId
          userAssociatedAddresses
        }
      }
      amount
      tokenAddress
      token {
        name
        symbol
      }
    }
    pageInfo {
      nextCursor
      prevCursor
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Ethereum": {
      "TokenBalance": [
        {
          "owner": {
            "socials": [
              {
                "profileName": "dwr.eth",
                "userId": "3",
                "userAssociatedAddresses": [
                  "0x74232bf61e994655592747e20bdf6fa9b9476f79",
                  "0xb877f7bb52d28f06e60f557c00a56225124b357f",
                  "0xa14b4c95b5247199d74c5578531b4887ca5e4909",
                  "0xd7029bdea1c17493893aafe29aad69ef892b8ff2"
                ]
              }
            ]
          }
          "amount": "1000000000000000000",
          "tokenAddress": "0x502527431b8f5d3cde71569ea810d19441952b48",
          "token": {
            "name": "TedToken",
            "symbol": "TED"
          }
        },
      ]
    },
    "Polygon": {
      "TokenBalance": [
        {
          "owner": {
            "socials": [
              {
                "profileName": "dwr.eth",
                "userId": "3",
                "userAssociatedAddresses": [
                  "0x74232bf61e994655592747e20bdf6fa9b9476f79",
                  "0xb877f7bb52d28f06e60f557c00a56225124b357f",
                  "0xa14b4c95b5247199d74c5578531b4887ca5e4909",
                  "0xd7029bdea1c17493893aafe29aad69ef892b8ff2"
                ]
              },
            ]
          },
          "amount": "2868191141756779000000",
          "tokenAddress": "0x086373fad3447f7f86252fb59d56107e9e0faafa",
          "token": {
            "name": "Yup",
            "symbol": "YUP"
          }
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get All NFTs Owned By Farcaster user(s)

You can fetch all NFTs on Ethereum and Polygon owned by any Farcaster user(s) using either their Farcaster names or IDs:

### Try Demo

{% embed url="https://app.airstack.xyz/DTyOZg/eEsGE50Xin" %}
Show NFT on Ethereum and Polygon owned by farcaster user name dwr.eth and user id 1
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query NFTsOwnedByFarcasterUser {
  Ethereum: TokenBalances(
    input: {filter: {owner: {_in: ["fc_fname:dwr.eth", "fc_fid:1"]}, tokenType: {_in: [ERC1155, ERC721]}}, blockchain: ethereum, limit: 50}
  ) {
    TokenBalance {
      owner {
        socials(input: {filter: {dappName: {_eq: farcaster}}}) {
          profileName
          userId
          userAssociatedAddresses
        }
      }
      amount
      tokenAddress
      tokenId
      tokenType
      tokenNfts {
        contentValue {
          image {
            extraSmall
            small
            medium
            large
          }
        }
      }
    }
    pageInfo {
      nextCursor
      prevCursor
    }
  }
  Polygon: TokenBalances(
    input: {filter: {owner: {_in: ["fc_fname:dwr.eth", "fc_fid:1"]}, tokenType: {_in: [ERC1155, ERC721]}}, blockchain: polygon, limit: 50}
  ) {
    TokenBalance {
      owner {
        socials(input: {filter: {dappName: {_eq: farcaster}}}) {
          profileName
          userId
          userAssociatedAddresses
        }
      }
      amount
      tokenAddress
      tokenId
      tokenType
      tokenNfts {
        contentValue {
          image {
            extraSmall
            small
            medium
            large
          }
        }
      }
    }
    pageInfo {
      nextCursor
      prevCursor
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Ethereum": {
      "TokenBalance": [
        {
          "owner": {
            "socials": [
              {
                "profileName": "dwr.eth",
                "userId": "3",
                "userAssociatedAddresses": [
                  "0x74232bf61e994655592747e20bdf6fa9b9476f79",
                  "0xb877f7bb52d28f06e60f557c00a56225124b357f",
                  "0xa14b4c95b5247199d74c5578531b4887ca5e4909",
                  "0xd7029bdea1c17493893aafe29aad69ef892b8ff2"
                ]
              }
            ]
          },
          "amount": "1",
          "tokenAddress": "0x1538c5ddbb073638b7cd1ae41ec2d9f9a4c24a7e",
          "tokenId": "1",
          "tokenType": "ERC721",
          "tokenNfts": {
            "contentValue": {
              "image": {
                "extraSmall": "https://assets.airstack.xyz/image/nft/1/0x1538c5ddbb073638b7cd1ae41ec2d9f9a4c24a7e/1/extra_small.jpg",
                "small": "https://assets.airstack.xyz/image/nft/1/0x1538c5ddbb073638b7cd1ae41ec2d9f9a4c24a7e/1/small.jpg",
                "medium": "https://assets.airstack.xyz/image/nft/1/0x1538c5ddbb073638b7cd1ae41ec2d9f9a4c24a7e/1/medium.jpg",
                "large": "https://assets.airstack.xyz/image/nft/1/0x1538c5ddbb073638b7cd1ae41ec2d9f9a4c24a7e/1/large.jpg"
              }
            }
          }
        }
      ]
    },
    "Polygon": {
      "TokenBalance": [
        {
          "owner": {
            "socials": [
              {
                "profileName": "dwr.eth",
                "userId": "3",
                "userAssociatedAddresses": [
                  "0x74232bf61e994655592747e20bdf6fa9b9476f79",
                  "0xb877f7bb52d28f06e60f557c00a56225124b357f",
                  "0xa14b4c95b5247199d74c5578531b4887ca5e4909",
                  "0xd7029bdea1c17493893aafe29aad69ef892b8ff2"
                ]
              }
            ]
          },
          "amount": "1",
          "tokenAddress": "0x0f92612c5f539c89dc379e8aa42e3ba862a34b7e",
          "tokenId": "8",
          "tokenType": "ERC721",
          "tokenNfts": {
            "contentValue": {
              "image": {
                "extraSmall": "https://assets.airstack.xyz/image/nft/1/0x0f92612c5f539c89dc379e8aa42e3ba862a34b7e/8/extra_small.jpg",
                "small": "https://assets.airstack.xyz/image/nft/1/0x0f92612c5f539c89dc379e8aa42e3ba862a34b7e/8/small.jpg",
                "medium": "https://assets.airstack.xyz/image/nft/1/0x0f92612c5f539c89dc379e8aa42e3ba862a34b7e/8/medium.jpg",
                "large": "https://assets.airstack.xyz/image/nft/1/0x0f92612c5f539c89dc379e8aa42e3ba862a34b7e/8/large.jpg"
              }
            }
          }
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Get All POAPs Owned By Farcaster user(s)

You can fetch all POAPs tokens owned by any Farcaster user(s) using either their Farcaster names or IDs:

### Try Demo

{% embed url="https://app.airstack.xyz/DTyOZg/9gNjxdNWsP" %}
Show POAPs owned by Farcaster user name dwr.eth and user id 1
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}
```graphql
query POAPsOwnedByFarcasterUser {
  Poaps(
    input: {filter: {owner: {_in: ["fc_fname:dwr.eth", "fc_fid:1"]}}, blockchain: ALL}
  ) {
    Poap {
      eventId
      poapEvent {
        eventName
        eventURL
        startDate
        endDate
        country
        city
        contentValue {
          image {
            extraSmall
            large
            medium
            original
            small
          }
        }
      }
    }
    pageInfo {
      nextCursor
      prevCursor
    }
  }
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "data": {
    "Poaps": {
      "Poap": [
        {
          "eventId": "6584",
          "poapEvent": {
            "eventName": "Pudgy Penguin owner as of August 2021",
            "eventURL": "https://www.stonercats.com/",
            "startDate": "2021-08-30T00:00:00Z",
            "endDate": "2021-09-30T00:00:00Z",
            "country": "United States",
            "city": "Ethereum",
            "contentValue": {
              "image": {
                "extraSmall": "https://assets.airstack.xyz/image/poap/100/6584/extra_small.png",
                "large": "https://assets.airstack.xyz/image/poap/100/6584/large.png",
                "medium": "https://assets.airstack.xyz/image/poap/100/6584/medium.png",
                "original": "https://assets.airstack.xyz/image/poap/100/6584/original_image.png",
                "small": "https://assets.airstack.xyz/image/poap/100/6584/small.png"
              }
            }
          }
        },
        {
          "eventId": "14498",
          "poapEvent": {
            "eventName": "ConstitutionDAO Contributor",
            "eventURL": "https://www.constitutiondao.com/",
            "startDate": "2021-11-18T00:00:00Z",
            "endDate": "2021-11-18T00:00:00Z",
            "country": "",
            "city": "",
            "contentValue": {
              "image": {
                "extraSmall": "https://assets.airstack.xyz/image/poap/1/14498/extra_small.png",
                "large": "https://assets.airstack.xyz/image/poap/1/14498/large.png",
                "medium": "https://assets.airstack.xyz/image/poap/1/14498/medium.png",
                "original": "https://assets.airstack.xyz/image/poap/1/14498/original_image.png",
                "small": "https://assets.airstack.xyz/image/poap/1/14498/small.png"
              }
            }
          }
        },
        {
          "eventId": "6481",
          "poapEvent": {
            "eventName": "Fractional Early Adopter",
            "eventURL": "https://fractional.art/",
            "startDate": "2021-08-27T00:00:00Z",
            "endDate": "2021-08-27T00:00:00Z",
            "country": "",
            "city": "",
            "contentValue": {
              "image": {
                "extraSmall": "https://assets.airstack.xyz/image/poap/1/6481/extra_small.png",
                "large": "https://assets.airstack.xyz/image/poap/1/6481/large.png",
                "medium": "https://assets.airstack.xyz/image/poap/1/6481/medium.png",
                "original": "https://assets.airstack.xyz/image/poap/1/6481/original_image.png",
                "small": "https://assets.airstack.xyz/image/poap/1/6481/small.png"
              }
            }
          }
        }
      ]
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Developer Support

If you have any questions or need help regarding fetching token balances of Farcaster user(s), please join our Airstack's [Telegram](https://t.me/+1k3c2FR7z51mNDRh) group.

## More Resources

* [TokenBalances API Reference](../../api-references/api-reference/tokenbalances-api/)