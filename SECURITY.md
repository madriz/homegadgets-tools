# Security policy

[Français](#politique-de-sécurité)

## Reporting a vulnerability

If you find a security problem in the HomeGadgets MCP server, the public API,
the HomeGadgets Price Check extension, the Price Now app or its installer, tell
us privately. Do not open a public issue for it.

Report it through the contact form at <https://www.homegadgets.ca/contact>.
Start the message with "Security report" and include:

* which tool and version it affects;
* what you found and what an attacker could do with it;
* the steps to reproduce it;
* how to reach you, if you want a reply.

Do not include personal information about anyone else, and do not send the
data you obtained.

## What to expect

We read every report and reply when you leave a way to reach you. When a fix
ships, it is listed in [CHANGELOG.md](CHANGELOG.md), with credit if you wish.

## Scope

In scope: `mcp.homegadgets.ca`, the `/public/v1` API on `www.homegadgets.ca`,
the extension as published in the Chrome Web Store, and the Price Now installer
published in this repository's Releases.

Please do not: run load or denial-of-service tests, try to get around the daily
limits at scale, access or change other people's data, or use social
engineering. Test only with your own accounts and keys.

## Verifying a Price Now download

The Price Now installer is not code-signed. Each release lists its SHA-256.
Check it before you run the file:

```powershell
Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256
```

If the checksum does not match, do not run it, and report it as above.

---

## Politique de sécurité

Si vous trouvez un problème de sécurité dans le serveur MCP de HomeGadgets,
l'API publique, l'extension HomeGadgets Price Check, l'application Price Now ou
son programme d'installation, signalez-le-nous en privé, par le formulaire de
contact : <https://www.homegadgets.ca/fr/contact>. Commencez le message par
« Rapport de sécurité ». N'ouvrez pas de signalement public pour ce problème.

Le programme d'installation de Price Now n'est pas signé numériquement. Avant
de le lancer, vérifiez son SHA-256 avec
`Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256`. Si la
somme de contrôle ne correspond pas, ne l'exécutez pas.
