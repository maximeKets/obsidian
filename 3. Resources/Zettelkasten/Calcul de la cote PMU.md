# Calcul de la cote PMU

## 🎯 Principe de base : la cote = reflet des mises

Le PMU n’**analyse pas** les chevaux pour “fixer” une cote, comme le ferait un bookmaker sur le foot.
C’est un **pari mutualisé** : la cote est **calculée à partir de la répartition des mises des parieurs**, en temps réel.

Autrement dit :
> plus un cheval reçoit d’argent misé sur lui, plus sa cote baisse.

---

## ⚙️ 1. Formule simplifiée de la cote PMU

Le PMU calcule les cotes à partir du **montant total des mises** après déduction du prélèvement de l’État et des frais de gestion.

Formule (version simplifiée) :

$$ \text{Cote du cheval} = \frac{\text{Mise totale (après prélèvement)}}{\text{Mise sur le cheval}} - 1 $$

### 🔢 Exemple concret :

* Total des mises (après prélèvements) : 100 000 €
* Mises sur le cheval n°5 : 25 000 €

$$ \text{Cote} = \frac{100 000}{25 000} - 1 = 3 $$

➡️ Le cheval n°5 a une **cote de 3/1** (ou “3 contre 1”)
→ cela correspond à environ **25 % de chances implicites de gagner**.

---

## 📊 2. Les indicateurs que le PMU utilise dans le calcul

Le PMU **ne prend en compte que des données de marché**, pas de données sportives.
Mais pour être complet, voici tout ce qu’il **observe et met à jour en continu** :

| Type d’indicateur | Description | Influence sur la cote |
| :--- | :--- | :--- |
| 💰 **Volume de mise sur chaque cheval** | Somme totale jouée par tous les parieurs sur ce cheval | Décisive (base du calcul) |
| ⏰ **Évolution dans le temps** | Fluctuation du volume de mises juste avant le départ | Ajuste la cote toutes les 30 secondes environ |
| 🧮 **Prélèvement PMU** | Environ 15–25 % selon le type de pari (gagnant, placé, quinté, etc.) | Réduit le “pot total” donc augmente légèrement les cotes |
| 🪙 **Montant total misé sur la course** | Sert à calculer la part de chaque cheval | Plus le total est grand, plus les variations sont fines |
| 🧠 **Correction automatique (arrondis, limites)** | Le PMU applique des arrondis (ex. pas de cote à 3,73 mais 3,7) et des règles pour éviter les erreurs statistiques | Marginal |

---

## 🧾 3. Ce que le PMU *ne* fait pas

Contrairement à un bookmaker :

* Il **n’utilise pas** les performances, ni les statistiques du cheval.
* Il **n’évalue pas** le risque sportivement.
* Il **ne fixe pas** la cote à l’avance : elle est **entièrement déterminée par le comportement collectif des parieurs**.

---

## 📈 4. Quand la cote devient officielle

* La **cote finale** (dite “cote définitive”) est figée **au moment du départ**.
* Avant, tu vois une **cote estimée**, recalculée automatiquement toutes les 30 secondes en fonction des dernières mises enregistrées.
