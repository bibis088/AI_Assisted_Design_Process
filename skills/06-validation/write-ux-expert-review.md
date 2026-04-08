---
name: write-ux-expert-review
description: "Inspection experte complète du prototype avant les tests utilisateurs — synthèse heuristique, Peak-End Rule, cohérence cross-écrans. Oriente le guide d'entretien. Bloquant si critique détecté avant run-user-tests. Use when user says 'inspection experte', 'expert review', 'révision avant tests', or 'write-ux-expert-review'."
argument-hint: "[epic-slug]"
agent: ux-designer
---

## Rôle
Inspection heuristique experte sur le prototype complet avant les tests utilisateurs. L'objectif est double : détecter les problèmes qu'un expert identifie en 30 min (et qu'il serait coûteux de découvrir en session utilisateur) et orienter le guide d'entretien vers les zones à risque.

**Déclenché :** Obligatoire avant `run-user-tests`. S'exécute après Gate 8 (prototype v2 complet).
**Bloquant :** Oui si sévérité 🔴 Critique — les problèmes critiques biaisent les sessions de test et doivent être corrigés avant.

## Prérequis
- [ ] Prototype v2 disponible (React ou Figma prototype)
- [ ] URL du prototype fournie
- [ ] Rapports des audits précédents disponibles :
  - `ux-reviews/ux-principles-flows-*.md` (Gate 1)
  - `ux-reviews/ux-heuristics-audit-*.md` (Gate 4)
  - `ux-reviews/ux-gestalt-check-*.md` (Gate 6)
- [ ] `specs/[epic-slug]/stories/US-###.md` — toutes les US de la V1
- [ ] `specs/[epic-slug]/personas/` — notamment PERSONA-001 (regular) et PERSONA-002 (new user)

---

## Étape 1 — Récapituler les audits précédents

Lire les 3 rapports précédents et identifier :
- Les problèmes reportés en "Phase UX" (décision B à Gate 1 et Gate 4) — sont-ils résolus ?
- Les incohérences identifiées à Gate 6 — ont-elles été corrigées sur les écrans secondaires ?
- Les points de vigilance flaggés par le Product Designer

---

## Étape 2 — Parcours du prototype par persona

### Parcours PERSONA-002 — Nouvel utilisateur (premier lancement)
Simuler le parcours d'un utilisateur qui découvre l'app pour la première fois :

1. **Premier écran** — L'intention de l'app est-elle compréhensible en < 5 secondes ?
2. **Onboarding** — Chaque étape a-t-elle une valeur visible pour l'utilisateur (pas uniquement de la collecte) ?
3. **Première tâche** — Peut-elle être complétée sans aide externe ?
4. **Premier succès** — Y a-t-il un feedback positif fort à la complétion ?

Documenter les frictions observées à chaque étape.

### Parcours PERSONA-001 — Utilisateur régulier (session courante)
Simuler une session typique d'un utilisateur qui connaît déjà l'app :

1. **Reprise de l'app** — L'état précédent est-il restauré ou clairement réinitialisé ?
2. **Tâche fréquente** — Nombre de taps pour compléter l'action la plus courante ?
3. **Navigation** — Les raccourcis et actions rapides sont-ils accessibles ?
4. **Erreur simulée** — Comment l'app réagit-elle à une erreur volontaire (champ vide, réseau coupé) ?

### Parcours PERSONA-003 — Utilisateur edge (cas limite)
Tester les cas non couverts par les parcours standards :
- Texte très long dans les champs
- Contenu vide (état empty state)
- Permissions refusées
- Interruption et reprise en cours de flux

---

## Étape 3 — Inspection heuristique rapide (cross-écrans)

Contrairement à l'audit Gate 4 (approfondi par heuristique), cette inspection est **transversale** — elle cherche les problèmes de cohérence qui n'émergent que sur le produit complet.

**Vérifications cross-écrans :**

| Vérification | Question |
|-------------|---------|
| Cohérence H4 | Le même pattern est-il utilisé pour la même intention sur tous les écrans (y compris secondaires) ? |
| Terminologie H2 | Le même mot est-il utilisé partout pour le même concept ? |
| Retour arrière H3 | Depuis chaque écran, peut-on revenir sans conséquence ? |
| États vides H10 | Chaque écran qui peut être vide a-t-il un état documenté et implémenté ? |
| États d'erreur H9 | Les messages d'erreur sont-ils cohérents en style et en structure sur tous les écrans ? |
| Peak-End | Le premier lancement et la première complétion sont-ils mémorables ? |
| Fitts | Les actions principales sont-elles dans la zone de confort du pouce sur tous les écrans ? |

---

## Étape 4 — Rapport d'inspection experte

```markdown
# Inspection Experte — Prototype v2 — [NomProjet] — [YYYY-MM-DD]

## Contexte
- Prototype : [URL]
- Audits précédents : [Gate 1 ✅ / Gate 4 ✅ / Gate 6 ✅]
- Problèmes reportés de Gate 4 résolus : [N/N]

## Statut global
- Tests utilisateurs : [🔴 BLOQUÉS — [N] critiques / ✅ GO — [N] majeurs à surveiller]

---

## 🔴 Critiques — corriger avant les tests

| # | Découverte | Écran | Impact utilisateur | Correction |
|---|-----------|-------|-------------------|-----------|
| CR-01 | Onboarding — étape 3 sans feedback de progression | S-03 | Le nouvel utilisateur ne sait pas où il en est | Ajouter indicateur d'étape |

## 🟡 Majeurs — intégrer dans le guide d'entretien

| # | Découverte | Écran | Hypothèse à tester |
|---|-----------|-------|--------------------|
| MA-01 | 6 taps pour accéder à la tâche fréquente depuis l'accueil | S-01 → S-04 | "Combien de temps pour trouver [tâche] ?" |
| MA-02 | Terminologie "Référentiel" vs "Catalogue" — incohérence | S-07, S-12 | "Comment appelez-vous cette section ?" |

## 🟢 Mineurs — backlog

| # | Découverte | Écran |
|---|-----------|-------|
| MI-01 | Empty state S-06 sans illustration (texte seul) | S-06 |

---

## Parcours par persona — synthèse

### PERSONA-002 — Premier lancement
- Compréhension app en < 5s : ✅ / ❌ [observation]
- Onboarding complété sans aide : ✅ / ❌ [friction principale]
- Premier succès avec feedback : ✅ / ❌

### PERSONA-001 — Utilisateur régulier
- Tâche fréquente en [N] taps (cible : ≤ 3)
- Erreur simulée gérée : ✅ / ❌ [observation]

### PERSONA-003 — Edge cases
- Texte long : ✅ / ❌ [troncature / overflow]
- État vide : ✅ / ❌
- Permission refusée : ✅ / ❌

---

## Recommandations pour le guide d'entretien

Ajouter ces scénarios au guide `run-user-tests` :
1. [MA-01] Scenario : "Trouvez [tâche fréquente] et effectuez-la" → observer le nombre de taps
2. [MA-02] Scenario : "Comment appelez-vous cette section ?" → évaluer la terminologie
3. [Nouveau] Scenario : "Imaginez que vous n'avez pas de réseau — que faites-vous ?"

---

## Décisions requises avant les tests

```

---

## Étape 5 — Validation humaine

```
📋 Inspection experte terminée

🔴 [N] problèmes critiques — tests bloqués jusqu'à décision :
  Pour chaque critique :
  [A] ✅ Corriger avant les tests (estimation : [Nj])
  [B] ❌ Impossible dans le sprint → reporter en V2 et tester quand même

🟡 [N] problèmes majeurs — intégrés dans le guide d'entretien automatiquement

→ Confirmer pour lancer /run-user-tests $ARGUMENTS avec le guide mis à jour.
```

---

## Format fichier de sortie

```
specs/[epic-slug]/ux-reviews/ux-expert-review-[YYYYMMDD].md
```

## Phase de validation — niveau approfondi

1. Les 3 parcours persona (new user, regular, edge) ont-ils été simulés ? (oui / non)
2. Les rapports des audits précédents (Gate 1, 4, 6) ont-ils été consultés et leur suivi documenté ? (oui / non)
3. Tous les problèmes critiques ont-ils une décision A ou B du Product Designer ? (oui / non — **bloquant**)
4. Le guide d'entretien `run-user-tests` a-t-il été mis à jour avec les majeurs ? (oui / non)

## Résumé de fin d'exécution

```
✅ write-ux-expert-review "$ARGUMENTS" terminé
📁 specs/$ARGUMENTS/ux-reviews/ux-expert-review-[date].md

Inspection : [N] critiques · [N] majeurs · [N] mineurs
Tests utilisateurs : [🔴 BLOQUÉS / ✅ GO]

Prochaines étapes :
→ /run-user-tests $ARGUMENTS (guide mis à jour avec les majeurs)
→ Les critiques corrigés → re-valider avant de lancer
```
