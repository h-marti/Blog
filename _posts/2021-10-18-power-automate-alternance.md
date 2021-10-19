---
layout: post
title:  "Réponse automatique dans Outlook avec Power Automate"
date:   2021-10-18 12:00:00 +0530
categories: posts
image: /images/Power-automate.png
---

Dans le cadre de mon alternance, je suis amené à être régulièrement absent de mon entreprise pour pouvoir suivre ma formation. Il me faut donc pour chaque jour de formation intégrer une entrée dans mon agenda afin de permettre aux personnes avec qui je suis amené à travailler de ne pas planifier de réunion à ces dates.

Dans l'entreprise dans laquelle je travaille nous utilisons depuis très récemment la suite collaborative Office 365. C'est donc le Outlook le logiciel que j'utilise pour gérer mes mails, mes rendez-vous et mon agenda. J'ai donc saisi dans mon planning toutes les dates auxquelles je serai indisponible. Malheureusement, la réponse automatique aux emails qui arrivent pendant ces périodes n'est pas configurable à l'avance dans Outlook.

J'ai donc utilisé l'outil [Power Automate](https://flow.microsoft.com/fr-fr/) de la [Power Platform](https://powerplatform.microsoft.com/fr-fr/) d'Office 365 pour automatiser cela.

### Ma solution

Une fois mon automatisation mise en place, une routine s'execute chaque jour à 6h du matin et analyse tous les évènements des prochaines 24h dans le calendrier. Si l'un d'eux a pour titre "Formation", alors une réponse automatique est configurée dans Outlook aux horaires de l'évènement. Le corps du message de réponse est configuré pour être le contenu de l'entrée d'agenda.

**Attention :** Cette automatisation ne fonctionne que s'il n'y a qu'une seule entrée "Formation" dans l'agenda pour le jour traité => A n'utiliser que pour des journée complètes.

### Comment faire ?

<div class="text-center mb-2">
    <img src="/images/Screenshot-Power-Auto.png" alt="Menu Win+X" width="100%">
</div>

1. Créer le flux
    - Se rendre dans l'espace de création de flux
    - Choisir "Créer un flux de cloud planifié"
    - Définir un titre ("Gestion absence formation")
    - Choisir une date et une heure de première exécution (le lendemain à 06h00)
    - Choisir une récurrence (tous les jours)
2. Obtenir le calendrier du jour
    - Utiliser le bloc "Outlook : Obtenir une vue Calendrier des événements (V3)"
    - Choisir le calendrier à analyser
    - Configurer "Heure de début" avec l'expression "utcNow()"
    - Configurer "Heure de fin" avec l'expression "addHours(utcNow(), 24)"
3. Identifier l'évènement
    - Créer une boucle "Appliquer à chacun"
    - Choisir de boucler sur le paramètre "value" du bloc précédent
    - Appliquer une condition
      - Inclure une condition "Condition"
      - Choisir la valeur "Objet" du bloc précédent "est égal à" -> "Formation" (dans cet exemple)
4. Créer une réponse automatique
    - Ajouter le bloc "Outlook : Configurer des réponses automatiques (V2)" dans la partie verte "Si oui"
    - Choisir "Heure de début" de l'évènement dans le champs "Heure de début Date/Heure"
    - Choisir "Heure de fin" de l'évènement dans le champs "Heure de fin Date/Heure"
    - Choisir "Corps" de l'évènement dans le champs "Message de réponse interne"
    - Choisir "Corps" de l'évènement dans le champs "Message de réponse externe"
5. Enregistrer
