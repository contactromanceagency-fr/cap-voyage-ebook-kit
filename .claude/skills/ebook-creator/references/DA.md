# DA & structure vendeuse — collection Cap Voyage

## Identité fixe (ne pas toucher)

- **Marque** : Cap Voyage — TikTok @cap.voyage0 — contact capvoyagepro@gmail.com.
- **Logo** : `assets/logo-capvoyage.svg` (rond flat : palmier, volcan, plage, traînée d'avion). Présent : bas de couverture, coin du sommaire, outro.
- **Polices** (woff2 locaux dans `assets/fonts/`) : Sacramento = titres script (nom du pays, « À toi de jouer ») ; Oswald = gros titres capitales espacées ; Montserrat = labels/encarts/wordmark ; PT Serif = corps de texte.
- **Tagline couverture** : « DESTINATIONS - BUDGETS - BONS PLANS » (la bio du compte).
- **Grammaire visuelle** (tout est dans `style.css`) : cadre photo autour des pages contenu (`.frame` + `.inner`), sommaire à lettres géantes pastel, texte 2 colonnes à intertitres colorés, encarts `.tip`, bandeau navy `.band`, cartes `.xp`, tableau `.isles`, barres budget `.bud`.

## Ce qui varie par volume

- **Palette** : override des variables `:root` dans le `<style>` local (voir exemple-volume.html). 2 accents tirés de l'imagerie du lieu (Thaïlande turquoise/magenta, Bali jungle/terracotta, Vietnam lanterne jaune/rouge, Japon rouge torii/indigo, Maroc majorelle/safran). `--cream` et `--pink` s'accordent aux accents.
- **Une page signature** (page 7) propre au sujet : itinéraire timeline (Vietnam), scénarios en tableau (Bali), myth-busting prix (Japon), négociation/désert (Maroc). C'est la page qui différencie le volume, y mettre la créativité.
- **Un micro-twist DA** optionnel : ornement trait fin (Japon), vignettes en arche (`border-radius` haut, Maroc)… Un seul par volume, discret.

## Structure des 10 pages

1. Couverture : photo iconique plein cadre, nom script, banner, **promesse chiffrée** (bandeau blanc), logo + VOL. xx.
2. Sommaire : 6 entrées à barres colorées, note « comment lire ce guide » + @cap.voyage0.
3. L'essentiel : visa, quand partir, argent, SIM, applis + `.band` checklist départ (pinnée bas).
4. Page section : photo pleine page + script + 3 mini-tips en bas sur dégradé sombre.
5. Bons plans zone 1 : strip 3 photos + 2 colonnes.
6. Zone 2 : bande photo + 2 colonnes.
7. **Page signature** (voir plus haut).
8. Food : photo + règle d'or + `.pricelist` 7-8 plats + codes locaux.
9. Budget & pièges : 3 profils `.bud`, top 5 arnaques numérotées, `.band` « le calcul final » qui BOUCLE avec la promesse de couverture.
10. Outro : « À toi de jouer », cartes des AUTRES volumes (upsell), CTA TikTok, stats (nb tips / prix réels / économies), demande de note 5 étoiles, crédits.

## Les leviers qui font acheter le volume suivant

- Promesse chiffrée en couverture, tenue et rappelée page 9 (« la promesse de la couverture, tenue »).
- Densité de chiffres : prix en monnaie locale partout, jamais d'à-peu-près vide.
- « LE TIP QUE PERSONNE NE DONNE » : 1 par page contenu, chacun doit valoir seul le prix du guide.
- Page 10 : le lecteur doit repartir avec le sentiment d'avoir déjà rentabilisé l'achat, et voir la collection.
- Ton : tutoiement, direct, complice, zéro brochure d'office de tourisme.
