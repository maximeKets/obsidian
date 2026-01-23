---
tags:
  - type/variable
  - context/hippique
  - category/course
format: integer
unit: eur
importance: high
---

## 1. Définition
Les **Mouvements de Cote** représentent la fluctuation de la valeur de gain potentiel d'un cheval au fil du temps (de l'ouverture des paris jusqu'au départ de la course).

La **Masse** (ou *Enjeux*) désigne le volume total d'argent parié sur la course.
* **Contexte PMU (Pari Mutuel) :** Contrairement aux bookmakers à cote fixe, au PMU, les joueurs jouent les uns contre les autres. La cote est une résultante directe de la répartition de la masse.
* **Relation Cote/Masse :** Si beaucoup d'argent est placé sur le Cheval A, sa cote baisse. Si personne ne le joue, sa cote monte.
* **Formule de base :** $$\text{Cote} \approx \frac{\text{Masse Totale} \times (1 - \text{Prélèvement})}{\text{Masse sur le Cheval}}$$

## 2. Usage Algorithmique (Feature Engineering)

L'argent est souvent considéré comme de l'information ("Money talks"). Les mouvements de cote agrègent la sagesse de la foule et, plus important, l'information privilégiée.

### A. Détection du "Smart Money" (Argent Avisé)
L'objectif est de distinguer l'argent du "grand public" (souvent influencé par la presse) de l'argent des "initiés" (écuries, pros).
* **Indicateur de chute (Steamer) :** Un cheval dont la cote passe de 20/1 le matin à 8/1 juste avant le départ. C'est un signal fort de confiance de l'entourage.
    * *Feature :* $$Delta_{cote} = \frac{Cote_{ouverture} - Cote_{finale}}{Cote_{ouverture}}$$
* **Indicateur de dérive (Drifter) :** Un favori dont la cote monte (ex: de 2/1 à 5/1). Cela signale souvent un problème de dernière minute (échauffement médiocre, cheval nerveux).

### B. Dynamique Temporelle (Velocity)
Ce n'est pas seulement la baisse qui compte, mais *quand* elle se produit.
* **Early Money :** Argent placé dès l'ouverture (souvent des algos ou des pros préparés).
* **Late Money :** Argent placé dans les 2 dernières minutes. Au trot, c'est crucial car c'est souvent après le "Heat" (échauffement) que les pros jouent.
* *Feature :* Calculer la pente de la courbe de cote sur les 10 dernières minutes ($dCote/dt$).

### C. Analyse de la Confiance du Marché (Entropie)
Une course où tous les chevaux sont entre 5/1 et 10/1 est une course "ouverte" (incertaine). Une course avec un favori à 1.5/1 est une course "verrouillée".
* *Feature :* **Entropie de Shannon** des probabilités implicites. Plus l'entropie est élevée, plus le modèle doit être prudent (baisse de l'indice de confiance de la prédiction).

### D. Spécificité Trot : Le facteur "Déferrage"
Au trot, l'annonce tardive d'un déferrage (D4 ou DA) entraîne souvent des mouvements de masse violents.
* *Feature combinée :* Corréler le mouvement de cote avec le changement de statut de ferrure par rapport à la dernière course.


## 3. Sources et Références

* **Théorie Financière :**
    * *Hypothèse des marchés efficaces (EMH) :* Dans quelle mesure la cote finale reflète-t-elle la vraie probabilité de gagner ?
* **Auteurs Clés :**
    * *William Ziemba :* "Efficiency of Racetrack Betting Markets". C'est la référence académique sur l'analyse des cotes hippiques comme marché financier.
    * *Benter, Bill :* Légende des algos hippiques (Hong Kong), qui utilisait la cote publique comme une variable fondamentale de son propre modèle (modèle composite).