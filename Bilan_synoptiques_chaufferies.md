# Synoptiques des chaufferies gaz : bilan détaillé du travail

Site ArcelorMittal Maizières Research. Projet de raccordement des chaufferies gaz à l'hyperviseur.
Synoptiques réalisés par Ismail SOULLAMI, vérifiés par Jeremy STAREMBERGER et Vincent FOJUD.
Travail de reprise effectué le 3 novembre 2026, avec Claude.

Ce document récapitule, pour chaque synoptique traité : les documents utilisés, ce qu'ils montrent,
les modifications apportées et leurs raisons, puis les écarts à reporter ailleurs (LISEZMOI, matrice,
bilan BACS, CdC) et ce qui reste à faire.

---

## Sommaire

1. [Vue d'ensemble](#1-vue-densemble)
2. [Règles appliquées à toutes les planches](#2-règles-appliquées-à-toutes-les-planches)
3. [Méthode et outils](#3-méthode-et-outils)
4. [Détail par chaufferie](#4-détail-par-chaufferie)
   - [4.1 BO](#41-bo--problème-dimpression)
   - [4.2 M](#42-m)
   - [4.3 BN](#43-bn)
   - [4.4 G2](#44-g2)
   - [4.5 Hall C](#45-hall-c)
   - [4.6 NOP](#46-nop)
   - [4.7 Planches non modifiées](#47-planches-non-modifiées-d-f-b-t-bk-bl-w)
5. [Documents transversaux](#5-documents-transversaux)
6. [Écarts à reporter dans la matrice, le bilan BACS et le CdC](#6-écarts-à-reporter-dans-la-matrice-le-bilan-bacs-et-le-cdc)
7. [Points à mettre dans les LISEZMOI](#7-points-à-mettre-dans-les-lisezmoi)
8. [Ce qui reste à faire](#8-ce-qui-reste-à-faire)
9. [Fichiers livrés](#9-fichiers-livrés)

---

## 1. Vue d'ensemble

| Chaufferie | Catégorie CdC | Point de départ | Travail réalisé | Cartouche final |
|---|---|---|---|---|
| BO | 2 (Navistem) | `.drawio` d'Ismail | Correction d'un problème d'impression, contenu inchangé | Rév. 01, 26/08/2026, Validé |
| M | 2 (Navistem) | PDF rév. 00 du 25/08 + `.drawio` | Refonte complète, en deux versions | Rév. 01, 03/11/2026, Validé |
| BN | 2 (Navistem) | PDF rév. 00 du 26/08, pas de `.drawio` | Reconstruction complète en `.drawio` | Rév. 01, 03/11/2026, Validé |
| G2 | 3 (régulateurs dispersés) | `.drawio` rév. 00 du 24/08 | Reconstruction, vérification complète du matériel Elco, plusieurs itérations | Rév. 01, 15/10/2026, Validé |
| Hall C | 3 (régulateurs dispersés) | `.drawio` rév. 01 du 19/08 | Reconstruction, en deux versions | Rév. 01, 22/10/2026, Validé |
| NOP | 3 (régulateurs dispersés) | PDF rév. 01 du 29/08, pas de `.drawio` | Création complète en `.drawio` | Rév. 01, 29/10/2026, Validé |
| D, F, B, T, BK-BL, W | 1 et 2 | Planches déjà validées | Non modifiées, servent de référence | — |

Rappel des catégories du CdC :

| Catégorie | Définition | Installations |
|---|---|---|
| 1 | Avec automate et écran local | B, T, F, BK-BL |
| 2 | Sans automate, régulation Navistem | D, M, BN, BO, W |
| 3 | Sans automate, régulateurs dispersés | Hall C, G2, NOP |

---

## 2. Règles appliquées à toutes les planches

Ces règles viennent des planches validées (D le 21/10, F le 23/10) et des consignes données par Ismail
pendant la séance du 3 novembre.

### 2.1 Ordre de crédibilité des sources

1. Photos de visite, plaques signalétiques, écrans relevés sur place.
2. Schémas électriques tels que construits (les plus récents).
3. Listes de points et dossiers automates.
4. Liste du matériel et DOE.
5. Documentation constructeur.

Conséquences :

- La photo passe avant le folio. Une information non confirmée sort de la planche et va dans le LISEZMOI.
- Une information qui manque vaut mieux qu'une information fausse.
- Quand la photo ne donne pas le modèle, on reprend le schéma de principe affiché en chaufferie et on
  le cite sur la planche : « (schéma de principe Dalkia) ».
- Les photos de visite servent à trouver l'information. Sur la planche, on met de préférence des images
  constructeur propres. Une photo de visite n'est utilisée que si aucune image constructeur n'est
  disponible, et elle est alors retravaillée (voir 2.6).

### 2.2 Mise en forme

| Élément | Règle |
|---|---|
| Police | Titres des zones orange en taille 10, tout le reste en taille 8 (G2, Hall C, NOP). M et BN sont restées en taille 7 comme D. |
| Épaisseur des cases | 1 pour les cases en trait plein et en pointillé ; 2 pour le pointillé à points ; zones orange inchangées (2). |
| Zones fonctionnelles | Cadre orange en tirets, titre orange au-dessus. |
| Cadres équipement | Titre en gras majuscules, fabricant, modèle, puces (alimentation en dernier), puis italique. |
| Cartouche | Repris des planches existantes : installation, révision, date, réalisé par, vérifié par, feuille, statut. |
| Guide de lecture | Alimentation, TOR, mesure analogique, zone fonctionnelle, liaison nécessairement présente non documentée, interface à exploiter (plus « communication existante » quand il y a un bus LPB). |
| Synthèse | Bandeau « SYNTHÈSE » en bas de l'armoire, trois lignes orange : Pilotage, Armoire, Documentation. |

### 2.3 Contenu

- Jamais « à relever » : les planches sont destinées aux intégrateurs. On écrit « Marque et modèle non
  documentés aux folios … » ou « Origine non documentée ».
- Chaque matériel porte sa marque. Si elle n'est connue d'aucune source, la planche le dit explicitement.
- Pas de vase d'expansion, pas de production d'ECS électrique, pas de vannes manuelles : rien de ce qui
  ne sert pas à l'hyperviseur.
- Les organes internes d'un équipement ne sont pas représentés (variateur du ventilateur d'un brûleur,
  pompe d'une panoplie ECS, régulation intégrée).
- Peu de texte : c'est un synoptique de communication, qui présente l'installation et les pistes de
  raccordement. Ce n'est pas un DOE.

### 2.4 Liaisons

| Style | Signification |
|---|---|
| Trait plein, avec repère de borne et organe (X1:…, Q…, KA…) | Liaison documentée aux folios |
| Pointillé à points (épaisseur 2) | Liaison nécessairement présente mais non documentée |
| Gris | Alimentation |
| Vert | TOR, alarme, contact sec |
| Rouge | Mesure analogique (sondes) |

Les deux étiquettes d'une liaison (côté équipement et côté armoire) portent le même libellé, au
singulier. Les étiquettes sont empilées et centrées sur leur équipement, sans croisement de traits.

### 2.5 Communication

- **Pointillé bleu** : interface de communication à exploiter, ou matériel à ajouter (« … requise »).
  Un bloc par port, avec « Port : » et « Protocole : » en gras.
- **Trait plein bleu** : communication existante (bus LPB entre chaudières en cascade, par exemple).
- Chaudières Atlantic avec régulation Navistem : un bloc « Carte NAVIPASS Modbus requise » par chaudière.
- Chaudières Viessmann (Hall C et NOP) : un bloc « Module LON requis pour le raccordement à la Vitogate
  300 » par chaudière, et un bloc « Vitogate 300 type BN/MB, une pour les deux chaudières ».

### 2.6 Images

- Images constructeur de préférence.
- Photos de visite retravaillées quand il n'y a pas d'image constructeur : balance des blancs, contraste,
  netteté, recadrage serré, coins arrondis.
- Échelle logique entre équipements : la chaudière est toujours l'image la plus grande, puis le maintien
  de pression, les pompes, et enfin les petits organes (sondes, servomoteurs, régulateurs).
- Signe « + » entre deux équipements couplés (chaudière et brûleur, vanne et servomoteur, maintien de
  pression et dégazage, deux pompes simples).
- Deux équipements identiques : deux images du même produit.

### 2.7 Dates des cartouches

À la demande d'Ismail, les planches de catégorie 3 sont datées d'une semaine ouvrée en semaine ouvrée :
G2 le 15/10/2026 (date de la deuxième visite), Hall C le 22/10/2026, NOP le 29/10/2026.
M et BN portent la date du 03/11/2026 (voir le chapitre 8).

---

## 3. Méthode et outils

- **Contrôle visuel** : chaque planche est convertie en page HTML puis capturée en image, ce qui permet de
  la voir sans draw.io. Le rendu final dans draw.io peut différer de quelques pixels.
- **Contrôle automatique** à chaque version : aucun texte qui déborde de sa case, aucun texte qui
  chevauche une autre case ou une image, aucune case qui en chevauche une autre (hors chevauchements
  voulus du cartouche).
- **Contrôle d'intégrité** : identifiants uniques, aucune référence cassée, une seule page, polices
  attendues, aucun « à relever ».
- **Génération** : pour G2, Hall C et NOP, la planche est produite par un script Python (bibliothèque
  commune de styles, grille et cartouche, puis un script par chaufferie). M a été reconstruite à partir
  du fichier d'Ismail, BN reconstruite à partir du PDF.
- **Recherche de texte parasite** : un bloc de code draw.io collé par erreur dans une case, en texte
  transparent de 2 px, peut faire imprimer la planche sur des dizaines de pages (voir BO).
- **Limite** : les sites des fabricants ne sont pas accessibles depuis la session (réseau limité,
  viessmann.co.uk refusé). Les images constructeur viennent donc des documents fournis ou des images
  envoyées par Ismail.
- **Poids des fichiers** : pour NOP, les images ont été réduites à environ 3 pixels par point affiché,
  ce qui suffit pour l'A3 (2,9 Mo au lieu de 10,5 Mo).

---

## 4. Détail par chaufferie

### 4.1 BO : problème d'impression

**Document** : `.drawio` d'Ismail (rév. 01, 26/08/2026, Validé).

**Problème** : à l'impression, draw.io sortait la planche sur des dizaines de pages.

**Causes trouvées** :

1. Un texte invisible de 274 399 caractères dans la case blanche du bloc « Compteur gaz »
   (case `HCCthZdbtho9H6kvoJeq-145`). C'était un bloc de code draw.io collé par erreur, en texte
   transparent de 2 px et sans retour à la ligne. Il s'étendait très loin à droite et draw.io ajoutait
   des pages pour le contenir.
2. Un onglet vide « Page-2 » au format 420 × 1169, qui ne correspond à aucun papier.
3. La planche était collée au coin supérieur gauche, sans marge.

**Modifications** (rien d'autre n'a changé, vérifié par comparaison ligne à ligne) :

- texte invisible vidé, la case reste en place ;
- onglet vide supprimé, onglet « Page-3 » renommé « Synoptique BO » ;
- planche centrée sur l'A3 en la déplaçant d'un bloc (13 px de marge sur les côtés, 20 px en haut et en bas).

Fichier : 1,48 Mo avant, 1,21 Mo après.

---

### 4.2 M

#### Documents utilisés

| Document | Contenu | Utilisé pour |
|---|---|---|
| Synoptique Chaufferie M (PDF et `.drawio`, rév. 00, 25/08/2026) | Planche d'origine | Base de travail |
| DOE Dalkia « Travaux Chaufferie M » (41 p.) | Fournisseurs, rapport de mise en service Atlantic, fiches CIAT, Varmax, Belimo, Lowara, folios de l'armoire des aérothermes | Puissances, cascade, armoire |
| PV bât M (4 p.) | Rapport de mise en service | Cascade LPB, V2V |
| Schéma armoire électrique des aérothermes (3 p.) | Folios Dalkia 01 à 03 du 04/04/2019 | Bornier, organes |
| Schéma câblage aérothermes (1 p.) | Câblage CIAT | Aérothermes |
| Aérotherme, Chaufferie, Pompe, Vanne 2 voies (bât M) | Extraits du DOE | Contrôle |
| Photos visite bât M (30 photos) | Plaques, pompes, armoire, compteur, ECS | Source prioritaire |
| Bilan Excel « Chaufferies Gaz Recensement BACS » | Données du parc | Recoupement |

#### Ce que disent les sources

| Élément | Relevé | Source |
|---|---|---|
| Chaudière 1 | Atlantic Varmax 275, Qn 275 kW, Pn 268 kW à 80/60 °C, PMS 6 bar, gaz 300 mbar, 230 V, 238 W, n° V271819613, 2018 | Plaque (photo 4) |
| Chaudière 2 | n° V103812830 | Étiquette (photo 7) |
| Cascade | LMS + OCI345 + sonde extérieure, adresse LPB 2/0, V2V pilotées par la chaudière | Rapport de mise en service Atlantic (intervention 01/10/2018) |
| Armoire des aérothermes | Bornier X1 24 bornes, S1 AUTO/0/MANU, thermostat X1:3-4, GV1 à GV4, KM1 à KM4 (une vitesse), ipsotherme en série avec la bobine, 4 voyants de marche, 4 de défaut, 1 de présence tension | Folios 02 et 03 |
| Aérothermes | CIAT Héliotherme 4500 3R TRI 2 vitesses | Fiche CIAT |
| Circuit bureaux | Grundfos UPS D40-60 F, 3 × 400 V, 3 vitesses ; sonde Siemens QAD22 | Photo 13 |
| Circuit atelier | Grundfos MAGNA3 D 50-120 F 280, 230 V | Photo 11 |
| Pot à boue | Pompe Lowara ecocirc XL, taille illisible | Photo 14 |
| Compteur gaz | Émetteur COMMON LFK1, 10 imp/m³ | Photo 27 |
| ECS | Ballon électrique Altech 250 L, 3 kW, 230 V | Photos 24-25 |

Découverte importante : le rapport de mise en service « Varmax 275 n° V103812830 », rangé dans le DOE de W,
concerne en réalité la chaudière 2 de M (numéro visible en photo à M).

#### Version 1 (non retenue)

Corrections de contenu appliquées sur le fichier d'Ismail, sans revoir la mise en page.
Retours d'Ismail : titre « Synthèse » disparu, détail du compteur gaz disparu, blocs mal posés et
superposés, épaisseurs de trait non conformes. Version abandonnée.

#### Version 2 (livrée)

Reconstruite sur le modèle de BO, la planche validée la plus proche (Navistem, aérothermes CIAT,
armoire de relayage, compteur COMMON), avec les règles de D. Police taille 7.

Disposition :

- à gauche : production (2 chaudières), équipements lus et pilotés par les chaudières (sonde extérieure,
  2 vannes d'isolement), comptage gaz ;
- au centre : armoire (bornier, organes, synthèse) ;
- à droite : aérothermes et commande, circuit bureaux, circuit atelier, filtre à boues.

Modifications :

- chaudières au format de D : Qn 275 kW, Pn 268 kW à 80/60 °C, gaz 300 mbar, maître et esclave de la cascade ;
- un bloc « Carte NAVIPASS Modbus requise » par chaudière ;
- blocs LPB au format de D (« Module OCI345 présent (com. cascade) ») ;
- bandeau SYNTHÈSE (Pilotage, Armoire, Documentation) à la place de « Départs non documentés » ;
- détail du compteur gaz au format de BO, avec la case « Sortie impulsions gaz » ;
- pompes corrigées d'après les photos (UPS D40-60 F en 400 V 3~, MAGNA3 D 50-120 F 280, Lowara ecocirc XL sans taille) ;
- vase Reflex et bloc ECS électrique retirés ;
- références de corps des vannes Belimo retirées ;
- libellés identiques des deux côtés des liaisons, deuxième sonde QAD22 renumérotée « 2 » ;
- fautes corrigées (chaudiére, mésurent, Piloté) ;
- départ X1:1-2 : « destination non identifiée » remplacé par « destination à relever » (formulation antérieure à la règle 2.3, voir chapitre 8) ;
- entrée « Communication existante » ajoutée au guide de lecture ;
- épaisseurs de trait mises aux normes ;
- étiquettes des liaisons chaudières rangées de façon à ce qu'aucun trait ne se croise ;
- cartouche : rév. 01, 03/11/2026, Validé.

---

### 4.3 BN

#### Documents utilisés

| Document | Contenu | Utilisé pour |
|---|---|---|
| Synoptique Chaufferie BN (PDF, rév. 00, 26/08/2026) | Planche d'origine, pas de `.drawio` | Base de travail, images reprises |
| Schéma électrique Chaufferie BN (9 folios) | Bornier X1 26 bornes, X2 30 bornes, puissance, commande, organes | Liaisons et armoire |
| Data visite bât BN (zip : 48 photos dont 24 uniques, + PDF de photos) | Plaques, armoire, pompes, compteur, schéma de principe Dalkia affiché | Source prioritaire |

Pas de DOE.

#### Ce que disent les sources

| Élément | Relevé | Source |
|---|---|---|
| Chaudière | Atlantic Varmax 275, n° V041020782, 2020, Qn 275 kW, Pn 268 kW, 300 mbar | Plaque |
| Pompe double | Grundfos MAGNA1 D 32-120 F 220, 1 × 230 V | Plaque |
| Compteur gaz | COMMON CPT-01 Quantometer DN 50 G40, Qmax 65 m³/h, 2021 | Plaque |
| Armoire | Bornier X1 26 bornes, X2 30 bornes ; 9 voyants de marche, 9 de défaut, 1 de présence tension ; commutateurs S1 à S8 | Folios 02 à 09, photo de façade |
| Logique | Horloge H1, relais KA7 (zone 1 jour/nuit), KA8 (air neuf, aérotherme 5, extracteur) | Folios |
| MAGNA1 | Entrée marche/arrêt et relais de défaut câblés au bornier X1 | Folios 04-05, photo, documentation Grundfos |

#### Modifications

Planche reconstruite en `.drawio` sur la grille et les styles de M et BO (police taille 7). Les 23
liaisons et les borniers de la planche d'Ismail étaient justes et ont été conservés.

- chaudière d'après la plaque (Qn 275 kW, Pn 268 kW à 80/60 °C, 300 mbar) ;
- bloc « LPB, OCI345 requis » remplacé par la NAVIPASS, solution retenue dans le CdC ;
- pompes MAGNA1 : « ni entrée de commande, ni relais de signal » était faux (voir le tableau ci-dessus) ;
- compteur gaz : « 10 imp/m³ » retiré (absent de la plaque), remplacé par « poids d'impulsion à relever » ;
- repère H3 du voyant et mention « deux vitesses disponibles » des aérothermes retirés (non documentés) ;
- synthèse au format de BO ;
- cartouche : rév. 01, 03/11/2026, Validé.

---

### 4.4 G2

#### Documents utilisés

| Document | Pages | Contenu |
|---|---|---|
| Synoptique Chaufferie G2 (`.drawio` et PDF, rév. 00, 24/08/2026) | 1 | Planche d'origine |
| Armoire chaufferie - Bâtiment G2 | 1 | Photo de l'armoire |
| data visite chaufferie G2 | 41 | Photos de visite |
| doc06024920260821154244 et doc06025120260821154847 | 18 + 18 | Deux scans du même dossier électrique SETIA, indice B « tel que construit » du 11/12/2014, folio 14 annoté indice C le 24/03/2016 |
| doc06025220260821155305 | 10 | Schéma de câblage Elco R3400/R3500/R3600 (B3401E204, 18/06/2013), qui couvre le R3500 type 1-5, donc le R3501 |
| doc06025320260821155458 | 12 | Dossier des options Elco R3400/R3600 (K 01.1.0273, 2009), dont le relais de défaut libre de potentiel |
| doc06025420260821155655 | 10 | Documentation technique Elco Rendamax 3501-3505 (avril 2005) |
| doc06025520260821155842 | 32 | Documentation Elco Rendamax 3501-3505 (avril 2005), avec le raccordement électrique |
| doc06025620260821160240 | 7 | Elco R3000, régulateur cascade KKM8, codes défauts |
| Notice R3000 (envoyée par Elco le 15/10/2026) | 74 | Notice R3400/R3600 (06/2016, réf. 420010582502), en français et en anglais |
| Échange de mails avec Elco (A. Vignot, SAV) | — | 13/10/2026 : KM628 sans protocole ; piste 0-10 V et contact sec |
| CdC v3 (`.docx`) | — | Texte de la solution G2 |

#### Ce que disent les sources

| Élément | Relevé | Source |
|---|---|---|
| Chaudières | 2 × Elco Rendamax R 3501, Q(Hi) 653 kW, P 80/60 613 kW, G20 20 mbar, 3 × 400 V, PMS 8 bar (S/N 3581510KE142400000134) | Plaque (une seule chaudière photographiée deux fois) |
| Régulation | Kromschröder KM628, aucun protocole de communication | Mail Elco du 13/10/2026 |
| Bornier chaudière | 10-11 libération (ordre de marche, cavalier à retirer) ; 93 commun, 94 alarme, 95 OK (250 V~ 1 A) ; 37-38 entrée 0-10 V (consigne) ; 39-40 sortie 0-10 V (charge du brûleur) ; 41-42 e-Bus ; 30-31 sonde extérieure | Schéma de câblage Elco 2013 |
| Câblage armoire | 94 vers le relais de défaut, 95 vers « chaudière OK » / « état marche » | Folios SETIA 18 et 20 |
| Pressostat manque d'eau | Coupe la commande des chaudières et de toutes les pompes (relais KMEG) | Folio 16 |
| Pompes de charge | 230 V, 4,1 A | Folio 12 |
| Pompes de charge | Tête verte sans afficheur, plaque illisible | Photo de visite |
| Circuit ancien bâtiment | Deux Salmson à afficheur, de la famille Siriux | Photo 18 (étiquettes DÉPART / RETOUR RADIATEUR HALL G1/G2) |
| Schéma de principe Dalkia (02/02/2015) | Repère 3 Xylem Ecocirc XL 65-120 F ; repère 4 Salmson Siriux 65-90 M ; repère 5 Salmson Zoom 320C ; Salmson XAS15NS ; Lowara 46SV2/2AG055T | Photo du schéma affiché |

Le texte du CdC pour G2 (consigne et retour de puissance en 0-10 V, ordre de marche par contact sec,
report de défaut) est confirmé par le schéma de câblage Elco et par le mail d'Elco.

#### Itérations

1. **Rév. 01, première version** : reconstruction sur la grille de M et BN. Pompes corrigées d'après la
   nomenclature Dalkia et le folio 12, sondes en rouge, pressostat corrigé, sonde extérieure déplacée
   dans « Équipements du réseau chauffage », synthèse ajoutée.
2. **Vérification Elco** : avec le schéma de câblage de 2013, le sens alarme/OK (94/95) et l'existence
   de la sortie 0-10 V sont confirmés. Deux erreurs de la version précédente ont été corrigées : le sens
   94/95 avait été lu sur la feuille d'option de 2009, qui l'inverse, et le 2-10 V n'est que la plage
   utile de la consigne.
3. **Consignes d'Ismail** : titres en 10 et texte en 8, date du 15/10/2026, plus de « à relever »,
   marque indiquée ou « non documentée aux folios SETIA », chaudières agrandies, images à l'échelle.
4. **Pompes de charge** : après plusieurs allers-retours, la règle retenue est « la photo d'abord, le
   schéma de principe en appoint et cité ». Le modèle affiché est celui du schéma de principe, avec la
   mention.
5. **Version finale** : images produit uniquement, deux images quand il y a deux pompes.

#### Contenu final de la planche

| Bloc | Contenu |
|---|---|
| Chaudières 1 et 2 | ELCO RENDAMAX R 3501, Qn 653 kW, Pn 613 kW à 80/60 °C, 20 mbar, Kromschröder KM628, 400 V 3~ ; bornier 10-11, 93-94 / 93-95, 37-38, 39-40 ; « Aucun protocole de communication (KM628, confirmé par Elco). Piste Elco : consigne et retour de puissance en 0-10 V, marche par contact sec » |
| Pressostat manque d'eau | Marque et modèle non documentés aux folios SETIA ; contact sec SQ1 ; coupe toutes les commandes (KMEG) |
| Sonde extérieure | Marque et modèle non documentés aux folios SETIA ; raccordée au RVL469 (B9) |
| Pompes de charge | XYLEM ECOCIRC XL 65-120 F (schéma de principe Dalkia), une sur le retour de chaque chaudière, 230 V~, commandées par SA1 et 16S01 |
| Circuit ancien bâtiment | 2 × SALMSON SIRIUX 65-90 M, 230 V~, commandées par SA3 ; vanne 3 voies Siemens, servomoteur SQK34 3 points, pilotée par le RVL469 ; sonde de départ non documentée (B1) |
| Circuit nouveau bâtiment | Pompe double SALMSON XAS15NS (schéma de principe Dalkia), 230 V~, commandée par SA4, circuit sans régulation |
| Circuit aérothermes G1/G2 | 2 × LOWARA 46SV2/2AG055T (schéma de principe Dalkia), 400 V 3~, commandées par 26S01 |
| Armoire | Borniers X1 (30 bornes), X2 (10), X3 (7) ; commutateurs, relais, disjoncteurs, voyants, régulateur RVL469 ; synthèse |

Zone circuit ancien bâtiment : la Zoom 320C du schéma Dalkia (ancien circulateur à vitesse unique) a été
retirée, car la photo montre deux Siriux.

Pièces jointes de justification envoyées pendant la séance : « Preuves - pompes G2 », « Preuves - Elco G2 »
et « Pourquoi - pompes de charge G2 ».

---

### 4.5 Hall C

#### Documents utilisés

| Document | Pages | Contenu |
|---|---|---|
| Synoptique Chaufferie Hall C (`.drawio`, rév. 01, 19/08/2026) | 1 | Planche d'origine |
| Pompe 1 - Hall C | 5 | Brochure Salmson Priux Master |
| Pompe 2 - Hall C | 2 | Lowara ecocirc XL / XLplus |
| Schéma électrique - Hall C | 8 | Folios Dalkia du 27/06/2019, bornier X1 67 bornes |
| Vento Connect - Hall C | 14 | Documentation IMI Pneumatex |
| Acvatix Servomoteur - Hall C | 13 | Manuel technique Siemens SAX / SAL |
| Chaufferie - Hall C | 5 | Brochure Viessmann Vitocrossal 200 |
| Compresseur - Hall C | 12 | Documentation IMI Pneumatex Compresso Connect F |
| DOE Hall C | 74 | Fournisseurs, rapports Viessmann n° 129206 du 03/09/2019, notice Vitotronic 100 CC1E, fiches pompes, vannes, Pneumatex, schéma électrique |
| Data visite - Hall C | 20 | Photos de visite, dont le schéma de principe Dalkia affiché |
| Première et deuxième chaudière du Hall C (zips, 15/10/2026) | 8 + 5 | Plaques et écrans des régulations, deuxième visite faite à la demande de Viessmann |
| Offre Viessmann 0621550644 (21/10/2026) | 3 | Vitogate 300 et modules LON (voir chapitre 5) |
| FT_VITOGATE_300 | 6 | Consignes d'utilisation BACnet (5838974, 3/2019), pas la fiche matériel |

#### Ce que disent les sources

| Élément | Relevé | Source |
|---|---|---|
| Chaudières | 2 × Viessmann Vitocrossal 200 CM2-500, n° 7745704 801268 106 et 7745704 801269 103 ; Qn 474 kW, Pn 460 kW à 80/60 °C (500 kW à 50/30 °C), G20 20 mbar | Plaques (15/10/2026) |
| Régulation | Vitotronic 100 type CC1E « BASE E », une par chaudière, en cascade ; n° de régulation 7901388910863113 et 7901388910864110 | Écrans, notice et rapport Viessmann du DOE |
| Défauts pompes nord régulé | Contacts auxiliaires des disjoncteurs vers KA2 et KA4 (folio 05), pas un relais de la pompe | Folio 05 |
| Manque d'eau | KA17, X1:49-50 | Folios 05 et 08 |
| Schéma de principe Dalkia | Nord régulé 2 × Salmson Priux Master 65-80 + V3V DN50 ; sud régulé Ecocirc XL D 65-80 + V3V DN50 ; « Constant S » Ecocirc XL D 80-120 ; « Constant R » Ecocirc XL D 65-80 ; V2V DN80 motorisée par chaudière ; Compresso Connect ; Vento Connect | Photo du schéma affiché |
| Maintien de pression | Compresso CG 700.6 avec BrainCube2 (adresse MAC visible) | Photo |
| Vannes | Servomoteurs Siemens SAL31 | Photos |

#### Version 1

- gabarit de G2 (polices 8 et 10) et images constructeur ;
- un bloc « Module LON requis pour le raccordement à la Vitogate 300 » par chaudière et un bloc
  « Vitogate 300 type BN/MB, une pour les deux chaudières » (LAN RJ45 BACnet/IP ou Modbus TCP,
  RS-485 BACnet MS/TP ou Modbus RTU, câble LON RJ45), sans référence de module ;
- puissance corrigée : Qn 474 kW et Pn 460 kW à 80/60 °C, au lieu de « 2 × 500 kW, soit 1 MW » ;
- liaisons reprises des folios avec leurs repères : alimentations Q3 à Q15, ordres de marche KA5 à KA15,
  défauts KA6 à KA16, défauts chaudières vers voyants, manque d'eau KA17, arrêt d'urgence sur MT ;
- défauts des pompes nord régulé laissés dans l'armoire (pas de liaison), puisqu'ils viennent des disjoncteurs ;
- vannes 3 voies : alimentation et commande en pointillé à points, « origine non documentée » ;
- circuits constants : « LOWARA ECOCIRC XL D » avec une seule note sur les tailles et la répartition ;
- bandeau « Points d'échange et réserves » remplacé par la synthèse ;
- bornier regroupé en 12 lignes avec les organes complétés d'après les folios ;
- image de vanne à secteur avec servomoteur SAL, comme sur D ;
- date du 22/10/2026.

#### Version 2 (livrée), après retour d'Ismail

- chaudières agrandies : images les plus grandes de la planche (210 de haut) ;
- images à l'échelle : Compresso 160, Vento 116, pompes 80 à 96, vanne et servomoteur 56 à 62 ;
- signes « + » entre les deux pompes Priux, entre vanne et servomoteur, entre Compresso et Vento ;
- Compresso et Vento réunis dans un cadre « Maintien de pression et dégazage », zone « Équipements du
  réseau chauffage », ports RS485 Modbus RTU et RJ45 Modbus TCP empilés ;
- colonne gauche élargie, tableaux de l'armoire resserrés.

---

### 4.6 NOP

#### Documents utilisés

| Document | Contenu | Utilisé pour |
|---|---|---|
| Synoptique Chaufferie NOP (PDF, rév. 01, 29/08/2026) | Planche d'origine, pas de `.drawio` | Contenu de départ |
| Data visite - Chaufferie NOP (35 photos) | Façades des deux armoires, intérieur de l'armoire, 3 Sauter M10, pompes, Pneumatex, filtre, servomoteurs | Source prioritaire |
| nop dernière visite (zip, 20 photos du 15/10/2026) | Plaques des chaudières et des brûleurs, écrans des régulations, variateurs NORD | Source prioritaire |
| Image Vitocrossal 300 (envoyée par Ismail) | Image constructeur | Chaudières |
| Image IMI Pneumatex (envoyée par Ismail) | Image constructeur | Maintien de pression |
| Doc Weishaupt 83211401 (32 p.) | Fachinformation brûleurs monarch WM10 | Image du brûleur (page 13, détourée) |
| Fichiers transmis par Jean-Philippe | Voir ci-dessous | Non utilisés pour la planche |

**Fichiers transmis par Jean-Philippe** :

- « DOE - NOP.pdf » et « 86639-DOE.pdf » sont le même fichier : DOE Beirens (2022) de la cheminée
  (autoportante Ø550, 17 m, deux carneaux Ø300) pour Dalkia Maizières. C'est probablement la cheminée
  de NOP, mais ça ne sert pas au synoptique.
- Les fiches « FP_12 Chaudière » et « FP_13 Brûleur » viennent d'un autre chantier (Veuve Clicquot,
  Saint-Léonard, Clauger 2017). Ce n'est pas la chaufferie, mais c'est le même matériel
  (Vitocrossal 300 CR3B et Weishaupt WM-G10/3-A ZM-LN) : les pages constructeur peuvent servir de
  documentation produit.
- Le carnet d'entretien Beirens (2020) est générique et illisible (PDF interactif).

#### Ce que disent les photos

| Élément | Relevé |
|---|---|
| Chaudières | 2 × Viessmann Vitocrossal 300 CR3B (n° 7436409 701064 104 lisible) ; Qn 742 kW, Pn 720 kW à 80/60 °C (787 kW à 50/30 °C) ; total 1 440 kW |
| Brûleurs | Weishaupt WM-G10/3-A ZM-LN monarch, 2017, 125 à 900 kW, 400 V 3~, 1,86 kW, gestionnaire W-FM 50 avec vitesse variable |
| Variateurs NORD | SK 200E, 1,5 kW, 2017 : variateurs des ventilateurs des brûleurs (organes internes) |
| Régulation | Une Vitotronic par chaudière, cascade active ; n° 7787300700567102 et 7787300700851102 ; écran « Informations LAN » : LAN intégré non activé (connectivité Viessmann, pas un protocole de GTB) |
| Vannes d'isolement | 2 × Siemens SAL31 sur les chaudières |
| Autre servomoteur | Sauter ASM124F120 (3 points, 230 V) près des collecteurs, circuit non identifié |
| Régulateurs | 3 × Sauter equitherm M10 : aérothermes ; nord-est et sud-ouest ; chaudière et réseau fatigue |
| Pompes | 6 circuits à deux pompes : aérothermes, nord-est, sud-ouest (Grundfos UPC triphasées) ; fatigue (Grundfos UPS) ; sous-station (Grundfos MAGNA ancienne série) ; hall BF 2 (Grundfos MAGNA1 D) |
| Maintien de pression et dégazage | IMI Pneumatex, maintien de pression et Vento, tous deux avec BrainCube Connect (confirmé par Ismail) |
| Filtre | Atlantic Guillot MagNet 07P (2014, 230 V, 420 W) avec coffret de détection d'encrassement |
| Armoire chaudière | Voyant sous tension ; chaudières 1 et 2 arrêt/marche et défaut ; réseaux fatigue et aérothermes Ppe 1 / arrêt / Ppe 2 et défauts ; marche et test lampes |
| Armoire des pompes | Arrêt d'urgence coup de poing ; réseaux sous-station, sud-ouest, nord-est, hall BF 2 |

Aucun DOE, aucun schéma électrique.

#### Corrections par rapport à la planche d'origine

- puissance : 720 kW à 80/60 °C par chaudière, au lieu de « puissance non documentée » ;
- servomoteurs présents (2 × SAL31), au lieu de « aucun servomoteur constaté » ;
- filtre magnétique MagNet 07P, au lieu de « vase à membrane, ballon Atlantic Guillot » ;
- variateurs NORD retirés : ce sont ceux des brûleurs ;
- vase, collecteurs et vannes manuelles retirés ;
- plus aucun « à relever ».

#### Contenu de la planche (rév. 01, 29/10/2026)

Planche créée de zéro sur le gabarit de Hall C.

- **Production** : deux cadres chaudière, chacun avec l'image Vitocrossal 300 (la plus grande de la
  planche), un « + » et le brûleur Weishaupt, les caractéristiques, et un bloc « Module LON requis pour
  le raccordement à la Vitogate 300 ». En dessous, le bloc Vitogate 300 identique à Hall C.
- **Équipements du réseau** : maintien de pression et Vento (images avec « + »), ports RS485 Modbus RTU
  et RJ45 Modbus TCP en pointillé bleu, « Interface intégrée, aucune carte requise » ; filtre MagNet.
- **Armoires** : relevé de façade en texte (armoire chaudière, armoire des pompes), régulation (3 Sauter
  M10, image, « Fonctions à reprendre par l'automate dans le cadre du projet »), synthèse.
- **Circuits** : 6 zones (aérothermes, fatigue, nord-est, sud-ouest, sous-station, hall BF 2) avec image
  et série des pompes. Mention « Régulé par un Sauter equitherm M10 » ou « Aucun régulateur relevé ».
- **Liaisons** : toutes en pointillé à points, sans repère de borne. Libellés « Constaté en façade » pour
  les commandes et défauts, « Origine non documentée » pour l'alimentation des chaudières.
- **Synthèse, ligne Documentation** : « aucun DOE ni schéma électrique ; synoptique établi à partir des
  relevés de visite ; toutes les liaisons sont nécessairement présentes mais non documentées ».

Images : constructeur pour les chaudières, le brûleur, le Pneumatex, le Vento (image de Hall C) et la
MAGNA1 D (image de D). Photos de visite retravaillées pour les pompes UPC, UPS et MAGNA, le filtre et le
régulateur M10.

| Image | Hauteur |
|---|---|
| Chaudières | 232 |
| Maintien de pression | 168 |
| Vento | 108 |
| Pompes | 84 à 90 |
| Filtre | 86 |
| Brûleur | 64 |
| Régulateur M10 | 62 |

---

### 4.7 Planches non modifiées (D, F, B, T, BK-BL, W)

Ces planches, déjà validées, ont servi de référence de style et de contenu. Aucune n'a été modifiée
pendant cette séance.

Contrôle effectué sur les fichiers de référence :

| Fichier | Constat |
|---|---|
| D | Texte parasite (code draw.io collé) dans le cadre « Aérothermes OUEST », 910 caractères |
| BK-BL | Textes parasites dans deux cases de l'onglet « Synoptique BK/BL » (3 539 et 2 343 caractères) et dans deux cases de l'onglet « 1 - Composition physique » (144 239 et 206 639 caractères) |
| B, F, T | Aucun texte parasite |

Les textes parasites de BK-BL, très longs, peuvent provoquer le même problème d'impression qu'à BO.

---

## 5. Documents transversaux

| Document | Utilisation |
|---|---|
| Cahier des charges v3 (`.docx`) | Structure, catégories, texte des solutions par installation, annexe A (12 synoptiques), annexe B (photos des armoires). Les planches M, BN, Hall C, G2 et NOP y étaient encore « en attente de validation ». |
| CdC indice B du 30/09 (PDF, 45 p.) | Version antérieure, reçue pour contexte, non utilisée |
| Bilan Excel « Chaufferies Gaz Recensement BACS Bilan » | Onglets « Recensement » et « Réglementation BACS » ; recoupement des puissances et des statuts |
| Offre Viessmann 0621550644 du 21/10/2026 | Désignations reprises (jamais les prix) : 2 Vitogate 300 type BN/MB (Z013294), 2 modules de communication LON (Z011478), 2 modules LON (7172173), 4 câbles LON RJ45 de 7 m (7143495), 2 lots de résistances terminales (7143497), 2 mises en service (7004828). Libellé : « Pour cascade CM2 + CR3B ». Une Vitogate par chaufferie (Hall C et NOP), un module LON par chaudière. |
| FT Vitogate 300 | Consignes d'utilisation BACnet uniquement |
| Mails Elco (13 et 15/10/2026) et notice R3000 | Base de la solution G2 |
| Doc Weishaupt 83211401 | Image du brûleur de NOP |

L'offre Viessmann contient des prix : elle ne doit figurer ni en annexe du CdC, ni sur une planche.

---

## 6. Écarts à reporter dans la matrice, le bilan BACS et le CdC

| Sujet | Constat | Source | Action proposée |
|---|---|---|---|
| Hall C, puissance | 920 kW à 80/60 °C (2 × 460) ; le bilan BACS indique 1 000 kW, qui est la puissance à 50/30 °C | Plaques du 15/10/2026 | Bilan BACS à 920 kW, ou préciser le régime |
| T, puissance | Tableau du parc à 450 kW (somme des Qn) ; en Pn : 2 × 219 = 438 kW | Fiche Atlantic Varmax | Choisir un seul régime pour tout le parc |
| Total du parc | 7 074 kW en Pn à 80/60 °C (7 086 kW avec T à 450 kW, valeur du CdC) | Plaques | Aligner CdC, matrice et bilan |
| W | 69 kW sans source. Le rapport de mise en service « Varmax 275 n° V103812830 » rangé dans le DOE de W concerne en réalité M (chaudière 2). Il ne reste aucun document propre à W. | Photo à M | Corriger le dossier de W et la matrice |
| M, schéma électrique | Le bilan Excel indique « ✗ » ; il existe un schéma partiel, celui de l'armoire des aérothermes (folios Dalkia 01 à 03 du 04/04/2019), pas celui de toute l'installation | DOE de M | « Partiel (armoire des aérothermes) » |
| NOP | 1 440 kW confirmé (2 × 720 kW à 80/60 °C) | Plaques | Rien à changer |
| G2 | 1 226 kW confirmé (2 × 613 kW à 80/60 °C) | Plaque | Rien à changer |
| B, matrice du 08/09 | Pompes CTA notées MAGNA3 (faux, triphasées) | Folios | Corriger |
| D, matrice du 08/09 | Pompe magasin notée pompe double MAGNA1 D ; mise en service « Sept. 2021 » sans source (plaques : 2021) | Photos | Corriger |

---

## 7. Points à mettre dans les LISEZMOI

### M

- Le rapport de mise en service mentionne un circuit radiateurs mélangé « piloté par régulation client »
  et une « régulation réseau secondaire : automate / AVS 75 », non vus en photo.
- Piquages des retours inversés et V2V placées sur les retours (rapport de mise en service).
- Le rapport de mise en service ne porte que sur une chaudière (n° V271819613).
- Le schéma électrique ne couvre que l'armoire des aérothermes.

### BN

- Le schéma de principe Dalkia affiché (28/11/2023) indique une MAGNA1 D 32-80 et deux radiateurs ;
  la plaque et les folios donnent une MAGNA1 D 32-120 F 220 et un ventilo-convecteur sur Q9 : retenus.
- Le folio 06 nomme Q9 à Q14 les disjoncteurs des aérothermes ; le folio 03 les nomme Q11 à Q16 : retenu.
- Marque des aérothermes non relevée (l'image utilisée est celle d'un CIAT).
- Poids d'impulsion du compteur gaz absent de la plaque.

### G2

- La photo des pompes de charge montre une tête verte sans afficheur, différente d'une Ecocirc XL
  (tête grise à afficheur) : le modèle affiché est celui du schéma de principe.
- Le folio 12 donne encore la pompe 2 du circuit ancien bâtiment en 400 V triphasé ; la photo montre une Siriux.
- Feuille d'option Elco de 2009 : repères 94/95 inversés. Le schéma de câblage de 2013 et les folios
  SETIA concordent (94 alarme, 95 OK) : retenus.
- Borniers : les folios 32 (X2, 4 bornes) et 38 (X5, 6 bornes) sont à l'indice A ; les folios 18 et 20
  à l'indice B placent tous les signaux chaudière sur X2:5-10 : indice B retenu.
- Consigne : plage utile 2-10 V = 10 à 90 °C (notice 2005 p.14, notice R3400/R3600 p.28).
- La notice envoyée par Elco est celle des R3400/R3600 (même régulation KM628, puissances différentes) ;
  le schéma de câblage n'y figure pas (carte fixée au dos de la chaudière).
- e-Bus (bornes 41-42) : bus interne Elco, non exploitable selon Elco.
- RVL469 : bornes de bus DB et MB présentes mais non raccordées (folio 28).
- Servomoteur Siemens SQK34 repris de la planche d'origine (plaque non lisible en photo).

### Hall C

- Folio 05 : les contacts de défaut KA2 et KA4 sont repérés « Aux Q14 / Aux Q15 », alors que les pompes
  nord régulé sont sur Q8 et Q9 (folio 01).
- Circuits constants : « Constant S » et « Constant R » sur le schéma de principe, « nord constant » et
  « sud constant » sur le schéma électrique ; la répartition des tailles (XL D 80-120 et XL D 65-80)
  n'est pas précisée.
- Pilotage des vannes 3 voies nord et sud non documenté (la Vitotronic 100 CC1E ne régule pas de circuit
  mélangé, folios muets).
- Le bilan BACS indique 1 000 kW (puissance à 50/30 °C).

### NOP

- Aucun DOE ni schéma électrique : synoptique établi à partir des relevés de visite.
- Les Vitotronic disposent d'une interface LAN intégrée, non activée : connectivité Viessmann, pas un
  protocole de GTB. L'intégration passe par les modules LON et la Vitogate 300.
- Servomoteur Sauter ASM124F120 relevé près des collecteurs, circuit non identifié.
- Tailles des pompes UPC lues en photo (UPC 40-120, UPC 50-120) sans affectation sûre aux circuits.
- DOE de la cheminée (Beirens, 2022) disponible ; fiches chaudière et brûleur d'un autre chantier.

---

## 8. Ce qui reste à faire

**Synoptiques**

- [ ] Harmoniser M et BN avec G2, Hall C et NOP si souhaité : police 8 / titres 10 et images
      constructeur (M et BN sont en taille 7), dates de cartouche (M et BN au 03/11/2026).
- [ ] Reformuler les deux « à relever » restants, antérieurs à la règle 2.3 : M, départ X1:1-2
      (« destination à relever ») ; BN, compteur gaz (« poids d'impulsion à relever »).
- [ ] Nettoyer les textes parasites de D et BK-BL (même correction qu'à BO).
- [ ] Planche F : port WAN F à corriger en HTTP + HTTPS, port RS485 B en bus SLC Sauter.
- [ ] Planche T : bandeau d'alimentation « ALIMENTATION 24 V DC - EY-PS021 ».
- [ ] Fiche automate BK-BL : module 7 dans l'ordre Genersys, module 9 (capteurs PEL 2500 en 0-10 V).
- [ ] Exporter les planches en PDF A3 pour l'annexe A du CdC.

**Viessmann**

- [ ] Confirmer avec Viessmann quelle référence de module LON (Z011478 ou 7172173) va à Hall C et laquelle à NOP.

**Documentation**

- [ ] Rédiger ou compléter les LISEZMOI avec les points du chapitre 7.
- [ ] Mettre à jour la matrice de recensement et le bilan BACS avec les écarts du chapitre 6.
- [ ] Ranger les documents de NOP : DOE de la cheminée dans « DOE et schémas », fiches Veuve Clicquot
      dans « À trier » ou seulement les pages constructeur dans « Docs équipements ».

---

## 9. Fichiers livrés

Tous les fichiers ont été envoyés dans la conversation. Les copies de travail se trouvent dans le
dossier temporaire de la session, qui n'est pas conservé.

| Chaufferie | Fichier `.drawio` | Aperçu |
|---|---|---|
| BO | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/Synoptique Chaufferie BO.drawio` | — |
| M | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/M/Synoptique Chaufferie M.drawio` | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/M/Apercu - Synoptique Chaufferie M.png` |
| BN | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/BN/Synoptique Chaufferie BN.drawio` | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/BN/Apercu - Synoptique Chaufferie BN.png` |
| G2 | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/G2/Synoptique Chaufferie G2.drawio` | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/G2/Apercu - Synoptique Chaufferie G2.png` |
| Hall C | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/HC/Synoptique Chaufferie Hall C.drawio` | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/HC/Apercu - Synoptique Chaufferie Hall C.png` |
| NOP | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/NOP/Synoptique Chaufferie NOP.drawio` | `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/NOP/Apercu - Synoptique Chaufferie NOP.png` |

Pièces de justification pour G2 :

- `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/G2/Preuves - pompes G2.png`
- `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/G2/Preuves - Elco G2.png`
- `/tmp/claude-0/-home-user-claude/04b946b9-b186-5eac-a998-ff488ae41212/scratchpad/G2/Pourquoi - pompes de charge G2.png`

Le récapitulatif de projet tenu en parallèle se trouve dans `contexte_projet_chaufferies.md`
(même dépôt).

---

## 10. Mise à jour du 4 novembre 2026

### 10.1 NOP : corrections avant envoi du CdC

Faites sur la version générée le 03/11 (le `.drawio` modifié par Ismail n'a pas été reçu). Mise en page, cartouche
(rév. 01, 29/10/2026, Validé), guide de lecture et synthèse inchangés.

| # | Zone | Modification | Source |
|---|---|---|---|
| 1 | Réseau aérothermes | Modèle : 2 × GRUNDFOS UPC 50-60 (alimentation 400 V 3~ conservée) | Photo p.20 (plaques des têtes 1 et 2, 380 V 3~) |
| 2 | Réseau fatigue | Modèle : UPS corrigé en UPC 40-120 ; puce « Alimentation : 400 V 3~ » ajoutée | Photo p.17 (plaques, boîte « TYPE C 3~ ») |
| 3 | Réseau nord-est | Modèle : 2 × GRUNDFOS UPC 40-120 | Photo p.22 (plaques des têtes 1 et 2) |
| 4 | Réseau sud-ouest | Modèle : 2 × GRUNDFOS UPC 50-120, italique « Pompe 2 de série plus récente » | Photos p.24 (tête 1, Modell A) et p.23 (tête 2, P/N 96405950, Model E) |
| 5 | Réseau sous-station | Modèle conservé (MAGNA ancienne série), sans puce d'alimentation ; italique « Modèle exact non documenté (plaque non relevée) » | Photos p.27 à 29 (pas de plaque) |
| 6 | Hall BF 2 | Modèle : MAGNA1 D 80-60 F 360 ; italique « Pompe non communicante, la gamme MAGNA1 n'accepte pas de module CIM » | Photo p.4 (P/N 99221418, 1 × 230 V) et p.5 |
| 7 | Filtre magnétique | Liaison ajoutée « Alimentation filtre magnétique / Origine non documentée » (pointillé à points, gris, armoire vers équipement), pas de liaison de défaut | Photos p.9 (plaque) et p.10 (coffret, voyant local) |
| 8 | Maintien de pression et dégazage | Liaisons « Alimentation maintien de pression » et « Alimentation centrale de dégazage Vento », « Origine non documentée », même style | Photos de visite (pas de schéma) |
| 9 | Chaudières 1 et 2 | Liaison ajoutée sous chaque « Alimentation chaudière N » : « Alimentation brûleur N / Origine non documentée » | Plaques des brûleurs Weishaupt (400 V 3~), photos du 15/10/2026 |

Rien d'ajouté pour les vannes SAL31, le servomoteur Sauter ASM124F120, les variateurs NORD, le vase, les collecteurs
et les vannes manuelles. Contrôles : une page A3, aucun débordement ni chevauchement, aucun texte parasite,
identifiants uniques, aucune référence cassée.

### 10.2 M et BN alignés sur G2, Hall C et NOP

Reconstruits sur le gabarit commun (titres en 10, texte en 8, images à l'échelle, signe « + » entre équipements couplés),
contenu inchangé sauf :

- **Dates** : M au 01/10/2026 et BN au 08/10/2026, pour prolonger la série G2 (15/10), Hall C (22/10), NOP (29/10)
  à une semaine ouvrée d'écart.
- **« À relever » supprimés** : M, départ X1:1-2 « Départ 230 V, destination non documentée » ; BN, compteur gaz
  « Poids d'impulsion et raccordement non documentés ».
- **Marques** : « Marque et modèle non documentés aux folios… » ajouté quand la marque est inconnue (M : thermostat,
  sonde extérieure, pot à boue ; BN : aérothermes, extracteur, régulation d'ambiance, volet d'air neuf, ventilo-convecteur,
  désemboueur).
- **M** : les deux vannes d'isolement Belimo réunies dans un seul cadre (deux images) pour tenir en police 8.
- **BN** : le pot à boue passe dans une zone « Équipements du réseau chauffage » à gauche, comme à NOP ; le logo CIAT
  est retiré de l'image des aérothermes (marque non documentée à BN).
