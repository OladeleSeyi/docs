---
description: >-
  Learn how to fetch Farcaster Casts and related data using the Airstack API,
  and various use cases and combinations.
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

# 💬 Farcaster Casts

## Table Of Contents

In this guide, you will learn to use [Airstack](https://airstack.xyz) to:

- [Get All Casts Casted In A Channel](farcaster-casts.md#get-all-casts-casted-in-a-channel) (Channel Feed)
- [Get All Casts Casted By A Farcaster User ](farcaster-casts.md#get-all-casts-casted-by-a-farcaster-user)(User Feed)
- [Get All Casts That Have Frames](farcaster-casts.md#get-all-casts-that-have-frames) (Frames Feed)
- [Get All Casts That Have Embeds](farcaster-casts.md#get-all-casts-that-have-embeds)&#x20;
- [Get All Casts Casted At Certain Period Of Time](farcaster-casts.md#get-all-casts-casted-at-certain-period-of-time)
- [Get All Casts That Have Mentions](farcaster-casts.md#get-all-casts-that-have-mentions)
- [Get Details Of A Certain Cast By Cast URL](farcaster-casts.md#get-details-of-a-certain-cast-by-cast-url)
- [Get Details Of A Certain Cast By Cast Hash](farcaster-casts.md#get-details-of-a-certain-cast-by-cast-hash)

### Pre-requisites

- An [Airstack](https://airstack.xyz/) account
- Basic knowledge of GraphQL

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

const { data, error } = await fetchQuery(query);

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

## Get All Casts Casted In A Channel

{% embed url="https://www.youtube.com/watch?v=kb0HykrEYYg" %}
Get All Casts Casted In A Channel
{% endembed %}

You can fetch all the casts casted in a certain Farcaster channel by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and providing the Farcaster channel's URL to the `channelUrl` filter:

{% hint style="info" %}
If you don't know the channel's URL, then find the channel's URL with this query [here](farcaster-channels.md#get-channel-details). The `url` field will return you the channel's URL associated with the given channel ID.
{% endhint %}

### Try Demo

{% embed url="https://app.airstack.xyz/query/kXhn9i70Lh" %}
Show me all the casts in /airstack channel
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        rootParentUrl: {
          # add channel URL here
<strong>          _eq: "https://warpcast.com/~/channel/airstack"
</strong>        }
      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      castedBy {
        profileName
        fid: userId
      }
      embeds
      fid
      hash
      text
      numberOfLikes
      numberOfRecasts
      numberOfReplies
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-05-15T10:42:06Z",
          "castedBy": {
            "profileName": "juampi",
            "fid": "6730"
          },
          "embeds": [
            {
              "url": "https://imagedelivery.net/BXluQx4ige9GuW0Ia56BHw/84b11c9b-2308-43c5-821b-b73d7687b400/original"
            }
          ],
          "fid": "6730",
          "hash": "0xb2a16ed043b762e097627ed5b080d5c482b4664b",
          "text": "Everyone loving the Airstack frame, super smooth experience!\n\nNow you can buy $BUILD on it 🫡",
          "numberOfLikes": 3,
          "numberOfRecasts": 0,
          "numberOfReplies": 0
        }
        // More casts from /airstack channel
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get All Casts Casted By A Farcaster User

You can fetch all the casts casted by a Farcaster user by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and providing the Farcaster user's fname or fid to the `castedBy` filter:

### Try Demo

{% embed url="https://app.airstack.xyz/query/TPbgbs18jN" %}
Show me all the casts casted by Farcaster user betashop.eth
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

```graphql
query MyQuery {
  FarcasterCasts(
    input: {
      filter: { castedBy: { _eq: "fc_fname:betashop.eth" } }
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      url
      text
      numberOfRecasts
      numberOfLikes
      channel {
        channelId
      }
      mentions {
        fid
        position
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
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-03-27T15:27:38Z",
          "embeds": [],
          "url": "https://warpcast.com/betashop.eth/0x82bbbf0c",
          "text": "Whoops",
          "numberOfRecasts": 0,
          "numberOfLikes": 1,
          "channel": {
            "channelId": "farcaster"
          },
          "mentions": []
        }
        // Other casts casted by Farcaster user betashop.eth
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get All Casts That Have Frames

You can fetch all the casts casted that contain Frames by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and set the `hasFrames` filter to `true`:

### Try Demo

{% embed url="https://app.airstack.xyz/query/hv7xgCCD2p" %}
Show me all the casts that contain Farcaster Frames
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        # Make sure to have `hasFrames` to true
<strong>        hasFrames: {_eq: true}
</strong>      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      url
      text
      numberOfRecasts
      numberOfLikes
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
      frame {
        buttons {
          action
          id
          index
          target
        }
        frameUrl
        imageAspectRatio
        imageUrl
        inputText
        postUrl
        state
      }
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:24Z",
          "embeds": [
            {
              "url": "https://i.imgur.com/znWzuFb.jpg"
            },
            {
              "url": "https://api.anky.lat/farcaster-frames/newen-tldr"
            }
          ],
          "url": "https://warpcast.com/kregitmhun/0x949a4e0e",
          "text": "Mint free or not try to get a place earlier than anyone else, I will provide specific updates later\nhttps://api.anky.lat/farcaster-frames/newen-tldr",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "channel": {
            "channelId": "base"
          },
          "mentions": [],
          // Frame details
          "frame": {
            "buttons": [
              {
                "action": "",
                "id": "0x85bffc4de32c70688855f31a868181613fe4182890c4d35224a0afa311cfc6df-1",
                "index": 1,
                "target": ""
              }
            ],
            "frameUrl": "https://api.anky.lat/farcaster-frames/newen-tldr",
            "imageAspectRatio": "",
            "imageUrl": "https://jpfraneto.github.io/images/newen2.png",
            "inputText": "",
            "postUrl": "http://api.anky.lat/farcaster-frames/newen-tldr?page=1",
            "state": ""
          }
        }
        // Other casts that contains Frames
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get All Casts That Have Embeds

You can fetch all the casts casted that contain Frames by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and set the `hasEmbeds` filter to `true`:

### Try Demo

{% embed url="https://app.airstack.xyz/query/sgTvN7NktX" %}
Show me all the casts that contains embeds
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        # Make sure to set `hasEmbeds` to true
<strong>        hasEmbeds: {_eq: true}
</strong>      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      url
      text
      numberOfRecasts
      numberOfLikes
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:25Z",
          "embeds": [
            {
              "url": "https://audius.co/dannylove/lovestruck"
            }
          ],
          "url": "https://warpcast.com/dannylove/0xabc68559",
          "text": "https://audius.co/dannylove/lovestruck\n\n@audius it works!!",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "channel": {
            "channelId": "music"
          },
          "mentions": [
            {
              "fid": "366747",
              "position": 40
            }
          ]
        }
        // Other casts that have embeds
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get All Casts Casted At Certain Period Of Time

You can fetch all the casts casted that contain Frames by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and providing the time period to the `castedAtTimestamp` filter with the appropriate [operators](../../api-references/overview/working-with-graphql.md):

### Try Demo

{% embed url="https://app.airstack.xyz/query/0fSubz9nW8" %}
Show me all the casts casted since Jan 1, 2024
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        # Make sure to set `castedTimestamp` with the matching operator
        # to filter by the desired time period
<strong>        castedAtTimestamp: {_gte: "2024-01-01T00:00:00Z"}
</strong>      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      url
      text
      numberOfRecasts
      numberOfLikes
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:28Z",
          "embeds": [],
          "url": "https://warpcast.com/qdau.eth/0x654ed051",
          "text": "not siue if that's a warpcast or zora problem, but mint with warps in a frame don't seem to work for base nfts\n\ncc @incarterseyes.eth @rawtoast @l444u",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "channel": {
            "channelId": "warpcast"
          },
          "mentions": [
            {
              "fid": "5952",
              "position": 115
            },
            {
              "fid": "17129",
              "position": 116
            },
            {
              "fid": "15037",
              "position": 117
            }
          ]
        }
        // Other casts casted since Jan 1, 2024
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get All Casts That Have Mentions

You can fetch all the casts casted that contain mentions by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and set the `hasMentions` filter to `true`:

### Try Demo

{% embed url="https://app.airstack.xyz/query/YSPcZTGeOk" %}
Show me all the casts that has mentions
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        # Make sure to set `hasMentions` to true
<strong>        hasMentions: {_eq: true}
</strong>      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      url
      text
      numberOfRecasts
      numberOfLikes
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:28Z",
          "embeds": [],
          "url": "https://warpcast.com/qdau.eth/0x654ed051",
          "text": "not siue if that's a warpcast or zora problem, but mint with warps in a frame don't seem to work for base nfts\n\ncc @incarterseyes.eth @rawtoast @l444u",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "channel": {
            "channelId": "warpcast"
          },
          "mentions": [
            {
              "fid": "5952",
              "position": 115
            },
            {
              "fid": "17129",
              "position": 116
            },
            {
              "fid": "15037",
              "position": 117
            }
          ]
        }
        // Other casts that have mentions
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get Details Of A Certain Cast By Cast URL

You can fetch all the details, including text, embeds, url, [social capital value](../../abstractions/social-capital-value-and-social-capital-scores.md), etc., of a given cast by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and provide the cast's URL from Warpcast to the `url` filter:

### Try Demo

{% embed url="https://app.airstack.xyz/query/bNR6cMHtXr" %}
Show me details of a given casts, e.g. likes, recasts, mentions, embeds, text, social capital value, etc.
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

```graphql
query MyQuery {
  FarcasterCasts(
    input: {
      filter: { url: { _eq: "https://warpcast.com/dannylove/0xabc68559" } }
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      text
      numberOfRecasts
      numberOfLikes
      numberOfReplies
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
      castValue {
        rawValue
        formattedValue
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
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:25Z",
          "embeds": [
            {
              "url": "https://audius.co/dannylove/lovestruck"
            }
          ],
          "text": "https://audius.co/dannylove/lovestruck\n\n@audius it works!!",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "numberOfReplies": 0,
          "channel": {
            "channelId": "music"
          },
          "mentions": [
            {
              "fid": "366747",
              "position": 40
            }
          ],
          "castValue": {
            "rawValue": "40837104",
            "formattedValue": 0.00040837104
          }
        }
      ]
    }
  }
}
```

{% endtab %}
{% endtabs %}

## Get Details Of A Certain Cast By Cast Hash

You can fetch all the details, including text, embeds, url, [social capital value](../../abstractions/social-capital-value-and-social-capital-scores.md), etc., of a given cast by using the [`FarcasterCasts`](../../api-references/api-reference/farcastercasts-api.md) API and provide the cast's hash to the `hash` filter:&#x20;

{% hint style="info" %}
If the cast is a reply and not a root cast, then you should use this query [here](farcaster-replies.md#get-farcaster-reply-details-by-reply-cast-hash).
{% endhint %}

### Try Demo

{% embed url="https://app.airstack.xyz/query/6VEOId85Tb" %}
show me the cast details of cast hash 0xabc6855945863f4fb9ebfe350c4366b74448d974
{% endembed %}

### Code

{% tabs %}
{% tab title="Query" %}

<pre class="language-graphql"><code class="lang-graphql">query MyQuery {
  FarcasterCasts(
    input: {
      filter: {
        # specify cast hash
<strong>        hash: {_eq: "0xabc6855945863f4fb9ebfe350c4366b74448d974"}
</strong>      },
      blockchain: ALL
    }
  ) {
    Cast {
      castedAtTimestamp
      embeds
      text
      numberOfRecasts
      numberOfLikes
      numberOfReplies
      channel {
        channelId
      }
      mentions {
        fid
        position
      }
      castValue {
        rawValue
        formattedValue
      }
    }
  }
}
</code></pre>

{% endtab %}

{% tab title="Response" %}

```json
{
  "data": {
    "FarcasterCasts": {
      "Cast": [
        {
          "castedAtTimestamp": "2024-02-27T19:07:25Z",
          "embeds": [
            {
              "url": "https://audius.co/dannylove/lovestruck"
            }
          ],
          "text": "https://audius.co/dannylove/lovestruck\n\n@audius it works!!",
          "numberOfRecasts": 0,
          "numberOfLikes": 0,
          "numberOfReplies": 0,
          "channel": {
            "channelId": "music"
          },
          "mentions": [
            {
              "fid": "366747",
              "position": 40
            }
          ],
          "castValue": {
            "rawValue": "40837104",
            "formattedValue": 0.00040837104
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

If you have any questions or need help regarding fetching Farcaster Casts data, please join our Airstack's [Telegram](https://t.me/+1k3c2FR7z51mNDRh) group.

## More Resources

- [Farcaster Frames Guides](farcaster-frames.md)
- [FarcasterCasts API Reference](../../api-references/api-reference/farcastercasts-api.md)
