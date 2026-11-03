# Projet : raccordement des chaufferies gaz à l'hyperviseur

Site ArcelorMittal Maizières Research. Réalisé par Ismail SOULLAMI.
Vérification : Jérémy STAREMBERGER, Vincent FOJUD. Notes de réunion : Stéphan, Vincent, Jérémy.

## 1. Livrables en cours

| Livrable | Format | État |
|---|---|---|
| Présentation « Point avancement chaufferies » | Beamer (.tex) | Compilée, aucun débordement. Au moins 18 diapos (arbitrage des compteurs en diapo 18) |
| Cahier des charges « Raccordement des chaufferies gaz à l'hyperviseur » | .docx | Première émission en cours de reprise |
| Synoptiques + fiches E/S automate | draw.io | B, D, F, BK/BL, T faits. Les autres sont à remplacer plus tard |

## 0. État au 03/11/2026 (le plus à jour, prime sur la suite)

### Catégories du CdC (version actuelle)

| Cat. | Définition | Installations |
|---|---|---|
| 1 | Avec automate et écran local | B (Sauter modulo 5), T et F (Sauter modulo 6), BK-BL (Schneider SmartX AS-P) |
| 2 | Sans automate, régulation Navistem | D, M, BN, BO, W |
| 3 | Sans automate, régulateurs dispersés | Hall C, G2 (Elco), NOP (Viessmann) |

Les sections 2 et 3 plus bas reprennent l'ancienne numérotation de la présentation.

### Avancement des synoptiques

- Faits : D, F, B, T, BK-BL, W, BO.
- Restants pour l'annexe A du CdC : M, BN, Hall C, G2, NOP.
- Décision Vincent (02/11) : juste le CdC pour le moment, aucun dossier documentaire joint. Réunion sur site ensuite. Puis livrets techniques des produits demandés (NAVIPASS, Vitogate, module Modbus Diehl, AS-P…) en annexe. Le dossier refondu interne vient après.
- Sources draw.io chez Ismail : `Desktop\téléchargements\Brouillon\brouillon syn\Synoptiques_`.

### Règles d'harmonisation des synoptiques (validées sur D le 21/10, complétées sur F le 23/10)

- Cadre : titre gras majuscules, fabricant majuscules, modèle, puces (Alimentation en dernier). Chaudières : Qn / Pn à 80/60 °C.
- Pas de vase ni de détail inutile pour l'hyperviseur. Organes internes (pompe d'irrigation, brûleur, régulation intégrée) non représentés.
- Zones fonctionnelles seulement si la disposition s'y prête (D oui, F non). Bloc automate et armoire obligatoire s'il y a un automate.
- Infos complémentaires en italique sous les blocs.
- Trait plein bleu : com existante. Pointillé bleu : interface COM à exploiter, un bloc par port, « … requise » si matériel à ajouter, « Port : » et « Protocole : » en gras.
- Liaisons : trait plein = folio + repère ; pointillé à points = forcément présente mais non documentée. Libellés au singulier, identiques des deux côtés.
- Vocabulaire : « à relever », « raccordement à déterminer », jamais « non raccordé ». Limiter les « à relever ».
- Vannes : « Vanne 3 voies » + photo vanne à secteur à brides + servomoteur SAL, sans réf de corps.
- Pas de nouveaux styles ni couleurs.
- Sans automate : bloc « ARMOIRE ÉLECTRIQUE - RELAYAGE », bandeau « BORNIER X1 - nn BORNES » (Repère gras | Désignation | Organe gris, ordre du bornier, une ligne par groupe), bandeau « ORGANES DE COMMANDE ET DE SIGNALISATION » (commutateurs, relais, contacteurs, voyants), ligne finale italique orange vers l'extérieur, pas de bloc COM sur l'armoire. Folio manquant : repères connus seulement, sinon « à relever ».
- Avec automate : un seul bloc automate et armoire (zone orange), pas de tableau de bornier ni de repères X, bandeau de synthèse du bornier, renvoi à la fiche automate. Tous les ports COM montrés : câblés en plein, libres en pointillé.
- Lignes finales orange (sans automate uniquement) : Pilotage / Armoire / Documentation.
- Ordre de crédibilité : photos et plaques > schémas as-built récents > listes de points et dossiers automate > liste matériel / DOE > doc constructeur. Photo > folio. Une info manquante vaut mieux qu'une info fausse.

### Besoin exprimé (S. Niedzwiedz, 07/09/2026)

1. Températures des circuits. 2. Pression du réseau (valeur). 3. Marche réelle des circulateurs (retour de marche). 4. Marche/arrêt à distance des chaudières.

### Points en suspens

- Planche F : port WAN F à corriger en HTTP + HTTPS, port RS485 B en bus SLC Sauter.
- T : bandeau alimentation « ALIMENTATION 24 V DC - EY-PS021 ».
- BK-BL : fiche automate module 7 (ordre Genersys) et module 9 (PEL 2500 en 0-10 V) ; RS485 et LON de l'AS-P sont câblés (pas libres).
- W : photos = Condensinox, DOE = Varmax 275. Photo retenue. 69 kW sans source.
- G2 : Elco KM628 sans protocole, seulement 0-10 V consigne, 0-10 V retour puissance, contact sec de marche.
- Hall C / NOP : offre Viessmann (jamais en annexe, prix) : 1 Vitogate 300 par chaufferie, 1 module LON par chaudière. NOP : les 3 Sauter equitherm M10 seront retirés, l'AS-P reprend la distribution.
- Matrice de recensement et bilan BACS à mettre à jour en fin de projet.

## 2. Catégorisation des chaufferies (ancienne numérotation de la présentation)

Principe : une catégorie = un régulateur = une interface = une solution à répliquer.

| Cat. | Famille | État |
|---|---|---|
| 1 | Schneider SmartX (BK/BL) | Installation récente, même constructeur que l'hyperviseur, protocole natif, intégration prise en charge par Schneider |
| 2 | Sauter (modulo 5 / modulo 6) | Demande des fichiers EDE des 3 automates, réunion du 16 septembre. Repli prévu sur le modulo 5 du B |
| 3 | Atlantic Navistem B3000 (BO, BN, W, M, D) | Solution trouvée, décision à prendre |
| 4 et 5 | Autres (dont NOP) | À étudier au prochain point |

Fichier EDE : liste normalisée des points d'un automate (identifiant, type, nom, unité). Permet à l'intégrateur de déclarer les points sans reprendre le programme.

## 3. Solution catégorie 3 (Navistem)

Chaîne : Navistem B3000 -> passerelle NAVIPASS Modbus (Atlantic) -> [convertisseur RTU/TCP] -> hyperviseur EcoStruxure.

- Aucun automate ajouté, la même chaîne sur les cinq chaufferies.
- NAVIPASS : lecture et écriture sur 42 registres, évite l'achat des cartes OCI345.
- Points à confirmer avec Atlantic : voir la liste des 3 questions dans la présentation.

### Pistes écartées

| Piste | Raison |
|---|---|
| Connect Box | 12 000 € par chaufferie (60 000 € pour 5), compatibilité B3000 non garantie |
| OZW672 | Accès navigateur et application, pas de protocole lisible par l'hyperviseur |
| BSB-LAN | Carte de bricolage, pas acceptable sur site industriel |

### Les deux cas présentés (diapos 6 et 7)

| Cas | Ce qui lit le RS485 | Coût ajouté |
|---|---|---|
| 1 | Un équipement côté hyperviseur avec entrée RS485 | Aucun boîtier en plus de la NAVIPASS |
| 2 (retenu au chiffrage) | Convertisseur Modbus RTU vers TCP, rail DIN | 100 à 300 € par chaufferie |

Point de vigilance : l'Enterprise Server est un logiciel sur serveur, sans port série. Seul un automate SmartX lit le RS485 nativement, ce qui coûterait 1 500 à 3 000 € par chaufferie. Le convertisseur est donc ce qui permet de ne pas mettre d'automate.

## 4. Comptage

Un seul bus RS485 par chaufferie :

| Adresse | Équipement | Données |
|---|---|---|
| 1 | NAVIPASS Modbus | Températures, modulation, défauts, consignes, horaires |
| 2 | Module compteur d'impulsions (~150 €) | Consommation gaz |
| 3 | Compteur d'énergie thermique | Énergie produite, débit, delta T |

- À vérifier avant achat : même vitesse et même parité pour tous les équipements du bus.
- Le décret impose de suivre, enregistrer et analyser la consommation, de la comparer à des références et de détecter les pertes d'efficacité. Tout repose sur le comptage.
- Gaz = entrée (ce que le site paie, base ISO 50001). Énergie thermique = sortie utile. Les deux ensemble donnent le rendement.
- Gaz : compteur déjà présent sur M, BO, BN, W (10 imp/m³, jamais raccordé). Rien sur D. Donc 4 modules à 150 € + 1 compteur à créer au D.
- Énergie thermique : 800 à 2 000 € posé (ultrasons, vidange, arrêt chauffage).
- Arbitrage proposé : au D, un seul compteur sur le départ commun au lieu de trois. Même logique possible au M.

### Énergie thermique : notions

- Puissance (kW) = valeur instantanée. Énergie (kWh) = puissance x temps. C'est l'énergie qu'on compte.
- Le compteur d'énergie thermique (compteur de calories) mesure le débit, la T° départ et la T° retour, puis intègre : sortie en kWh.
- Le compteur gaz mesure l'énergie qui entre (m³ convertis en kWh), le compteur thermique celle qui sort vers le bâtiment. Leur rapport donne le rendement.

### Où poser les compteurs thermiques

| Chaufferie | Circuits | Départ général | Par circuit |
|---|---|---|---|
| D | 3 | 1 | 3 |
| M | 2 | 1 | 2 |
| BO, BN, W | 1 chacune | 1 chacune | 1 chacune |
| Total | | 5 | 8 |

Recommandation : départ général partout (5 compteurs, rendement des 5 chaufferies). On ajoute un compteur par circuit plus tard si la répartition devient un sujet de gestion. Arbitrage présenté en diapo 18.

### Décret BACS (art. R. 175-3 du CCH)

Quatre fonctions exigées :
1. Suivre, enregistrer et analyser en continu la production et la consommation d'énergie
2. Situer l'efficacité énergétique du bâtiment
3. Détecter les pertes d'efficacité et en informer le responsable
4. Permettre l'interopérabilité

- Comptage gaz : obligation directe (le mot « consommation » y est).
- Compteur thermique : pas cité, mais c'est ce qui rend les points 2 et 3 exploitables.
- Communication seule sans compteurs : pilotage et interopérabilité oui, mais 3 exigences sur 4 tombent. La communication donne le pilotage, les compteurs donnent la conformité.
- À faire : vérifier la formulation exacte du texte avant la réunion.

### Consommation gaz estimée par la chaudière

La chaudière ne mesure pas le gaz, mais elle donne les heures de marche brûleur, le nombre de démarrages et le taux de modulation. On en tire une estimation gratuite dès la mise en communication (marche le week-end, conso qui double). Écart de 10 à 20 %, donc insuffisant pour un rendement. La communication donne un indicateur approché, le compteur en fait une mesure.

### Liaison vers l'hyperviseur (sans-fil)

- Dans la chaufferie (régulateur, passerelle, compteurs) : RS485 filaire, quelques mètres. Rien à changer.
- De la chaufferie vers l'hyperviseur : le convertisseur sort de l'Ethernet, qui peut voyager par n'importe quel moyen.

| Option | Coût | Remarque |
|---|---|---|
| Câble ou fibre | Élevé, génie civil | Le plus fiable, délai long |
| Wi-Fi sur point d'accès existant | Quasi nul | Rare : locaux techniques enterrés et métalliques |
| Pont Wi-Fi entre bâtiments | 500 à 1 500 € par lien | Demande une vue directe |
| Routeur 4G industriel | 300 à 600 € + abonnement | VPN obligatoire, validation par l'informatique du site |
| LoRaWAN / IoT | Faible | À écarter : débit trop faible, pas de pilotage fiable |

- Même problème pour les automates : BK/BL n'est raccordé que grâce au serveur local du bâtiment. F, B et T ont du BACnet/IP natif mais ne sont raccordés à rien.
- Le lien réseau est un coût commun à toutes les catégories. Il faut le lancer maintenant, en parallèle. La 4G se discute avec l'informatique (matrice de flux Schneider avec DMZ et VPN).

### Réponse : pourquoi relever les raccordements actuels au bornier

Parce que ce qui est déjà câblé décide de ce qu'il faut ajouter.
- D : 12 contacts de marche et de défaut déjà au bornier, rien à faire.
- W : la pompe a déjà une commande externe et un contact de signalisation.
- BO, BN, M : pompes en alimentation permanente, sans commande, il faut ajouter un organe.

Sans ce relevé, chiffrage au pire cas partout. Avec, le nombre exact d'organes à poser par installation. Le relevé est aussi réutilisable : Schneider demande des tables d'échange, des plans d'adressage et des plans d'implantation dans ses prérequis.

## 5. Les cinq chaufferies catégorie 3

| Chaufferie | Points clés |
|---|---|
| BO | Cas de référence : 1 chaudière, 1 circuit, 4 aérothermes, thermostat mural remplacé par une sonde. Relevé de bornier à compléter |
| BN | Deux zones. L'horloge mécanique jour/nuit disparaît. Extracteur et volet d'air neuf hors périmètre |
| W | Pompe avec commande externe et retour défaut. 3 groupes d'aérothermes. 69 kW, sous le seuil : périmètre complet ou allégé ? |
| M | Cartes de com déjà présentes (cascade), sondes existantes, comptage gaz existant. La mieux dotée |
| D | 3 circuits à vanne, 3 vannes motorisées absentes du bornier et des folios. Premier gisement d'économie potentiel, à vérifier en visite |

## 6. Dossier projet et refonte du CdC

### Dossier « Chaufferies gaz - Dossier refondu » (zip)

- Source chez Ismail : dossier `Chaufferies_Stage` (environ 940 Mo, trop lourd à envoyer d'un bloc). Inventaire obtenu avec `dir /s > liste.txt`.
- Structure : Livrables (CdC, bilan BACS, matrice de recensement, synoptiques), Echanges constructeurs et integrateurs (Schneider 6 docs dont organigramme et matrice de flux, Atlantic 6 docs, Viessmann Vitogate 300 + EA1), Reunions (point du 10/09, CR Sauter, SCS, Atlantic), un dossier par chaufferie (D, F, B remplis), LISEZMOI à la racine et par chaufferie.
- Pas de dossier racine dans le zip, pas de « v2 ». Chemin le plus long : 252 caractères (limite Windows 260).
- Volontairement exclus : offre Viessmann du 21/10 (contient des prix, à décider). Pas encore reçus : point d'avancement du 08/10, « Aspect réglementaire » (2 xlsx).
- Plus tard, une chaufferie à la fois (T, BK-BL, Hall C…) : envoyer seulement le sous-dossier « Annexes - docs techniques » + photo de l'armoire. Lourds : NOP 60 Mo, G2 87 Mo, M 85 Mo.
- À trier plus tard : NOP (86639-DOE.pdf et DOE - NOP.pdf probablement en double), G2 (12 scans doc0602…pdf sans nom parlant), T (Vento Connect et Vento Connect v2).

### Refonte du CdC (priorité actuelle)

Objectif : le dossier passe au second plan, on reconstruit le CdC à partir de la dernière version (« Cahier des charges - Raccordement des chaufferies gaz à lhyperviseur 2.docx », version du 21/10). Le CdC doit dire précisément ce qu'on veut pour chaque installation. Les documents intégrateurs et constructeurs vont en annexe.

Ce qui est bon : catégories, architecture AS-P, Modbus TCP, intégration par Schneider.

À reprendre :
- §4.1.6 à 4.1.8 (dispositions par installation) : 2 lignes chacune. Écrire pour chaque chaufferie le matériel à ajouter (NAVIPASS, Vitogate…), les liaisons et les points.
- §4.2 (performances) et §6.6 (paiement) : encore le texte du modèle.
- §4.1.2 : faute de frappe « jde la gamme SpaceLogic ».
- Ordre proposé : B, D, F d'abord (synoptiques vérifiés).

Incohérences à corriger :
- Hall C : 920 kW dans le CdC (total 7 086 kW) contre 1 000 kW dans le bilan BACS.
- Matrice de recensement du 08/09 pas à jour : pompes CTA de B notées MAGNA3, pompe du magasin de D notée pompe double, mise en service « Sept. 2021 » pour D sans source.

## 7. Consignes pour la première émission du CdC

- Viessmann, Elco, Atlantic : on suit les préconisations constructeur (modules LON, etc.). Préciser que c'est le constructeur qui l'a indiqué.
- Viessmann : un boîtier par installation, soit un boîtier pour deux chaudières.
- Standards, clés, etc. : pas bloquant pour la première émission (avis du tuteur). Indiquer « à transmettre ultérieurement ».
- Synoptiques : garder ceux rénovés, laisser les autres en place (remplacés plus tard). Les mettre le plus grand possible, sans perte de résolution. Le BO doit être lisible.
- Tableaux : plus simples, sans fond gris.
- Garder les liens cliquables de renvoi.
- Ajouter un petit organigramme par catégorie, comme celui du Viessmann.
- Intégrer les notes de Stéphan, Vincent et Jérémy.
- Ton : clair, pro, sobre, sans ambiguïté.
- Annexes : offres pertinentes.

## 8. Préférences de rédaction

- Pas de tirets cadratins (« — »). Utiliser deux-points, points médians ou tirets courts.
- Style sobre, pas de tournures qui font « IA ».

## 9. Reste à faire

- [ ] Reconstruire le CdC à partir de la version 2 (dispositions par installation, annexes)
- [ ] Corriger les incohérences Hall C et matrice de recensement
- [ ] Remplacer les synoptiques dans le CdC avec les nouvelles versions draw.io
- [ ] Questions à Atlantic sur la NAVIPASS
- [ ] Question à Schneider : entrée RS485 côté hyperviseur (cas 1) ?
- [ ] Visite au D (vannes motorisées)

## 10. Chaufferie M (relecture du 03/11/2026)

Docs reçus : planche rev 00 (25/08/2026), DOE Dalkia « Travaux Chaufferie M » (41 p.), folios armoire aérothermes Dalkia 02-03 (04/04/2019), schéma câblage CIAT, fiche Belimo, extraits Varmax et Lowara, 30 photos de visite.

Relevé (photo > folio > DOE) :
- Chaudière 1 : plaque Varmax 275, Qn 66-275 kW, Pn 64,3-268 kW à 80/60, PMS 6 bar, gaz 300 mbar, 230 V mono, 238 W, n° V271819613, 2018. Maître.
- Chaudière 2 : étiquette interne n° V103812830 (photo 7). C'est le numéro du rapport de mise en service rangé dans le DOE de W : ce rapport concerne en fait M. A corriger dans les notes W.
- Cascade LMS + OCI345 + sonde extérieure, adresse LPB 2/0, V2V pilotées par la chaudière (rapport de mise en service Atlantic, intervention 01/10/2018, édité le 24/03/2021). Le rapport mentionne aussi un circuit radiateur mélangé « piloté par régulation client » et « régulation réseau secondaire : automate / AVS 75 » : non vu en photo.
- Armoire aérothermes : bornier X1 24 bornes, S1 AUTO/0/MANU, thermostat X1:3-4, GV1-GV4 + KM1-KM4 (une vitesse), ipsotherme en série avec la bobine KM (X1:8-9…), 4 voyants marche, 4 défaut, 1 sous tension. Conforme aux folios 02 et 03.
- Circuit bureaux : pompe double Grundfos UPS D40-60 F, 3 x 400 V, 3 vitesses, sans communication (photo 13). Sonde Siemens QAD22 sur la tuyauterie.
- Circuit atelier : Grundfos MAGNA3 D 50-120 F 280, 230 V (photo 11).
- Pot à boue : pompe Lowara ecocirc XL, taille illisible en photo.
- Compteur gaz : émetteur COMMON LFK1, 10 imp/m³ (photo 27, propre à M).
- Hors hyperviseur (à retirer) : vase Reflex, ballon électrique Altech CE ALT 250 (3 kW, 230 V), filtre Honeywell, disconnecteur.
- LISEZMOI : piquages des retours inversés et V2V sur les retours (rapport de mise en service).

### Planche M rev 01 (03/11/2026)

- Reconstruite à partir du fichier d'Ismail, sur le modèle de BO (planche validée la plus proche : Navistem, aérothermes CIAT, armoire de relayage, compteur COMMON) et des règles de D. Police conservée à 7 comme D.
- Colonnes : à gauche production (2 chaudières), équipements lus et pilotés par les chaudières (sonde extérieure, 2 vannes d'isolement), comptage gaz ; au centre l'armoire (bornier, organes, SYNTHÈSE) ; à droite aérothermes et commande, circuit bureaux, circuit atelier, filtre à boues.
- Étiquettes de liaison des chaudières vers leurs organes rangées dans l'ordre inverse des cibles pour qu'aucun trait ne se croise.
- Retirés : vase d'expansion, bloc ECS électrique. Ajoutés : NAVIPASS (pointillé bleu) par chaudière, bandeau SYNTHÈSE, entrée « Communication existante » au guide de lecture.
- Épaisseurs de trait : cases en trait plein et en pointillé à 1, pointillé à points à 2 ; zones orange inchangées (2).
- Texte parasite invisible (code draw.io collé) trouvé aussi dans D (cadre « AÉROTHERMES OUEST ») et BK-BL : même cause que les impressions à rallonge de BO.

### Planche BN rev 01 (03/11/2026)

- Reconstruite à partir du PDF (pas de .drawio fourni), sur la grille et les styles de M / BO. Sources : schéma électrique de l'armoire (9 folios, bornier X1 26 bornes et X2 30 bornes), photos du 26/08/2026, schéma de principe Dalkia affiché en chaufferie (28/11/2023). Pas de DOE.
- Plaques : Varmax 275 n° V041020782 (2020), Qn 275 / Pn 268 kW, 300 mbar ; Grundfos MAGNA1 D 32-120 F 220, 1 x 230 V ; compteur COMMON CPT-01 QUANTOMETER DN 50 G40, Qmax 65 m³/h, 2021.
- Corrigé : bloc LPB « OCI345 requis » remplacé par la NAVIPASS ; MAGNA1 = entrée marche/arrêt + relais de défaut (doc Grundfos), câblés au bornier X1 selon folios 04-05 et visibles en photo ; « 10 imp/m³ » retiré (absent de la plaque) ; repère H3 et « deux vitesses disponibles » retirés (non documentés).
- À mettre au LISEZMOI BN : schéma de principe = MAGNA1 D 32-80 et deux radiateurs (plaque et folios retenus : 32-120 F 220, un ventilo-convecteur Q9) ; folio 06 nomme Q9 à Q14 les disjoncteurs des aérothermes (Q11 à Q16 au folio 03, retenu) ; marque des aérothermes non relevée (la photo utilisée est celle d'un CIAT).

### Planche G2 rev 01 (03/11/2026)

- Reconstruite sur la grille M / BN à partir du .drawio d'Ismail (images reprises). Sources lues : dossier électrique SETIA (indice B tel que construit 11/12/2014, folio 14 annoté indice C 24/03/2016 ; les deux scans doc0249 et doc0251 sont le même dossier), schéma de principe Dalkia affiché (02/02/2015, nomenclature), documentation Elco Rendamax 3501-3505 (avril 2005), option Elco « Potentialfreie Sammelstörung », codes défauts R3000 / KKM8, 41 photos.
- Plaque (une seule chaudière photographiée deux fois, S/N 3581510KE142400000134) : R 3501, Q(Hi) 653 kW, P 80/60 613 kW, G20 20 mbar, 3 x 400 V, PMS 8 bar.
- Corrigé : pompes de charge = Xylem Ecocirc XL 65-120 F (nomenclature Dalkia, folio 12 : 230 V 4,1 A, tête verte en photo) et non Salmson Siriux ; pompe 2 ancien bâtiment = Salmson Zoom 320C 400 V 3~ (nomenclature + folio 12) ; sondes en rouge (mesure) ; pressostat coupe toutes les commandes (folio 16), pas seulement les chaudières ; sonde extérieure déplacée dans « Équipements du réseau chauffage » ; synthèse ajoutée.
- Bornier chaudière, d'après le schéma de câblage Elco R3400/R3500/R3600 (B3401E204, 18/06/2013, scan doc...155305 ; couvre le R3500 type 1-5) : 10-11 libération (ordre de marche, cavalier à retirer) ; 93 commun, 94 alarme, 95 OK (250 V~ 1 A max) ; 37-38 entrée 0-10 V « signal de compensation » (consigne) ; 39-40 sortie « charge 0-10 V » (retour de puissance) ; 41-42 e-Bus ; 30-31 sonde extérieure ; 50-51 pompe 0-10 V. Concorde avec le mail Elco du 13/10/2026 (KM628 sans protocole ; consigne 0-10 V, retour de puissance 0-10 V, ordre de marche par contact sec) et avec les folios SETIA 18 et 20 (94 vers le relais de défaut, 95 vers « chaudière OK » / « état marche »).
- À mettre au LISEZMOI G2 :
  - Feuille d'option Elco « Potentialfreie Sammelstörung » (dossier options R3400/R3600 K 01.1.0273, 2009) : repères inversés (94 OK, 95 ALARM). Le schéma de câblage 2013 et les folios SETIA concordent (94 alarme, 95 OK) : retenus.
  - Borniers : folios 32 (X2, 4 bornes) et 38 (X5, 6 bornes) à l'indice A ; les folios 18 et 20 à l'indice B placent tous les signaux chaudière sur X2:5-10. Indice B retenu.
  - Mise à l'échelle de la consigne : 2-10 V = 10 à 90 °C (notice Rendamax 3501-3505 de 2005, p.14 ; notice R3400/R3600 p.28). Entrée 0-10 V selon le schéma 2013, la notice p.4 et Elco. Le texte du CdC (consigne et retour de puissance en 0-10 V, ordre de marche par contact sec, report de défaut) est confirmé.
  - Notice transmise par Elco le 15/10/2026 = R3400/R3600 (06/2016, réf. 420010582502), pas R3500 : même régulation KM628 mais puissances différentes (R3401 : 656/702 kW) ; plaque retenue pour le R3501. Le schéma de câblage n'est pas dans la notice (carte fixée au dos de la chaudière, p.13 et p.19).
  - e-Bus (bornes 41-42) présent sur le schéma Elco : bus interne Elco (cascade, régulateurs E6 / KKM). Elco indique qu'aucun protocole de communication n'est disponible : non repris sur la planche.
  - RVL469 : bornes de bus DB / MB présentes mais non raccordées (folio 28). Le CdC dit « aucune interface de communication » pour les régulateurs de circuits.
  - Modèles des pompes de charge et de la pompe 2 radiateurs d'après la nomenclature Dalkia, plaques non relevées.

### Planche G2 rev 01, version du 15/10/2026 (refaite le 03/11/2026)

- Consignes d'Ismail appliquées à G2 uniquement (M et BN inchangés) : titres de zones orange en 10, tout le reste en 8 ; date du cartouche 15/10/2026 ; pas de « à relever » ; pour chaque matériel, la marque est indiquée ou la planche dit « Marque et modèle non documentés aux folios SETIA » ; photos des chaudières agrandies (h 292) et photos des pompes à leur échelle (84 à 140).
- Règle confirmée par Ismail (03/11) : la photo de visite passe avant tout ; le schéma de principe Dalkia ne sert de source que si la photo ne dit rien, et il est alors cité. Planche courte : c'est un synoptique de communication, pas un DOE.
- Pompes de charge (photo 7, retour chaudière) : tête verte sans afficheur, plaque illisible ; le modèle Dalkia (Xylem Ecocirc XL, tête grise à afficheur) ne correspond pas → « Marque et modèle non documentés aux folios SETIA » + photo de visite retravaillée.
- Circuit ancien bâtiment (photo 18, étiquettes DÉPART / RETOUR RADIATEUR HALL G1/G2) : deux Salmson à afficheur, de la famille Siriux → 2 × SALMSON SIRIUX 65-90 M, 230 V~. La Zoom 320C du schéma Dalkia (ancien circulateur monovitesse) est retirée ; le folio 12 donne encore la pompe 2 en 400 V 3~ (à signaler au LISEZMOI). Servomoteur de la vanne : photo de visite.
- Pompe double du nouveau bâtiment : photo de visite (deux têtes Salmson, câbles repérés W-M5 et W-M6) à la place de l'image brochure Siriux Master.
- Modèles repris du schéma de principe Dalkia (cités sur la planche) : Salmson XAS15NS (photo 40 : deux têtes Salmson), Lowara 46SV2/2AG055T (photo 35 : Lowara).
- Servomoteur Siemens SQK34 : repris de la planche rev 00 d'Ismail (plaque non lisible sur les photos).
- Générateur : scratchpad/lib/synlib.py (styles, grille, cartouche) et lib/body_G2.py.

### Règles pour les planches suivantes (Ismail, 03/11/2026)

- Les photos de visite servent à trouver l'information (marque, modèle, alimentation) ; elles ne vont pas sur la planche si elles sont de mauvaise qualité. Sur la planche : des images produit propres.
- Si les photos ne donnent pas l'information, on se base sur le schéma de principe affiché en chaufferie, en le citant : « (schéma de principe Dalkia) ».
- Deux équipements identiques (2 pompes, 2 chaudières) : deux images du même produit.
- Polices : titres de zones orange en 10, tout le reste en 8. Jamais « à relever » : « Marque et modèle non documentés aux folios ... ».
- Planche courte : c'est un synoptique de communication pour présenter l'installation et les pistes, pas un DOE.
- G2 clos le 03/11/2026 (rev 01, 15/10/2026).

### Hall C : préparation (03/11/2026)

- Interfaces à montrer en pointillé bleu, comme la NAVIPASS sur les planches Navistem :
  - une Vitogate 300 type BN/MB (réf. Z013294) pour la chaufferie, c'est-à-dire pour les deux chaudières : LAN RJ45 en BACnet/IP ou Modbus TCP (ou RS-485 en BACnet MS/TP ou Modbus RTU), liaison LON vers les chaudières (notice de montage 5837575) ;
  - un module LON par chaudière.
- Offre Viessmann 0621550644 du 21/10/2026 (« Pour cascade CM2 + CR3B ») : 2 Vitogate 300 BN/MB Z013294 (une pour Hall C, une pour NOP), 2 modules de communication LON Z011478, 2 modules LON 7172173, 4 câbles LON RJ45 7 m 7143495, 2 lots de résistances terminales 7143497, 2 mises en service 7004828. Contient des prix : jamais en annexe ni sur une planche.
- Répartition des modules LON : un même modèle pour les deux chaudières de Hall C, l'autre pour les deux de NOP. 7172173 convient aux Vitotronic 100 CC1E, CC1I, GC1, GC1B, GC4, GC4B, GC7B et 300 FW1, GW2, GW2B, GW4, GW4B (notice de montage du module) ; Z011478 non trouvé en ligne. À trancher avec le type de Vitotronic de Hall C (plaque ou photo).
- Fiche transmise « FT_VITOGATE_300 » = consignes d'utilisation BACnet (5838974, 3/2019), pas la fiche matériel.
