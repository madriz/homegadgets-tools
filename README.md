# HomeGadgets.ca Tools

[Français](README.fr.md)

> [!CAUTION]
> **EXPERIMENTAL SOFTWARE. USE AT YOUR OWN RISK.** Price Now is experimental and provided "as is", without warranty of any kind. HomeGadgets accepts no liability for any loss or damage arising from its download, installation or use, to the extent the law allows. The installer is not code-signed, so Windows will show a warning. Prices it returns may be wrong, incomplete or out of date: always check the retailer before you buy. Do not install it if you do not accept these terms.

[HomeGadgets.ca](https://www.homegadgets.ca) compares what Canadian retailers
charge for electronics and appliances, in Canadian dollars. This repository is
the public home of the tools that use that data outside the website: what each
one is, where it stands, how to install it, and what it sends.

There is no source code in this repository. The MCP server and the API are
hosted services, the extension is installed from the Chrome Web Store, and the
Price Now installer is attached to this repository's
[Releases](https://github.com/madriz/homegadgets-tools/releases).

## The tools

| Tool | Status | What it is | Page on homegadgets.ca |
|------|--------|------------|------------------------|
| **MCP server** | Live | A remote MCP server an AI assistant can call for Canadian prices. No key. | [/mcp](https://www.homegadgets.ca/mcp) |
| **Public API** | Live | A read-only REST API for Canadian prices: anonymous, free key, or Live tier. | [/api](https://www.homegadgets.ca/api) |
| **Browser extension** | Live in Chrome (0.4.5). Not in Edge Add-ons yet. | Click it on a Canadian retailer product page to see the lowest price we recorded. | [/extension](https://www.homegadgets.ca/extension) |
| **Price Now** (Windows) | **Experimental** | A Windows app that checks a product's price live, from your own computer. | [/apps/price-now](https://www.homegadgets.ca/apps/price-now) |
| **Android app** | Coming soon | Not available yet. | |

Every tool is read-only: it reports prices and links, and never places an
order. Every price is from a Canadian retailer or brand store, in CAD.

## MCP server

A remote [Model Context Protocol](https://modelcontextprotocol.io) server over
streamable HTTP. There is nothing to install.

```
https://mcp.homegadgets.ca/mcp
```

* **No key, no account, no signup.** Leave authentication empty.
* **Read-only.** It reports prices and links. It cannot place an order.
* **Canada only.** A request that names a location outside Canada is declined
  before any lookup.
* **Recorded prices, not live quotes.** Each price carries the date we
  recorded it. An offer we have not confirmed within 14 days is not returned.

**Add it to a client:** in any client that supports remote MCP servers, add a
new server (some clients call it a connector), paste the URL above and leave
authentication empty. The client then lists the four tools. A client that only
supports local servers it starts itself cannot use this endpoint.

**The four tools:**

| Tool | What it does |
|------|--------------|
| `search_products` | Free-text search (brand, model or name) with optional category, brand and price filters. Returns ranked matches, each with its best in-stock price and the retailer offering it. Location is optional; without one the result is national. |
| `get_price` | The best current in-stock offer for one product, identified by a keyword, a brand and model, a manufacturer part number, or a product id. A Canadian location (province, city or postal code) is required. |
| `compare_retailers` | For one product: the best price, the average, the highest, and how many retailers carry it. Location is optional. |
| `server_info` | The server version and what it does and does not support. |

**Limits (free, anonymous):**

* 25 lookups a day per caller, and at most 100 a day from one address.
* At most 5 products per answer.
* The same question again within the hour is free.
* Connecting and listing the tools never count.
* The count resets at 00:00 UTC. Over the limit, the tool returns a normal
  result that says when it resets, never an HTTP error.

Guide: [docs/mcp-server.md](docs/mcp-server.md).

## Public API

A read-only REST API. Full reference: <https://www.homegadgets.ca/api>.
Machine-readable: <https://www.homegadgets.ca/public/v1/openapi.json>.

| Access | How to get it | Allowance | What it returns |
|--------|---------------|-----------|-----------------|
| Anonymous | Nothing to ask for | 25 lookups a day per caller, at most 5 products per answer | Recorded prices: the two cheapest in-stock offers and a count of retailers |
| Free key | The form on [/api](https://www.homegadgets.ca/api) (name and email) | 500 lookups a day per key | Same as anonymous |
| Live tier | Issued by hand to approved partners, through [/contact](https://www.homegadgets.ca/contact) | Per key | A price fetched at the moment you ask, with the full per-retailer list (up to about 90 seconds) |

Search the catalogue:

```bash
curl "https://www.homegadgets.ca/public/v1/search?q=lg%2065%20inch%20tv&limit=5"
```

Best recorded price for one model number, deliverable in Ontario:

```bash
curl "https://www.homegadgets.ca/public/v1/price?mpn=98UT9000PUA&province=ON"
```

With a free key, send it in the `X-API-Key` header. Limits reset at 00:00 UTC.
Over the limit the API answers HTTP 429 with a `Retry-After` header and a JSON
body that says why.

Guide: [docs/public-api.md](docs/public-api.md).

## Browser extension

**HomeGadgets Price Check**, version 0.4.5, in the
[Chrome Web Store](https://chromewebstore.google.com/detail/homegadgets-price-check/lfmjfgondkackobifkklnajlinilaeel).
It is not in the Microsoft Edge Add-ons store yet.

**What it does:** on a product page at a Canadian retailer we follow, click its
icon. If we carry that product, the panel shows the lowest price we recorded
for a new unit, the retailer, and the date we saw it. A cheaper open box or
returned unit is shown separately and labelled. Where we have the history, it
also shows the lowest and highest new price over the last 90 days.

**What it does not do:** it does not run when a page loads, does not read the
pages you visit, does not change the page, does not touch a cart or checkout,
has no coupons, and puts no number on its icon.

**Recorded prices, not live.** Every price is one we recorded, with its date.
Check the retailer before you buy.

**Permissions:** `activeTab` (the one tab you clicked it on, after the click),
`scripting` (to read the product details that page publishes, after the click)
and `storage` (your language choice and a random number used for anonymous
usage counts, kept on your device). It asks for no access to any website.

**Privacy:** after a click on a retailer site we follow, it sends the page
address, the product details the page publishes, and a model number if the
page shows one. It counts five anonymous usage events, each the result of a
click. Some links are affiliate links. Full policy:
<https://www.homegadgets.ca/extension#privacy>.

Guide: [docs/browser-extension.md](docs/browser-extension.md).

## Price Now (Windows): Experimental

Read the caution notice at the top of this page before you download it.

**What it does:** searches the HomeGadgets catalogue and checks a product's
price live, from your own computer and your own internet connection, at the
moment you ask. A live check reads the retailer's own page, so it can take a
while, and some retailers do not answer.

**System requirements:** Windows 10 or Windows 11, 64-bit; Microsoft Edge
WebView2 (already in Windows 11; the installer downloads it if missing); about
90 MB for the installer; an internet connection whenever you use the app.
There is no Mac or Linux version.

**Download:** `HomeGadgets-windows-x64-setup.exe` from this repository's
[Releases](https://github.com/madriz/homegadgets-tools/releases). Each release
lists the file's SHA-256.

**Install:**

1. Download `HomeGadgets-windows-x64-setup.exe`.
2. Check the SHA-256 in PowerShell, from the folder you saved it to:
   `Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256`.
   Compare it with the value in the release notes. **If the checksum does not
   match, do not run it.**
3. Run it. The installer is not code-signed, so Windows shows "Windows
   protected your PC". Choose **More info**, then **Run anyway**.
   Step by step: [Windows protected your PC](docs/price-now.md#windows-protected-your-pc).
4. Read the notice on the installer's first screen and tick **I accept** to
   continue.

**First run:** search for a product by name, brand or model number. Each result
shows the price we recorded and its date. Choose **Price Now** on a result to
check it live.

**Limits:** 50 live checks a day; 100 catalogue searches a day per install.
Each version stops working on a set date (the first Sunday of the month after
it was built) and asks you to install the new one.

**Uninstall:** Settings > Apps > Installed apps > HomeGadgets > Uninstall.

**What it sends:** to the HomeGadgets server (`mcp.homegadgets.ca`): what you
typed in the search box or the product a live check is for, a random install id
made on your computer, and the app's name, version, build date and app
identifier. No account, name, email, location or browsing history. A live
check contacts the retailer's website directly from your computer, so that
retailer sees your IP address, as with any visit.

**Privacy:** [docs/price-now.md#privacy](docs/price-now.md#privacy) and
<https://www.homegadgets.ca/privacy>.

**Licence:** Price Now is free to download and use, and is not open source. It
ships under its own licence: [PRICE_NOW_LICENSE.md](PRICE_NOW_LICENSE.md).

Guide: [docs/price-now.md](docs/price-now.md).

## Android app

Coming soon.

## Security, contributing, changes

* Report a vulnerability: [SECURITY.md](SECURITY.md).
* Issues are welcome: [CONTRIBUTING.md](CONTRIBUTING.md).
* Changes: [CHANGELOG.md](CHANGELOG.md).
* Contact: <https://www.homegadgets.ca/contact>.

## Licence

The MIT licence in [LICENSE](LICENSE) covers the documentation in this
repository only. It does not cover the Price Now program or its installer
([PRICE_NOW_LICENSE.md](PRICE_NOW_LICENSE.md)), the HomeGadgets name and logo,
or the price data served by the MCP server and the API (see
<https://www.homegadgets.ca/terms>).

HomeGadgets is independent and is not affiliated with or endorsed by any
retailer or manufacturer. Product, brand and retailer names belong to their
owners.
