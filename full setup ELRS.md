# Mise en place du protocole Express LRS sur un TX R9M et RX R9 Mini/MM

Bienvenue dans ce tuto de mise en place du protocole Express LRS. 
Le but est de vous montrer comment mettre en place de A a Z ce protocole 
de manière complète et simple sur de matériel commun. Il sera à adapter
à votre propre matériel si nécessaire, vous trouverez tout ce dont vous aurez
besoin le cas échéant sur le [wiki du projet](https://github.com/ExpressLRS/ExpressLRS/wiki)

1. [Installation des outils nécessaires](https://github.com/albebert/how-to-ELRS/blob/main/full%20setup%20ELRS.md#installation-des-outils-n%C3%A9cessaires)
2. Mise à jours de la radio
3. Modification hardware du TX
4. Compilation du firmware TX
5. Installation du firmware TX
6. Compilation et installation du firmware RX


## Installation des outils nécessaires

Nous aurons besoin de 3 outils (je ne détaille pas l'installation et vous mes les liens pour windows) : [Betaflight Configurator](https://github.com/betaflight/betaflight-configurator/releases/download/10.7.0/betaflight-configurator-installer_10.7.0_win32.exe),
[Tx Companion](https://downloads.open-tx.org/2.3/release/companion/windows/companion-windows-2.3.10.exe) pour gérer la radio, et [ExpressLRS Configurator](https://github.com/ExpressLRS/ExpressLRS-Configurator/releases/download/v0.4.11/ExpressLRS-Configurator-Setup-0.4.11.exe)

## Mise à jours de la radio

Pour que ELRS fonctionne il faut installer une version spécifique de OpenTX sur votre radio, la dernière en date est la version 2.3.10 pour ELRS).
Vous pouvez télécharger le firmware pour votre radio directement sur le [git](https://github.com/ExpressLRS/ExpressLRS/tree/master/OpenTX) du projet ELRS, ATTENTION à prendre le fichier correspondant à VOTRE radio (par exemple [opentx-x9d+-2.3.10.bin](https://github.com/ExpressLRS/ExpressLRS/blob/master/OpenTX/opentx-x9d%2B-2.3.10.bin) pour la X9D+)

il vous faudra également l'archive de la SD en version [2.3.10](https://downloads.open-tx.org/2.3/release/sdcard/) il faut également prendre la version pour votre radio. ([ici](https://downloads.open-tx.org/2.3/release/sdcard/opentx-x9d%2B/sdcard-212x64-2.3V0035.zip) pour la X9D+)

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

