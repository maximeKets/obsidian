---
tags:
  - type/area
  - status/evergreen
---

# 🏗️ Area : [Nom du Domaine]
*(ex: Finances, Santé, Maison, Dev Pro)*

## 🎯 Vision / Standard
*Quelle est mon intention pour ce domaine ? Qu'est-ce que je veux maintenir ?*
> "Je veux être en bonne santé..." ou "Je veux garder mes finances saines..."

## 🔄 Routines & Checklists
*Actions récurrentes pour maintenir ce domaine.*
- [ ] Routine Hebdo : 
- [ ] Routine Mensuelle : 

## 📋 Projets Actifs
*Ce domaine a-t-il des projets en cours ?*
```dataview
TABLE deadline, status
FROM "1. Projects"
WHERE contains(tags, "type/project")
AND file.folder = this.file.folder
```
*(Astuce : Placez ce fichier Area dans un dossier dédié, ex: `2. Areas/Santé`, et mettez les projets Santé dedans pour que la requête marche)*

## 🗄️ Ressources Spécifiques
*Liens vers des documents de référence importants.*

