---
description: >-
  Learn all the detailed references of TokenBalances API that provide
  ERC20/721/1155 token balances/holders information, including the input
  filters, supported chains, and output fields.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# TokenBalances API

The TokenBalances API covers the owners and balances of ERC20, ERC721, and ERC1155 tokens.

## Inputs

### filter

| Name                   | Type                       | Description                                                                           |
| ---------------------- | -------------------------- | ------------------------------------------------------------------------------------- |
| `formattedAmount`      | `Float_Comparator_Exp`     | Allows filtering based on Balance amount in decimals, e.g. show me Balances above 200 |
| `lastUpdatedTimestamp` | `Time_Comparator_Exp`      | Timestamp when the token balance was last updated                                     |
| `owner`                | `Identity_Comparator_Exp`  | Identity: blockchain address, domain name, social identity                            |
| `tokenAddress`         | `Address_Comparator_Exp`   | Token contract address on the blockchain (ERC20, ERC721, ERC1155)                     |
| `tokenId`              | `String_Comparator_Exp`    | Unique NFT token ID                                                                   |
| `tokenType`            | `TokenType_Comparator_Exp` | ERC20, ERC721, ERC1155                                                                |

### blockchain

| Enum       | Description      |
| ---------- | ---------------- |
| `ethereum` | Ethereum mainnet |
| `base`     | Base mainnet     |
| `zora`     | Zora mainnet     |
| `gold`     | Gold Chain L3    |
| `degen`    | Degen Chain L3   |
| `ham`      | Ham Chain L3     |
| `stp`      | Clique Chain L3  |

## Outputs

```graphql
type TokenBalance {
  amount: String! # Token balance amount
  blockchain: Blockchain # Blockchain where the token balance is located
  chainId: String! # Unique blockchain identifier
  id: ID! # Airstack unique identifier for the data point
  lastUpdatedBlock: Int! # Block number when the token balance was last updated
  lastUpdatedTimestamp: Time # Timestamp when the token balance was last updated
  owner: Wallet! # **Nested query** allowing to retrieve address, domain names, and social profiles of the owner
  token: Token # **Nested query** to get token contract level data
  tokenAddress: Address! # Token contract address
  tokenId: String # Unique NFT token ID, if applicable
  tokenNfts: # **Nested query** allowing to get NFT token data (images, traits, etc.)
  tokenTransfer: # **Nested query** with token transfer history and details
  tokenType: TokenType # ERC20, ERC721, or ERC1155
}
```

{% hint style="success" %}
See [here](../../guides/resolve-identities/) for how to query with ENS or web3 social identities, such as Farcaster
{% endhint %}
