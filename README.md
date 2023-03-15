# Configuration Klipper pour FLSUN Super Racer avec BigTreeTech Manta M4P

![maxresdefault](https://user-images.githubusercontent.com/12702322/187098254-be0a0182-cc04-401a-9e95-97dda4bdb1b6.jpeg)

Klipper est un firmware d'imprimante 3D. Il combine la puissance d'un ordinateur à usage général avec un ou plusieurs microcontrôleurs.

Consultez le [document sur les fonctionnalités](https://www.klipper3d.org/Features.html) pour plus d'informations sur les raisons pour lesquelles vous devriez utiliser Klipper.

<br />

## Table des matières

- [Informations](#informations)
- [Liens utiles](#liens-utiles)
- [Fichiers STL nécessaires](#fichiers-stl-nécessaires)
- [Schémas de câblage](#schémas-de-câblage)
- [Installation de Klipper via MainsailOS](#installation-de-klipper-via-mainsailos)
- [Connexion via SSH](#connexion-via-ssh)
- [Mise à jour des dépendances](#mise-à-jour-des-dépendances)
- [Installation de KlipperScreen](#installation-de-klipperscreen)
- [Désactivation du PCI Express sur le CM4](#désactivation-du-pci-express-sur-le-cm4)
- [Installation de l'image de démarrage](#installation-de-limage-de-démarrage)
- [Installation du driver pour écran DSI & Caméra CSI](#installation-du-driver-pour-écran-dsi--caméra-csi)
- [Modification du fichier /boot/cmdline.txt](#modification-du-fichier-bootcmdlinetxt)
- [Modification du fichier /boot/config.txt](#modification-du-fichier-bootconfigtxt)
- [Installation du firmware Klipper sur la Manta M4P](#installation-du-firmware-klipper-sur-la-manta-m4p)
- [Configuration pour l'ADXL345](#configuration-pour-ladxl345)
- [Utilisation des fichiers de configuration](#utilisation-des-fichiers-de-configuration)
- [Changements coté Slicers](#changements-coté-slicers)
- [Calibrer l'imprimante](#calibrer-limprimante)
- [Mettre à jour KlipperScreen](#mettre-à-jour-klipperscreen)
- [Activer la fonction Exclude Objects](#activer-la-fonction-exclude-objects)
- [Activer et mettre à jour la fonction Timelapse](#activer-et-mettre-à-jour-la-fonction-timelapse)
- [Utilisation du Neopixels Ring Light](#utilisation-du-neopixels-ring-light)
- [Remerciements](#remerciements)

<br />

Si vous aimez mon travail, n'hésitez pas à me soutenir en me payant une 🍺 ou un ☕. Merci 🙂 

[ ![Download](https://user-images.githubusercontent.com/12702322/115148445-e5a40100-a05f-11eb-8552-c1f5d4355987.png) ](https://www.paypal.me/CyrilGuislain)

<br />

## Informations

Cette configuration est compatible avec la FLSUN Super Racer uniquement et avec cette configuration :

- Carte mère BigTreeTech Manta M4P
- Raspberry Pi Compute Module 4
- Extrudeur Bondtech LGX Lite
- Bloc de chauffe Trianglelab CHC Pro (104NT-4-R025H42G) (en option, voir fichier printer.cfg)
- Drivers TMC 2209/2226
- LED Neopixel (en option, voir fichier printer.cfg)
- Ecran BigTreeTech PITFT70 V2.0

<br />

Cette configuration de Klipper pour la Super Racer doit être utilisée avec cette version de KlipperScreen disponible ici : [KlipperScreen-Flsun-Super-Racer](https://github.com/Guilouz/KlipperScreen-Flsun-Super-Racer)

<br />

## Liens utiles

- Pour calibrer votre extrudeur, voir ici : https://www.klipper3d.org/Rotation_Distance.html

- Pour régler le Pressure Advance, voir ici : https://www.klipper3d.org/Pressure_Advance.html

- Pour ajuster manuellement la compensation de résonance, voir ici : https://www.klipper3d.org/Resonance_Compensation.html

- Pour mesurer les Resonances avec l'ADXL, voir ici : https://www.klipper3d.org/Measuring_Resonances.html

- Pour afficher les vignettes à l'écran, voir ici : https://klipperscreen.readthedocs.io/en/latest/Thumbnails/

<br />

## Fichiers STL nécessaires

- Support pour BigTreeTech Manta M4P : https://www.printables.com/model/268979-flsun-super-racer-manta-m4p-mount
- Case pour écran BigTreeTech PITFT70 + Support : https://www.printables.com/model/268989-flsun-super-racer-pitft70-case-mount
- Easy connection pour ADXL : https://www.printables.com/model/268986-flsun-super-racer-easy-connection-for-adxl345
- Support ADXL : https://www.printables.com/model/245136-adxl345-mount-for-flsun-super-racer

<br />

## Schémas de câblage

- Avec branchement ADXL sur GPIO :

![Manta M4P SR](https://user-images.githubusercontent.com/12702322/187642336-86ce7061-2d1e-45b7-9825-e911b071344c.png)

- Avec branchement ADXL sur SPI :

![Manta M4P SR SPI](https://user-images.githubusercontent.com/12702322/209481248-77f039a0-3b70-4f84-8a0f-e2a2b1da71f2.png)

- Pins :

![Pins](https://user-images.githubusercontent.com/12702322/187642527-ae006f09-ed8e-44cc-a29e-cc6f2cf0a496.jpg)

<br />

## Installation de Klipper via MainsailOS

- Téléchargez et installez la dernière version de Raspberry Pi Imager ici : https://www.raspberrypi.com/software/
- Si vous utilisez un Raspberry Pi CM4 avec mémoire eMMC, vous aurez également besoin de RpiBoot :
	- Pour Windows : http://github.com/raspberrypi/usbboot/raw/master/win32/rpiboot_setup.exe
	- Pour MacOS : https://github.com/raspberrypi/usbboot#macos

- Lors de l'ouverture de Raspberry Pi Imager, les éléments suivants s'affichent :

![001](https://user-images.githubusercontent.com/12702322/209439292-4f0a528c-35f6-4648-a61c-d26c853f5343.jpg)

- Sélectionnez `CHOISISSEZ L'OS` et une fenêtre contextuelle s'ouvrira comme illustré ci-dessous.
- Faites défiler jusqu'à `Other specific-purpose OS` :

![002](https://user-images.githubusercontent.com/12702322/209439343-4af9c111-219e-47a3-b659-ce6bea414a8d.jpg)

- Sélectionnez `3D printing` :

![003](https://user-images.githubusercontent.com/12702322/209439366-c497b0cf-9d77-45ab-abd6-a1977951e220.jpg)

- Sélectionnez `Mainsail OS` :

![004](https://user-images.githubusercontent.com/12702322/209439427-b7fe98f3-d38e-46b5-bc8d-9109d87557bf.jpg)

- Puis la version désirée (32-bit ou 64-bit) :

![005](https://user-images.githubusercontent.com/12702322/209439432-099b1f87-9c28-4bb5-81dc-99362dddc877.jpg)

- Une fois cela fait, cliquez sur `CHOISISSEZ LE STOCKAGE` et sélectionnez la carte microSD souhaitée ou l'eMMC (voir la documentation de BigTreeTech page 21 : [ici](https://github.com/bigtreetech/Manta-M4P/blob/master/BIGTREETECH_M4P%26CB1%20User%20Manual.pdf)) :

![006](https://user-images.githubusercontent.com/12702322/209439491-9802bf1a-c9c8-4115-bd37-ba8be03c32a1.jpg)

- Le nom d'hôte, le SSH, le Wi-Fi, la langue et de nombreux autres paramètres peuvent désormais être parcourus et préconfigurés dans un menu de configuration, en cliquant sur la petite roue dentée dans le coin droit :

![007](https://user-images.githubusercontent.com/12702322/209439780-be655081-de4d-4516-bb54-612022e7b1f0.jpg)

- Configurez les divers paramètres comme suit :

![Sans titre](https://user-images.githubusercontent.com/12702322/210407996-71867cc7-5a5b-469f-b6bb-9dcee71441be.png)

Note : Si vous modifiez le paramètre `Set hotname`, l'URL de votre Raspberry Pi sera modifiée en conséquence.                                              Comme indiqué dans la capture d'écran ci-dessus, votre URL sera : http://flsun-super-racer.local

Veuillez également à ne pas changer le nom d’utilisateur `pi` !  La configuration de MainsailOS repose sur cet utilisateur.                                                                                                                             
- Cliquez ensuite sur `SAVE` pour sauvegarder ces paramètres.

- Vous pouvez ensuite cliquer sur `ÉCRIRE` :
     
![012](https://user-images.githubusercontent.com/12702322/209439815-56274a2a-e7ed-4454-9fb0-c67b75d3a724.jpg)

- Puis acceptez l'avertissement :

![013](https://user-images.githubusercontent.com/12702322/209439842-911fe29b-1682-40d7-85e5-499a423b6345.jpg)

- Cela prendra un certain temps pour écrire l'image sur la carte microSD ou l'eMMC :

![014](https://user-images.githubusercontent.com/12702322/209439856-64d53e40-028c-4e3a-a348-885ba5a25890.jpg)

-  Une fois l'écriture terminée, une vérification sera effectuée :

![015](https://user-images.githubusercontent.com/12702322/209439890-190698fc-4908-481d-8c1b-3fd1f6632a54.jpg)

- Une fois la vérification terminée, cliquez sur `CONTINUER` :

![016](https://user-images.githubusercontent.com/12702322/209439914-a571c3ea-7ccb-4bb7-bb28-66c980f196cb.jpg)

- L'installation est maintenant terminée.

<br />

## Connexion via SSH

- Téléchargez et installez le logiciel MobaXterm ici : https://mobaxterm.mobatek.net/download-home-edition.html

- Lancez-le puis cliquez sur l'icône `Session` puis `SSH` : 

![01](https://user-images.githubusercontent.com/12702322/209440762-d9efc473-22c3-484b-8250-71bb05db1e5f.jpg)
![02](https://user-images.githubusercontent.com/12702322/209440764-45f23603-8b33-4700-af43-ede574bf6287.jpg)

- Renseignez l'adresse IP de votre Raspberry Pi dans le champ `Remote Host`, cochez la case `Specify username` et saisissez le nom d'utilisateur `pi` dans le champ puis cliquez sur `OK` :

![Capture d’écran 2022-12-24 à 15 34 31](https://user-images.githubusercontent.com/12702322/209440775-9cb69f62-15b2-4407-8907-33c1733d8983.jpg)

- Sur la fenêtre qui s'affiche, saisissez votre mot de passe précédemment défini dans Raspberry Pi Imager (il ne s'affiche pas à la saisie, c'est normal) : 

![Capture d’écran 2022-12-24 à 15 39 29](https://user-images.githubusercontent.com/12702322/209440822-6af829bc-0f36-42c1-be75-faf411ea6a5c.jpg)

- Une fenêtre d'autorisation va s'afficher, autorisez-la. Il est également possible qu'une autre fenêtre vous demandant de changer le mot de passe s'affiche, ignorez-là.

- Une fois connecté, sur la partie gauche de la fenêtre vous avez l'accès aux dossiers et fichiers de votre Raspberry Pi et à la fenêtre d'invite de commande SSH sur la partie droite :

![Capture d’écran 2022-12-24 à 15 36 40](https://user-images.githubusercontent.com/12702322/209440829-aa86e3ff-5e24-4026-b321-370150fa3e58.jpg)

<br />

## Mise à jour des dépendances

- Dans la fenêtre d'invite de commande SSH, entrez la commande suivante pour télécharger la liste des mises à jour (vous devrez entrer le mot de passe root) :
```
sudo apt update
```

- Puis cette commande pour les installer :
```
sudo apt full-upgrade
```

- Supprimez ensuite les dépendances inutiles (une commande à la fois) :
```
sudo apt autoremove
```
```
sudo apt autoclean
```
```
sudo apt clean
```

- Vous pouvez également mettre à jour le firmware de votre Raspberry Pi en saisissant cette commande :
```
sudo rpi-update
```

- Puis saisissez la commande suivante (une à la fois) :
```
sudo rm -rf /home/pi/mainsail-config
```
```
sudo rm /home/pi/printer_data/config/mainsail.cfg
```

- Puis saisissez la commande suivante pour redémarrer :
```python
sudo reboot
```

<br />

## Installation de KlipperScreen

- Dans la fenêtre d'invite de commande SSH, saisissez les commandes suivantes (une à la fois) :
```
cd ~ && git clone https://github.com/Guilouz/KlipperScreen-Flsun-Super-Racer.git
```
```
sudo mv /home/pi/KlipperScreen-Flsun-Super-Racer /home/pi/KlipperScreen
```
```
./KlipperScreen/scripts/KlipperScreen-install.sh
```
- Puis saisissez la commande suivante pour redémarrer :
```python
sudo reboot
```

<br />

## Désactivation du PCI Express sur le CM4

La Manta M4P ne dispose pas de port PCI Express, il est donc nécessaire de désactiver la fonctionnalité pour éviter un message au démarrage.

- Créez le fichier `disable-pcie-overlay.dts` avec la commande suivante : 
```python
sudo nano /boot/overlays/disable-pcie-overlay.dts
```
- Copiez ce code dans la fenêtre qui s'affiche :
```
/*
 * disable-pcie-overlay.dts
 */

/dts-v1/;
/plugin/;

/ {
	compatible = "brcm,bcm2835";

	fragment@0 {
		target = <&pcie0>;
		__overlay__  {
			status = "disabled";
		};
	};
};
```
- Puis sur votre clavier appuyez sur les touches `Ctrl+X` pour quitter, `Y` pour sauvegarder et `Entrée` pour valider.

- Il faut ensuite convertir le fichier `disable-pcie-overlay.dts` en `disable-pcie-overlay.dtbo` avec la commande suivante :
```python
sudo dtc -@ -I dts -O dtb -o /boot/overlays/disable-pcie-overlay.dtbo /boot/overlays/disable-pcie-overlay.dts
```
- Puis supprimez le fichier `disable-pcie-overlay.dts` avec la commande suivante :
```python
sudo rm /boot/overlays/disable-pcie-overlay.dts
```

<br />

## Installation de l'image de démarrage

Cette section permet d'avoir un logo de démarrage à la place des textes de démarrage du Rapsberry Pi jusqu’à l’apparition du menu KlipperScreen :

![Sans titre](https://user-images.githubusercontent.com/12702322/210775238-db5592eb-8d63-4bec-b8d4-18c98394315b.png)

- Téléchargez ce pack si vous utilisez l'écran BigTreeTech PITFT puis dézipez-le : [Pack Boot (800x480)](https://github.com/Guilouz/Klipper-Flsun-Super-Racer-Manta-M4P/raw/main/Downloads/Pack_Boot_800x480.rar)

- Téléchargez ce pack si vous utilisez un autre écran avec une résolution de 1024x600 puis dézipez-le : [Pack Boot (1024x600)](https://github.com/Guilouz/Klipper-Flsun-Super-Racer-Manta-M4P/raw/main/Downloads/Pack_Boot_1024x600.rar)

- Faites glisser les 3 fichiers `initramfs.img`, `splash.txt` et `splash.png` dans la fenêtre de gauche en vous assurant d'être bien dans le répertoire `/home/pi/`.

- Dans la fenêtre d'invite de commande SSH, saisissez les commandes suivantes (une à la fois) :
```python
sudo cp /home/pi/splash.png /boot/
```
```python
sudo cp /home/pi/splash.txt /boot/
```
```python
sudo cp /home/pi/initramfs.img /boot/
```
- Vous pouvez ensuite supprimer ces 3 fichiers du répertoire `/home/pi/` en saisissant les commandes suivantes (une à la fois) :
```python
sudo rm /home/pi/splash.png
```
```python
sudo rm /home/pi/splash.txt
```
```python
sudo rm /home/pi/initramfs.img
```

<br />

## Installation du driver pour écran DSI & Caméra CSI

- Saisissez la commande suivante : 
```python
sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-disp1-cam1.bin -O /boot/dt-blob.bin
```

<br />

## Modification du fichier /boot/cmdline.txt

- Saisissez la commande suivante : 
```python
sudo nano /boot/cmdline.txt
```
- Sur la fenêtre qui s'affiche, remplacez le paramètre `console=tty1` par `console=tty3`

- Puis ajoutez ces éléments à la fin de la ligne :
```python
logo.nologo loglevel=0 vt.global_cursor_default=0 splash silent quiet
```
![Capture d’écran 2022-12-24 à 17 15 56](https://user-images.githubusercontent.com/12702322/209443857-f6760a96-c6aa-46ce-8f60-f439775c2dd2.jpg)

- Puis sur votre clavier appuyez sur les touches `Ctrl+X` pour quitter, `Y` pour sauvegarder et `Entrée` pour valider.

<br />

## Modification du fichier /boot/config.txt

- Saisissez la commande suivante : 
```python
sudo nano /boot/config.txt
```
- Sur la fenêtre qui s'affiche, ajoutez ces éléments au début du fichier :
```
## Splashcreen settings
initramfs initramfs.img
dtoverlay=disable-pcie-overlay
disable_splash=1
boot_delay=0
```
![Capture d’écran 2022-12-24 à 16 07 40](https://user-images.githubusercontent.com/12702322/209442001-4a7a2e8c-d9c0-455a-a0ea-c4e31f396155.jpg)

- Puis modifiez également ces lignes déjà présentes en ajoutant un "#" devant `dtoverlay=vc4-fkms-v3d` comme suit :
```
# Enable DRM VC4 V3D driver
#dtoverlay=vc4-kms-v3d
max_framebuffers=2
```
![Capture d’écran 2022-12-24 à 16 08 48](https://user-images.githubusercontent.com/12702322/209442063-3cc9816e-2477-4fba-8e12-bc1940143833.jpg)

- Puis également ces lignes en remplaçant la ligne `otg_mode=1` par `dtoverlay=dwc2,dr_mode=host` comme suit :

```
[cm4]
# Enable host mode on the 2711 built-in XHCI USB controller.
# This line should be removed if the legacy DWC2 controller is required
# (e.g. for USB device mode) or if USB support is not required.
dtoverlay=dwc2,dr_mode=host
```
![Capture d’écran 2022-12-24 à 17 01 17](https://user-images.githubusercontent.com/12702322/209443460-a3067521-2496-4134-9d15-36dbf2763f37.jpg)

- Puis sur votre clavier appuyez sur les touches `Ctrl+X` pour quitter, `Y` pour sauvegarder et `Entrée` pour valider.

- Vous pouvez maintenant saisir la commande suivante pour redémarrer le Raspberry Pi :
```python
sudo reboot
```

<br />

## Installation du firmware Klipper sur la Manta M4P

- Connectez-vous de nouveau en SSH et saisissez ces commandes (une à la fois) :
```shell
cd ~/klipper/
```
```shell
make menuconfig
```
- Sélectionnez ces paramètres :
```
[*] Enable extra low-level configuration options
    Micro-controller Architecture (STMicroelectronics STM32) --->
    Processor model (STM32G0B1)  --->
    Bootloader offset (8KiB bootloader) --->
    Clock Reference (8 MHz crystal) --->
    Communication interface (USB (on PA11/PA12)) --->
    USB ids  --->
()  GPIO pins to set at micro-controller startup
```
- Puis sur votre clavier appuyez sur la touche `Q` puis sur `Y` pour sauvegarder la configuration.

- Saisissez les commandes suivantes pour compiler le firmware (une à la fois) :
```python
make clean
```
```python
make
```
- Récupérez le firmware nommé `Klipper.bin` sur la page de gauche dans le répertoire `/home/pi/klipper/out/`.

- Renommez-le en `firmware.bin`.

- Copiez-le à la racine d'une carte SD (et non microSD) formatée en FAT32 et une taille d'allocation de 4096.

- Insérez la carte SD dans la Manta M4P puis allumez l'imprimante.

- L'installation dure que quelques secondes, pour vérifier que le firmware a bien été installé, le fichier sur la carte SD doit avoir été renommé en `FIRMWARE.CUR`.

- Connectez-vous de nouveau en SSH puis saisissez la commande suivante afin de récupérer le serial USB de la Manta M4P :
```shell
ls /dev/serial/by-id/*
```
- Copiez la ligne qui s'affiche (dans un fichier texte par exemple), elle nous sera utile après.

<br /><br />

- Note :  Pour les futures mises à jour du firmware Klipper pour la Manta M4P, il est possible de flasher directement le firmware via SSH, pour cela :
  - Saisissez la commande suivante :
  ```python
  make flash FLASH_DEVICE=/dev/serial/by-id/XXXXX (en remplaçant les XXXXX par le serial obtenu précédemment)
  ```
  - Cela doit ressembler à ça :
  ```python
  make flash FLASH_DEVICE=/dev/serial/by-id/usb-Klipper_stm32g0b1xx_2F0034001050415833323520-if00
  ```
  - Il y aura un message d'erreur `dfu-util: Error during download get_status` après la mise à jour. N'y prêtez pas attention, le plus important c'est d'obtenir la ligne `File downloaded successfully`.

![Capture d’écran 2023-01-03 à 18 26 01](https://user-images.githubusercontent.com/12702322/210409758-87adfbc1-e817-4350-96a1-14418f6c6535.jpg)

<br />

## Configuration pour l'ADXL345

- Connectez-vous de nouveau en SSH puis saisissez les commandes suivantes (une à la fois) :
```python
cd ~/klipper/
```
```python
sudo cp ./scripts/klipper-mcu.service /etc/systemd/system/
```
```python
sudo systemctl enable klipper-mcu.service
```
- Il faut ensuite compiler le code du microcontrôleur en saisissant ces commandes (une à la fois) :
```python
cd ~/klipper/
```
```python
make menuconfig
```
- Sur le menu, définissez `Microcontroller Architecture` sur `Linux process`, puis sur votre clavier appuyez sur la touche `Q` puis sur `Y` pour sauvegarder la configuration :

![Capture d’écran 2022-12-25 à 00 40 14](https://user-images.githubusercontent.com/12702322/209453373-8491cbee-75ad-47f3-a144-793fc4a85d13.jpg)

- Pour compiler et installer le microcontrôleur, saisissez les commandes suivantes (une à la fois) :
```python
sudo service klipper stop
```
```python
make clean
```
```python
make flash
```
```python
sudo service klipper start
```
- Il suffit ensuite de dé-commenter (retirer le #) de la ligne suivante dans le fichier `printer.cfg` pour activer le support de l'ADXL :
```
[adxl345_gpio.cfg]
```
ou
```
[adxl345_spi.cfg]
```
- Cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Après redémarrage du firmware vous devriez voir le MCU de l'ADXL se connecter à Klipper.

- Vous pouvez tester l'accéléromètre en saisissant cette commande :
```
ACCELEROMETER_QUERY
```
- Quelque chose comme ceci doit être retourné :
```
accelerometer values (x, y, z): 5551.544565, 7048.078582, -1924.535449
```
- Entrez ensuite cette commande pour mesurer le bruit de l'accéléromètre pour chaque axe :
```
MEASURE_AXES_NOISE
```
- Vous devriez obtenir des chiffres de référence pour le bruit de l'accéléromètre sur les axes (ils devraient être compris dans la plage de ~ 1-100). Un bruit d'axes trop élevé (par exemple 1000 et plus) peut indiquer des problèmes de capteur, des problèmes d'alimentation ou des ventilateurs déséquilibrés trop bruyants.

- Utilisez cette macro pour mesurer les résonances de l’axe X : `ADXL_AXE_X`

- Suivi de la macro suivante pour enregistrer : `SAUVEGARDER`

- Utilisez cette macro pour mesurer les résonances de l’axe Y : `ADXL_AXE_Y`

- Suivi de la macro suivante pour enregistrer : `SAUVEGARDER`

**Note :** Après les tests, il est préférable de désactiver l'ADXL en commentant à nouveau la ligne suivante `[adxl345_gpio.cfg]` ou `[adxl345_spi.cfg]` dans le fichier `printer.cfg`.

Plus d’informations ici : https://www.klipper3d.org/Measuring_Resonances.html


<br />

## Utilisation des fichiers de configuration

- Téléchargez et décompressez le fichier zip de mon référentiel ici : https://github.com/Guilouz/Klipper-Flsun-Super-Racer-Manta-M4P/archive/refs/heads/main.zip

- Rendez-vous sur l'interface Web de Mainsail via votre navigateur en saisissant l'adresse IP de votre Raspberry Pi.

- Rendez-vous dans l'onglet `Machine` puis importez les fichiers `KlipperScreen.conf`, `printer.cfg`, `neopixels.cfg`, `macros.cfg`, `adxl345_gpio.cfg` et `adxl345_spi.cfg` situés dans le répertoire `Configurations`.

- Une fois importés, ouvrez le fichier `printer.cfg` et modifiez la ligne suivante dans la section `Paramètres MCU` :
```python
serial: /dev/serial/by-id/XXXXX (en remplaçant les XXXXX par le serial obtenu précédemment)
```
- Cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Après redémarrage du firmware, vous devriez voir le MCU de la Manta M4P se connecter à Klipper.

- Ouvrez ensuite le fichier `moonraker.conf` et supprimez les lignes suivantes :
```
[update_manager mainsail-config]
type: git_repo
primary_branch: master
path: ~/mainsail-config
origin: https://github.com/mainsail-crew/mainsail-config.git
managed_services: klipper
```
- Cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Redémarrez ensuite l'imprimante.

<br />

## Changements coté Slicers

- Changez le Gcode de démarrage et le Gcode de fin dans les paramètres de votre Slicer tels quels :

  - Pour **Cura**:
    - Gcode de démarrage :
      ```
      ;Nozzle diameter = {machine_nozzle_size}
      ;Filament type = {material_type}
      ;Filament name = {material_brand} {material_name}
      ;Filament weight = {filament_weight}
      ;M109 S{material_print_temperature}
      ;M190 S{material_bed_temperature}

      START_PRINT BED_TEMP={material_bed_temperature_layer_0} EXTRUDER_TEMP={material_print_temperature_layer_0}
      ```
    - Gcode de fin :
      ```
      END_PRINT
      ```
    
  - Pour **PrusaSlicer** / **SuperSlicer**:
    - Gcode de démarrage :
      ```
      START_PRINT BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP=[first_layer_temperature]
      M104 S[first_layer_temperature]
      M190 S[first_layer_bed_temperature]
      ```
    - Gcode de fin :
      ```
      END_PRINT
      ```

  - Pour **LycheeSlicer**:
    - Gcode de démarrage :
      ```
      START_PRINT BED_TEMP={bed_temp} EXTRUDER_TEMP={temp}
      ```
    - Gcode de fin :
      ```
      END_PRINT
      ```

 <br />

- La rétraction Firmware donne un avantage comparé à la rétraction Slicer, elle peut être modifiée pendant une impression (depuis Mainsail ou Klipperscreen) et donc qu'un même gcode peut être imprimé avec des paramètres différents sans nécéssité d'être re-slicer.

  - Pour **Cura**, il est nécessaire d'installer le plugin `Klipper Settings Plugin` (disponible ici : [Klipper Settings Plugin](https://github.com/jjgraphix/KlipperSettingsPlugin)) et d'activer le paramètre `Enable Firmware Retraction` comme cela :
  
  ![190531375-dc2def8d-9190-47c8-ae6e-bc7efaf2ce04](https://user-images.githubusercontent.com/12702322/197653257-9a4c29cc-64c0-4aa4-9077-32b30a9634d2.jpg)

  - Pour **PrusaSclicer / SuperSlicer**, il est juste nécessaire d'activer le paramètre `Utiliser la rétraction du firmware` comme cela :

![206947349-f522cf58-ce9f-4bd4-88a6-e73893efeaa3](https://user-images.githubusercontent.com/12702322/209440013-48d939ae-3d20-46bd-aed7-29a66cddfd08.jpg)

<br />

## Calibrer l'imprimante

- Démarrez un **PID du plateau** depuis la macro `CALIBRATION_PID_BED_65` et enregistrez la configuration.
  - Note : Il est possible de choisir la température de calibration en cliquant sur la flèche de la macro.
  
- Démarrez un **PID de la buse** depuis la macro `CALIBRATION_PID_HOTEND_220` et enregistrez la configuration.
  - Note : Il est possible de choisir la température de calibration en cliquant sur la flèche de la macro.

<br />

A noter que les calibrations suivante doivent être exécutées dans cet ordre et peuvent être effectuées via les macros ou directement depuis l'écran :

- Mesure du **Z-Offset** via la macro `Z_OFFSET_CALIBRATION` ou depuis l'écran.
  - Note : Le capteur de nivellement doit être branché pour cette opération. Une fois que le capteur a palpé le plateau, la hotend remonte de quelques centimètres, il faut alors retirer le palpeur et ajuster le Z.

- Calibration des **Capteurs de fin de course** via la macro `ENDSTOPS_CALIBRATION` ou depuis l'écran.

- Calibration **Delta** via la macro `DELTA_CALIBRATION` ou depuis l'écran.
  - Note : Le capteur de nivellement doit être branché pour cette opération.

- **Nivellement** du plateau via la macro `BED_LEVELING` ou depuis l'écran.
  - Note : Le capteur de nivellement doit être branché pour cette opération.
  
- Suite à une mesure du Z-Offset, après toutes vos calibrations effectuées, je recommande d'appliquer un Offset de sécurité de 2 mm via la macro `SECURITY_OFFSET`.
  
  Cela pourrait éviter que la buse vienne gratter ou s'enfoncer sur le plateau en cas d'un mauvais ajustement du Z-Offset.

- Après avoir effectué toutes les calibrations de l'imprimante, démarrez ensuite une impression et ajustez la première couche à l'aide des babysteps via le bouton `Ajustements` de KlipperScreen ou via la section `Tête d'impression` de Mainsail.

  **Important**: Ne pas sauvegarder la valeur du Z-Offset, une macro se charge de le faire automatiquement dans le fichier `variables.cfg` et de recharger cette valeur automatiquement au démarrage de Klipper.

- Vous trouverez un STL de test de première couche ici :  [First_Layer_Test.stl](https://github.com/Guilouz/Klipper-Flsun-Super-Racer-Manta-M4P/raw/main/Downloads/First_Layer_Test.stl)

<br /><br />

### Calibration de l'extrudeur :


**Assurez-vous que l'extrudeur contient du filament, que la hotend est chauffée à une température appropriée et que l'imprimante est prête à extruder.**

- Utilisez un marqueur pour placer une marque sur le filament à 120 mm de l'entrée de l'extrudeur.

- Utilisez ensuite un pied à coulisse numérique pour mesurer la distance réelle de cette marque aussi précisément que possible. Notez 120 mm comme `< distance_de_la_marque >`.

- Extrudez 100 mm de filament avec la séquence de commande suivante (une à la fois) :
```
G91
G1 E100 F100
```

Notez 100 mm comme `< distance_demandée >`. 

- Attendez que l'extrudeur termine le mouvement (cela prendra plusieurs secondes). Il est important d'utiliser la vitesse d'extrusion lente pour ce test, car une vitesse plus rapide peut provoquer une pression élevée dans l'extrudeur, ce qui fausserait les résultats. (N'utilisez pas les boutons d'extrusion depuis Mainsail ou l’écran pour ce test car ils s'extrudent à un rythme rapide).

- Utilisez ensuite un pied à coulisse numérique pour mesurer la nouvelle distance entre l’entrée de l'extrudeur et la marque sur le filament. Notez ceci comme `< distance_mesurée >`.

- Calculez ensuite : `< distance_de_la_marque >` **-** `< distance_mesurée >` **=** `< distance_extrusion >`

- Calculez la rotation_distance comme suit :

`< rotation_distance_actuelle >` **X** `< distance_extrusion >` **/** `< distance_demandée >` **=** `rotation_distance`

Note : Vous pouvez récupérer la valeur `< rotation_distance_actuelle >` dans le fichier **printer.cfg** à la ligne `rotation_distance:` de la section `Paramètres Extrudeur & Driver`.

- Remplacez ensuite la nouvelle valeur dans le fichier **printer.cfg** en arrondissant la nouvelle `rotation_distance` à trois décimales.

<br />

## Mettre à jour KlipperScreen

- Rendez-vous sur l'interface Web de Mainsail puis cliquez sur l'onglet `Machine`.

- Ouvrez le fichier `moonraker.conf` et ajoutez les lignes suivantes :
```
[update_manager KlipperScreen]
type: git_repo
path: /home/pi/KlipperScreen
origin: https://github.com/Guilouz/KlipperScreen-Flsun-Super-Racer.git
env: /home/pi/.KlipperScreen-env/bin/python
requirements: scripts/KlipperScreen-requirements.txt
install_script: scripts/KlipperScreen-install.sh
```
- Une fois terminé, cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Vous pouvez maintenant cliquer sur le bouton d'actualisation (toujours dans l'onglet Machine) sur la tuile `Gestionnaire de mise à jour`.

- Vous verrez apparaître une nouvelle ligne `KlipperScreen`.

<br />

## Activer la fonction Exclude Objects

La fonction Exclude Objects permet d’exclure des objets individuels d'une impression en cours via ce bouton :

![Sans titre](https://user-images.githubusercontent.com/12702322/210622141-4f5ce933-41a1-45ea-ae1b-39f3c31ac218.png)

Le bouton ouvre une boîte de dialogue dans laquelle vous pouvez sélectionner chaque objet individuel et l'exclure de l'impression en cours :

![Sans titre11](https://user-images.githubusercontent.com/12702322/210622156-68e11508-1ee1-46e7-8316-4d0b537c2271.png)

- Rendez-vous sur l'interface Web de Mainsail puis cliquez sur l'onglet `Machine`.

- Ouvrez le fichier `moonraker.conf` et remplacez la ligne suivante :
```
enable_object_processing: False

```
par
```
enable_object_processing: True
```
- Une fois terminé, cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

<br />

Plus d'informations sur la fonction Exclude Objects ici : https://docs.mainsail.xyz/features/exclude_objects

<br />

## Activer et mettre à jour la fonction Timelapse

- Rendez-vous sur l'interface Web de Mainsail puis cliquez sur l'onglet `Machine`.

- Ouvrez le fichier `moonraker.conf` et décommentez (retirez le # devant chaque ligne) les lignes suivantes comme ceci :
```python
[timelapse]
###   Directory where the generated video will be saved
output_path: ~/timelapse/
###   Directory where ffmpeg is installed
ffmpeg_binary_path: /usr/bin/ffmpeg

[update_manager timelapse]
type: git_repo
primary_branch: main
path: ~/moonraker-timelapse
origin: https://github.com/mainsail-crew/moonraker-timelapse.git
managed_services: klipper moonraker
```
- Une fois terminé, cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Vous pouvez maintenant cliquer sur le bouton d'actualisation (toujours dans l'onglet Machine) sur la tuile `Gestionnaire de mise à jour`.

- Vous verrez apparaître une nouvelle ligne `timelapse`.

<br />

## Utilisation du Neopixels Ring Light

### Modes disponibles :

Les NeoPixels peuvent être pilotées via ces macros ou depuis l’écran via le menu NeoPixels :

- **NEOPIXEL_ON** : Allumer les NeoPixels
- **NEOPIXEL_OFF** : Éteindre les NeoPixels
- **NEOPIXEL_BLUE** : Allumer les NeoPixels en bleu
- **NEOPIXEL_RED** : Allumer les NeoPixels en rouge
- **NEOPIXEL_GREEN** : Allumer les NeoPixels en vert
- **NEOPIXEL_YELLOW** : Allumer les NeoPixels en jaune
- **NEOPIXEL_ORANGE** : Allumer les NeoPixels en orange
- **NEOPIXEL_VIOLET** : Allumer les NeoPixels en violet
- **HOTEND_GLOW** : Allumer toutes les NeoPixels en fonction de la température de la buse
- **HOTEND_PROGRESS** : Allumer les NeoPixels une à une en fonction de la température de la buse
- **BED_GLOW** : Allumer toutes les NeoPixels en fonction de la température du plateau
- **BED_PROGRESS** : Allumer les NeoPixels une à une en fonction de la température du plateau
- **PERCENT_GLOW** : Allumer toutes les NeoPixels en fonction de la progression d'impression
- **PERCENT_PROGRESS** : Allumer les NeoPixels une à une en fonction de la progression d'impression
- **SPEED_GLOW** : Allumer toutes les NeoPixels en fonction de la vitesse d'impression
- **SPEED_PROGRESS** : Allumer les NeoPixels une à une en fonction de la vitesse d'impression

### Nécéssaire :

- Neon Flexible Tube 1m T1616-Side 10mm PCB : [Ici](https://fr.aliexpress.com/item/4000095850068.html?spm=a2g0o.store_pc_allProduct.8148356.60.19667739Amjjs4&pdp_npi=2%40dis%21EUR%21%E2%82%AC%2013%2C34%21%E2%82%AC%209%2C34%21%21%21%21%21%402100bddd16626284472777282ed43e%2112000015942927508%21sh)

- LED Strip 1 m 60 IP 30 : [Ici](https://fr.aliexpress.com/item/32699391341.html?spm=a2g0o.store_pc_groupList.8148356.1.58d547644pkzbu&pdp_npi=2%40dis%21EUR%21%E2%82%AC%208%2C79%21%E2%82%AC%205%2C71%21%21%21%21%21%402100bdde16626287458333294e75cc%2112000026565180770%21sh)

- Colliers de serrage 2.5 mm

- Support (STL) : [Ici](https://www.printables.com/model/272995-flsun-neopixels-ring-light-support)


### Configuration :

- Rendez-vous sur l'interface Web de Mainsail puis cliquez sur l'onglet `Machine`.

- Ouvrez le fichier `printer.cfg` et modifiez la ligne suivante en supprimant le `#` au tout début :
```python
[include neopixels.cfg]
```
  - **Note :** Vous pouvez également modifier le nombre de LED de vos NeoPixels dans la section Paramètres Neopixels à la ligne : `chain_count: 34`

- Cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

- Toujours sur l'onglet `Machine`, ouvrez maintenant le fichier `KlipperScreen.conf` et copiez tout ce code juste avant la ligne `#~# --- Do not edit below this line. This section is auto generated --- #~#` :
```python
[menu __main actions neopixels]
name: {{ gettext('Neopixels') }}
icon: neopixels

[menu __main actions neopixels led_off]
name: {{ gettext('Off') }}
icon: neopixels-off
method: printer.gcode.script
params: {"script":"NEOPIXEL_OFF"}

[menu __main actions neopixels led_on]
name: {{ gettext('On') }}
icon: neopixels-on
method: printer.gcode.script
params: {"script":"NEOPIXEL_ON"}

[menu __main actions neopixels led_blue]
name: {{ gettext('Blue') }}
icon: neopixels-blue
method: printer.gcode.script
params: {"script":"NEOPIXEL_BLUE"}

[menu __main actions neopixels led_red]
name: {{ gettext('Red') }}
icon: neopixels-red
method: printer.gcode.script
params: {"script":"NEOPIXEL_RED"}

[menu __main actions neopixels led_green]
name: {{ gettext('Green') }}
icon: neopixels-green
method: printer.gcode.script
params: {"script":"NEOPIXEL_GREEN"}

[menu __main actions neopixels led_yellow]
name: {{ gettext('Yellow') }}
icon: neopixels-yellow
method: printer.gcode.script
params: {"script":"NEOPIXEL_YELLOW"}

[menu __main actions neopixels led_orange]
name: {{ gettext('Orange') }}
icon: neopixels-orange
method: printer.gcode.script
params: {"script":"NEOPIXEL_ORANGE"}

[menu __main actions neopixels led_violet]
name: {{ gettext('Violet') }}
icon: neopixels-violet
method: printer.gcode.script
params: {"script":"NEOPIXEL_VIOLET"}

[menu __main actions neopixels hotend_glow]
name: {{ gettext('Hotend (All)') }}
icon: extruder
method: printer.gcode.script
params: {"script":"HOTEND_GLOW"}

[menu __main actions neopixels hotend_progress]
name: {{ gettext('Hotend (One by One)') }}
icon: extruder
method: printer.gcode.script
params: {"script":"HOTEND_PROGRESS"}

[menu __main actions neopixels bed_glow]
name: {{ gettext('Bed (All)') }}
icon: bed
method: printer.gcode.script
params: {"script":"BED_GLOW"}

[menu __main actions neopixels bed_progress]
name: {{ gettext('Bed (One by One)') }}
icon: bed
method: printer.gcode.script
params: {"script":"BED_PROGRESS"}

[menu __main actions neopixels percent_glow]
name: {{ gettext('Progress (All)') }}
icon: clock
method: printer.gcode.script
params: {"script":"PERCENT_GLOW"}

[menu __main actions neopixels percent_progress]
name: {{ gettext('Progress (One by One)') }}
icon: clock
method: printer.gcode.script
params: {"script":"PERCENT_PROGRESS"}

[menu __main actions neopixels speed_glow]
name: {{ gettext('Speed (All)') }}
icon: speed+
method: printer.gcode.script
params: {"script":"SPEED_GLOW"}

[menu __main actions neopixels speed_progress]
name: {{ gettext('Speed (One by One)') }}
icon: speed+
method: printer.gcode.script
params: {"script":"SPEED_PROGRESS"}

[menu __print neopixels]
name: {{ gettext('Neopixels') }}
icon: neopixels

[menu __print neopixels led_off]
name: {{ gettext('Off') }}
icon: neopixels-off
method: printer.gcode.script
params: {"script":"NEOPIXEL_OFF"}

[menu __print neopixels led_on]
name: {{ gettext('On') }}
icon: neopixels-on
method: printer.gcode.script
params: {"script":"NEOPIXEL_ON"}

[menu __print neopixels led_blue]
name: {{ gettext('Blue') }}
icon: neopixels-blue
method: printer.gcode.script
params: {"script":"NEOPIXEL_BLUE"}

[menu __print neopixels led_red]
name: {{ gettext('Red') }}
icon: neopixels-red
method: printer.gcode.script
params: {"script":"NEOPIXEL_RED"}

[menu __print neopixels led_green]
name: {{ gettext('Green') }}
icon: neopixels-green
method: printer.gcode.script
params: {"script":"NEOPIXEL_GREEN"}

[menu __print neopixels led_yellow]
name: {{ gettext('Yellow') }}
icon: neopixels-yellow
method: printer.gcode.script
params: {"script":"NEOPIXEL_YELLOW"}

[menu __print neopixels led_orange]
name: {{ gettext('Orange') }}
icon: neopixels-orange
method: printer.gcode.script
params: {"script":"NEOPIXEL_ORANGE"}

[menu __print neopixels led_violet]
name: {{ gettext('Violet') }}
icon: neopixels-violet
method: printer.gcode.script
params: {"script":"NEOPIXEL_VIOLET"}

[menu __print neopixels hotend_glow]
name: {{ gettext('Hotend (All)') }}
icon: extruder
method: printer.gcode.script
params: {"script":"HOTEND_GLOW"}

[menu __print neopixels hotend_progress]
name: {{ gettext('Hotend (One by One)') }}
icon: extruder
method: printer.gcode.script
params: {"script":"HOTEND_PROGRESS"}

[menu __print neopixels bed_glow]
name: {{ gettext('Bed (All)') }}
icon: bed
method: printer.gcode.script
params: {"script":"BED_GLOW"}

[menu __print neopixels bed_progress]
name: {{ gettext('Bed (One by One)') }}
icon: bed
method: printer.gcode.script
params: {"script":"BED_PROGRESS"}

[menu __print neopixels percent_glow]
name: {{ gettext('Progress (All)') }}
icon: clock
method: printer.gcode.script
params: {"script":"PERCENT_GLOW"}

[menu __print neopixels percent_progress]
name: {{ gettext('Progress (One by One)') }}
icon: clock
method: printer.gcode.script
params: {"script":"PERCENT_PROGRESS"}

[menu __print neopixels speed_glow]
name: {{ gettext('Speed (All)') }}
icon: speed+
method: printer.gcode.script
params: {"script":"SPEED_GLOW"}

[menu __print neopixels speed_progress]
name: {{ gettext('Speed (One by One)') }}
icon: speed+
method: printer.gcode.script
params: {"script":"SPEED_PROGRESS"}
```
- Une fois terminé, cliquez sur `SAUVEGARDER ET REDÉMARRAGE` en haut à droite pour enregistrer le fichier.

<br />

## Remerciements

- [digitalninja-ro](https://github.com/digitalninja-ro/klipper-neopixel) pour les templates NeoPixels.
- [Desuuuu](https://github.com/Desuuuu/klipper-macros) & [danorder](https://github.com/danorder) pour les bases de certaines macros.
