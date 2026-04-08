---
name: write-ux-gestalt-check
description: "Vérifie la direction artistique des écrans principaux contre les principes Gestalt, la hiérarchie visuelle et la charge cognitive. Déclenché après Gate 6 (direction artistique), avant les écrans secondaires. Use when user says 'vérifie la DA', 'check Gestalt', 'hiérarchie visuelle', or 'write-ux-gestalt-check'."
argument-hint: "[epic-slug]"
agent: ux-designer
---

## Rôle
Évaluer la direction artistique des écrans principaux contre les principes de perception visuelle **avant** de la décliner sur les écrans secondaires. Une correction sur 3 écrans principaux coûte 10× moins cher que sur 30 écrans.

**Déclenché :** Par le Product Designer après Gate 6 (direction artistique validée).
**Bloquant :** Non — checklist courte, décision rapide. Produit 3 questions binaires auxquelles l'humain répond.

## Prérequis
- [ ] Écrans principaux (happy path) disponibles dans Figma — page `Work In Progress UI`
- [ ] Direction artistique choisie par le Product Designer (couleurs, typographie, style iconographique)
- [ ] `SCREENS-MAP.md` disponible pour identifier les écrans principaux

---

## Étape 1 — Identifier les écrans à évaluer

Depuis `SCREENS-MAP.md`, sélectionner les 3 à 5 écrans du flux principal (happy path uniquement).
Demander l'URL Figma de chaque écran principal pour analyse via `get_screenshot`.

---

## Étape 2 — Analyse via MCP Figma

Pour chaque écran principal, utiliser `get_design_context` pour extraire :
- La liste des éléments et leur position
- Les tailles relatives des éléments interactifs vs décoratifs
- Le nombre d'éléments distincts par zone

---

## Étape 3 — Évaluation Gestalt

### Hiérarchie visuelle — 3 niveaux obligatoires
Un écran bien hiérarchisé a exactement 3 niveaux de lecture distincts :
1. **Niveau 1** — Ce que l'œil voit en premier (< 0,5 sec) → action principale ou titre
2. **Niveau 2** — Ce qu'il voit ensuite (1-2 sec) → contenu et contexte
3. **Niveau 3** — Ce qu'il cherche intentionnellement → détails et actions secondaires

**Évaluation :** Peut-on identifier les 3 niveaux sur chaque écran en < 5 secondes ?

### Proximité
- Les éléments liés sont-ils visuellement proches ?
- L'espacement entre groupes est-il ≥ 1,5× l'espacement interne ?
- Les labels sont-ils adjacents à leurs contrôles (pas à travers une autre zone) ?

### Similarité
- Tous les boutons primaires ont-ils le même style visuel ?
- Tous les textes de même niveau hiérarchique ont-ils le même style ?
- Les icônes sont-elles stylistiquement cohérentes (même stroke, même fill convention) ?

### Figure / Fond
- Les éléments interactifs principaux ressortent-ils du fond sans ambiguïté ?
- Les zones de contenu et les zones d'action sont-elles visuellement distinctes ?
- Le contraste fond/figure respecte-t-il RAAM 2.2 (≥ 3:1 pour les interactifs) ?

### Charge cognitive par écran
Compter pour chaque écran principal :
- Zones d'intérêt distinctes (signal si > 5)
- Couleurs sémantiques différentes utilisées (signal si > 4 hors gris)
- Familles typographiques distinctes (signal si > 2)
- Niveaux d'élévation (ombre) distincts (signal si > 3)

---

## Étape 4 — Cohérence inter-écrans

Vérifier entre les écrans principaux :
- Le pattern d'action principale est-il identique (même position, même style) ?
- Le header/navigation est-il strictement identique en structure ?
- Les transitions documentées (push, modal) sont-elles cohérentes avec la direction artistique ?

---

## Étape 5 — Rapport et validation humaine

Produire un rapport court puis poser **3 questions binaires** au Product Designer :

```markdown
# Check Gestalt — Direction Artistique — [NomProjet] — [YYYY-MM-DD]

## Écrans analysés
[S-01 · S-02 · S-03]

## Observations

### Hiérarchie visuelle
[S-01] : ✅ 3 niveaux identifiables — action principale (CTA), contenu (liste), secondaire (filtres)
[S-02] : ⚠️ 2 éléments partagent le même poids visuel — ambiguïté sur l'action principale

### Gestalt
✅ Proximité : groupements cohérents sur les 3 écrans
⚠️ Similarité : 2 styles de boutons secondaires — S-01 (ghost) vs S-02 (text-only)
✅ Figure/Fond : éléments interactifs bien différenciés

### Charge cognitive
S-01 : 4 zones · 3 couleurs → ✅ dans les seuils
S-02 : 7 zones · 4 couleurs → ⚠️ limite haute
S-03 : 3 zones · 2 couleurs → ✅ optimal

### Cohérence inter-écrans
⚠️ Pattern bouton secondaire incohérent entre S-01 et S-02

---

## 3 questions pour le Product Designer

Q1 — L'action principale est-elle immédiatement visible sur chaque écran sans chercher ?
  → OUI : continuer · NON : retravailler la hiérarchie avant les écrans secondaires

Q2 — La direction artistique est-elle cohérente entre les 3 écrans principaux
      (mêmes patterns pour les mêmes intentions) ?
  → OUI : continuer · NON : identifier et corriger les incohérences

Q3 — La charge cognitive de S-02 (7 zones) est-elle intentionnelle
      (écran de dashboard complexe) ou peut-elle être réduite ?
  → Intentionnelle : documenter la justification · Réductible : simplifier avant de continuer
```

---

## Format fichier de sortie

```
specs/[epic-slug]/ux-reviews/ux-gestalt-check-[YYYYMMDD].md
```

## Phase de validation — niveau standard

1. Les 3 écrans principaux (minimum) ont-ils été analysés ? (oui / non)
2. Le Product Designer a-t-il répondu aux 3 questions ? (oui / non — attendre)
3. Les incohérences identifiées ont-elles été documentées pour les écrans secondaires ? (oui / non)

## Résumé de fin d'exécution

```
✅ write-ux-gestalt-check "$ARGUMENTS" terminé
📁 specs/$ARGUMENTS/ux-reviews/ux-gestalt-check-[date].md

[N] écrans analysés
Hiérarchie : [✅ / ⚠️] · Gestalt : [✅ / ⚠️] · Charge cognitive : [✅ / ⚠️]

Prochaines étapes :
→ /write-screen $ARGUMENTS (écrans secondaires)
→ Les observations sont intégrées comme contraintes pour les écrans suivants
```
