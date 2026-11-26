# HomeGadgets Price Now (Windows): Experimental

[Instructions en français](fr/installation.md#price-now-windows)

> [!CAUTION]
> **EXPERIMENTAL SOFTWARE. USE AT YOUR OWN RISK.** Price Now is experimental and provided "as is", without warranty of any kind. HomeGadgets accepts no liability for any loss or damage arising from its download, installation or use, to the extent the law allows. The installer is not code-signed, so Windows will show a warning. Prices it returns may be wrong, incomplete or out of date: always check the retailer before you buy. Do not install it if you do not accept these terms.

Page on the site: <https://www.homegadgets.ca/apps/price-now>.
Licence: [PRICE_NOW_LICENSE.md](../PRICE_NOW_LICENSE.md) (not the MIT licence).

## What it is

A Windows desktop app. It searches the HomeGadgets catalogue and shows the
price we recorded for each product, with its date. Its **Price Now** button
checks a product's price live: the app reads the retailers' own pages from your
computer and your internet connection, at the moment you ask, and shows what
they charge, cheapest first. Each live row says whether it was read from the
retailer just now or is a price we recorded, with the date.

## System requirements

* Windows 10 or Windows 11, 64-bit.
* Microsoft Edge WebView2. Windows 11 already has it. If it is missing, the
  installer downloads it, so the first install needs an internet connection.
* About 90 MB for the installer.
* An internet connection whenever you use the app.

There is no Mac or Linux version.

## Install

1. Open this repository's
   [Releases](https://github.com/madriz/homegadgets-tools/releases) and
   download `HomeGadgets-windows-x64-setup.exe` from the newest release. Note
   the SHA-256 printed in its release notes (also in `SHA256SUMS.txt` on that
   release).
2. Verify the file before you run it. See below.
3. Run it, and get past the Windows warning. See below.
4. On the installer's first screen, read the notice. Tick **I accept** to
   continue. The install cannot continue without it.
5. Finish the installer and open HomeGadgets from the Start menu.

To update, install the new version over the old one.

### Windows protected your PC

When you run the installer, Windows may show a blue window titled "Windows
protected your PC" (Microsoft Defender SmartScreen).

<!-- SCREENSHOT PLACEHOLDER: no screenshot of this warning for the Price Now
installer exists yet. The owner, or the installer lane, must capture it on a
clean Windows machine and save it as docs/images/smartscreen-price-now.png,
then replace this comment with:
![Windows protected your PC, with More info and Run anyway](images/smartscreen-price-now.png)
-->
> **[Screenshot to come: the "Windows protected your PC" window shown for
> `HomeGadgets-windows-x64-setup.exe`.]**

**Why it appears:** the installer is not code-signed. Windows shows this
warning for programs that are not signed with a code-signing certificate and
that it has not seen often. It does not mean Windows found a virus.

**Check the file first.** Before you continue, confirm the file is the one we
published:

1. Open PowerShell in the folder you saved the installer to (for example,
   your Downloads folder).
2. Run:

   ```powershell
   Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256
   ```

   The general form is `Get-FileHash <file> -Algorithm SHA256`.
3. Compare the `Hash` value with the SHA-256 in the release notes. Case does
   not matter.

**If the checksum does not match, do not run it.** Delete the file and download
it again from this repository's Releases page. If it still does not match,
tell us through <https://www.homegadgets.ca/contact>.

**Then, to run it:** in the warning window, choose **More info**, check that
the file name is `HomeGadgets-windows-x64-setup.exe`, then choose
**Run anyway**.

## First run

1. Open HomeGadgets.
2. Type a product name, brand or model number in the search box.
3. Each result shows the price we recorded and its date.
4. Choose **Price Now** on a result to check it live. A live check waits on the
   retailers and can take a while. It covers only the retailers that answer at
   that moment.

## Limits

* 50 live checks a day.
* 100 catalogue searches a day for each install, and further limits by address
  and in total on our server.
* Each version stops working at 00:00, your computer's local time, on the first
  Sunday of the month after the month it was built in, and asks you to install
  the new one. The date is in each release's notes. HomeGadgets can also switch
  the app off at any time.
* Some retailers refuse automated page reads or change their pages; then a live
  check fails or finds nothing.
* Taxes, delivery, installation and fees are not included unless the app says
  so. Stock is not guaranteed.

## Uninstall

Settings > Apps > Installed apps > HomeGadgets > Uninstall.

## Troubleshooting

| What you see | What to do |
|--------------|------------|
| "Windows protected your PC" | See [Windows protected your PC](#windows-protected-your-pc). Verify the SHA-256 first. |
| The installer stops at the notice | Tick **I accept**. The install cannot continue without it. |
| The app says this version has stopped working | Download and install the newest release. Changing your computer's date does not keep an expired version working. |
| A live check finds nothing for a retailer | That retailer did not answer or refused the read. Try again later, or check the retailer's page. |
| The daily limit is reached | Live checks and searches reset at 00:00 UTC. |
| The installer fails on WebView2 | Connect to the internet and run the installer again, or install Microsoft Edge WebView2 from Microsoft first. |

## Privacy

To the HomeGadgets server (`mcp.homegadgets.ca`), with each request, the app
sends:

* what you typed in the search box, or the product a live check is for;
* a random install id, made on your computer the first time the app starts;
* the app's version, its build date, an app identifier (not a password; it only
  counts the app's searches against its own allowance) and the name of the app.

There is no account. The app sends no name, email address, location or browsing
history, and the language you choose stays on your computer.

A live check contacts the retailer's website directly from your computer and
your internet connection, the same way your browser would. That retailer sees
your IP address, as with any visit.

Retailer links go through homegadgets.ca. Some are affiliate links, and
HomeGadgets may earn a commission if you buy; it costs you nothing extra and
never changes which price is shown or the order. The Amazon button opens the
product's page on homegadgets.ca at its Amazon section, never Amazon directly.

HomeGadgets privacy policy: <https://www.homegadgets.ca/privacy>.

## FAQ

**Is it free?** Yes. It is free to download and use. It is not open source.

**Why is it called experimental?** It is early software. It may misbehave, and
its live checks depend on retailer pages that change.

**Why is the installer not signed?** It ships unsigned for now. The SHA-256 in
the release notes lets you check the file you downloaded.

**Why did my version stop working?** Each version stops on a set date (in its
release notes). A new version is published before that date; install it.

**Is there a Mac or Linux version?** No.

**Can I redistribute the installer?** No. See
[PRICE_NOW_LICENSE.md](../PRICE_NOW_LICENSE.md).
