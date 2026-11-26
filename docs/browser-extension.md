# HomeGadgets Price Check (browser extension)

Status: live in the Chrome Web Store, version 0.4.5. Not in the Microsoft Edge
Add-ons store yet. Page on the site: <https://www.homegadgets.ca/extension>.
[Instructions en français](fr/installation.md#extension-de-navigateur)

## Install

1. Open the listing in Chrome:
   <https://chromewebstore.google.com/detail/homegadgets-price-check/lfmjfgondkackobifkklnajlinilaeel>
2. Choose **Add to Chrome**, then **Add extension**.
3. Optional: pin it. Open the puzzle-piece menu in the toolbar and choose the
   pin next to HomeGadgets Price Check.

Requires Chrome 111 or later. English and French; switch from the panel.

To remove it: right-click its icon and choose **Remove from Chrome**.

## Use

1. Open a product page at a Canadian retailer.
2. Click the HomeGadgets icon.
3. If we carry that product, the panel shows:
   * the lowest price we recorded for a new unit, the retailer and the date;
   * a link to that retailer (nothing happens until you click it);
   * a cheaper open box or returned unit, if there is one, shown separately and
     labelled;
   * where we have the history, the lowest and highest new price over the last
     90 days;
   * a "Check price on Amazon.ca" button, which opens our own product page, not
     an Amazon site.

The prices are records, not live quotes. Check the retailer's page before you
buy.

What it does not do: it does not run when a page loads, does not read the pages
you visit, does not change the page, does not touch a cart or checkout, has no
coupon feature, and puts no number on its icon.

## Permissions

| Permission | Why |
|------------|-----|
| `activeTab` | Lets it see the one tab you clicked it on, only after you click. |
| `scripting` | Lets it read the product details that page publishes for search engines, after the click. |
| `storage` | Keeps your language choice and a random number used for anonymous usage counts, on your device. |

It asks for no access to any website.

## Troubleshooting

| What you see | What to do |
|--------------|------------|
| The panel says the site is not one we follow | The extension reads nothing and sends nothing on sites we do not follow. |
| The product is not recognised | The page may not publish a model number or product data, or we may not carry it. Search for it on <https://www.homegadgets.ca>. |
| The price differs from the retailer | Prices are recorded, with their date. The retailer's page is the one that counts. |
| Nothing happens on click | Reload the page and click again. Check the extension is enabled in `chrome://extensions`. |

## Privacy

Only after you click, and only on a retailer site we follow, it sends: the
address of that product page, the product details the page publishes, and one
short piece of text if the page shows a model number. If we recognise the
product, it also asks for the 90-day range, and that request carries only our
own product identifier.

It counts five anonymous usage events, each the result of a click, keyed to a
random number made on your device. It never sends your browsing history,
anything you type, your location, your name or your email. It sets no cookie.

Some links in the panel are affiliate links: HomeGadgets may earn a commission
if you buy. It costs you nothing and does not change what is shown.

Full policy: <https://www.homegadgets.ca/extension#privacy>.

## FAQ

**Does it work in Microsoft Edge?** It is not in the Edge Add-ons store yet.

**Does it check prices live?** No. It shows prices we recorded, with their
dates.

**Can I turn off the usage counts?** There is no setting. They are only sent
after a click; to stop them, do not click the icon, or remove the extension.

**Does it apply coupons?** No, and it has no coupon feature.
