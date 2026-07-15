# Cap Voyage — Ebook Kit

Kit prêt à l'emploi pour générer les guides voyage PDF **Cap Voyage** (même format que les volumes Thaïlande/Bali/Vietnam/Japon/Maroc) directement avec Claude Code, sans repartir de zéro à chaque fois.

Tout le travail de mise en page (charte graphique, polices, structure des 23 pages, mécanique de vente) est déjà encodé dans le skill `.claude/skills/ebook-creator/`. Pour un nouveau volume, tu n'as plus qu'à donner le pays à Claude : il source les photos, écrit le contenu, génère le PDF et se corrige tout seul si une page déborde.

## Prérequis

1. **Claude Code** installé et un abonnement Claude actif → [claude.com/claude-code](https://claude.com/claude-code)
2. **Google Chrome** installé (sert de moteur de génération PDF en arrière-plan)
3. **Pillow** (Python, sert à assembler les planches contact photos) : `pip3 install pillow` (ou `pip install pillow`)

**Sur Mac :**
```bash
brew install poppler   # outil de contrôle qualité des PDF
```

**Sur Windows :** les commandes du skill sont en syntaxe bash, donc installer Claude Code sous **WSL2 (Ubuntu)** plutôt qu'en PowerShell natif — c'est ce qui évite le plus de frictions. Une fois dans WSL :
```bash
sudo apt install poppler-utils
```
Chrome reste celui installé côté Windows, le pipeline va le chercher via son chemin par défaut (`/mnt/c/Program Files/Google/Chrome/...`) — voir `references/PIPELINE.md` section 3 si le chemin diffère chez toi.

## Installation

```bash
git clone https://github.com/contactromanceagency-fr/cap-voyage-ebook-kit.git
cd cap-voyage-ebook-kit
claude
```

Une fois dans Claude Code, le skill `ebook-creator` est détecté automatiquement (dossier `.claude/skills/`). Aucune autre config.

## Utilisation

Dans Claude Code, demande simplement, par exemple :

```
Crée un ebook Cap Voyage pour la Grèce, volume 6
```

Claude va :
1. Lire les references du skill (charte + pipeline technique)
2. Te proposer le sommaire, la palette et l'itinéraire 7 jours (ou décider seul si tu le laisses en mode auto)
3. Sourcer les photos (Wikimedia Commons, licences libres avec attribution)
4. Écrire les 23 pages en HTML
5. Générer le PDF et vérifier visuellement chaque page
6. Livrer le fichier dans `~/Downloads/CAP-VOYAGE-EBOOKS/`

Compte en moyenne **1h-1h30** par volume selon les allers-retours de correction.

## Ce que contient le repo

- `.claude/skills/ebook-creator/` — le skill : instructions (`SKILL.md`), charte graphique et structure vendeuse (`references/DA.md`), commandes techniques exactes (`references/PIPELINE.md`), assets fixes (CSS, polices, logo)
- `example/` — le volume Thaïlande complet (HTML + photos + PDF final) : sert de gabarit de référence pour Claude et de preuve que le pipeline tourne bien chez toi (tu peux régénérer son PDF pour tester ton install, voir commande dans `references/PIPELINE.md` section 3)

## Point d'attention avant une vente réelle

Les photos sont sourcées sur Wikimedia Commons (licences CC, gratuites mais avec obligation d'attribution nominative : auteur + licence, pas juste « Wikimedia Commons »). Le skill met une mention « document de démonstration » en attendant. Avant de vendre un volume :
- soit tu mets les crédits complets (auteur/licence) en dernière page,
- soit tu remplaces les photos par des images libres de droits commerciales (banque payante ou tes propres photos).
