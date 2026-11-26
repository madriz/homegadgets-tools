# HomeGadgets MCP server

Status: live. Page on the site: <https://www.homegadgets.ca/mcp>.
[Instructions en français](fr/installation.md#serveur-mcp)

## Install

There is nothing to install. The server is remote:

```
https://mcp.homegadgets.ca/mcp
```

Transport: streamable HTTP. Authentication: none.

In any client that supports remote MCP servers:

1. Add a new server. Some clients call it a connector or an integration.
2. Paste the URL above.
3. Leave authentication empty. Do not enter a key or start a sign-in.
4. Save. The client lists four tools: `search_products`, `get_price`,
   `compare_retailers`, `server_info`.

Where that setting lives differs from client to client and changes often, so
this guide does not give per-product steps. A client that only supports local
servers it starts itself cannot use this endpoint.

## Use

Ask your assistant a question about a Canadian price, for example "What is the
best price in Canada for a 65 inch LG OLED TV?" or "Compare prices for model
98UT9000PUA in Ontario". The assistant decides which tool to call.

| Tool | Inputs | Returns |
|------|--------|---------|
| `search_products` | `query` (free text); optional `location` (Canadian, default national); optional `filters` (`category`, `brand`, `min_price`, `max_price`, and `specs` for some categories) | Ranked matches, each with its best in-stock price, the retailer, a buy link, the average and highest price, and the retailer count |
| `get_price` | `identifier` (one of `keyword`, `brand` and `model`, `mpn`, `product_id`); `location` (required, Canadian) | The best current in-stock offer, the average, the highest, the retailer count and the rating where we hold one |
| `compare_retailers` | `product_id` or `mpn`; optional `location` | The best price, the average, the highest and how many retailers carry the product |
| `server_info` | none | Version, scope, categories, limits and what is and is not supported |

What a result means:

* The best price names its retailer and carries a link. It is the one offer in
  a result you can follow.
* The average and the highest are statistics over real offers. They name no
  retailer and carry no link, and are not prices you can pay.
* New and not-new are never mixed into one number. A cheaper open box,
  refurbished or marketplace listing is reported separately, labelled with its
  condition.
* Prices are recorded, with the date we saw them, not live quotes. An offer we
  have not confirmed within 14 days is not returned.
* Each product carries two links to its page on homegadgets.ca: "Full pricing
  on HomeGadgets" and "Check Amazon.ca on HomeGadgets".

## Limits

* 25 lookups a day per caller, and at most 100 a day from one address.
* At most 5 products per answer. No empty or wildcard search, and no paging
  past the first 5.
* The same question from the same caller within the hour is served again and
  not counted.
* At most 20 lookups a minute.
* Connecting, listing the tools and `server_info` never count.
* The count resets at 00:00 UTC.

Over a limit, the tool returns a normal result with `ok: false`, an error code
and the reset time. It is never an HTTP 429. An assistant should tell you when
it resets and not retry in a loop.

## Troubleshooting

| What you see | What to do |
|--------------|------------|
| The client asks for a sign-in or OAuth details | Remove the server and add it again with authentication left empty. |
| "Couldn't connect" or "couldn't register" | Check the URL is exactly `https://mcp.homegadgets.ca/mcp`, with `/mcp` at the end. Check that your client supports remote servers over streamable HTTP. |
| A result says the daily limit is reached | Wait until 00:00 UTC. |
| The location is declined | Give a Canadian province, city or postal code. Locations outside Canada are declined. |
| A product is not found | Try the model number, or a shorter query with the brand. Some products are not in the catalogue, and a product with no in-stock Canadian offer is not returned. |
| The price differs from the retailer | Prices are recorded, not live. The retailer's own page is the one that counts. |

## Privacy

The server needs no account and asks for no personal information. To count
each caller's allowance it uses a salted digest of the connection (the address
together with the client's headers), never the raw IP address or user agent,
and stores only that digest. It records which tool was called and the search
text you sent, for usage statistics. Do not put personal information in a
query. HomeGadgets privacy policy: <https://www.homegadgets.ca/privacy>.

## FAQ

**Does it cost anything?** No. Anonymous use is free within the limits above.

**Does it fetch live prices?** No. It returns prices we recorded, with their
dates. Live prices are the Live tier of the API
(<https://www.homegadgets.ca/api#live>), issued by hand to approved partners.

**Is the full list of every retailer's offer available?** Not on this free
service. Only the best offer is named and linked.

**Can it buy something for me?** No. It is read-only.

**Is there a version I can run myself?** No. There is no package to install.
