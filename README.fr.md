# Outils HomeGadgets.ca

[English](README.md)

> [!CAUTION]
> **LOGICIEL EXPÉRIMENTAL. UTILISATION À VOS PROPRES RISQUES.** Price Now est expérimental et fourni « tel quel », sans garantie d'aucune sorte. Dans la mesure permise par la loi, HomeGadgets n'accepte aucune responsabilité pour toute perte ou tout dommage découlant de son téléchargement, de son installation ou de son utilisation. Le programme d'installation n'est pas signé numériquement, donc Windows affichera un avertissement. Les prix qu'il donne peuvent être erronés, incomplets ou périmés : vérifiez toujours auprès du détaillant avant d'acheter. Ne l'installez pas si vous n'acceptez pas ces conditions.

[HomeGadgets.ca](https://www.homegadgets.ca/fr) compare les prix des
détaillants canadiens pour l'électronique et les électroménagers, en dollars
canadiens. Ce dépôt est la page publique des outils qui utilisent ces données
hors du site : ce que fait chacun, où il en est, comment l'installer et ce qu'il
envoie.

Ce dépôt ne contient aucun code source. Le serveur MCP et l'API sont des
services hébergés, l'extension s'installe depuis le Chrome Web Store, et le
programme d'installation de Price Now est joint aux
[versions publiées](https://github.com/madriz/homegadgets-tools/releases) de ce
dépôt.

## Les outils

| Outil | État | Ce que c'est | Page sur homegadgets.ca |
|-------|------|--------------|-------------------------|
| **Serveur MCP** | En service | Un serveur MCP distant qu'un assistant IA peut appeler pour obtenir des prix canadiens. Aucune clé. | [/fr/mcp](https://www.homegadgets.ca/fr/mcp) |
| **API publique** | En service | Une API REST en lecture seule pour les prix canadiens : anonyme, clé gratuite ou niveau Live. | [/fr/api](https://www.homegadgets.ca/fr/api) |
| **Extension de navigateur** | Offerte dans Chrome (0.4.5). Pas encore dans Edge Add-ons. | Cliquez-la sur la page d'un produit chez un détaillant canadien pour voir le prix le plus bas que nous avons relevé. | [/fr/extension](https://www.homegadgets.ca/fr/extension) |
| **Price Now** (Windows) | **Expérimental** | Une application Windows qui vérifie le prix d'un produit en direct, depuis votre propre ordinateur. | [/fr/apps/price-now](https://www.homegadgets.ca/fr/apps/price-now) |
| **Application Android** | Bientôt | Pas encore offerte. | |

Chaque outil est en lecture seule : il donne des prix et des liens, et ne passe
jamais de commande. Chaque prix vient d'un détaillant canadien ou d'une
boutique de marque, en dollars canadiens.

## Serveur MCP

Un serveur [Model Context Protocol](https://modelcontextprotocol.io) distant,
en HTTP diffusable (streamable HTTP). Il n'y a rien à installer.

```
https://mcp.homegadgets.ca/mcp
```

* **Aucune clé, aucun compte, aucune inscription.** Laissez l'authentification
  vide.
* **Lecture seule.** Il donne des prix et des liens. Il ne peut pas passer de
  commande.
* **Canada seulement.** Une demande qui nomme un lieu hors du Canada est
  refusée avant toute recherche.
* **Des prix relevés, pas des prix en direct.** Chaque prix porte la date où
  nous l'avons relevé. Une offre que nous n'avons pas confirmée depuis 14 jours
  n'est pas retournée.

**L'ajouter à un client :** dans tout client qui accepte les serveurs MCP
distants, ajoutez un serveur (certains clients disent « connecteur »), collez
l'adresse ci-dessus et laissez l'authentification vide. Le client affiche alors
les quatre outils. Un client qui n'accepte que les serveurs locaux qu'il lance
lui-même ne peut pas utiliser cette adresse.

**Les quatre outils :** `search_products` (recherche dans le catalogue),
`get_price` (la meilleure offre pour un produit, avec un lieu canadien
obligatoire), `compare_retailers` (meilleur prix, moyenne, prix le plus élevé
et nombre de détaillants pour un produit) et `server_info` (version et
capacités du serveur).

**Limites (gratuit, anonyme) :** 25 recherches par jour par appelant, et au
plus 100 par jour depuis une même adresse ; au plus 5 produits par réponse ; la
même question dans l'heure ne compte pas ; la connexion et la liste des outils
ne comptent jamais. Le compte repart à 0 h UTC. Une fois la limite atteinte,
l'outil donne une réponse normale qui indique l'heure de remise à zéro, jamais
une erreur HTTP.

## API publique

Une API REST en lecture seule. Référence complète :
<https://www.homegadgets.ca/fr/api>.

| Accès | Comment l'obtenir | Allocation | Ce qu'elle retourne |
|-------|-------------------|------------|---------------------|
| Anonyme | Rien à demander | 25 recherches par jour par appelant, au plus 5 produits par réponse | Prix relevés : les deux offres en stock les moins chères et le nombre de détaillants |
| Clé gratuite | Le formulaire de [/fr/api](https://www.homegadgets.ca/fr/api) (nom et courriel) | 500 recherches par jour par clé | Comme l'accès anonyme |
| Niveau Live | Remise à la main aux partenaires approuvés, par [/fr/contact](https://www.homegadgets.ca/fr/contact) | Par clé | Un prix obtenu au moment de la demande, avec la liste complète par détaillant (jusqu'à environ 90 secondes) |

```bash
curl "https://www.homegadgets.ca/public/v1/search?q=lg%2065%20inch%20tv&limit=5"
curl "https://www.homegadgets.ca/public/v1/price?mpn=98UT9000PUA&province=ON"
```

Avec une clé gratuite, envoyez-la dans l'en-tête `X-API-Key`.

## Extension de navigateur

**HomeGadgets Price Check**, version 0.4.5, dans le
[Chrome Web Store](https://chromewebstore.google.com/detail/homegadgets-price-check/lfmjfgondkackobifkklnajlinilaeel).
Elle n'est pas encore dans la boutique Microsoft Edge Add-ons.

Sur la page d'un produit chez un détaillant canadien que nous suivons,
cliquez son icône. Si nous avons ce produit, le panneau affiche le prix le plus
bas que nous avons relevé pour un appareil neuf, le détaillant et la date. Une
offre de boîte ouverte ou de retour moins chère est affichée à part, avec son
étiquette. Ce sont des prix relevés, pas des prix en direct : vérifiez auprès
du détaillant avant d'acheter.

Elle ne fait rien avant que vous cliquiez, ne lit pas les pages que vous
visitez, ne modifie pas la page et n'a aucune fonction de coupons.
Autorisations : `activeTab`, `scripting` et `storage` ; aucun accès à un site
Web. Politique de confidentialité :
<https://www.homegadgets.ca/fr/extension#privacy>.

## Price Now (Windows) : expérimental

Lisez l'avis de mise en garde en haut de cette page avant de le télécharger.

Price Now cherche dans le catalogue de HomeGadgets et vérifie le prix d'un
produit en direct, depuis votre propre ordinateur et votre propre connexion
Internet, au moment où vous le demandez.

**Configuration requise :** Windows 10 ou Windows 11, 64 bits ; Microsoft Edge
WebView2 (déjà présent dans Windows 11 ; le programme d'installation le
télécharge s'il manque) ; environ 90 Mo pour le programme d'installation ; une
connexion Internet chaque fois que vous utilisez l'application. Il n'existe
aucune version pour Mac ni pour Linux.

**Installation :**

1. Téléchargez `HomeGadgets-windows-x64-setup.exe` depuis les
   [versions publiées](https://github.com/madriz/homegadgets-tools/releases).
2. Vérifiez le SHA-256 dans PowerShell, depuis le dossier où vous l'avez
   enregistré :
   `Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256`.
   Comparez-le à la valeur des notes de version. **Si la somme de contrôle ne
   correspond pas, ne l'exécutez pas.**
3. Lancez-le. Le programme d'installation n'est pas signé numériquement ;
   Windows affiche donc « Windows a protégé votre ordinateur ». Choisissez
   **Informations complémentaires**, puis **Exécuter quand même**. Étape par
   étape : [docs/fr/installation.md](docs/fr/installation.md).
4. Lisez l'avis du premier écran du programme d'installation et cochez
   **J'accepte** pour continuer.

**Limites :** 50 vérifications en direct par jour ; 100 recherches dans le
catalogue par jour pour chaque installation. Chaque version cesse de
fonctionner à une date fixe (le premier dimanche du mois qui suit sa
construction) et vous demande d'installer la nouvelle.

**Désinstallation :** Paramètres > Applications > Applications installées >
HomeGadgets > Désinstaller.

**Ce qu'elle envoie :** au serveur de HomeGadgets (`mcp.homegadgets.ca`), ce
que vous avez tapé ou le produit visé par une vérification en direct, un
identifiant d'installation aléatoire créé sur votre ordinateur, ainsi que le
nom, la version, la date de construction et l'identifiant de l'application.
Aucun compte, nom, courriel, emplacement ni historique de navigation. Une
vérification en direct communique directement avec le site du détaillant
depuis votre ordinateur ; ce détaillant voit votre adresse IP, comme pour toute
visite. Confidentialité : <https://www.homegadgets.ca/fr/privacy>.

**Licence :** Price Now est gratuit et n'est pas un logiciel libre. Il est
distribué sous sa propre licence :
[PRICE_NOW_LICENSE.fr.md](PRICE_NOW_LICENSE.fr.md).

## Application Android

Bientôt.

## Sécurité, contributions, modifications

* Signaler une vulnérabilité : [SECURITY.md](SECURITY.md).
* Les signalements de problèmes sont les bienvenus :
  [CONTRIBUTING.md](CONTRIBUTING.md).
* Modifications : [CHANGELOG.md](CHANGELOG.md).
* Nous joindre : <https://www.homegadgets.ca/fr/contact>.

## Licence

La licence MIT du fichier [LICENSE](LICENSE) couvre seulement la documentation
de ce dépôt. Elle ne couvre pas le programme Price Now ni son programme
d'installation ([PRICE_NOW_LICENSE.fr.md](PRICE_NOW_LICENSE.fr.md)), ni le nom
et le logo de HomeGadgets, ni les données de prix fournies par le serveur MCP
et l'API (voir <https://www.homegadgets.ca/fr/terms>).

HomeGadgets est indépendant et n'est affilié à aucun détaillant ni fabricant,
ni approuvé par eux. Les noms de produits, de marques et de détaillants
appartiennent à leurs propriétaires.
