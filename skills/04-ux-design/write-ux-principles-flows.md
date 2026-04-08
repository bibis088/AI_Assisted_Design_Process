---
name: write-ux-principles-flows
description: "Évalue les flux fonctionnels contre les heuristiques Nielsen H1/H3/H5/H9 et la loi de Miller. Détecte les problèmes cognitifs avant la traduction en écrans. Non bloquant — produit un rapport priorisé. Use when user says 'vérifie le flux', 'audit heuristique specs', 'principes UX flux', or 'write-ux-principles-flows'."
argument-hint: "[epic-slug]"
agent: ux-designer
---

## Rôle
Évaluer les flux fonctionnels (`FLUX-###`) et les specs (`EPIC.md`) contre les principes UX de référence **avant** leur traduction en user flows et écrans. C'est le moment où une correction ne coûte rien — modifier du texte plutôt que des maquettes.

**Déclenché :** Automatiquement à la fin de `write-specs`, avant validation Gate 1.
**Bloquant :** Non — produit un rapport et soumet les décisions à l'humain.

## Prérequis
- [ ] `specs/[epic-slug]/EPIC.md` disponible
- [ ] `specs/[epic-slug]/features/FLUX-###.md` disponibles (au moins 1)
- [ ] `specs/[epic-slug]/personas/` disponibles

---

## Étape 1 — Lire les sources

Extraire depuis les flux fonctionnels :
- Toutes les étapes séquentielles de chaque FLUX-###
- Les cas d'erreur et flux alternatifs documentés
- Le nombre d'étapes par flux (compter)
- Les décisions demandées à l'utilisateur (compter les choix par étape)

---

## Étape 2 — Évaluation par heuristique

### H1 — Visibilité de l'état du système
Pour chaque étape du flux, répondre :
> "L'utilisateur sait-il ce qui se passe pendant et après cette étape ?"

**Signaux d'alerte à détecter dans le flux :**
- Étape sans feedback défini (ex : "l'utilisateur soumet" → pas de suite documentée)
- Action asynchrone sans état intermédiaire mentionné
- Résultat d'une action non explicité

### H3 — Liberté et contrôle
Pour chaque étape :
> "L'utilisateur peut-il annuler, revenir ou corriger à ce stade ?"

**Signaux d'alerte :**
- Étape irréversible sans confirmation préalable dans le flux
- Flux sans point de sortie documenté
- Action destructive (suppression, envoi définitif) sans mention d'une étape de confirmation

### H5 — Prévention des erreurs
Pour chaque saisie ou choix utilisateur :
> "Le flux anticipe-t-il l'erreur avant qu'elle se produise ?"

**Signaux d'alerte :**
- Champ de saisie sans format guidé documenté
- Choix multiple sans aide contextuelle
- Validation uniquement post-soumission (pas de validation inline mentionnée)

### H9 — Aide à la correction des erreurs
Pour chaque cas d'erreur documenté :
> "Le flux définit-il une condition + cause + action corrective ?"

**Signaux d'alerte :**
- Cas d'erreur sans message associé
- Message d'erreur sans action corrective proposée
- Erreur technique exposée à l'utilisateur (code HTTP, message système)

### Loi de Miller (7 ± 2)
Compter par flux :
- Nombre d'étapes séquentielles (> 7 = signal d'alerte)
- Nombre de choix présentés simultanément à une même étape (> 5 = signal d'alerte)
- Nombre d'informations à mémoriser d'une étape à l'autre (> 3 = signal d'alerte)

---

## Étape 3 — Produire le rapport

```markdown
# Rapport UX Principes — Flux Fonctionnels — [NomProjet] — [YYYY-MM-DD]

## Résumé
- Flux analysés : [N]
- Problèmes détectés : [N] (dont [N] priorité haute)
- Recommandation globale : [✅ Flux sains / ⚠️ Corrections suggérées avant UX]

---

## Problèmes détectés

### [FLUX-###] — [Nom du flux]

| # | Heuristique | Étape concernée | Problème détecté | Priorité |
|---|-------------|----------------|-----------------|---------|
| 1 | H1 — Visibilité | Étape 3 : soumission | Aucun feedback défini après envoi du formulaire | 🔴 Haute |
| 2 | H5 — Prévention | Étape 2 : saisie email | Format non guidé, validation uniquement à la soumission | 🟡 Moyenne |
| 3 | Miller | Global | 9 étapes séquentielles — dépasse le seuil de 7 | 🟡 Moyenne |

### [FLUX-###] — [Nom du flux]
[même structure]

---

## Recommandations

| # | Action suggérée | Coût | Impact |
|---|----------------|------|--------|
| 1 | Ajouter une étape de confirmation post-soumission dans FLUX-001 | Faible (modifier le flux texte) | Élimine le problème H1 |
| 2 | Spécifier la validation inline dans les CA de l'US-### concernée | Faible | Élimine H5 |
| 3 | Découper FLUX-003 en 2 sous-flux (étapes 1-4 et 5-9) | Moyen | Réduit la charge cognitive |
```

---

## Étape 4 — Demande de validation humaine

Présenter systématiquement ce bloc au Product Designer :

```
📋 Rapport UX Principes — [N] problèmes détectés

Pour chaque problème, choisir une action :

Problème 1 (🔴 Haute) — H1 Visibilité — FLUX-001 étape 3
  [A] ✅ Corriger maintenant dans le flux → le BA met à jour FLUX-001
  [B] ⏭️ Corriger en phase UX → le UX Designer intègre le feedback dans les specs d'écrans
  [C] 📋 Reporter en V2 → documenter comme dette UX connue

Problème 2 (🟡 Moyenne) — Miller — FLUX-003
  [A] / [B] / [C]

→ Indiquer A, B ou C pour chaque problème.
→ Le process continue dans tous les cas — ce rapport ne bloque pas Gate 1.
```

---

## Format fichier de sortie

```
specs/[epic-slug]/ux-reviews/ux-principles-flows-[YYYYMMDD].md
```

## Phase de validation — niveau standard

1. Tous les FLUX-### disponibles ont-ils été analysés — aucun oublié ? (oui / non)
2. Chaque problème détecté a-t-il une priorité et une recommandation actionnables ? (oui / non)
3. Le Product Designer a-t-il statué sur chaque problème (A/B/C) ? (oui / non — attendre la réponse)

## Résumé de fin d'exécution

```
✅ write-ux-principles-flows "$ARGUMENTS" terminé
📁 specs/$ARGUMENTS/ux-reviews/ux-principles-flows-[date].md

[N] flux analysés · [N] problèmes détectés
  🔴 Haute   : [N] → [N] corrigés maintenant / [N] en phase UX / [N] V2
  🟡 Moyenne : [N] → répartition idem
  🟢 Mineure : [N]

Prochaines étapes :
→ Gate 1 — validation fonctionnelle (non bloquée par ce rapport)
→ /write-user-story $ARGUMENTS
```
