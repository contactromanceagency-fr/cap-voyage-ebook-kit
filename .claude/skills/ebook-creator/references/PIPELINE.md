# Pipeline technique — commandes exactes

Dossier de travail : un dossier de scratch/temp (ex `~/Desktop/ebook-tmp/`, ou le scratchpad de session si Claude Code en propose un). Y copier d'abord `assets/style.css`, `assets/fonts/` (dossier `fonts/`), `assets/logo-capvoyage.svg` (en `img/logo.svg`), et `example/thailande.html` comme squelette de départ (copier sa structure de balises, pas son contenu Thaïlande).

**Windows** : les commandes de ce fichier sont en syntaxe bash (curl, pipes). Utiliser Claude Code sous WSL2 (Ubuntu) pour que le shell exécute tout tel quel — sinon adapter au shell natif (PowerShell/Git Bash).

## 1. Photos Wikimedia Commons

```bash
curl -s "https://commons.wikimedia.org/w/api.php?action=query&format=json&generator=search&gsrnamespace=6&gsrlimit=4&prop=imageinfo&iiprop=url%7Cmime&iiurlwidth=1600" \
  --data-urlencode "gsrsearch=filetype:bitmap <REQUETE>" -G
```
- Prendre `thumburl` du premier résultat `image/jpeg`, télécharger avec `curl -sL -A "Mozilla/5.0" -o img/x.jpg <url>`.
- L'API rend parfois du vide : retry avec `time.sleep(3)`, et `--max-time 30`.
- Requêtes en anglais, spécifiques (« Chureito Pagoda Mount Fuji » bat « Japan temple »).

## 2. Planche contact (1 seule lecture pour tout vérifier)

PIL (`pip3 install pillow` si absent) : thumbnails 320px collés sur une grille 4 colonnes avec le nom de fichier, sauver en PNG, puis **Read** le PNG. Jamais lire les photos une par une.

## 3. Génération PDF

Mac :
```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
  --no-pdf-header-footer --virtual-time-budget=12000 \
  --print-to-pdf="$PWD/volume.pdf" "file://$PWD/volume.html"
```

Windows (WSL, Chrome installé côté Windows — chemin par défaut) :
```bash
"/mnt/c/Program Files/Google/Chrome/Application/chrome.exe" --headless --disable-gpu \
  --no-pdf-header-footer --virtual-time-budget=12000 \
  --print-to-pdf="$(wslpath -w "$PWD/volume.pdf")" "file://$PWD/volume.html"
```

```bash
pdfinfo volume.pdf | grep Pages   # attendu : 23
```

## 4. Pièges connus (déjà payés, ne pas re-débugger)

- `.page` fait `height:296.8mm` (PAS 297) sinon pages blanches intercalées.
- `@page{size:A4;margin:0}` + `-webkit-print-color-adjust:exact` déjà dans style.css.
- Polices : `@font-face` avec chemins relatifs `fonts/*.woff2` (déjà dans style.css) — jamais de Google Fonts distant (rendu non garanti au print).
- `.inner` est en flex-column : la classe **`.push`** (`margin-top:auto`) pinne un bloc en bas de page — c'est l'outil anti-« bas de page vide ».
- Si une page a un creux central : bande photo `<div style="height:40mm;background:url(...) center/cover;">` entre le contenu et le bloc pinné.
- Cadrage d'une photo dans une bande : jouer `background-position` (`center 30%`…), vérifier au QC.
- `pdftoppm` (poppler) requis pour le QC visuel : `brew install poppler` (Mac) ou `sudo apt install poppler-utils` (Windows/WSL Ubuntu).
- Vérifier TOUTES les pages au QC (une seule passe Read du PDF entier) ; corriger puis ne relire que les pages touchées.
