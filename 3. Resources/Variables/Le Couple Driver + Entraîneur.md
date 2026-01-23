---
tags:
  - type/variable
  - context/hippique
  - category/cheval
format: integer
unit: km/h
importance: high
---
## 1. Définition
Ce facteur analyse la performance et la stratégie des deux humains responsables du cheval :
* **L'Entraîneur :** Celui qui prépare le cheval au quotidien. Il connaît la forme physique réelle de l'animal.
* **Le Driver (ou Jockey au monté) :** Le pilote le jour J. Au trot, la "main" du driver est cruciale pour garder un cheval au trot.

**La nuance clé :** Souvent, l'entraîneur *est* le driver. Mais quand l'entraîneur (qui conduit moins bien) laisse sa place à un "Catch Driver" (un pilote mercenaire d'élite comme E. Raffin ou J.M. Bazire), c'est un signal fort d'intention de victoire.



## 2. Usage Algorithmique (Feature Engineering)

Il ne faut pas utiliser le nom des personnes (string) mais leurs statistiques.

### A. La Forme de l'Écurie (Entraîneur)
Les écuries fonctionnent par cycles (virus, mauvaise qualité du foin, ou au contraire pic de forme saisonnier).
* **Feature :** `Stable_Form_Index`
    * Pourcentage de réussite (dans les 3 premiers) de l'entraîneur sur les 30 derniers jours (tous chevaux confondus).
    * *Seuil d'alerte :* Si un entraîneur a 50 partants et 0 podiums ce mois-ci, il faut pénaliser tous ses chevaux (l'écurie est "malade").

### B. L'Impact du "Catch Driver" (Driver Change)
L'algorithme doit détecter l'amélioration du pilotage.
* **Feature :** `Driver_Switch_Bonus`
    * On compare le `WinRate` du driver d'aujourd'hui avec le `WinRate` du driver de la course précédente.
    * $$Delta_{Skill} = WinRate_{Driver\_Today} - WinRate_{Driver\_Previous}$$
    * Si $Delta_{Skill} > 0.15$ (ex: passage d'un apprenti à un Top Driver), la probabilité de victoire augmente significativement.

### C. La Synergie du Couple (Couple Success)
Certains drivers s'entendent parfaitement avec certains entraîneurs (habitudes de travail), ou avec un cheval spécifique (le driver connaît ses manies).
* **Feature :** `Couple_ROI` (Retour sur Investissement).
    * Est-ce que le couple *Entraîneur X + Driver Y* est rentable historiquement ?
    * *Exemple :* L'entraîneur X gagne peu, mais quand il appelle le driver Y, ils gagnent 40% du temps. C'est une info cachée critique.

### D. Le Coefficient de Réussite lissé (Bayesian Average)
Attention aux petits échantillons. Un driver qui a couru 1 course et gagné 1 fois a 100% de réussite. C'est trompeur comparé à un pro à 20% sur 1000 courses.
* **Formule :** Utiliser le **Lissage de Laplace**.
    * $$Score = \frac{Victoires + 1}{Courses + 2}$$
    * Cela évite les valeurs extrêmes (0% ou 100%) sur les faibles volumes.

## 3. Implémentation Technique

### Vectorisation (Embeddings)
Comme pour la "Musique", l'approche moderne consiste à utiliser des **Entity Embeddings**.
* Chaque Driver et Entraîneur est représenté par un vecteur (ex: dimension 10).
* Le réseau de neurones va apprendre à regrouper les drivers de même "style" ou de même "niveau" dans l'espace vectoriel.
* *Avantage :* Si un jeune driver commence à avoir les mêmes stats que "Bazire", le modèle le détectera via la proximité vectorielle, même s'il est peu connu.

### Gestion des ID
Il est impératif d'avoir une table de référence unique.
* *Problème :* "J.M. Bazire", "J-M. Bazire", "Jean-Michel Bazire" sont la même personne.
* *Solution :* Nettoyage strict des noms et attribution d'un `Driver_ID` unique integer avant l'entraînement du modèle.

## 4. Sources et Références

* **Concepts clés :**
    * *UDR (Universal Driver Rating) :* Standard utilisé aux USA/Suède pour noter les drivers (basé sur Victoires, 2ème, 3ème places pondérées).
        * Formule US : $\frac{9 \times 1st + 5 \times 2nd + 3 \times 3rd}{2 \times Starts}$
    * *L'écart du driver :* Suivre la "méforme" d'un driver (ex: 40 courses sans gagner). Au trot, la confiance du pilote influe sur sa main.
* **Articles Connexes :**
    * [[Embeddings pour variables catégorielles]] (Technique ML)
    * [[Analyse des Ecarts]] (Statistique pure)