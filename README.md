# Door Creator Blender

**GTA Door Creator - add-on Blender (Sollumz)**

Crée des **portes GTA V / FiveM** directement dans Blender : pivot sur la charnière, collision, archétype YTYP avec les bons flags de porte, son de porte GTA, et une **ressource FiveM prête** à mettre sur ton serveur.

<p align="center"><img src="docs/panel.png" alt="Door Creator panel in Blender" width="380"></p>

*English version below.*

---

## 🇫🇷 Tutoriel

### Ce qu'il faut

| | |
|---|---|
| **Blender** | 4.2 ou plus récent (testé sur 5.2) |
| **Sollumz** | installé et activé ([docs.sollumz.org](https://docs.sollumz.org)) |
| **PyMateria** | conseillé : Sollumz › Préférences › export **Native**, pour sortir directement des `.ydr` / `.ytyp` utilisables en jeu (Windows) |

### 1. Installer

1. Télécharge **`Door-Creator-Blender.zip`** dans la page **[Releases](../../releases/latest)** (ne le dézippe pas).
   *(ou : bouton vert **Code › Download ZIP**, dézippe, et re-zippe seulement le dossier `gta_door_creator`)*
2. Dans Blender : **Edit › Preferences › Add-ons**.
3. En haut à droite, menu **⌄** › **Install from Disk…** › choisis le `.zip`.
4. Coche **GTA Door Creator (Sollumz)**.
5. Dans la vue 3D, appuie sur **N** › onglet **Door Creator**.

> Mise à jour : désactive puis supprime l'ancienne version, installe le nouveau zip, redémarre Blender.

**Langue :** boutons **Auto / Français / English** en haut du panneau (Auto = langue de Blender).

### 2. Faire une porte

**① Ton modèle**
- Importe ou modélise ta porte, debout (Z en haut), puis **sélectionne-la** : un ou plusieurs mesh, ou un Drawable Sollumz déjà fait.
- Clique **Détection auto** : l'add-on devine le type (normale / coulissante / garage) et le côté de la charnière (à l'opposé de la poignée, sinon avec le nom `_l` / `_r`).

**② Réglages**
- **Nom** : le nom du modèle en jeu (évite les noms GTA vanilla comme `v_ilev_...`, sinon tu remplaces la porte d'origine partout).
- **Type** :
  - *Normale* → choisis la **charnière** Gauche / Droite.
  - *Coulissante* → direction Gauche / Droite / Haut.
  - *Garage* → Sectionnelle ou Enroulable.
- **Collision** : *Boîte (recommandé)* + matériau (bois, métal, verre…), *Garder la mienne*, ou *Aucune*.
- **Son** : *Auto* (le son GTA par défaut du type) ou un des 47 sons de portes GTA.
- **Distance LOD** : 100 m par défaut.
- **YTYP** : *Nouveau ytyp* ou **ton propre ytyp** (par ex. celui de ton MLO) - le bouton ⤓ à côté importe ton `.ytyp` avec Sollumz.
- Clique **Créer la porte** :
  - l'origine va sur la charnière (ou en bas au centre pour coulissante / garage) ;
  - le Drawable Sollumz est créé (matériaux convertis en shader Sollumz si besoin) ;
  - la boîte de collision est ajoutée ;
  - l'archétype YTYP est créé : flags `67239936` (Dynamic + Door Physics) et specialAttribute 7 / 8 / 10 / 5.

> Tu peux recliquer **Créer la porte** après avoir changé la charnière : l'origine se déplace.

**③ Aperçu**
- Le curseur **Ouverture** ouvre la porte dans Blender pour vérifier le sens (bouton ⇄ pour inverser, angle réglable).
- **Fermer** remet la porte fermée. En jeu, c'est le système de portes de GTA qui la bouge (sans script).

**④ Export**
- **Exporter la ressource FiveM** › choisis un dossier. Tu obtiens :

```
my_door/
├─ stream/
│  ├─ my_door.ydr
│  └─ my_door.ytyp        (ou TON ytyp + la porte)
├─ audio/
│  └─ my_door_game.dat151.rel   (le son)
├─ fxmanifest.lua
└─ README.txt
```

- Copie le dossier dans les `resources` de ton serveur, ajoute `ensure my_door` dans `server.cfg`, place `my_door` dans ton ymap / MLO avec CodeWalker.
- **Après chaque changement : déconnecte-toi et reconnecte-toi au serveur** (FiveM garde les fichiers en cache, un restart ne suffit pas).

> Si tu as exporté dans **ton ytyp**, ce fichier **remplace** l'original : enlève l'ancien de ta ressource MLO (ne streame jamais les deux).

> Si Sollumz sort des `.ydr.xml` / `.ytyp.xml` : active **Native (PyMateria)** dans les préférences de Sollumz, ou convertis les `.xml` avec CodeWalker.

### 3. Son seulement (porte déjà faite)

Pour donner un son GTA à des portes qui existent déjà (rien d'autre n'est exporté) :
1. **Portes** : tape les noms des portes (`porte_a, porte_b`) ou sélectionne-les et clique ➚.
2. **Son** : choisis le son.
3. **Fichier** : nom du fichier (`door_sounds`).
4. **Créer le fichier son** › choisis un dossier → `door_sounds_game.dat151.rel`.
5. Mets-le dans `audio/` de ta ressource et colle les lignes fxmanifest (déjà copiées, **Ctrl+V**) :

```lua
files {
  'audio/door_sounds_game.dat151.rel',
}
data_file 'AUDIO_GAMEDATA' 'audio/door_sounds_game.dat'
```

### Problèmes fréquents

| Problème | Solution |
|---|---|
| « Sollumz n'est pas activé » | Installe / coche Sollumz, puis réactive l'add-on |
| La porte tourne du mauvais côté | Change **Charnière** puis reclique **Créer la porte** |
| La porte n'a pas de son en jeu | Vérifie la ligne `AUDIO_GAMEDATA` (`.dat`, pas `.dat151.rel`) et reconnecte-toi |
| La porte ne bouge pas en jeu | Elle doit être **seule** (pas fusionnée avec le mur) et avoir sa collision |
| « has no Sollumz materials » | Reclique **Créer la porte** : l'add-on convertit les matériaux |

---

## 🇬🇧 Tutorial

### Requirements
Blender **4.2+** (tested on 5.2) · **Sollumz** enabled · **PyMateria** recommended (Sollumz › Preferences › **Native** export, Windows) so you get game-ready `.ydr` / `.ytyp`.

### Install
1. Download **`Door-Creator-Blender.zip`** from **[Releases](../../releases/latest)** (don't unzip it).
2. Blender › **Edit › Preferences › Add-ons** › **⌄** › **Install from Disk…** › pick the zip › enable **GTA Door Creator (Sollumz)**.
3. 3D view › **N** › **Door Creator** tab. Language: **Auto / Français / English** buttons at the top.

### Make a door
1. **Your model**: select your door (mesh(es) or a Sollumz Drawable), standing up (Z up) › **Auto detect** (type + hinge side, opposite the handle).
2. **Settings**: name (avoid vanilla names), type (hinged › hinge left/right · sliding › left/right/up · garage › sectional/roll-up), collision (box + material), GTA door sound (Auto or one of 47), LOD distance, **YTYP** (new, or your own ytyp e.g. your MLO's - ⤓ imports it with Sollumz) › **Make the door**: origin on the hinge, Sollumz Drawable, box collision, YTYP archetype (flags `67239936`, specialAttribute 7/8/10/5).
3. **Preview**: the **Open** slider swings the door in Blender (⇄ flips it). In-game the GTA door system moves it, no script.
4. **Export FiveM resource** › pick a folder → `stream/` (.ydr + .ytyp), `audio/` (sound), `fxmanifest.lua`. Copy it to your server resources, `ensure` it, place the model in your ymap / MLO. **Disconnect and reconnect** after every change.

### Sound only (door already made)
Doors (type the names or pick the selection) › Sound › File › **Make the sound file** → `<file>_game.dat151.rel` + the fxmanifest lines copied to the clipboard.

---

## Structure

```
gta_door_creator/__init__.py   l'add-on / the add-on
README.md                      ce tuto / this tutorial
.github/workflows/release.yml  tag vX.Y.Z -> Release with Door-Creator-Blender.zip
```

Licence MIT · par **byfred** · fait avec [Sollumz](https://github.com/Sollumz/Sollumz).
