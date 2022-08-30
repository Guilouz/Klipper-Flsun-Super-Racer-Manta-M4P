# Klipper Configuration for FLSUN Super Racer

![maxresdefault](https://user-images.githubusercontent.com/12702322/187098254-be0a0182-cc04-401a-9e95-97dda4bdb1b6.jpeg)

Klipper est un firmware d'imprimante 3D. Il combine la puissance d'un ordinateur à usage général avec un ou plusieurs microcontrôleurs.

Consultez le [document sur les fonctionnalités](https://www.klipper3d.org/Features.html) pour plus d'informations sur les raisons pour lesquelles vous devriez utiliser Klipper.


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


## Installation de Kiauh et de KlipperScreen
