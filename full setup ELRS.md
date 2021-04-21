# Mise en place du protocole Express LRS sur un TX R9M et RX R9 Mini/MM

# WORK IN PROGRESS !!!


Bienvenue dans ce tuto de mise en place du protocole Express LRS. 
Le but est de vous montrer comment mettre en place de A à Z ce protocole 
de manière complète et simple sur de matériel commun. Il sera à adapter
à votre propre matériel si nécessaire, vous trouverez tout ce dont vous aurez
besoin le cas échéant sur le [wiki du projet](https://github.com/ExpressLRS/ExpressLRS/wiki)

1. [Installation des outils nécessaires](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#installation-des-outils-n%C3%A9cessaires)
2. [Mises à jour de la radio](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#mise-%C3%A0-jours-de-la-radio)
3. [Modification hardware du TX](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#modification-hardware-du-tx)
4. [Compilation du firmware TX](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#compilation-du-firmware-tx)
5. [Installation du firmware TX](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#installation-du-firmware-tx)
6. [Configuration d'openTX sur la radio](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#configuration-dopentx-sur-la-radio)
7. [Compilation et installation du firmware RX](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#compilation-et-installation-du-firmware-rx)


## Installation des outils nécessaires

Nous aurons besoin de 3 outils (je ne détaille pas l'installation et vous mets les liens pour windows) : [Betaflight Configurator](https://github.com/betaflight/betaflight-configurator/releases/download/10.7.0/betaflight-configurator-installer_10.7.0_win32.exe),
[Tx Companion](https://downloads.open-tx.org/2.3/release/companion/windows/companion-windows-2.3.10.exe) pour gérer la radio, et [ExpressLRS Configurator](https://github.com/ExpressLRS/ExpressLRS-Configurator/releases/download/v0.4.11/ExpressLRS-Configurator-Setup-0.4.11.exe)

## Mises à jour de la radio

Pour que ELRS fonctionne il faut installer une version spécifique de OpenTX sur votre radio, la dernière en date est la version 2.3.10 pour ELRS).
Vous pouvez télécharger le firmware pour votre radio directement sur le [git](https://github.com/ExpressLRS/ExpressLRS/tree/master/OpenTX) du projet ELRS, ATTENTION à prendre le fichier correspondant à VOTRE radio (par exemple [opentx-x9d+-2.3.10.bin](https://github.com/ExpressLRS/ExpressLRS/blob/master/OpenTX/opentx-x9d%2B-2.3.10.bin) pour la X9D+)

il vous faudra également l'archive de la SD en version [2.3.10](https://downloads.open-tx.org/2.3/release/sdcard/) il faut également prendre la version pour votre radio. ([ici](https://downloads.open-tx.org/2.3/release/sdcard/opentx-x9d%2B/sdcard-212x64-2.3V0030.zip) pour la X9D+)

### backup de la radio

Avant toute chose il est important de sauvegarder votre radio, pour ce faire nous allons utiliser TX Companion et sauvegardé :
- le firmware
- la SD
- la conf de vos modèles

Il faut commencer par allumer votre radio en mode bootloader pour ce faire appuyer simultanément sur les trims YAW et ROLL vers le centre (garder appuyer) et allumer votre radio. Brancher là ensuite en USB sur votre PC et lancer Tx Companion.

#### backup du firmware
Onglet transfert / Lire le firmware de la radio


<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_firmware.png"/>


Sélectionner le dossier souhaitez et choisissez un nom.


<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_firmware2.png"/>


Patientez pendant la sauvegarde du firmware


<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_firmware3.png"/>


#### backup de la SD

Onglet Fichier / Synchroniser la SD

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_SD.png"/>

Choisissez le dossier local où sauvegarder votre SD et vérifier les paramètre en suivant la capture suivante et cliquez sur Démarrer 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_SD2.png"/>

Patientez pendant la sauvegarde de la SD 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_SD3.png"/>


#### Backup de vos modèles

Onglet Transfert / Lire les paramètres et modèles depuis la radio

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_models.png"/>

Vous Verrez apparaître une fenêtre avec le snom de vos modèles, allez dans l'onglet Fichier/Enregistrer sous...

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_models2.png"/>

Choisissez l'emplacement et le nom de la sauvegarde

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/backup_radio_models3.png"/>

### Mise à jour du firmware

Maintenant que tout est sauvegarder passons aux choses sérieuses !

Nous allons mettre à jour le firmware de la radio : 

Onglet Transfert/Transférer le firmware à la radio

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/update_radio_firmware.png"/>

Sélectionner le firmware précédement télécharger (exemple : opentx-x9d+-2.3.1.bin) cochez "Vérifier la compatibilité du hardware" et cliquez sur Transférer.

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/update_radio_firmware2.png"/>

Patientez pendant la mise à jour : 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/update_radio_firmware3.png"/>

### Mise à jour de la SD

Une fois l'archive de la SD en 2.3.10 décompressée copier les fichiers depuis Windows vers la SD de votre radio (attention le débit est faible cette opération est plutôt longie)

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/update_radio_sd.png"/>

Lorsque Windows vous indique des fichiers identiques cliquez sur Remplacer les fichiers dans la destination.

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/update_radio_sd2.png"/>

## Modification hardware du TX

**Cette opération n'est nécessaire** <ins>**UNIQUEMENT</ins> **si vous avez un R9M 2018 (accst)**

Elle vise à permettre un baudrate de 400K sur ces modèles. Vous aurez besoin d'une résistance entre 300Ω et 1000Ω.

Il faut souder la résistance entre le régulateur 3.3V et une autre résistance située au dos du TX :

<img src="https://raw.githubusercontent.com/AlessandroAU/ExpressLRS/master-dev/img/FrSky%20R9M%20(2018%20model)%20resistor%20mod.png" width="100%">

Il se peut que votre régulateur ne soit pas dans le même sens, il faut prendre la pate toute seule. Attention à mettre la broche de la résistance au plus prêt du circuit sur le côté sinon cela ne rentrera plus dans le boitier. 

## Compilation du firmware TX

Après avoir installer ExpressLRS Configurator lancé le et configurer les options suivantes : 

Chaque option dispose d'une aide (en anglais ainsi qu'un liens vers le wiki bien pratique)

Choisir la dernière version en date : 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation.png"/>

Dans Target choisir votre TX via stock BL : 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation2.png"/>

Dans Device options sur la partie gauche : 

Choisir votre fréquence puis une binding phrase. Attention cette phrase devra être la même entre votre TX et TOUS vos RX elle sert de clef pour établir le bind direct entre le TX et les RX ! 

<ins>ne mettez pas testlrs mais quelque chose pour vous et RETENEZ le !</ins> 

SURTOUT NE PAS COCHER R9M_UNLOCK_HIGHER_POWER ! cela nécessite un mod hardware afin de ventiler le TX, en effet vous ne pourrez pas dépasser les 250mW sans ce mode, ELRS utilisant des fréquence plus élevé que le firmware R9 le CPU chauffe énormément et nécessite un [refroidissement actif](https://github.com/ExpressLRS/ExpressLRS/wiki/R9M-Fan-Mod-Cover).

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation3.png"/>

Dans Device options sur la partie droite :

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation4.png"/>

Enfin cliquez sur BUILD 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation5.png"/>

Une fois le build terminer l'outil vous ouvre le dossier de compilation, il faut copier le fichier "firmware.elrs" sur la SD de votre radio (créer un dossier ELRS)

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/tx_firmware_compilation6.png"/>

## Installation du firmware TX

Vous aurez donc besoin du fichier "firmware.elrs" ainsi que du fichier [r9m_elrs_bl.frk](https://github.com/ExpressLRS/ExpressLRS/blob/master/src/bootloader/r9m_elrs_bl.frk?raw=true) qu'il faudra également transférer sur la SD de votre radio (dans le dossier ELRS).

Selectionner un modèle où le module externe est désactiver (non obligatoire mais je préfère cela évite que le module externe démarre)

Faire un clique long sur la touche MENU de la radio, puis cliquez sur PAGE afin d'afficher le contenue de votre SD.
Naviguer dans le dossier ELRS, puis sur le fichier "r9m_elrs_bl.frk", faire un appuie long sur ENT puis sélectionner "Flasher le module externe"

Patientez pendant le flash du fichier (bootloader ELRS)

Maintenant selectionner le fichier "firmware.elrs" et flasher de nouveau le module externe.

Selectionner maintenant le modèle où vous souhaitez passer en ELRS, et dans la configuration du module externe choisir le mode CRSF.
Normalement si vous avez bien fait les choses votre R9 devrait emettre sa music de startup.

## Configuration d'openTX sur la radio

Nous avons deux actions à faire sur la radio afin que tout soit propre : 
 
### Désactivation de l'ADC Filter

Par défaut sur OpenTX l'ADC Filter est actif par defaut, il sert à "lisser" les commandes RC et va poser problème avec le bitrate du ELRS.

### Ajout du script Lua ELRS

ELRS fournit un script lua pour gérer le module, vous pouvez le télécharger [ici](https://github.com/AlessandroAU/ExpressLRS/raw/master/src/lua/ELRS.lua).
IL faut le déposer dans le dossier `Scripts/Tools` de la SD de votre radio. Une fois fait vous pouvez le lancer avec un clique long sur la touche MENU puis choisir ELRS.

Cet outil permet entre autre de choisir la puissance. Mais la partie intéressante pour le moment est sur la première ligne.

Vous devriez voir un 0:200, ce qui indique la chose suivante : 0 mauvais packet et 200 bon packets par secondes entre la radio et le TX cela indique que tout fonctionne.


## Compilation et installation du firmware RX

Le flash du firmware du RX s'effectue également en deux étapes : 
- flash du bootloader depuis la radio
- flash du firmware via le passtrought Betaflight (d'autres méthodes existent mais celle-ci est préférable)

### Flash du bootloader

Il faut récupérer le fichier [r9mm_elrs_bl.frk](https://github.com/AlessandroAU/ExpressLRS/blob/master/src/bootloader/r9mm_elrs_bl.frk?raw=true) et le transférer sur la radio (toujours dans le dossier ELRS).
Puis le flasher via la méthode habituelle : 

connection du rx à la radio via le smartport (⚫  - `GND`, 🔴  - `5V`, 🟡  - `S.Port`)


<img src="https://cdn.discordapp.com/attachments/738450139693449258/773630998822780948/image0.jpg" width="40%">

<img src="https://oscarliang.com/ctt/uploads/2017/07/flash-frsky-r9-mini-rx-firmware-taranis-connection.jpg">

En suivant la même procédure que pour le flash du bootloader du TX flasher le fichier "r9mm_elrs_bl.frk".

### flash du firmware

#### Connection du RX à la FC

Connecté votre RX sur un UART libre (de préférence un UART non dédié au sbus si possible et avec TX et RX dispo, l'utilisation du port spécifique au sbus doit être possible mais sur certaines FCs disposant d'un inversseur matériel cela pourrais posé problème)

<img src="https://media.discordapp.net/attachments/738450139693449258/771835630426128444/image0.png" width="60%">

<ins>Pensez à bien croisé TX et RX !</ins>

Bien évidement connecter GND et +5V sur des pads correspondant (préférer un +5VUSB si possible)

#### Configuration de la FC

Dans Betaflight Configurator dans l'onglet port configurer le port sur lequel vous avez soudé votre rx en serial RX 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/betaflight_configuration.png"/>

Puis dans l'onglet Configuration définir le récepteur en `RX Série` et `CRSF`

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/betaflight_configuration2.png"/>

ensuite dans le `CLI` rentré les commandes suivantes : 

    set serialrx_inverted = OFF
    set serialrx_halfduplex = OFF
    save

#### Flash du firmware

Ouvrir de nouveaux ExpressLRS Configurator.

Choisir la même release que pour le TX et ensuite la Target `Frsky_RX_R9MM_R9MINI_via_BetaflightPassthrough` 

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/rx_firmware_compilation.png"/>

Ensuite dans le Device options sélectionner la même fréquence que pour le TX et <ins>SURTOUT</ins> la même Binding phrase (normalement elle devrait déjà être renseigner avec la précédente valeur)

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/rx_firmware_compilation2.png"/>

Fermer Betaflight Configurator, débrancher puis rebrancher la FC (mettre une lipo si vous n'avez pas de +5VUSB) et cliquer sur `BUILD & FLASH`

<img src="https://github.com/albebert/how-to-ELRS/blob/main/imgs/rx_firmware_compilation.png"/>

La procédure prends quelques minutes la première fois le temps de compiler le firmware puis l'uploader (les prochaines fois la compilation ne sera pas faite si vous n'effectuer pas de changement de configuration)

une fois le RX flasher vous pouvez reboot la FC, allumer votre radio et votre RX devrait être bind (led fixe), et normalement vos voies devrait répondre sous Betaflight ! 

