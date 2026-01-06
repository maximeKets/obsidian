<%*
// Réglages date
const date = tp.date.now("YYYY-MM-DD");
%>
# 📅 Daily Note: <% date %>

<< [[<% tp.date.now("YYYY-MM-DD", -1) %>]] | [[<% tp.date.now("YYYY-MM-DD", 1) %>]] >>

## 📥 Quick Capture (Inbox)
*Capturez tout ici sans réfléchir. Traitez plus tard.*

- [ ] 

## 📝 Journal de bord
*Réflections, événements marquants, idées en vrac.*

## ✅ Tâches du jour (Import TickTick/Todoist si plugin)
- [ ] 

## 🔗 Notes créées aujourd'hui
```dataview
LIST FROM "" WHERE file.cday = date("<% date %>") AND file.name != "<% date %>"
```
