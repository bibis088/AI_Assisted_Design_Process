# Principes UX de référence — règle globale

> Ce fichier est lu automatiquement par les agents `ux-designer`, `business-analyst` et `product-owner`.
> Il encode les principes de référence qui s'appliquent à tout moment du process — pas seulement lors des audits dédiés.

---

## Sources de référence

| Source | Domaine | Utilisation dans le process |
|--------|---------|----------------------------|
| Nielsen Norman Group — 10 heuristiques | Utilisabilité générale | Audits Gate 1, 4, 8 |
| Laws of UX (Jon Yablonski) | Psychologie cognitive | Gate 4 et Gate 8 |
| Gestalt (Wertheimer, Köhler) | Perception visuelle | Gate 6 (post-DA) |
| Shneiderman's 8 Golden Rules | Cohérence et contrôle | Intégré dans Nielsen |
| Apple HIG — Principles | iOS : déférence, clarté, profondeur | Gate 4 et Gate 5 |
| Material 3 — Foundations | Android : motion, layout, communication | Gate 4 et Gate 5 |

---

## Les 10 heuristiques de Nielsen Norman

### H1 — Visibilité de l'état du système
Le système informe toujours l'utilisateur de ce qui se passe, avec un feedback approprié dans un délai raisonnable.

**Mobile :** États de chargement visibles, indicateurs de progression, confirmation après action.
**Signal d'alerte :** Action sans feedback → l'utilisateur retappe, s'interroge, abandonne.

### H2 — Correspondance entre le système et le monde réel
Le système parle le langage de l'utilisateur. Concepts, mots, conventions du monde réel plutôt que du monde technique.

**Mobile :** Métaphores naturelles (corbeille, enveloppe), vocabulaire métier du persona, pas de jargon technique.
**Signal d'alerte :** Termes techniques dans les messages d'erreur, icônes sans label sur des actions non conventionnelles.

### H3 — Liberté et contrôle de l'utilisateur
L'utilisateur fait des erreurs et a besoin d'une sortie de secours. Annuler et refaire toujours disponibles.

**Mobile :** Swipe pour annuler, bouton retour cohérent, confirmation avant action destructive, undo disponible.
**Signal d'alerte :** Actions irréversibles sans confirmation, retour arrière incohérent entre les écrans.

### H4 — Cohérence et standards
Les utilisateurs ne devraient pas avoir à se demander si des mots, situations ou actions différents signifient la même chose.

**Mobile :** Mêmes patterns pour les mêmes actions sur tous les écrans, conventions iOS/Android respectées.
**Signal d'alerte :** Bouton primaire à gauche sur un écran, à droite sur un autre. Terme différent pour la même action.

### H5 — Prévention des erreurs
Concevoir en évitant les problèmes plutôt qu'en proposant des messages d'erreur après.

**Mobile :** Validation inline, format de saisie guidé, désactivation des actions impossibles plutôt qu'erreur post-soumission.
**Signal d'alerte :** Formulaire qui valide uniquement à la soumission, champs qui acceptent n'importe quel format.

### H6 — Reconnaissance plutôt que rappel
Minimiser la charge mémorielle. Rendre visibles les objets, actions et options disponibles.

**Mobile :** Labels sur les icônes de navigation, historique récent accessible, choix visibles plutôt que mémorisés.
**Signal d'alerte :** Navigation par onglets sans labels, formulaire multi-étapes sans récapitulatif.

### H7 — Flexibilité et efficacité d'utilisation
Les accélérateurs permettent aux utilisateurs experts d'aller plus vite, sans gêner les novices.

**Mobile :** Swipe actions pour les experts, shortcuts sur les actions fréquentes, personnalisation possible.
**Signal d'alerte :** Toujours 3 taps pour une action fréquente, pas de raccourci possible.

### H8 — Esthétique et design minimaliste
Ne pas afficher d'informations non pertinentes. Chaque unité d'information supplémentaire en cache une autre.

**Mobile :** Un écran = une intention principale, contenu progressif (afficher les détails à la demande).
**Signal d'alerte :** Écran avec plus de 5 zones d'intérêt distinctes, texte dense sans hiérarchie.

### H9 — Aide à la reconnaissance, au diagnostic et à la correction des erreurs
Les messages d'erreur expriment clairement le problème et suggèrent une solution.

**Mobile :** Message d'erreur = condition + cause + action corrective (pas de code d'erreur seul).
**Signal d'alerte :** "Erreur 404", "Une erreur s'est produite", messages sans action proposée.

### H10 — Aide et documentation
Si une aide est nécessaire, elle est facile à trouver, focalisée sur la tâche, concrète.

**Mobile :** Onboarding contextuel, tooltips au premier usage, aide inline plutôt que FAQ externe.
**Signal d'alerte :** Fonctionnalité complexe sans guidage, aide accessible uniquement via le menu principal.

---

## Lois UX — appliquées au mobile

### Loi de Fitts
Le temps pour atteindre une cible dépend de sa taille et de sa distance.

**Application mobile :**
- Actions principales → grande zone tactile (≥ 44pt iOS / ≥ 48dp Android), position pouce accessible
- Actions destructives → petites, éloignées des actions fréquentes
- CTA principal → toujours dans la zone de confort du pouce (bas d'écran)

### Loi de Hick
Le temps de décision augmente avec le nombre et la complexité des choix.

**Application mobile :**
- Maximum 5 choix par écran au même niveau hiérarchique
- Navigation principale : 3 à 5 items maximum
- Formulaires : un champ à la fois si possible (mode wizard pour les formulaires complexes)

### Loi de Miller (7 ± 2)
La mémoire de travail humaine gère 5 à 9 unités d'information simultanément.

**Application mobile :**
- Ne pas demander de mémoriser des informations d'un écran à l'autre
- Regrouper les éléments connexes (chunking)
- Navigation multi-niveaux : maximum 3 niveaux de profondeur

### Loi de Jakob
Les utilisateurs passent la majorité de leur temps sur d'autres apps. Ils préfèrent que votre app fonctionne comme celles qu'ils connaissent.

**Application mobile :**
- Respecter les conventions iOS (tab bar en bas, navigation push/pop, swipe back)
- Respecter les conventions Android (navigation system, back gesture, FAB)
- Innover sur le contenu, pas sur les patterns de navigation

### Peak-End Rule (Kahneman)
Les utilisateurs jugent une expérience principalement par son pic émotionnel et sa fin.

**Application mobile :**
- Premier lancement → expérience mémorable et rassurante
- Première tâche clé complétée → feedback positif fort (celebration state)
- Fin de session → récapitulatif valorisant, invitation à revenir

### Loi de Proximity (Gestalt)
Les éléments proches sont perçus comme liés.

**Application mobile :**
- Labels proches de leurs champs (pas au-dessus d'une autre zone)
- Actions regroupées par contexte
- Espacement cohérent : plus d'espace entre groupes qu'entre éléments d'un groupe

### Loi de Similarité (Gestalt)
Les éléments visuellement similaires sont perçus comme appartenant au même groupe.

**Application mobile :**
- Même style visuel pour les éléments de même type (tous les boutons primaires identiques)
- Différenciation visuelle claire entre éléments interactifs et décoratifs

### Principe de Figure / Fond (Gestalt)
L'œil distingue naturellement les éléments au premier plan (figure) du fond.

**Application mobile :**
- Éléments interactifs clairement différenciés du fond (contraste, élévation, bordure)
- Fond neutre pour mettre en valeur le contenu principal

---

## Application dans le process

Ces principes sont **évalués formellement** à 4 moments :

| Gate | Skill dédié | Principes évalués |
|------|------------|------------------|
| Gate 1 | `write-ux-principles-flows` | H1, H3, H5, H9 + Miller |
| Gate 4 | `write-ux-heuristics-audit` | Tous — 10 Nielsen + Lois + Gestalt |
| Gate 6 | `write-ux-gestalt-check` | Gestalt + H4 + H8 + charge cognitive |
| Gate 8 | `write-ux-expert-review` | Tous + Peak-End + cohérence cross-écrans |

**Entre ces gates**, les agents utilisent ces principes comme garde-fous implicites dans leur production — sans audit formel.
