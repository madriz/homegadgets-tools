# HomeGadgets public API

Status: live. Full reference: <https://www.homegadgets.ca/api>.
OpenAPI 3.1: <https://www.homegadgets.ca/public/v1/openapi.json>.
[Instructions en français](fr/installation.md#api-publique)

## Install

Nothing to install. Any HTTP client works. Base URL:

```
https://www.homegadgets.ca/public/v1
```

## Access levels

| Access | How to get it | Allowance | Returns |
|--------|---------------|-----------|---------|
| Anonymous | Nothing. No account, no email, no key. | 25 lookups a day per caller, at most 5 products per answer | Recorded prices: the two cheapest in-stock offers plus a count of Canadian retailers carrying the item |
| Free key | The form on <https://www.homegadgets.ca/api>: your name and email. The key is shown once; keep it. | 500 lookups a day per key, 30 a minute | Same answer shape as anonymous |
| Live tier | Keys are issued by hand to approved partners. Ask through <https://www.homegadgets.ca/contact> and say what you are building. | Per key | A price fetched at the moment you ask, with the full per-retailer offer list. A job can take up to about 90 seconds: submit it, then poll. See <https://www.homegadgets.ca/api#live>. |

## Use

Search the catalogue (free text):

```bash
curl "https://www.homegadgets.ca/public/v1/search?q=lg%2065%20inch%20tv&limit=5"
```

Best recorded price for one model number, limited to offers deliverable in
Ontario:

```bash
curl "https://www.homegadgets.ca/public/v1/price?mpn=98UT9000PUA&province=ON"
```

The same with a free key:

```bash
curl -H "X-API-Key: YOUR_KEY" "https://www.homegadgets.ca/public/v1/price?mpn=98UT9000PUA&province=ON"
```

`/public/v1/price` takes exactly one of `mpn` or `product_id`, and an optional
`province`. `/public/v1/search` takes `q`. Every endpoint and field is in the
reference above.

Every response carries `X-RateLimit-Limit`, `X-RateLimit-Remaining` and
`X-RateLimit-Reset` (seconds until reset).

## Troubleshooting

| Status | Meaning | What to do |
|--------|---------|------------|
| 400 | A parameter is missing or invalid, for example both `mpn` and `product_id`, or neither | Send exactly one identifier. |
| 404 | No product, or no in-stock Canadian offer for it | Resolve the identifier with `/public/v1/search` first. |
| 429 | A daily or per-minute limit is spent | Wait for `Retry-After`. A daily limit resets at 00:00 UTC. The JSON body says whether your own allowance or the shared service allowance is spent. |

Never retry in a tight loop: a spent daily limit does not free up before
00:00 UTC.

## Privacy

Anonymous use needs no account, email, name or key, and we store no personal
information to serve it. Callers are counted by a salted digest, never the raw
IP address. The free key is opt-in: the name and email you enter are kept with
the key, used only to reach you about that key, and never sold or shared. Keys
are stored as a hash, never the key itself. Do not put personal information in
a query string: parameters outside a fixed list are dropped. Full text:
<https://www.homegadgets.ca/api> and <https://www.homegadgets.ca/privacy>.

## FAQ

**Are the prices live?** Anonymous and free-key answers are recorded prices
with their dates. Only the Live tier fetches at the moment you ask.

**Why only two offers?** Two offers answer what it costs and who has it, and the
retailer count shows how deep the comparison is. The full per-retailer list is
part of keyed access.

**Can I request a key for someone else?** Request it for yourself, with your
own name and email. A key can be revoked.

**Is there an SLA?** No. The API is provided as is, and the terms at
<https://www.homegadgets.ca/terms> apply, including attribution.
