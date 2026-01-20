# Simulation : Comment le PMU répartit la masse des enjeux

Voici une **simulation concrète** pour comprendre la mécanique du pari mutuel.
Imaginons une course fictive simple en **Pari Gagnant**.

## 1. Les données de départ

*   **100 parieurs** participent.
*   Chacun mise **10 €** sur un cheval.
*   **Montant total des enjeux** : $100 \times 10 = 1\,000\ €$.

**Répartition des mises (qui joue quoi ?) :**
*   **Cheval A (Favori)** : 50 parieurs (Masse : 500 €)
*   **Cheval B** : 30 parieurs (Masse : 300 €)
*   **Cheval C** : 15 parieurs (Masse : 150 €)
*   **Cheval D (Outsider)** : 5 parieurs (Masse : 50 €)

## 2. Le prélèvement (La part du PMU/État)

Le PMU ne joue pas contre les parieurs, il organise le jeu. Il prélève sa commission **avant** la redistribution.
*   Hypothèse de prélèvement : **15 %**.
*   Calcul : $1\,000\ € - 15\% = 150\ €$ de frais.
*   **Masse à partager (Net)** = $850\ €$.

C'est ce montant de **850 €** qui sera redistribué aux gagnants, quel que soit le résultat.

## 3. Le calcul des rapports (Cotes finales)

Le rapport pour 1 € de mise se calcule ainsi :
$$ \text{Rapport} = \frac{\text{Masse à partager}}{\text{Mises sur le cheval gagnant}} $$

### Scénario 1 : Le Favori (Cheval A) gagne
*   Mises sur A : 500 €
*   Calcul : $850 / 500 = 1,70\ €$
*   **Cote : 1,7 contre 1**
*   **Gain :** Chaque parieur ayant misé 10 € reçoit **17 €**.

### Scénario 2 : L'Outsider (Cheval D) gagne
*   Mises sur D : 50 €
*   Calcul : $850 / 50 = 17,00\ €$
*   **Cote : 17 contre 1**
*   **Gain :** Chaque parieur ayant misé 10 € reçoit **170 €**.

## 4. Ce qu'il faut retenir

1.  **Mutualisation :** Si le Cheval D gagne, les 5 gagnants se partagent l'argent perdu par les 95 autres parieurs.
2.  **Transparence :** Le PMU n'a aucun intérêt à ce que le favori ou l'outsider gagne, car son prélèvement (150 €) est fixe dès le départ.
3.  **Cote = Confiance :** Une cote faible (1,7) signifie que beaucoup de gens ont joué ce cheval (50 % des mises). Une cote élevée (17) signifie que peu de gens y croient (5 % des mises).
