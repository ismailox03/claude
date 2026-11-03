# Projet : raccordement des chaufferies gaz à l'hyperviseur

Site ArcelorMittal Maizières Research. Réalisé par Ismail SOULLAMI.
Vérification : Jérémy STAREMBERGER, Vincent FOJUD. Notes de réunion : Stéphan, Vincent, Jérémy.

## 1. Livrables en cours

| Livrable | Format | État |
|---|---|---|
| Présentation « Point avancement chaufferies » | Beamer (.tex) | Compilée, aucun débordement. Au moins 18 diapos (arbitrage des compteurs en diapo 18) |
| Cahier des charges « Raccordement des chaufferies gaz à l'hyperviseur » | .docx | Première émission en cours de reprise |
| Synoptiques + fiches E/S automate | draw.io | B, D, F, BK/BL, T faits. Les autres sont à remplacer plus tard |

## 2. Catégorisation des chaufferies

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
