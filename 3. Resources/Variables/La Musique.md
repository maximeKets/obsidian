---
tags:
  - type/variable
  - context/hippique
  - category/market
format: float
unit: eur
importance: high
---
## 1. Définition
La "Musique" est la représentation codée des dernières performances d'un cheval, lue de la plus récente (à gauche) à la plus ancienne.

**Structure standard :** `[Classement][Discipline] [Classement][Discipline] ...`

**Légende (Spécifique Trot) :**
* **Chiffres (1 à 9) :** La place à l'arrivée.
* **0 :** Non placé (au-delà de la 9ème place ou 10ème selon les sources).
* **D :** Disqualifié (pour allures irrégulières - galop ou amble).
* **T :** Tombé / Arrêté.
* **a :** Attelé (Sulky).
* **m :** Monté (Jockey sur le dos).
* **(25) :** Changement d'année (indique que les perfs suivantes datent de 2025).

*Exemple :* `1a Da 2m (25) 0a`
*Lecture :* Vient de gagner à l'attelé, a été disqualifié à l'attelé juste avant, a fini 2ème au monté, et (en 2025) a fini non placé à l'attelé.

## 2. Usage Algorithmique (Feature Engineering)

La donnée brute (String) est inutilisable telle quelle par un modèle (Random Forest ou Réseau de Neurones). Il faut l'encoder.

### A. Filtrage Contextuel (Le piège de la polyvalence)
Un cheval peut être un champion au "Monté" et médiocre à l'"Attelé".
* *Règle :* Si la course à prédire est de l'Attelé, il faut pondérer à la baisse (ou exclure) les performances finissant par `m` dans la musique.
* *Feature :* `WinRate_SameDiscipline` vs `WinRate_Global`.

### B. Le Cas des Disqualifications ("D")
Au trot, un "D" n'est pas toujours synonyme de mauvaise performance (contrairement à un "0").
* **Le "D" de vitesse :** Un cheval qui galope car il va trop vite ou est poussé à la faute par le driver a souvent un gros potentiel physique ("La vitesse est là, la sagesse manque").
* **Le "D" de fatigue :** Un cheval qui galope en fin de parcours car il n'en peut plus.
* *Feature :* **Taux de Fiabilité.** $$Reliability = \frac{N_{courses} - N_{Disqualifications}}{N_{courses}}$$
* *Usage :* Un cheval avec une fiabilité faible mais de bonnes places quand il reste au trot (ex: `1a Da 1a Da`) est un **Outsider spéculatif** (Tout ou Rien).

### C. Pondération Temporelle (Recency Bias)
Une victoire il y a 2 semaines vaut plus qu'une victoire il y a 6 mois.
* *Méthode :* Appliquer une **décroissance exponentielle** aux performances passées.
* *Formule Score de Forme :* $$Score = \sum_{i=1}^{n} \frac{Performance_i}{Place_i} \times e^{-\lambda \cdot Temps_i}$$

### D. Normalisation par la "Valeur" de la course
Une victoire (`1a`) à l'hippodrome de Carpentras n'a pas la même valeur mathématique qu'une victoire (`1a`) à Vincennes.
* *Feature avancée :* Ne jamais utiliser le classement brut seul. Toujours le croiser avec l'**Allocation (Prix)** de la course ou le niveau du lot.
* *Performance Réelle :* $$\text{Perf\_Value} = \frac{1}{\text{Classement}} \times \log(\text{Allocation de la course})$$

## 3. Sources et Références

* **Bases de données officielles :**
    * *LeTrot.com :* La référence absolue pour la qualification des allures (D).
    * *IFCE :* Données institutionnelles.
* **Techniques ML :**
    * *Time Series Classification :* Littérature sur la classification de séquences temporelles.
    * *Entity Embedding of Categorical Variables (Guo/Berkhahn) :* Papier essentiel pour comprendre comment transformer des catégories ("1a") en vecteurs.
* **Articles Connexes :**
    * [[Allocation et Niveaux de Course]] (À créer - pour pondérer la musique)
    * [[Ecarts et Gestion de Bankroll]] (L'importance de la musique dans la gestion des écarts)