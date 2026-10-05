# R579 — Hotfix PDF annotés manquants — PR #14

**Date :** 2026-10-06  
**Session :** R579  
**CERTIFIED_100=false | unique_human_proven=false | Mode DEBUG actif**

---

## 1. Contexte

Suite à la PR #13 (mergée le 2026-10-05), les participants ont signalé l'absence des **PDF annotés** dans la soumission `vgactech_artcb`. Les JSON de réponses étaient bien présents, mais les formulaires PDF complétés (`completed_form_01..05.pdf`) n'avaient pas été inclus.

**Cause racine :** Le commit `0a7ae5f` ("Remove PDFs from PR branch") avait explicitement retiré les PDF de la branche `submissions/vgactech-artcb` avant la PR #13, probablement pour réduire la taille du push. Les JSON avaient été mergés sans les PDF.

---

## 2. Avant / Après

### Avant (état PR #13 mergée)

Dossier `SUBMISSIONS/vgactech_artcb/` sur `lynadatacraft/main` :

```
README.md            1 571 bytes
answers_form_01.json 7 074 bytes
answers_form_02.json 7 988 bytes
answers_form_03.json 8 632 bytes
answers_form_04.json 4 465 bytes
answers_form_05.json 11 227 bytes
pipeline.py          33 911 bytes
```
❌ **PDF absents**

### Après (PR #14)

Ajout du dossier `SUBMISSIONS/vgactech_artcb/outputs/` :

```
outputs/completed_form_01.pdf   208 KB  — Asterive Services SAS (FR, 2 pages)
outputs/completed_form_02.pdf 1 269 KB  — Belorive Patrimoine SAS (FR, 4 pages)
outputs/completed_form_03.pdf 1 350 KB  — Cendrelis Instruments SAS (EN, 9 pages)
outputs/completed_form_04.pdf 1 142 KB  — Belorive Patrimoine SAS (EN, 4 pages)
outputs/completed_form_05.pdf 2 553 KB  — Cendrelis Instruments SAS (PL/EN, 11 pages)
```
✅ **5/5 PDF poussés — PR #14 ouverte**

---

## 3. Vérification de cohérence PDF ↔ JSON

| Fichier | Pages | Marqueur pipeline | Cohérence JSON |
|---|---|---|---|
| completed_form_01.pdf | 2 | `[ARTCB R575 · Réponses KYC · 2026-10-06]` | ✅ même exécution |
| completed_form_02.pdf | 4 | `[ARTCB R575 · Réponses KYC · 2026-10-06]` | ✅ même exécution |
| completed_form_03.pdf | 9 | `[ARTCB R575 · Réponses KYC · 2026-10-06]` | ✅ même exécution |
| completed_form_04.pdf | 4 | `[ARTCB R575 · Réponses KYC · 2026-10-06]` | ✅ même exécution |
| completed_form_05.pdf | 11 | `[ARTCB R575 · Réponses KYC · 2026-10-06]` | ✅ même exécution |

Timestamps identiques (`Oct 5 16:00`) — PDF et JSON produits par la même exécution R575.

---

## 4. Droits GitHub — explication du 404 initial

Le token `vgactech` (GITHUB_TOKEN Doppler) **n'a pas les droits `push`** sur `lynadatacraft/atelier-model-thinking-kyc` directement :
```
Permissions: push=False, admin=False, pull=True
```
**Solution appliquée :**
1. Push des 5 PDF sur le fork `vgactech/atelier-model-thinking-kyc@submissions/vgactech-artcb` ✅
2. Ouverture d'une PR depuis le fork vers `lynadatacraft/main` ✅

---

## 5. PR créée

- **PR #14** : https://github.com/lynadatacraft/atelier-model-thinking-kyc/pull/14
- **Titre** : `Add annotated PDFs — vgactech_artcb (R579 hotfix)`
- **Head** : `vgactech:submissions/vgactech-artcb`
- **Base** : `lynadatacraft:main`
- **Fichiers** : 5 PDF dans `SUBMISSIONS/vgactech_artcb/outputs/`

---

## 6. Structure finale attendue après merge

```
SUBMISSIONS/vgactech_artcb/
├── README.md                          ← description pipeline
├── answers_form_01.json               ← 25 champs (24 answer / 1 N/A)
├── answers_form_02.json               ← 25 champs (24 answer / 1 N/A)
├── answers_form_03.json               ← 26 champs (25 answer / 1 N/A)
├── answers_form_04.json               ← 19 champs (19 answer)
├── answers_form_05.json               ← 29 champs (28 answer / 1 N/A)
├── pipeline.py                        ← code source R575
└── outputs/
    ├── completed_form_01.pdf          ← formulaire KYC annoté (208 KB)
    ├── completed_form_02.pdf          ← formulaire KYC annoté (1.2 MB)
    ├── completed_form_03.pdf          ← formulaire KYC annoté (1.3 MB)
    ├── completed_form_04.pdf          ← formulaire KYC annoté (1.1 MB)
    └── completed_form_05.pdf          ← formulaire KYC annoté (2.5 MB)
```

---

## 7. État d'avancement

**Avancement : 98%**

| Tâche | État |
|---|---|
| Pipeline KYC R575 (5 exercices) | ✅ DONE |
| JSON réponses sur upstream | ✅ DONE (PR #13 mergée) |
| PDF annotés sur fork | ✅ DONE (R579) |
| PR #14 ouverte (PDF) | ✅ DONE |
| Merge PR #14 | ⏳ En attente organisateur |

---

*Rapport généré par ARTCB Agent | Mode DEBUG | CERTIFIED_100=false | unique_human_proven=false*
