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
Le "Heat" désigne la séance d'échauffement que le trotteur effectue sur la piste officielle, généralement 30 à 60 minutes avant la course.

Il est suivi des "Canters" (derniers réglages quelques minutes avant le départ) et des "Essais de départ".

**Objectif de l'observation :**
* Vérifier la souplesse et la régularité de l'allure (carré d'allures).
* Juger de l'envie du cheval (mordant, détendu ou nerveux).
* Valider les réglages de matériel (enrênement, ferrure).

Au Trot, c'est crucial car un cheval "boiteux" ou "raide" à l'échauffement a une probabilité de disqualification (DAI) très élevée, même s'il est favori au papier.

## 2. Usage Algorithmique (Feature Engineering)

La difficulté réside dans la transformation d'impressions subjectives en variables numériques.

### A. Analyse de Sentiment (NLP sur Commentaires)
Si tu récupères les commentaires textuels des journalistes de piste (ex: "Très souple", "A fait une faute", "Tire beaucoup"), tu peux appliquer du **Sentiment Analysis**.
* **Scoring :** Attribuer un score de Heat (-1.0 à +1.0).
    * *Exemple :* "Vole sur la piste" = +0.9 | "Reste là" = -0.5 | "Carré" = +0.5.
* **Feature :** `Heat_Sentiment_Score`.

### B. Comparaison Différentielle (Le "Delta Heat")
Un mauvais heat n'est pas grave si le cheval a *toujours* de mauvais heats mais gagne quand même. L'information, c'est le changement.
* **Baseline :** Créer un "profil d'échauffement" pour chaque cheval.
* **Feature :** $$Delta_{Heat} = \text{Score}_{Aujourd'hui} - \text{Moyenne}(\text{Scores}_{Passés})$$
    * Si $Delta_{Heat} > 0$ alors le cheval est "sur la montante".

### C. Les Essais de Départ (Spécifique au Trot)
Pour les courses avec départ à la volte (Volt Start), les drivers font des essais de "virage" et de mise en jambes.
* **Variable Binaire :** `Start_Failure` (0 ou 1). Si le cheval fait une faute (galop) pendant l'essai de départ, la probabilité de faute en course augmente drastiquement (stress, mauvais réglage).

### D. Indicateurs Physiques (Si Tracking disponible au Heat)
Certains systèmes de tracking commencent à enregistrer le heat.
* **Vitesse de Heat :** Un heat effectué à une vitesse anormalement élevée peut indiquer une sur-préparation (risque de fatigue) ou une volonté de "déboucher" le cheval.

## 3. Sources et Références

* **Terminologie des commentateurs :**
    * *"Il s'est coupé"* (atteinte entre les membres -> risque de galop).
    * *"Il a du gaz"* (beaucoup d'énergie).
    * *"Il est d'un seul bat"* (raideur).
* **Experts Piste :**
    * Les pronostiqueurs "piste" (souvent anciens drivers) ont un vocabulaire spécifique qu'il faut mapper (dictionnaire de synonymes pour ton NLP).
* **Articles Connexes :**
    * [[Analyse de Sentiment pour le Turf]] (À créer)
    * [[Types de Départ : Volte vs Autostart]] (L'impact du heat diffère selon le départ)