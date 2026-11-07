# Guide d'entretien du site ve2cuy.github.io

Le site <https://ve2cuy.github.io/> est construit par GitHub Pages (Jekyll) à chaque
poussée sur `main`. Il n'y a rien à installer : on modifie des fichiers Markdown, on pousse, et le
site se met à jour en une ou deux minutes.

**Tout le contenu de l'accueil est dans `index.md`, en Markdown ordinaire.** Le fichier se lit tel
quel sur github.com; sur le site, un petit script (`assets/js/accueil.js`) en fait la mise en page
(vignettes, cartes, encadrés) en suivant quelques règles simples, décrites plus bas.

## Où se trouve quoi

| Fichier ou dossier | Rôle |
|---|---|
| `index.md` | **L'accueil** : en-tête, cours, émulateurs, atelier et auteur |
| `dessins/*.svg` | Les dessins des cartes et des sections |
| `Images/` | Les photos (auteur, breadboard-PC, centre de données) |
| `_config.yml` | Le titre du site, le menu du haut |
| `_layouts/`, `assets/` | Le thème, la mise en page de l'accueil et le tableau de bord (normalement, on n'y touche pas) |
| `assets/data/sessions.json` | Le calendrier de la session, pour le tableau de bord |
| `README.md` | La page du dépôt sur github.com |
| `outils/` | L'aperçu local (`outils/apercu.sh`), non publié |

## L'accueil : `index.md`

### L'en-tête

Les quatre lignes du haut du fichier, entre les deux `---`, remplissent l'en-tête :

```yaml
---
layout: accueil
bandeau: "cours · laboratoires · machines d'époque"
titre: "Microcontrôleurs, Serveurs et Orchestration."
accroche: "Arduino, serveurs, conteneurs, sécurité : le matériel de mes cours…"
image: Images/moi.jpg
image_ronde: true
---
```

`layout: accueil` doit rester tel quel. Les initiales des mots du titre (de quatre lettres et
plus) sont mises en couleur automatiquement. Le tableau de bord de la session s'ajoute à droite.

### Les règles de mise en page

| Ce qu'on écrit en Markdown | Ce que le site affiche |
|---|---|
| `## Titre` | Une section, séparée des autres par un trait |
| `## C) Titre` (une lettre majuscule et une parenthèse) | Une section lettrée, avec sa vignette dans la rangée du haut |
| Juste sous le titre : `![](dessins/nom.svg) *Description*` | Le dessin de la section, à côté du titre; la description sert à la vignette du haut |
| Une liste dont chaque élément commence par un dessin | Des cartes de documents, cinq par rangée |
| Une liste dont chaque élément commence par `**Libellé**` | Des encadrés « libellé / valeur » (programme, pondération, courriel…) |
| Un paragraphe qui ne contient qu'une photo | La photo ronde, avec le paragraphe suivant à côté |
| Un paragraphe qui ne contient que des liens, séparés par `·` | Des boutons |
| Tout le reste (paragraphes, listes ordinaires, **gras**, liens) | Du texte normal |

### Une carte de document

Une carte, c'est **une ligne de liste** :

```markdown
- ![](dessins/conteneur.svg) 420-4D4 · [Conteneurs et orchestration](https://ve2cuy.github.io/4204d4/)
```

| Partie | Effet |
|---|---|
| `![](dessins/conteneur.svg)` | Le dessin (obligatoire, en premier); liste des dessins plus bas |
| `420-4D4` | Le numéro (un code de cours, ou 1 à 4 lettres ou chiffres), suivi de ` · `; `+` pour un élément sans numéro, `-` pour n'en afficher aucun |
| `[Titre](lien)` | Le titre et le lien : une adresse `https://…` ou une page du site |
| ` · 👍` | Facultatif : une petite étiquette (`👍`, `🧠`, `désuet`, `30 %`…) |

Sans lien (seulement du texte à la place de `[Titre](lien)`), la carte est grisée avec la mention
« sans page ». Une **sous-liste** (deux espaces puis `-`) ajoute une ligne de détails en petit :

```markdown
- ![](dessins/conteneur.svg) 420-4D4 · [Conteneurs et orchestration](https://ve2cuy.github.io/4204d4/)
  - Docker, Compose, Kubernetes
```

Les couleurs des dessins alternent d'elles-mêmes d'une carte à l'autre. Une liste dont toutes les
cartes sont numérotées par une seule lettre (`A`, `B`) s'affiche en grandes cartes; pour les garder
de la taille des autres, ajouter `grandes_cartes: false` dans l'en-tête d'`index.md`.

### Autres possibilités

| Ce qu'on écrit | Effet |
|---|---|
| `- ![Description](images/photo.jpg) - · [Titre](lien)` | Une carte avec une **photo** au lieu d'un dessin (toute image qui n'est pas dans `dessins/`) |
| `… · [Titre](lien) · étiquette · [Dépôt GitHub](https://github.com/…)` | Des **liens de plus** sur la carte, en boutons; le titre reste le lien principal |
| `-` à la place du numéro | Aucun numéro affiché sur le dessin |
| `420-1C4` comme numéro | Un code de cours sert aussi de numéro |
| `image_ronde: true` dans l'en-tête d'`index.md` | L'image de l'en-tête s'affiche en rond (pour une photo) |
| Un titre de plus de 30 caractères | Il s'affiche un peu plus petit, pour rester moins haut que le tableau de bord |

Le menu du haut se règle dans `_config.yml` (sinon : ve2cuy.github.io, Documents, Enseignant) :

```yaml
navigation:
  - titre: "Cours"
    lien: "/#section-a"
  - titre: "Blogue"
    lien: "https://ve2cuy.github.io/blog/"
```

## Exemples

### Ajouter un cours

Dans la liste de la section A, à l'endroit voulu :

```markdown
- ![](dessins/bouclier.svg) 420-6E5 · [Sécurité des réseaux](https://ve2cuy.github.io/4206e5/)
  - Pare-feu, VPN et détection d'intrusion
```

### Ajouter un émulateur, avec le lien vers son dépôt

```markdown
- ![](dessins/micro-ordinateur.svg) - · [Apple II](https://ve2cuy.github.io/apple2-emu/) · micro-ordinateur · [Dépôt GitHub](https://github.com/ve2cuy/apple2-emu)
  - Apple II et IIe
```

### Ajouter un projet, avec une photo

Déposer la photo dans `Images/` (environ 720 px de large suffit), puis :

```markdown
- ![Le montage du projet](Images/mon-projet.jpg) - · [Mon projet](https://github.com/ve2cuy/mon-projet) · github · 2027
  - Une ligne de description
```

### Modifier, déplacer ou retirer une carte

- **Changer un titre ou une description :** modifier la ligne.
- **Changer l'ordre ou la section :** couper la ligne et la coller à sa nouvelle place.
- **Retirer une carte :** supprimer la ligne.

### Modifier le menu du haut

Dans `_config.yml`, la liste `navigation` : un `titre` et un `lien` par entrée. Les sections
lettrées A, B, C… ont les adresses `/#section-a`, `/#section-b`, etc.

## Les dessins

Dessins disponibles (`dessins/`) :

`accolades`, `autoscale`, `badge`, `balance`, `bande-del`, `bits`, `bouclier`, `bouton`, `capteur-sans-fil`, `carte-arduino`, `chat`, `cle`, `cle-a-molette`, `cluster`, `compose`, `conteneur`, `conteneur-vm`, `copier-coller`, `couches`, `coupe`, `crayon`, `disque`, `document`, `dossier-lien`, `drapeau`, `ecran-commande`, `eeprom`, `engrenage`, `enseignant`, `espaces`, `etiquette`, `feuilles`, `fiche-info`, `fiole`, `fureteur`, `horloge`, `infrarouge`, `jauge`, `lcd`, `lien`, `liste`, `livres`, `mallette`, `micro-ordinateur`, `microcontroleur`, `minuterie`, `mouvement`, `multi-services`, `nuage`, `oeil`, `ordinateur-central`, `plume`, `porte-documents`, `potentiometre`, `puce-del`, `registre`, `reseau`, `resistance-del`, `rfid`, `roue`, `serveur`, `solutions`, `station`, `structure`, `tableau-de-bord`, `telechargement`, `terminal`, `thermometre`, `uart`, `wifi`, `yaml`.

Sur github.com, ils s'affichent en bleu; sur le site, ils prennent les couleurs du thème clair ou
sombre.

### Ajouter un dessin

Copier un fichier de `dessins/` sous un nouveau nom, par exemple `dessins/ingress.svg`, et
remplacer les formes. Le dessin occupe une surface de 200 × 100, en traits sans remplissage :

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 100" width="200" height="100" fill="none"
     stroke="#4a8fd0" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
  <rect x="70" y="26" width="60" height="48" rx="6"/><path d="M80 26v-9M120 26v-9"/>
</svg>
```

Puis l'utiliser avec `![](dessins/ingress.svg)`. Les formes simples (`rect`, `circle`, `path`)
rendent le mieux; s'inspirer des dessins existants.

## Le tableau de bord de la session

Il lit `assets/data/sessions.json` (jours de classe et numéros de semaine de chaque session). À
chaque nouvelle session, refaire ce fichier avec l'outil du site ve2cuy.com
(`ve2cuy-site/tools/calendrier.py`, voir son README) à partir du PDF du calendrier du Cégep, puis
copier le même `sessions.json` ici.

Pour vérifier une date précise : <https://ve2cuy.github.io/?date=2027-03-31>.

## Aperçu local (valider avant de publier)

Le script `outils/apercu.sh` construit et sert le site sur le Mac avec la **même version de
Jekyll que GitHub Pages**, pour voir le résultat avant de pousser.

### Une seule fois

Installer Ruby par Homebrew (le Ruby fourni avec macOS est trop ancien) :

```bash
brew install ruby
```

Au premier lancement, le script installe lui-même les gemmes de GitHub Pages dans
`~/.gem/pages` (quelques minutes; rien n'est installé dans le système).

### À chaque séance

Depuis le dossier du dépôt :

```bash
outils/apercu.sh
```

puis ouvrir <http://127.0.0.1:4000/>. À chaque fichier enregistré (`index.md`, un dessin, `_config.yml`…), le site se
reconstruit en moins d'une seconde et la page ouverte se recharge seule. **Ctrl+C** arrête
l'aperçu.

Autres usages :

| Commande | Effet |
|---|---|
| `outils/apercu.sh 4001` | Aperçu sur un autre port (si 4000 est déjà pris) |
| `outils/apercu.sh --build` | Construit seulement le site dans `_site/` et s'arrête : pratique pour vérifier qu'il n'y a pas d'erreur avant de pousser |

Le tableau de bord se teste aussi en local : <http://127.0.0.1:4000/?date=2027-03-31>.

### Le contenu d'`outils/`

| Fichier | Rôle |
|---|---|
| `apercu.sh` | Le script : prépare Ruby, installe les gemmes au besoin, construit et sert le site |
| `Gemfile` | Les gemmes : `github-pages` (la même version de Jekyll que GitHub) et quelques bibliothèques retirées du Ruby récent |
| `apercu.yml` | Les extensions que GitHub Pages active d'office (pages Markdown sans en-tête, liens `.md` convertis en `.html`, titres tirés du premier titre) |
| `ruby4-compat.rb` | Comble l'écart entre ce Jekyll et le Ruby récent (méthodes `tainted?` et `untaint` retirées) |

### Ce qu'il faut savoir

- `_site/` (le site construit) et `.jekyll-cache/` ne vont pas dans Git (`.gitignore`).
- Une erreur dans un fichier s'affiche dans le terminal, avec son nom : la corriger,
  enregistrer, et l'aperçu repart.
- Le dossier `outils/` (le script, sa configuration et son `Gemfile`) n'est pas publié sur le site.
- Ce Jekyll est plus ancien que le Ruby de Homebrew : `outils/ruby4-compat.rb` et les gemmes
  supplémentaires du `Gemfile` comblent l'écart, pour l'aperçu seulement. GitHub, lui, construit
  le site dans son propre environnement.
- Dans de rares cas, une différence peut apparaître entre l'aperçu et le site publié : vérifier le
  site en ligne après chaque publication importante.

## Publier

```bash
git add -A
git commit -m "Ajout du cours 420-6E5"
git push
```

Le site se met à jour en une ou deux minutes (onglet **Actions** du dépôt pour suivre). Faire
Cmd+Maj+R dans le fureteur pour voir la nouvelle version.

Si GitHub envoie un courriel « deploy failed » alors que l'étape **build** a réussi, c'est
presque toujours un délai dépassé de son côté : dans **Actions**, ouvrir l'exécution et cliquer
**Re-run failed jobs**, ou simplement pousser le commit suivant.

Si l'étape **build** échoue, c'est en général une erreur dans l'en-tête d'`index.md` ou dans
`_config.yml` (guillemet oublié, indentation) : le message de l'onglet **Actions** donne le
fichier et la ligne. Si une carte ne s'affiche pas comme prévu, vérifier sa ligne : l'image doit
venir en premier, suivie du numéro et de ` · `.

