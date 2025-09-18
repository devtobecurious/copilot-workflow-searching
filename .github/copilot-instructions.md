# Instructions globales pour le projet de roman

## 1. Gestion des versions
- Utiliser un système de contrôle de version (ex : Git).
- Commiter chaque ajout ou modification significative avec un message clair.

## 2. Workflow des features (avec création auto d’issue si absente)
Avant chaque feature ou tâche :

1. Vérifier la branche courante.
   - Si sur `main`, demander: "Donne-moi l'ID ou l'URL de l'issue à réaliser." (ne pas continuer sans).
2. Exiger un identifiant d’issue (format accepté : `#123`, `PROJ-123` ou URL GitHub/GitLab).
   - Si absent ou texte libre → refuser et redemander.
3. Rechercher l’issue distante :
   - Utiliser le remote `origin` (GitHub prioritaire).
   - Si trouvée → lire et afficher son contenu, demander confirmation si ambigu.
   - Si non trouvée → demander: "Donne le titre de la feature (impératif, clair)."
4. Création automatique de l’issue (si absente) via l’agent (MCP tool):
   - Titre: fourni par l’utilisateur.
   - Corps généré avec le gabarit :

     ```
     Contexte:
     (résumé du besoin)

     Problème:
     (ce qui manque ou bloque)

     Objectif:
     (résultat attendu)

     Critères d’acceptation:
     - [ ]
     ```

   - Labels suggérés: `feature` ou `bug`.
   - L’agent retourne l’URL de l’issue créée et l’ID.
5. Vérifier la clarté:
   - Si critères d’acceptation manquants ou vagues → demander précisions avant de coder.
6. Nommer et créer la branche :
   - feature/{id}-{slug-titre} ou bugfix/{id}-{slug-titre}
   - slug: minuscules, tirets, sans accents, max ~8 mots.
7. Travailler sur la branche (tests + lint).
8. Commits (Conventional Commits) :
   - `feat: ... (#id)` / `fix: ... (#id)` / etc.
9. Push de la branche.
10. Création automatique de la Pull Request (sans demander) :
    - Titre: même que l’issue (ou précisé si implémentation partielle).
    - Corps: Contexte / Solution / Tests / Checklist / Lien issue.
11. Attendre revue.
12. Appliquer corrections si demandées.
13. Merge (selon politique: squash conseillé).
14. (Optionnel) Tag si livraison versionnée.

> IMPORTANT : L’agent ne commence JAMAIS à coder sans issue valide distante (existante ou créée).

### Détails sur la création automatique (MCP)
- Tool attendu: `createIssue` (ou équivalent GitHub).
- Paramètres minimum:
  - repository: dérivé du remote `origin`.
  - title: fourni.
  - body: gabarit ci-dessus (adapté si info fournie).
  - labels: ex: `["feature"]` ou `["bug"]`.
- Retour stocké: issueNumber, issueUrl.

### Règles de refus
Refuser d’avancer et redemander si :
- Pas d’ID ou d’URL issue.
- Titre absent lors de création.
- Critères d’acceptation trop vagues (ex: "faire mieux", "optimiser").

## 3. Branch protection
- main: protégée (PR obligatoire, 1 review minimum, tests verts).

## 4. Issues
- Format ID: #123 (GitHub) ou PROJ-123.
- Titre: impératif, concis.
- Doit contenir: Contexte / Problème / Objectif / Critères d’acceptation.

## 5. Branches
- feature/{id}-{slug-titre}
- bugfix/{id}-{slug-titre}
- slug: minuscules, tirets, sans accents.

## 6. Commits (Conventional Commits)
- feat: ..., fix: ..., refactor: ..., docs: ...
- Inclure `(#id)` en fin de sujet.

## 7. Processus synthèse
1. Vérifier branche ≠ main.
2. Identifier / créer issue (auto si absente).
3. Créer branche.
4. Développer (tests, lint).
5. Commits propres.
6. Push.
7. PR auto.
8. Revue / corrections.
9. Merge.
10. Tag si release.

## 8. PR Checklist
- [ ] Issue liée (auto via #id)
- [ ] Tests ajoutés / mis à jour
- [ ] Lint OK
- [ ] Description complète
- [ ] Pas de secrets

## 9. Qualité
- Tests obligatoires pour logique nouvelle.
- Couverture cible (ex: 70%+).

## 10. Conflits / Rebase
- Rebase avant merge si divergence > 10 commits.
- Pas de force push sur main.
