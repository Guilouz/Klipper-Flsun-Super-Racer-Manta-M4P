# Klipper Configuration for FLSUN Super Racer

![maxresdefault](https://user-images.githubusercontent.com/12702322/187098254-be0a0182-cc04-401a-9e95-97dda4bdb1b6.jpeg)

Klipper est un firmware d'imprimante 3D. Il combine la puissance d'un ordinateur à usage général avec un ou plusieurs microcontrôleurs.

Consultez le [document sur les fonctionnalités](https://www.klipper3d.org/Features.html) pour plus d'informations sur les raisons pour lesquelles vous devriez utiliser Klipper.

<br />

## Informations

Cette configuration est compatible avec la FLSUN Super Racer uniquement et avec cette configuration :

- Carte mère BigTreeTech Manta M4P
- Raspberry Pi Compute Module 4
- Extrudeur Bondtech LGX Lite
- Bloc de chauffe Trianglelab CHC Pro (104NT-4-R025H42G) (en option)
- Drivers TMC 2209/2226
- LED Neopixel (en option)

Si vous aimez mon travail, n'hésitez pas à me soutenir en me payant une 🍺 ou un ☕. Merci 🙂 

[ ![Download](https://user-images.githubusercontent.com/12702322/115148445-e5a40100-a05f-11eb-8552-c1f5d4355987.png) ](https://www.paypal.me/CyrilGuislain)

<br />

## Installation de Klipper via MainsailOS

- Téléchargez et installez la dernière version de Raspberry Pi Imager ici : https://www.raspberrypi.com/software/
- Si vous utilisez un Raspberry Pi CM4 avec mémoire eMMC, vous aurez également besoin de RpiBoot :
	- Pour Windows : http://github.com/raspberrypi/usbboot/raw/master/win32/rpiboot_setup.exe
	- Pour MacOS : https://github.com/raspberrypi/usbboot#macos

- Lors de l'ouverture de Raspberry Pi Imager, les éléments suivants s'affichent :

![1](https://user-images.githubusercontent.com/12702322/187550209-0614dc72-369c-4dbd-be49-226c02d87a56.png)

- Sélectionnez `CHOOSE OS` et une fenêtre contextuelle s'ouvrira comme illustré ci-dessous.
- Faites défiler jusqu'à `Other specific-purpose OS` :

![rpi-os-popup](https://user-images.githubusercontent.com/12702322/187550564-abc9dc12-edd4-4057-8bdf-85db27ec5158.png)

- Sélectionnez `3D printing` :

![rpi-3d-printing](https://user-images.githubusercontent.com/12702322/187550693-8ab015a1-f267-41c0-afbd-0a01717c3198.png)

- Sélectionnez `Mainsail OS` :

![rpi-mainsailos](https://user-images.githubusercontent.com/12702322/187551003-b290bab8-4f2b-4ff7-bf77-7baa79296cf3.png)
![rpi-mainsailos-choosen](https://user-images.githubusercontent.com/12702322/187551046-dcfd049b-3fad-45b3-966d-bc9693e967c1.png)

- Une fois cela fait, cliquez sur `STORAGE` et sélectionnez la carte microSD souhaitée ou l'eMMC (voir la documentation de BigTreeTech page 21 : [ici](https://github.com/bigtreetech/Manta-M4P/blob/master/BIGTREETECH_M4P%26CB1%20User%20Manual.pdf)) :

![rpi-choose-storage](https://user-images.githubusercontent.com/12702322/187551309-86af4395-e9b4-45c7-bae8-964357d6e8c2.png)

- Le nom d'hôte, le SSH, le Wi-Fi, la langue et de nombreux autres paramètres peuvent désormais être parcourus et préconfigurés dans un menu de configuration, en cliquant sur la petite roue dentée dans le coin droit :

![rpi-cogwheel](https://user-images.githubusercontent.com/12702322/187552384-b01a7219-66eb-4906-aab1-c5e61db1a123.png)

- Facultatif : Configurez votre nom d'hôte préféré. Si vous le modifiez, l'URL sera modifiée en conséquence.
Comme indiqué dans la capture d'écran ci-dessous, votre URL sera `http://mainsail.local`

![rpi-setup-ssh](https://user-images.githubusercontent.com/12702322/187552731-a68581d8-d678-4db2-a9fa-0a56085fd505.png)

- Changez votre mot de passe, cette étape est fortement recommandée ! Veuillez ne pas changer le nom d'utilisateur !
À ce stade, la configuration de MainsailOS repose sur l'utilisateur `pi`.

![rpi-setup-username](https://user-images.githubusercontent.com/12702322/187552946-fbdc26c9-d097-497d-be7c-d2ed47d7b00a.png)

- Entrez les informations de votre réseau votre Wi-Fi :

![rpi-setup-wifi](https://user-images.githubusercontent.com/12702322/187553076-6cd4d36d-684a-4655-a16e-47e3517be9ba.png)

- La dernière étape gère votre fuseau horaire et la disposition du clavier (cette dernière peut affecter votre langue dans certains cas) :

![rpi-timezone](https://user-images.githubusercontent.com/12702322/187553285-465ca67b-48b9-404b-aa14-1d1f5b04d82a.png)

- Avec toutes les options souhaitées préconfigurées, cliquez sur `WRITE` et acceptez l'avertissement :

![rpi-write](https://user-images.githubusercontent.com/12702322/187553421-ececfaed-034d-4e11-99c5-7434f152f3f7.png)
![rpi-warning](https://user-images.githubusercontent.com/12702322/187553453-c095f88d-27a2-4ef0-adcb-c7db5a1f481a.png)

- Cela prendra un certain temps pour écrire l'image sur la carte microSD ou l'eMMC. Une fois le transfert terminé, une vérification sera effectuée.

![rpi-writing](https://user-images.githubusercontent.com/12702322/187553852-fae8bc38-a616-430f-a09d-303bf053a891.png)

- Une fois terminé, cliquez sur `CONTINUE` :

![rpi-finished](https://user-images.githubusercontent.com/12702322/187553911-d12384ae-1c1c-4529-9115-da5d283d85cc.png)

- L'installation est maintenant terminée.

<br />

## Connexion via SSH

- Téléchargez et installez le logiciel MobaXterm ici : https://mobaxterm.mobatek.net/download-home-edition.html

- Lancez-le puis cliquez sur l'icône `Session` puis `SSH` : 

![Capture d’écran 2022-08-31 à 00 27 15](https://user-images.githubusercontent.com/12702322/187554613-7c3b7776-2e9e-41cd-a331-9bcb29324e07.jpg)

![Capture d’écran 2022-08-31 à 00 28 03](https://user-images.githubusercontent.com/12702322/187554724-47adc66d-b76a-4351-8d81-c077c41072c2.jpg)

- Renseignez l'adresse IP de votre Raspberry Pi dans le champ `Remote Host`, cochez la case `Specify username` et saisissez le nom d'utilisateur `pi` dans le champ puis cliquez sur `OK` :

![Capture d’écran 2022-08-31 à 00 31 14](https://user-images.githubusercontent.com/12702322/187555264-3c1497d8-b329-46e5-8df4-bd8609678e5c.jpg)

- Sur la fenêtre qui s'affiche, saisissez votre mot de passe précédemment défini dans Raspberry Pi Imager (il ne s'affiche pas à la saisie, c'est normal) : 

![Capture d’écran 2022-08-31 à 00 34 09](https://user-images.githubusercontent.com/12702322/187555380-327b9ae3-29c5-4d81-a595-d754525cc044.jpg)

- Une fenêtre d'autorisation va s'afficher, autorisez-la. Il est également possible qu'une autre fenêtre vous demandant de changer le mot de passe s'affiche, ignorez-là.

- Une fois connecté, sur la partie gauche de la fenêtre vous avez l'accès aux dossiers et fichiers de votre Raspberry Pi et sur la partie droite à la fenêtre d'invite de commande SSH :

![Capture d’écran 2022-08-31 à 00 37 25](https://user-images.githubusercontent.com/12702322/187555942-ff82a7b1-a43e-4c75-9fd8-7a1ccd43fd58.jpg)

<br />

## Installation de Kiauh et de KlipperScreen

- Dans la fenêtre d'invite de commande SSH, saisissez la commande suivante pour installer Kiauh :
```
git clone https://github.com/th33xitus/kiauh.git
```
- Puis saisissez la commande suivante pour lancer Kiauh :
```
./kiauh/kiauh.sh
```
- Saisissez `1` pour sélectionner `Installation` puis `5` pour installer KlipperScreen.

- Une fois l'installation terminée, vous pouvez également mettre le système à jour en saisissant `2` pour sélectionner `Update`.

- Vous pouvez ensuite quitter Kiauh en saisissant `B` puis `Q`.

<br />

## Désactivation du PCI Express sur le CM4

La Manta M4P ne dispose pas de port PCI Express, il est donc nécessaire de désactiver la fonctionnalité pour éviter un message au démarrage.

- Créez le fichier `disable-pcie-overlay.dts` avec la commande suivante : 
```
sudo nano /boot/overlays/disable-pcie-overlay.dts
```
- Copier ce code dans la fenêtre qui s'affiche :
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
```
sudo dtc -@ -I dts -O dtb -o /boot/overlays/disable-pcie-overlay.dtbo /boot/overlays/disable-pcie-overlay.dts
```
- Puis supprimer le fichier `disable-pcie-overlay.dts` avec la commande suivante :
```
sudo rm /boot/overlays/disable-pcie-overlay.dts
```

<br />

## Installation de l'image de démarrage

- Téléchargez ce pack puis dézipez-le : [Pack Boot](https://github.com/Guilouz/Klipper-Flsun-Super-Racer/files/9457081/Boot.Pack.zip)

- Faites glisser les 3 fichiers `initramfs.img`, `splash.txt` et `splash.png` dans la fenêtre de gauche en vous assurant d'être bien dans le répertoire `/home/pi/`.

- Dans la fenêtre d'invite de commande SSH, saisissez la commande suivante :
```
sudo cp /home/pi/splash.png /boot/
```
- Puis celle-ci :
```
sudo cp /home/pi/splash.txt /boot/
```
- Et encore celle-là :
```
sudo cp /home/pi/initramfs.img /boot/
```
- Vous pouvez ensuite supprimer ces 3 fichiers du répertoire `/home/pi/` en faisant un clic-droit sur chacun d'eux puis `Delete`.

<br />

## Installation du driver pour écran DSI & Caméra CSI

- Saisissez la commande suivante : 
```
sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-disp1-cam1.bin -O /boot/dt-blob.bin
```

<br />

## Modification du fichier /boot/cmdline.txt

- Saisissez la commande suivante : 
```
sudo nano /boot/cmdline.txt
```
- Sur la fenêtre qui s'affiche, ajoutez ces éléments à la fin de la ligne :
```
logo.nologo loglevel=0 vt.global_cursor_default=0 splash silent quiet
```
- Puis sur votre clavier appuyez sur les touches `Ctrl+X` pour quitter, `Y` pour sauvegarder et `Entrée` pour valider.

<br />

## Modification du fichier /boot/config.txt

- Saisissez la commande suivante : 
```
sudo nano /boot/config.txt
```
- Sur la fenêtre qui s'affiche, ajoutez ces éléments :
```
## Splashcreen settings
initramfs initramfs.img
dtoverlay=disable-pcie-overlay
disable_splash=1
boot_delay=0

[cm4]
## Enable USB serial
dtoverlay=dwc2,dr_mode=host
```
- Et modifiez également ces lignes déjà présentes :
  - Retirez le "#" devant : disable_overscan=1
  - Ajoutez un "#" devant : #dtoverlay=vc4-fkms-v3d
```
disable_overscan=1
#dtoverlay=vc4-fkms-v3d
```
- Puis sur votre clavier appuyez sur les touches `Ctrl+X` pour quitter, `Y` pour sauvegarder et `Entrée` pour valider.

- Vous pouvez maintenant saisir la commande suivante pour redémarrer le Raspberry Pi :
```
sudo reboot
```

<br />

## Installation du firmware Klipper sur la Manta M4P

- Connectez-vous de nouveau en SSH puis saisissez la commande suivante afin de récupérer le serial USB de la Manta M4P :
```
ls /dev/serial/by-id/
```
- Copier la ligne qui s'affiche (dans un fichier texte par exemple), elle nous sera utile plus tard.

- Saisissez ensuite les commandes suivantes :
```
cd ~/klipper/
```
puis
```
make menuconfig
```
- Sélectionnez ces paramètres :
```
* [*] Enable extra low-level configuration options
* Micro-controller Architecture (STMicroelectronics STM32) --->
* Processor model (STM32G0B1) --->
* Bootloader offset (8KiB bootloader) --->
* Clock Reference (8 MHz crystal) --->
* Communication interface (USB (on PA11/PA12)) --->
```
- Puis sur votre clavier appuyez sur la touche `Q` puis sur `Y` pour sauvegarder la configuration.

- Saisissez la commande suivante pour compiler le firmware :
```
make
```
- Une fois la compilation terminée, vous avez alors deux possibilités :

  - Installation manuelle du firmware :
    - Récupérez le firmware nommé `Klipper.bin` sur la page de gauche dans le répertoire `/home/pi/klipper/out/`.
    - Renommez-le en `firmware.bin`.
    - Copiez-le à la racine d'une carte SD (et non microSD) formatée en FAT32 et une taille d'allocation de 4096.
    - Insérez la carte SD dans la Manta M4P puis allumez l'imprimante.
    - L'installation dure que quelques secondes, pour vérifier que le firmware a bien été installé, le fichier sur la carte SD doit avoir été renommé en `FIRMWARE.CUR`.

  - Installation directe du firmware :
    - Saisissez la commande suivante :
    ```
    make flash FLASH_DEVICE=/dev/serial/by-id/XXXXX (en remplaçant les XXXXX par le serial obtenu précédemment)
    ```
    - Cela doit ressembler à ça :
    ```
    make flash FLASH_DEVICE=/dev/serial/by-id/usb-Klipper_stm32g0b1xx_2F0034001050415833323520-if00
    ```
    - Il y aura un message d'erreur `dfu-util: Error during download get_status` après la mise à jour. N'y prêtez pas attention, le plus important c'est d'obtenir la ligne `File downloaded successfully`.

- Vous pouvez ensuite accéder à l'interface Web de Mainsail via votre navigateur en saisissant l'adresse IP de votre Raspberry Pi ou l'URL  `http://mainsail.local`.

- Rendez-vous dans l'onglet `Machine` puis importez les fichiers `printer.cfg`, `neopixels.cfg`, `macros.cfg` et `adxl345.cfg`.

- Une fois importés, ouvrez le fichier `printer.cfg` et modifiez la ligne suivante dans la section `Paramètres MCU` :
```
serial: /dev/serial/by-id/XXXXX (en remplaçant les XXXXX par le serial obtenu précédemment)
```
- Après sauvegarde et redémarrage du firmware, vous devriez voir le MCU de la Manta M4P se connecter à Klipper.

<br />

## Configuration pour l'ADXL345

- Connectez-vous de nouveau en SSH puis saisissez les commandes suivantes (une à la fois) :
```
cd ~/klipper/
sudo cp "./scripts/klipper-mcu-start.sh" /etc/init.d/klipper_mcu
sudo update-rc.d klipper_mcu defaults
```
- Il faut ensuite compiler le code du microcontrôleur en saisissant ces commandes (une à la fois) :
```
cd ~/klipper/
make menuconfig
```
- Sur le menu, définissez `Microcontroller Architecture` sur `Linux process`, puis sur votre clavier appuyez sur la touche `Q` puis sur `Y` pour sauvegarder la configuration.

- Pour compiler et installer le microcontrôleur, saisissez les commandes suivantes (une à la fois) :
```
sudo service klipper stop
make flash
sudo service klipper start
```
- Il faut ensuite installer les dépendances nécessaires en saisissant ces commandes (une à la fois) :
```
sudo apt update
sudo apt install python3-numpy python3-matplotlib libatlas-base-dev
```
- Suivi de cette commande pour installer Numpy dans l'environnement de Klipper :
```
~/klippy-env/bin/pip install -v numpy
```
- Il suffit ensuite dé-commenter (retirer le #) la ligne suivante dans le fichier `printer.cfg` pour activer le support de l'ADXL :
```
#[include adxl345.cfg]
```
- Après sauvegarde et redémarrage du firmware vous devriez voir le MCU de l'ADXL se cnnecter à Klipper.
