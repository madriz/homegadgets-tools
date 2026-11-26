# Installation des outils HomeGadgets

[English](../../README.md)

## Serveur MCP

Il n'y a rien à installer. Le serveur est distant :

```
https://mcp.homegadgets.ca/mcp
```

Transport : HTTP diffusable (streamable HTTP). Authentification : aucune.

Dans tout client qui accepte les serveurs MCP distants :

1. Ajoutez un serveur. Certains clients disent « connecteur » ou
   « intégration ».
2. Collez l'adresse ci-dessus.
3. Laissez l'authentification vide. N'entrez aucune clé et ne lancez aucune
   connexion.
4. Enregistrez. Le client affiche quatre outils : `search_products`,
   `get_price`, `compare_retailers` et `server_info`.

Limites : 25 recherches par jour par appelant, au plus 100 par jour depuis une
même adresse, au plus 5 produits par réponse. Le compte repart à 0 h UTC.
Page sur le site : <https://www.homegadgets.ca/fr/mcp>.

## API publique

Il n'y a rien à installer ; tout client HTTP convient. Adresse de base :

```
https://www.homegadgets.ca/public/v1
```

* **Anonyme :** rien à demander. 25 recherches par jour par appelant.
* **Clé gratuite :** remplissez le formulaire de
  <https://www.homegadgets.ca/fr/api> (nom et courriel). La clé n'est affichée
  qu'une fois : conservez-la. 500 recherches par jour. Envoyez-la dans
  l'en-tête `X-API-Key`.
* **Niveau Live :** clés remises à la main aux partenaires approuvés. Faites
  la demande par <https://www.homegadgets.ca/fr/contact>.

```bash
curl "https://www.homegadgets.ca/public/v1/search?q=lg%2065%20inch%20tv&limit=5"
curl -H "X-API-Key: VOTRE_CLE" "https://www.homegadgets.ca/public/v1/price?mpn=98UT9000PUA&province=ON"
```

## Extension de navigateur

HomeGadgets Price Check, version 0.4.5. Offerte dans Chrome ; pas encore dans
Microsoft Edge Add-ons.

1. Ouvrez la fiche dans Chrome :
   <https://chromewebstore.google.com/detail/homegadgets-price-check/lfmjfgondkackobifkklnajlinilaeel>
2. Choisissez **Ajouter à Chrome**, puis **Ajouter l'extension**.
3. Facultatif : épinglez-la depuis le menu des extensions (l'icône en forme de
   pièce de casse-tête).

Chrome 111 ou plus récent. Pour la retirer : clic droit sur son icône, puis
**Supprimer de Chrome**. Politique de confidentialité :
<https://www.homegadgets.ca/fr/extension#privacy>.

## Price Now (Windows)

> [!CAUTION]
> **LOGICIEL EXPÉRIMENTAL. UTILISATION À VOS PROPRES RISQUES.** Price Now est expérimental et fourni « tel quel », sans garantie d'aucune sorte. Dans la mesure permise par la loi, HomeGadgets n'accepte aucune responsabilité pour toute perte ou tout dommage découlant de son téléchargement, de son installation ou de son utilisation. Le programme d'installation n'est pas signé numériquement, donc Windows affichera un avertissement. Les prix qu'il donne peuvent être erronés, incomplets ou périmés : vérifiez toujours auprès du détaillant avant d'acheter. Ne l'installez pas si vous n'acceptez pas ces conditions.

Licence : [PRICE_NOW_LICENSE.fr.md](../../PRICE_NOW_LICENSE.fr.md) (pas la
licence MIT).

**Configuration requise :** Windows 10 ou Windows 11, 64 bits ; Microsoft Edge
WebView2 (déjà présent dans Windows 11 ; le programme d'installation le
télécharge s'il manque) ; environ 90 Mo ; une connexion Internet. Aucune
version pour Mac ni pour Linux.

1. Ouvrez les
   [versions publiées](https://github.com/madriz/homegadgets-tools/releases) de
   ce dépôt et téléchargez `HomeGadgets-windows-x64-setup.exe` depuis la plus
   récente. Notez le SHA-256 indiqué dans ses notes de version (aussi dans
   `SHA256SUMS.txt`).
2. Vérifiez le fichier avant de le lancer (voir ci-dessous).
3. Lancez-le et passez l'avertissement de Windows (voir ci-dessous).
4. Au premier écran du programme d'installation, lisez l'avis et cochez
   **J'accepte**. L'installation ne peut pas continuer sans cela.
5. Terminez l'installation et ouvrez HomeGadgets depuis le menu Démarrer.

Pour mettre à jour, installez la nouvelle version par-dessus l'ancienne. Pour
désinstaller : **Paramètres > Applications > Applications installées >
HomeGadgets > Désinstaller**.

### Windows a protégé votre ordinateur

Au lancement du programme d'installation, Windows peut afficher une fenêtre
bleue intitulée « Windows a protégé votre ordinateur » (Microsoft Defender
SmartScreen).

> **[Capture d'écran à venir : la fenêtre « Windows a protégé votre
> ordinateur » affichée pour `HomeGadgets-windows-x64-setup.exe`.]**

**Pourquoi elle apparaît :** le programme d'installation n'est pas signé
numériquement. Windows affiche cet avertissement pour les programmes qui ne
sont pas signés avec un certificat de signature de code et qu'il a rarement
vus. Cela ne veut pas dire que Windows a trouvé un virus.

**Vérifiez d'abord le fichier :**

1. Ouvrez PowerShell dans le dossier où vous avez enregistré le programme
   d'installation (par exemple, Téléchargements).
2. Exécutez :

   ```powershell
   Get-FileHash .\HomeGadgets-windows-x64-setup.exe -Algorithm SHA256
   ```

   La forme générale est `Get-FileHash <fichier> -Algorithm SHA256`.
3. Comparez la valeur `Hash` au SHA-256 des notes de version. Les majuscules
   et les minuscules ne comptent pas.

**Si la somme de contrôle ne correspond pas, ne l'exécutez pas.** Supprimez le
fichier et téléchargez-le de nouveau depuis les versions publiées de ce dépôt.
Si elle ne correspond toujours pas, écrivez-nous par
<https://www.homegadgets.ca/fr/contact>.

**Ensuite, pour le lancer :** dans la fenêtre d'avertissement, choisissez
**Informations complémentaires**, vérifiez que le nom du fichier est
`HomeGadgets-windows-x64-setup.exe`, puis choisissez **Exécuter quand même**.

### Premier lancement

Tapez le nom, la marque ou le numéro de modèle d'un produit. Chaque résultat
affiche le prix que nous avons relevé et sa date. Choisissez **Price Now** sur
un résultat pour le vérifier en direct. Limites : 50 vérifications en direct
par jour, 100 recherches par jour pour chaque installation. Chaque version
cesse de fonctionner à une date fixe, indiquée dans ses notes de version.

## Application Android

Bientôt.
