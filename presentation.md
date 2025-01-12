---
title: Une courte introduction à rust
sub_title: "Rust : Un équilibre entre performance et sécurité"
author: Jean-Eudes Couignoux
---

Introduction
---

# Création d'une banque en ligne

## fonctionnalité

  - Créer un compte bancaire
  - pouvoir faire des dépots et des retraits
  - avoir des notifications SMS et ou mail pour chaque opération
  - avoir des comptes bancaires avec ou sans découvert
  - exposer avec une API REST


## Contrainte technique

  - empreinte écologique faible
  - sûre en terme de mémoire
  - performant
  - langage simple et expressif

<!-- end_slide -->

Choix du langage
---

# Etudes des performances de différents langages

| Name | Energy| Temps | Mémoire |
| ------ | ------ | ----- | ------ |
| C | 1.0 | 1.0 | 1.24 |
| Javascript | 4.45 | 6.52 | 4.59 |
| Java | 1.98 | 1.89 | 6.01 |
| Python | 75.88 | 71.90 | 2.80 |
| Rust | 1.03 | 1.04 | 1.54 |

**lien vers l'étude** [](https://repositorio.inesctec.pt/server/api/core/bitstreams/d606d7dd-be10-4bc7-ada6-5c0c91fe1afb/content)

<!-- end_slide -->

Choix du langage
---

# Autres facteurs

## Gestion de la mémoire

  - Gestion manuelle de la mémoire (C, C++)
  - Ramasse miette (GC) (Java, node, ...)
  - Comptage de référence (Swift)

Le compilateur de rust est responsable d'ajouter les instructions nécéssaire pour libérer la mémoire.

## Autres features
  * Typage fort
  * Utiliser par des acteurs de l'industrie
  * Large écosystème

<!-- end_slide -->

Présentation rapide de l'écosystème
---

# Outil de build

  - rustup
  - cargo
  - clippy
  - fmt

# Librairies

  - https://crates.io/
  - https://blessed.rs/crates

# IDE
  - helix
  - vscode
  - rustrover (jetbrains)
  - ...

<!-- end_slide -->

Codons un peu
---


<!-- end_slide -->

Gestion de la mémoire
---

<!-- end_slide -->

