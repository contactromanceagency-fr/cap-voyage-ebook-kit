---
name: ebook-creator
description: Crée un eBook PDF magazine (guide voyage Cap Voyage ou autre sujet) via template HTML + Chrome headless, photos Wikimedia Commons vérifiées. Déclencher sur : "crée un ebook", "nouveau volume Cap Voyage", "fais le guide [pays]", "un PDF style magazine".
---

# ebook-creator

Produit un eBook PDF A4 **~23 pages**, mise en page magazine (le style de la collection **Cap Voyage**), à partir du gabarit embarqué. Tout le coût fixe (CSS, polices, logo, structure) est déjà payé dans `assets/` : un nouveau volume = photos + contenu + palette, rien d'autre.

**Gabarit de référence à jour** : `example/thailande.html` (23 pages, complet, déjà rendu en PDF dans `example/thailande.pdf` pour voir le résultat visé). Copier sa structure page par page pour tout nouveau volume, pas son contenu.

**Lisibilité mobile** : les lecteurs sont sur téléphone. Corps de texte `.cols` à 14px, tables/tips à 12-13px, padding `.inner` resserré (9mm) pour compenser sans couper le contenu (pages A4 à hauteur fixe = tout débordement est coupé).

## Steps

1. **Charger les references.** Lire `references/DA.md` (système visuel + structure vendeuse) et `references/PIPELINE.md` (commandes exactes). Fini quand : les deux fichiers sont lus.

2. **Cadrer le volume.** Fixer : sujet/pays, n° de volume, palette (2 accents dérivés de l'imagerie du lieu, cf DA.md), promesse chiffrée de couverture RÉALISTE pour le lieu, ~10 sections de contenu, et surtout l'**itinéraire 7 jours** (route cohérente) qui alimente les 3 pages plan par budget. En mode auto : décider soi-même et annoncer les choix. Fini quand : sommaire (~10 entrées + bandeau plan) + palette + route 7 jours posés par écrit.

3. **Sourcer les photos.** ~7 requêtes Wikimedia Commons (commande dans PIPELINE.md), télécharger, générer UNE planche contact, la regarder, écarter les photos faibles (sombres, hors sujet, moches). Fini quand : chaque photo retenue a été vue et couvre couverture + 1 photo par page contenu.

4. **Écrire le HTML.** Copier `example/thailande.html` comme squelette de départ + `assets/style.css` + `assets/fonts/` + `assets/logo-capvoyage.svg` dans le dossier de travail, override la palette dans le `<style>` local, réécrire tout le contenu. Structure des 23 pages : couverture, sommaire (avec le **bandeau magenta de mise en avant du plan**), ~17 pages de contenu thématique, **3 pages plan (une par budget : ROUTARD/CONFORT/PREMIUM)** = itinéraire 7 jours ultra-détaillé pour ce budget (par jour : quoi faire/où dormir+prix/où manger+prix/budget du jour, total semaine, astuce ; classes `.bhead` + `.itin`), outro. Exigences : **prix réels en monnaie locale** partout, budgets calés sur le coût réel du pays, 1 encart « LE TIP QUE PERSONNE NE DONNE » par page environ, et chaque page de contenu comblée par une bande photo ou un **bandeau récap navy** (`.band push`) pour qu'aucune page n'ait plus d'1/4 de vide. Fini quand : 23 pages écrites, zéro texte générique type brochure.

5. **Générer et contrôler.** PDF via Chrome headless (PIPELINE.md ; attendu **23 pages**), puis **QC visuel de toutes les pages** via une planche contact `pdftoppm` (une seule lecture). Corriger : contenu coupé en bas (police trop grosse / trop de texte → alléger), pages avec plus d'un quart de vide (ajouter `.band push` ou bande photo), photos mal cadrées (`background-position`). Régénérer, ne relire que les pages retouchées. Fini quand : chaque page vue et aucune ne présente de défaut listé.

6. **Livrer.** Copier dans `~/Downloads/CAP-VOYAGE-EBOOKS/` sous `VOLxx_SUJET_CapVoyage.pdf` (ou le dossier demandé), annoncer le chemin. Fini quand : le fichier existe à destination.

## Garde-fous

- Photos Commons = licences CC avec attribution. Pour une **vente réelle**, les crédits auteur/licence doivent être nominatifs (pas juste « Wikimedia Commons ») ou les photos remplacées par des images libres de droits commerciales. Le signaler à chaque livraison tant que la mention « document de démonstration » figure dans les crédits.
- Ne jamais inventer un prix : donner des fourchettes plausibles datées (« prix constatés » + année), cohérentes entre pages (couverture ↔ page budget ↔ calcul final).
