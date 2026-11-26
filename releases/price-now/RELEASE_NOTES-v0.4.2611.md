> [!CAUTION]
> **EXPERIMENTAL SOFTWARE. USE AT YOUR OWN RISK.** Price Now is experimental and provided "as is", without warranty of any kind. HomeGadgets accepts no liability for any loss or damage arising from its download, installation or use, to the extent the law allows. The installer is not code-signed, so Windows will show a warning. Prices it returns may be wrong, incomplete or out of date: always check the retailer before you buy. Do not install it if you do not accept these terms.

> [!CAUTION]
> **LOGICIEL EXPÉRIMENTAL. UTILISATION À VOS PROPRES RISQUES.** Price Now est expérimental et fourni « tel quel », sans garantie d'aucune sorte. Dans la mesure permise par la loi, HomeGadgets n'accepte aucune responsabilité pour toute perte ou tout dommage découlant de son téléchargement, de son installation ou de son utilisation. Le programme d'installation n'est pas signé numériquement, donc Windows affichera un avertissement. Les prix qu'il donne peuvent être erronés, incomplets ou périmés : vérifiez toujours auprès du détaillant avant d'acheter. Ne l'installez pas si vous n'acceptez pas ces conditions.

# HomeGadgets Price Now 0.4.2611 for Windows (Experimental)

A Windows app that searches the HomeGadgets catalogue and checks a product's
price live, from your own computer, at the moment you ask.

| | |
|---|---|
| File | `HomeGadgets-windows-x64-setup.exe` |
| Size | 93,831,026 bytes |
| SHA-256 | `23366368c86c319085a127efab24b7cd8ee8a660d32ff711273acc17d00d61c1` |
| Built | 2026-11-18 |
| Stops working | 2026-12-06, 00:00 local time |
| Code-signed | No |

## Before you run it

1. Check the file. In PowerShell, in the folder you saved it to:

   ```powershell
   Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256
   ```

   The value must equal the SHA-256 above (also in `SHA256SUMS.txt`).
   **If the checksum does not match, do not run it.**
2. Windows shows "Windows protected your PC" because the installer is not
   code-signed. Choose **More info**, then **Run anyway**.
3. On the installer's first screen, read the notice and tick **I accept**.

Step by step, with what to do if something goes wrong:
<https://github.com/madriz/homegadgets-tools/blob/main/docs/price-now.md>
(français : <https://github.com/madriz/homegadgets-tools/blob/main/docs/fr/installation.md#price-now-windows>).

## Requirements

Windows 10 or Windows 11, 64-bit. Microsoft Edge WebView2 (the installer
downloads it if missing). An internet connection. No Mac or Linux version.

## What is in this version

- Catalogue search with the price we recorded and its date.
- Price Now: a live check of a product's price at the retailers, from your
  computer.
- 50 live checks a day; 100 catalogue searches a day per install.
- English and French.

## Licence

Free to download and use. Not open source. No redistribution. No warranty and
no liability. It may stop working or expire without notice. Full text:
`PRICE_NOW_LICENSE.md` (attached) and
<https://github.com/madriz/homegadgets-tools/blob/main/PRICE_NOW_LICENSE.md>.
