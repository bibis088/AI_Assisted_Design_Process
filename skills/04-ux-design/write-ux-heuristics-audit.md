---
name: write-ux-heuristics-audit
description: "Audit heuristique complet avant Gate 4 — évalue navigation map, user flows et specs écrans contre les 10 heuristiques Nielsen, les lois UX (Fitts, Hick, Miller, Jakob, Peak-End) et les principes Gestalt. Bloquant si sévérité critique détectée. Use when user says 'audit heuristique', 'évalue le design UX', 'Nielsen audit', or 'write-ux-heuristics-audit'."
argument-hint: "[epic-slug]"
agent: ux-designer
---

## Rôle
Audit heuristique complet du design UX avant la création des composants et frames UI. C'est le **point idéal** : le design existe (navigation, flows, specs) mais aucun pixel n'est rendu — le coût de correction est minimal.

**Déclenché :** Obligatoire avant Gate 4. À exécuter après `write-accessibility-annotations`.
**Bloquant :** Oui si sévérité 🔴 Critique détectée — Gate 4 ne peut pas s'ouvrir sans décision humaine sur chaque critique.

## Prérequis
- [ ] `design/[feature-slug]/SCREENS-MAP.md` disponible
- [ ] `design/[feature-slug]/ux/user-flow-FLUX-###.md` disponibles
- [ ] `specs/[epic-slug]/stories/US-###.md` disponibles
- [ ] `specs/[epic-slug]/personas/` disponibles
- [ ] Rapport `write-ux-principles-flows` disponible (Gate 1) — s'appuyer dessus pour ne pas redoubler

---

## Étape 1 — Cartographie des écrans à auditer

Depuis `SCREENS-MAP.md`, lister :
```
Flux principal     → [N écrans] — chemin critique
Flux alternatifs   → [N écrans] — déviations positives
États d'erreur     → [N écrans] — cas dégradés
Écrans partagés    → [N écrans] — navigation globale
```

Prioriser l'audit dans cet ordre : flux principal → erreurs → alternatifs → partagés.

---

## Étape 2 — Audit par heuristique

Pour chaque heuristique, évaluer l'ensemble des écrans. Signaler chaque problème avec sa localisation exacte (écran + élément).

### H1 — Visibilité de l'état du système
Questions d'audit :
- Chaque action asynchrone a-t-elle un état de chargement défini dans les specs ?
- Les transitions entre écrans indiquent-elles la progression dans le parcours ?
- Après chaque action majeure, l'utilisateur reçoit-il une confirmation visible ?
- Les étapes d'un processus multi-étapes sont-elles visibles (stepper, breadcrumb, indicateur) ?

### H2 — Correspondance monde réel
Questions d'audit :
- Les termes utilisés dans les specs correspondent-ils au vocabulaire du persona (issu de `insights.md`) ?
- Les icônes utilisées sans label correspondent-elles à des conventions universelles ?
- Les métaphores visuelles prévues sont-elles naturelles pour la cible ?

### H3 — Liberté et contrôle
Questions d'audit :
- Chaque écran a-t-il un chemin de retour documenté dans `SCREENS-MAP.md` ?
- Les actions destructives ont-elles une étape de confirmation dans les user flows ?
- L'utilisateur peut-il interrompre et reprendre chaque flux sans perdre de données ?
- Les actions modales ont-elles toujours une sortie sans conséquence (annuler) ?

### H4 — Cohérence et standards
Questions d'audit :
- Le même pattern d'action est-il utilisé partout pour la même intention (ex: toujours un FAB pour créer) ?
- La position des éléments de navigation est-elle cohérente entre tous les écrans ?
- Les conventions de la plateforme cible (iOS/Android) sont-elles respectées dans les specs ?

### H5 — Prévention des erreurs
Questions d'audit :
- Les champs de saisie critiques ont-ils une validation inline spécifiée ?
- Les actions irréversibles sont-elles protégées (confirmation, délai d'annulation) ?
- Les formats attendus sont-ils guidés (ex: date picker plutôt que champ libre) ?

### H6 — Reconnaissance plutôt que rappel
Questions d'audit :
- L'utilisateur doit-il mémoriser une information d'un écran à l'autre pour compléter une tâche ?
- Les options disponibles sont-elles toujours visibles (pas de menu caché sans affordance) ?
- Les écrans de liste affichent-ils assez de contexte pour reconnaître chaque item sans l'ouvrir ?

### H7 — Flexibilité et efficacité
Questions d'audit :
- Les actions fréquentes (selon le persona régulier) sont-elles accessibles en ≤ 2 taps ?
- Des raccourcis existent-ils pour les utilisateurs réguliers (swipe actions, shortcuts) ?

### H8 — Esthétique et design minimaliste
Questions d'audit :
- Chaque écran a-t-il une intention principale clairement identifiable ?
- Les informations secondaires sont-elles masquées ou accessibles progressivement ?
- Le contenu de chaque écran est-il suffisamment aéré pour ne pas surcharger visuellement ?

### H9 — Aide à la correction des erreurs
Questions d'audit :
- Chaque cas d'erreur documenté dans les US a-t-il un message en 3 parties (condition + cause + action) ?
- Les erreurs de validation identifient-elles précisément le champ concerné ?
- Les erreurs réseau proposent-elles une action de reprise ?

### H10 — Aide et documentation
Questions d'audit :
- Les fonctionnalités complexes ont-elles un guidage contextuel prévu dans les specs ?
- L'onboarding couvre-t-il les fonctionnalités non intuitives ?
- Les états vides ont-ils un contenu explicatif et une action initiatrice ?

---

## Étape 3 — Audit Lois UX

### Fitts — Accessibilité des cibles
- Identifier les actions principales de chaque écran
- Vérifier leur position dans la zone de confort du pouce (≤ 75% de hauteur d'écran depuis le bas)
- Vérifier les zones tactiles ≥ 44pt iOS / ≥ 48dp Android pour chaque action principale
- Identifier les actions destructives — sont-elles éloignées des actions fréquentes ?

### Hick — Nombre de choix
- Compter les choix présentés simultanément par écran (signal : > 5)
- Compter les items de navigation principale (signal : > 5)
- Identifier les écrans avec plus de 2 niveaux de décision simultanés

### Miller — Charge mémorielle
- Identifier les informations à mémoriser d'un écran à l'autre
- Compter les éléments dans les listes sans regroupement (signal : > 7)
- Identifier les formulaires multi-étapes sans récapitulatif

### Jakob — Conventions plateforme
- iOS : tab bar en bas (≤ 5 items), navigation push/pop, swipe back, Safe Areas
- Android : navigation gesture system, FAB pour action principale, bottom nav ≤ 5 items
- Signaler chaque déviation aux conventions de la plateforme cible

### Peak-End Rule — Moments clés
- Identifier le premier lancement dans les flows — est-il mémorable et rassurant ?
- Identifier la complétion de la première tâche clé — y a-t-il un celebration state ?
- Identifier les fins de session documentées — y a-t-il un feedback positif ?

---

## Étape 4 — Audit Gestalt

### Proximité
- Les labels sont-ils proches de leurs champs associés ?
- Les actions sont-elles groupées par contexte dans les specs ?
- L'espacement entre groupes est-il supérieur à l'espacement interne des groupes ?

### Similarité
- Les éléments de même type ont-ils le même style visuel dans toutes les specs ?
- La différenciation entre éléments interactifs et décoratifs est-elle cohérente ?

### Continuité
- Le regard est-il guidé naturellement vers l'action principale par la disposition des éléments ?
- Les listes et grilles respectent-elles des alignements réguliers ?

### Figure / Fond
- Les éléments interactifs principaux ressortent-ils clairement du fond dans les specs ?
- Les overlays et modales ont-ils un fond suffisamment contrasté ?

---

## Étape 5 — Rapport d'audit

```markdown
# Audit Heuristique UX — [NomProjet] — [YYYY-MM-DD]

## Résumé exécutif
- Écrans audités : [N]
- Problèmes détectés : [N total] — [N 🔴 Critiques] [N 🟡 Majeurs] [N 🟢 Mineurs]
- Gate 4 : [🔴 BLOQUÉE — corriger les critiques d'abord / ✅ Ouverte avec recommandations]

---

## Problèmes critiques 🔴 — à corriger avant Gate 4

| # | Heuristique | Écran / Flow | Problème | Recommandation |
|---|-------------|-------------|---------|----------------|
| C-01 | H3 — Liberté | S-04 paiement | Aucune sortie documentée après saisie CB | Ajouter écran d'abandon avec confirmation |
| C-02 | H5 — Prévention | FLUX-002 étape 2 | Action irréversible (suppression compte) sans confirmation | Ajouter étape de confirmation + délai 5s |

## Problèmes majeurs 🟡 — décision requise

| # | Heuristique | Écran / Flow | Problème | Priorité suggérée |
|---|-------------|-------------|---------|-------------------|
| M-01 | Hick | S-02 home | 8 actions disponibles simultanément | Regrouper en catégories ou limiter à 5 |
| M-02 | Jakob | Navigation | Bottom tab bar avec 6 items (iOS max = 5) | Fusionner 2 items ou utiliser "Plus" |

## Problèmes mineurs 🟢 — backlog

| # | Heuristique | Écran | Problème |
|---|-------------|-------|---------|
| m-01 | H8 | S-07 profil | 3 sections secondaires affichées par défaut — pourraient être masquées |

## Lois UX — synthèse

| Loi | Statut | Observations |
|-----|--------|-------------|
| Fitts | ⚠️ | Action principale S-03 positionnée à 85% de hauteur — hors zone confort pouce |
| Hick | ❌ | 3 écrans dépassent 5 choix simultanés |
| Miller | ✅ | Aucun flux > 7 étapes |
| Jakob | ⚠️ | Tab bar 6 items sur iOS |
| Peak-End | ✅ | Onboarding et complétion première tâche documentés |

## Gestalt — synthèse

| Principe | Statut | Observations |
|---------|--------|-------------|
| Proximité | ✅ | Labels correctement associés aux champs |
| Similarité | ⚠️ | 2 patterns de boutons secondaires différents sur S-02 et S-05 |
| Continuité | ✅ | |
| Figure/Fond | ✅ | |
```

---

## Étape 6 — Validation humaine obligatoire

```
🔴 Gate 4 — [N] problèmes critiques à résoudre

Pour chaque critique, choisir :
  [A] ✅ Corriger maintenant dans les specs UX → UX Designer met à jour SCREENS-MAP + flows
  [B] ❌ Impossible à corriger sans changer le scope → escalader au PO

Pour chaque majeur, choisir :
  [A] ✅ Corriger avant l'UI
  [B] ⏭️ Accepter le risque — justification : [...]
  [C] 📋 Tester avec les utilisateurs (Gate 8) avant de décider

→ Gate 4 s'ouvre uniquement quand tous les critiques sont en [A] ou [B-escaladé].
```

---

## Format fichier de sortie

```
specs/[epic-slug]/ux-reviews/ux-heuristics-audit-[YYYYMMDD].md
```

## Phase de validation — niveau approfondi

1. Chaque heuristique Nielsen a-t-elle été évaluée sur au moins le flux principal ? (oui / non)
2. Les 5 lois UX (Fitts, Hick, Miller, Jakob, Peak-End) ont-elles été vérifiées ? (oui / non)
3. Tous les problèmes critiques ont-ils une décision A ou B du Product Designer ? (oui / non — **bloquant Gate 4**)
4. Le rapport a-t-il été mis en lien dans `SCREENS-MAP.md` pour référence future ? (oui / non)

## Résumé de fin d'exécution

```
✅ write-ux-heuristics-audit "$ARGUMENTS" terminé
📁 specs/$ARGUMENTS/ux-reviews/ux-heuristics-audit-[date].md

Audit : [N] écrans · [N] critiques · [N] majeurs · [N] mineurs
Gate 4 : [🔴 BLOQUÉE / ✅ Ouverte]

Prochaines étapes (si Gate 4 ouverte) :
→ /setup-figma-frames $ARGUMENTS
→ /write-component $ARGUMENTS/[premier-composant]
```
