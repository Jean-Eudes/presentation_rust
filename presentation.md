---
title: Une courte introduction à rust
sub_title: "Rust : Un équilibre entre performance et sécurité"
authors:
  - Jean-Eudes Couignoux
  - Youssef Nait Belkacem
---


Speakers
---

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

![](images/jean-eudes.jpeg)
_Jean-Eudes Couignoux (capco)_

<!-- column: 1 -->
![](images/youssef.jpeg)
_Youssef Nait Belkacem (freelance)_

<!-- end_slide -->

Programme
---

# Programme du workshop

  - Présentation des spécificités du langage
  - Live coding
  - Exercice
  
<!-- end_slide -->

Introduction
---

# Création d'une banque en ligne


<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

## fonctionnalité

- Créer un compte bancaire
- pouvoir faire des dépots et des retraits
- exposer avec une API REST
- utiliser une base de donnée in memory

<!-- column: 1 -->

## Contrainte technique

- empreinte écologique faible
- sûre en terme de mémoire
- performant
- langage simple et expressif

<!-- end_slide -->

Choix du langage - performance
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

Choix du langage - coût
---

# Estimation des couts sur aws lambda

Nombre de requête : 20 000 000.


| Name | Coût |
| ------ | ------ |
| Javascript | 8 736 $ |
| Scala | 20 000 $ |
| Python | 2 506.56 $ |
| Rust | 672 $ |

**lien vers l'étude** [](https://xebia.com/blog/aws-lambda-benchmarking/)
<!-- end_slide -->
Choix du langage - technique
---

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->
<!-- list_item_newlines: 1 -->

# Autres facteurs

## Gestion de la mémoire

- Gestion manuelle de la mémoire (C, C++)
- Tracing garbage collector (Java, node, ...)
- Reference Counting (Swift)


<!-- column: 1 -->
<!-- list_item_newlines: 1 -->
## Autres features
* Typage fort
* Utiliser par des acteurs de l'industrie
  * linux
  * amazon
  * microsoft
  * discord
* Large écosystème

<!-- reset_layout -->

Le compilateur de rust est responsable d'ajouter les instructions nécéssaire pour libérer la mémoire.
<!-- end_slide -->

Présentation rapide de l'écosystème
---

<!-- list_item_newlines: 1 -->
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
Découvrons rust ensemble
---

![](./images/mario-finite-state-machine.jpg)
**source** https://www.ashishvishwakarma.com/GoF-Design-Patterns-by-Example/State-Pattern/
<!-- end_slide -->
Récapitulatif : Gestion de la mémoire
---

# Concept clefs

## Ownership

- Chaque variable rust a **un et un seul** propriétaire.
- Une fois que la valeur a été transféré (move), elle ne peut plus être utilisée.

## Borrowing

- Les **références** permettent d'emprunter une valeur sans transférer la propriété.
- Il est possible de prêter **plusieurs fois** une variable en lecture.
- Il est possible de prêter **qu'une fois** une variable en écriture.
<!-- end_slide -->

Récapitulatif (struct)
---

```rust {1-4|6-22|all} +line_numbers
struct Person {
    name: String,
    age: u32,
    email: String,
}

impl Person {
    fn new(name: String, age: u32, email: String) -> Person {
        Person { name, age, email }
    }
    fn get_name(&self) -> &str {
        &self.name
    }
    fn set_email(&mut self, new_email: String) {
        self.email = new_email;
    }
}
```

<!-- end_slide -->

Récapitulatif (enum)
---

```rust {1-4|6-16|all} +line_numbers
enum Figure {
    Circle { radius: f64 },
    Square { side: f64 },
    Rectangle { width: f64, height: f64 },
}

impl Figure {
    fn perimeter(&self) -> f64 {
        match self {
            Figure::Circle { radius } => 2.0 * std::f64::consts::PI * radius,
            Figure::Square { side } => 4.0 * side,
            Figure::Rectangle { width, height } => 2.0 * (width + height),
        }
    }
}
```

<!-- end_slide -->

Les types de données algébriques
---

<!-- column_layout: [1, 2] -->

<!-- column: 0 -->
```rust
#[derive(Clone, PartialEq)]
enum Character {
    Mario,
    SuperMario,
    FireMario,
    CapeMario,
}
```

``` rust 
enum Food {
    MushRoom,
    Fire,
    Feather,
}
```

<!-- column: 1 -->
``` rust
impl Character {

    fn eat(&self, food: Food) -> Character {
        match (self, food) {
            (Mario, MushRoom) => SuperMario,
            (Mario | SuperMario | FireMario | CapeMario, Fire) => FireMario,
            (Mario | SuperMario | FireMario | CapeMario, Feather) => CapeMario,
            (_, MushRoom) => self.clone(),
        }
    }
    
}
```

<!-- end_slide -->
Gestions des erreurs en rust
---

# Type Option

Le type *Option* est utilisé pour représenter une valeur qui peut ou non exister. Il a deux variantes :

- ```Some(T)```
- ```None```


# Type Result
Le type *Result* est utilisé pour représenter le résultat d'une opération qui peut réussir ou échouer. Il a deux variantes :
- ```Ok(T)```
- ```Err(E)```

L'opérateur *?* est utilisé pour simplifier la gestion des erreurs lorsqu'on travaille avec des valeurs de type Result. Il permet de propager automatiquement les erreurs vers le code appelant.

``` rust
fn read_file(file_path: &str) -> Result<String, std::io::Error> {
    let content = std::fs::read_to_string(file_path)?;
    Ok(content)
}
```

<!-- end_slide -->
Le polymorphisme en rust (les traits)
---
``` rust
// Définition de la structure
struct Circle {
    radius: f64,
}

// Définition d'un trait nommé `Shape` avec une méthode `area`
trait Shape {
    fn area(&self) -> f64;
}

// Implémentation du trait `Shape` pour la structure `Circle`
impl Shape for Circle {
    fn area(&self) -> f64 {
        std::f64::consts::PI * self.radius * self.radius
    }
}
```
<!-- end_slide -->
Conclusion
---

- Des fonctionnalités hauts niveaux, avec les performance du C
- Un système de mémoire sûre, et sans surcout
- Un écosystème très riche
- Une courbe d'apprentissage rude.

<!-- end_slide -->
Lien vers le répository
---

![](./images/lien_kata.jpeg)
https://github.com/Jean-Eudes/handson_bank_account_rust
<!-- end_slide -->
Merci
---

![](./images/lien_devoxx.png)
