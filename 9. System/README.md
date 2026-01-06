# 🧠 Manuel du Système Obsidian

Ce document décrit la philosophie, la structure et le fonctionnement de votre "Second Cerveau".

---

## 🏗️ Architecture & Logique

Ce vault utilise une méthode **hybride** optimisée pour l'action et la réflexion.

### 1. Structure de Dossiers (Le Squelette)
Nous utilisons **PARA** modifié pour séparer clairement l'action (Projets) de la connaissance (Ressources).

- **`0. Inbox`** : Le point d'entrée. Tout atterrit ici via les *Daily Notes*. C'est le chaos temporaire.
- **`1. Projects`** : Ce sur quoi vous travaillez *maintenant*. Un projet a un but et une fin.
- **`2. Areas`** : Vos domaines de responsabilité permanents (Santé, Finance, Maison). Pas de fin.
- **`3. Resources`** : Votre bibliothèque de connaissances.
    - `Zettelkasten` : Vos notes atomiques (pensées interconnectées).
    - `References` : Documents statiques, manuels, PDF.
- **`4. Archives`** : Le cimetière des projets finis.
- **`9. System`** : La salle des machines (Templates, ce Manuel, Tags).

### 2. Connecter les Idées (Le Moteur)
La structure physique (dossiers) est secondaire. Le vrai pouvoir vient des liens.

- **Liens [[Wikilinks]]** : L'outil principal. Reliez les idées entre elles. "L'inertie ([[Inertia]]) explique pourquoi..."
- **Tags (#)** : Utilisés pour le *statut* de la note ou son *type*, pas pour le sujet (sauf exceptions). Voir [[Tag Taxonomy]].

---

## 🔄 Workflows Quotidiens

### Matin : Démarrage
1.  Ouvrez Obsidian.
2.  Créez la **Daily Note** du jour (Alt+D ou bouton Calendrier).
3.  Vérifiez les notes à revoir (via le dashboard automatique en bas du template Daily).

### Durant la journée : Capture (Inbox)
Si une idée surgit :
1.  Allez sur votre Daily Note.
2.  Écrivez-la en vrac sous "Quick Capture".
3.  Ne classez rien maintenant. Restez dans le flux.

### Soir : Traitement & Atomisation
Le moment clé pour transformer le bruit en signal (Hacks Obsidian).
1.  Relisez votre Daily Note.
2.  Pour chaque point intéressant :
    - Est-ce une **Tâche** ? -> Ajoutez-la à votre Todo app ou créez un projet.
    - Est-ce une **Connaissance** ? -> Transformez-la en **Note Atomique** (Zettel).

### Création d'une Note Atomique
1.  Créez une nouvelle note (`Cmd+N`).
2.  Insérez le template `tpl_zettel`.
3.  **Titre** : Une phrase complète (ex: "La friction réduit l'usage", pas juste "Friction").
4.  **Contenu** : Expliquez l'idée avec vos mots.
5.  **Connexions** : Ajoutez au moins 2 liens vers d'autres notes.
6.  Déplacez la note dans `3. Resources/Zettelkasten`.

---

## 🛠️ Outils & Standards

### Templates
Utilisez le plugin `Templater` pour insérer rapidement des structures.

**Comment insérer un template ?**
1.  Ouvrez une note vide.
2.  Utilisez le raccourci `Cmd+P` (Palette de commande).
3.  Tapez `Templater: Insert template`.
4.  Choisissez le template (ex: `tpl_zettel`) dans la liste.

> [!TIP] Raccourci
> Je vous conseille de mapper la commande "Templater: Insert template" sur un raccourci clavier (ex: `Alt+E`) dans `Settings > Hotkeys`.
- `tpl_meeting` : Pour vos réunions (Date, participants, actions).
- `tpl_project` : Pour lancer un nouveau projet (Objectifs SMART).
- `tpl_book` : Pour prendre des notes sur un livre.

### Composants UI
Besoin d'un tableau ou d'une alerte ?
-> Copiez-collez depuis [[Components Library]].

### Tags
Ne créez pas de tags au hasard. Référez-vous à [[Tag Taxonomy]].
- `#type/permanent` pour une note de savoir.
- `#status/seed` pour une ébauche.

---

> [!QUOTE] Philosophie
> *"Votre cerveau est fait pour avoir des idées, pas pour les retenir."* - David Allen
> Ce système est votre mémoire externe. Faites-lui confiance.
