# Rosette
## Sommaire

1) Liste des fichiers contenant du contenu modifiable.
2) Mise en Production (Deployment).
3) Gestion du site
    1) Ajouter une page
    2) Changer une image

# 1 - Liste des fichiers contenant du contenu modifiable.
- [address.html](./address.html) : Page "Adresse".
- [index.html](./index.html) : Page principale (avec le caroussel).
- [help.html](./help.html) : Page "Ils nous ont aidés".
- [table.html](./table.html) : Page "La table".
- [vins.html](./vins.html) : Page "Les vins".
- [description.html](./description.html) : Page "Qui sommes nous?"
- [_config.yml](./_config.yml) : Contient des variables gloabales au site :
    - `title` : titre du site.
    - `instagram_url` : Adresse utilisé pour l'instagrame de rosette.
    - `facebook_url` : Adresse utilisée pour le facebook de rosette.
    - `description` : sert en partie pour le référencement.
    - `theme` & `plugins` ne doivent pas être modifié.
- [navigation.yaml](./_data/navigation.yaml) : Fichier qui décrit la barre de navigation. (cf Ajouter une page)
- [footer.html](./_includes/footer.html) : Fichier contenant le texte & les boutons du footer.
- [Dossier assets/](./assets/) : Dossier dans lequel on met les "assets" : images, css, fonts, tout ce qui est à "coté" de la page.
    - [assets/images/](./assets/images/) : Stocke toute les images dans ce dossier pour pouvoir les importer dans ton site.
    - [assets/fonts/](./assets/fonts/) : Vous n'avez pas besoin de vous en occuper sauf si vous souhaitez changer la police d'écriture.
    - [assets/css/](./assets/css/) : Vous n'avez pas besoin de vous en occuper. Ce sont toutes les feuilles de style du site.
- [_layouts/main.html](./_layouts/main.html) : Ce fichier est la base du theme si il y a une nouvelle feuille de style il faut l'ajouter ici. Vous n'avez pas à la modifier.
- [_data/menu_soir.yaml](./_data/menu_soir.yaml) : Modification du menu du soir.
- [_data/menu_midi.yaml](./_data/menu_midi.yaml) : Modification du menu du midi.
- [_data/menu_carte.yaml](./_data/menu_carte.yaml) : Modification du menu de la carte.

# 2 - Mise en production
Tout est automatique via `Github Action`.
Dès qu'un changement à été enregistré sur l'interface et `push` une action se lance et répercute les modifications sur le site en production.

# 3 - Gestion du site
## 1 - Ajouter une page
- Créer à la racine du dépot un nouveau fichier `.html` nommé après la page que vous souhaitez créer.
- Ajouter une entrée dans le fichier [navigation.yaml](./_data/navigation.yaml) précisant le titre de la page et l'url.
- Le fichier `html` nouvellement créé doit avoir une en-tête comme les autres fichier `html` cf [description.html](./description.html):
    - `layout: main`
    - `permalink:` url de la page
    - `title:` titre de la page 

## 2 - Changer une image
- Ajouter l'image souhaitée dans le dossier [images](./assets/images/).
- Vous pouvez ensuite faire référence à cette image dans n'importe quel fichier `.html` en face d'un champs `img` de préférence dans l'en-tête du fichier avec le lien suivant : `/assets/images/<nom-de-ton-image>`.

### Exemple : 
```html
---
layout: main
permalink: table
title: "À table!"
images:
  - ligne:
    - img: "/assets/images/ROSETTE_N1__2.jpg"
      alt: "belle assiette"
    - img: "/assets/images/ROSETTE_N1__5.jpg"
      alt: "belle assiette"
    - img: "/assets/images/ROSETTE_N1__7.jpg"
      alt: "belle assiette"
  - ligne:
    - img: "/assets/images/ROSETTE_N1__8.jpg"
      alt: "belle assiette"
    - img: "/assets/images/ROSETTE_N1__11.jpg"
      alt: "belle assiette"
    - img: "/assets/images/ROSETTE_N1__20.jpg"
      alt: "belle assiette"
---
<section>
    [...]
</section>
```
## 3 - Modifier les menus
Il y a 3 menu actifs décrits par ces fichiers:
- [menu_soir](_data/menu_soir.yaml)
- [menu_midi](_data/menu_midi.yaml)
- [menu_carte](_data/menu_carte.yaml)

Vous pouvez changer le contenu des variables dans le fichier de configuration correspondant mais attention les noms des variables sont importante. 

- `en-tete`: Est une liste des différents `titre` des menus exemple :
```yaml
en-tete:
  - titre: "A la carte de Rosette"
  - titre: "Nom du second menu"
  - titre: "Nom du troisième menu"
  [...]
```
- `date`: Date du menu
- `menus`: Les différentes déclinaisons des menu (`titre`), avec leur prix associés (`prix`) exemple :
```yaml
menus:
    - titre: "Entrée, plat, dessert"
      prix: "27€"
    - titre: "Entrée et plat"
      prix: "23€"
    - titre: "Plat et dessert"
      prix: "22€"
  [...]
```
- `temps`: Cet element est composé d'une liste de sections (Entrée, plats...), chacune de ces sections a un `titre` et une liste de `plats`. Chaque plat a un `titre` et un `prix`. Exemple : 
```yaml
temps:
    - section:
        - titre: "À GRIGNOTER" 
          plats: 
            - titre: "Rosette de Lyon"
              prix: "/6"
            - titre: "Paté en croûte cochon, canard, volaille, pickles"
              prix: "/10"
    - section: 
        - titre: "ENTRÉES"
          plats:
            - titre: "Tartare de boeuf, curry, citron vert, oignon frit"
              prix: "/12"
            - titre: "Carottes glacées au gingembre, condiment aux herbes"
              prix: "/9"
            - titre: "Oeuf mimosa, jaune d’oeuf confit, ciboulette (Retour du marché)"
              prix: ""
  [...]
```
- `footer`: Le texte en bas du menu peut être modifié grace à cette variable.