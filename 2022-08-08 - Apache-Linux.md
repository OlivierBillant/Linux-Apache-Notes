# Apache et Linux

## Linux

### Historique

Basé sur Multics entre 1965 et 1969 (Bell Lab) puis réécriture du projet en C dans les années 1970. Premier noyau dans les années 1991. Première distributions en 1995-1996.

**Distribution** : ensemble cohérente de logiciel assemblé autour du noyau linux.

Logiciel libre implique la possibilité de :

- exécuter le logiciel
- étudier son fonctionnement
- distribuer une version modifiée.

Commande :

- passwd pour modifier le mot de pw.
- man pour le manuel. basé sur vi permet avec esc / de lancer une recherche.

Le FHS (FileSsytemHierarchy standart) permet d'unifier l'arborescence de fichiers sous linux et est maintenu par la LF.
La **racine** sera toujours notée "/" .

- /bin : fichiers systeme
- /boot : lancemenbt du noyau
- /etc : installation des softs.
- /lib : libraries
- /media et /mnt : volumes externes montables
- /opt : applications tierces
- /usr :
- /var :
- /dev : partitions
- /proc : processus

Sous Unix, tout est fichier. Types de fichiers : standarts, repertoires, liens symboliques et fichiers spéciaux (_e.g._ cachés...).

```
Pas de notion d'extension de fichier.
Le seul caractère interdit est le "/" !
Linux est sensible à la casse.
```

Notion de chemin absolu vs. relatif.

pwd : print working directory, affiche le chemin de l'endroit.  
cd : choose directory
cd (seul) : amène à la racine de l'utilisateur.
ls : lister les fichiers. (-l)

ip a : puor accéder à l'adresse ip de la machine.

touch : creation de fichier
nana ou vi + nom de fichier : editeur de texte
cat : imprime le contenu du fichier.

### Configuration ssh

```bash
su -
cd /etc/ssh
nano sshd_config
```

Par défautl le permit root login est prohibé.

On modifie le port de connexion puis on relance le service avec :

```bash
/etc/init.d/ssh restart
ssh user@ipadress -p port
```

Installation en distance de Apache, php, getKirby, Symfony, Laravel.

```bash
su
apt install apache2

```

Test d'apache : ip dans le navigateur doit donner la page d'accueil d'apache2.  
L'activation des modules permettra d'utiliser par exemple plusieurs versions de php en parrallèle.  
On accède au fichier index.html dans

```bash
/var/www/
```

On pourra ensuite :

- Créer un utilisateur
- Y créer un dossier www
- Intégrer une page html de test.

Avant il faudra autoriser apache à accéder à des pages localisées dans d'autres dossiers.

```bash
nano /etc/apache2/apache2.conf
<Directory /home/>
AllowOverride All
```

On va ensuite créer un utilisateur avec

```bash
su -
adduser site1
```

Créer un dossier www in home/site1/
Créer un fichier index.html dans /site1

Puis créer les virtual hosts :

```bash
su -
cd /etc/apache2/sites-available/
```

Copie de sauvegarde de la configuration par défault:

```bash
cp 000-default.conf 000-default.conf.save
```

Créer une copie pour le site 1 :

```bash
cp 000-default.conf site1.fr.conf
```

Modifier le fichier ligne 9 :

```bash
ServerNanem site1.fr
ServerAlias www.site1.fr

DocumentRoot /home/site1/www

ErrorLog ${APACHE_LOG_DIR}/site1.fr_error.log
CustomLog ${APACHE_LOG_DIR}/site1.fr_access.log combined
```

Activer les virtualhosts

```bash
a2ensite site1.fr.conf
systemctl reload apache2
systemctl status apache2
```

Installer un navigateur en ligne de commande :

```bash
apt install lynx
```

Modifier les hosts windows :

- Ouvrir le bloc note win en adminsitrateur
- Fichier Ouvrir /windows/system32/drivers/etc
- Afficher tous fichiers => hosts

On ajoute dans le fichier :

```
#site de test
10.170.200.36 site1.fr www.site1.fr
```

```bash

```

## CREATION DE L'UTILISATEUR

1. On crée un utilisateur (nom du site)
   on se met en root (su -) puis on fait adduser (ou useradd) pour créer l'utilisateur

## RECUPERATION D'UN TEMPLATE

2. On se connecte sur cet utilisateur  
   On crée un dossier www/ ou public/ ou se que vous voulez (le nom du projet par exemple)  
   On telecharge sur internet un site de template en HTML

3. Pour telecharger le template sur mon serveur
   Il va falloir utiliser wget

   ```html
   apt install wget (si il n'est pas installé)
   ```

   Pour utiliser la commande wget:

   ```html
   wget url-de-mon-lien.zip
   ```

4. decompresser le .zip

   ```html
   unzip nom-du-fichier.zip
   ```

   ```html
   apt install unzip (si il n'est pas installé)
   ```

5. une fois decompresser il faut soit:  
   renommer le dossier en www/  
   ou  
   deplacer les fichiers dans votre www/

   <br>

## CONFIGURATION DU VIRTUALHOST

6.  Copier un virtual host et renommer le fichier

    ```bash
    cd /etc/apache2/sites-available
    ```

    Exemple:

    ```bash
    cp site1.fr.conf mon-super-site.com.conf
    ```

7.  Modifier le virtualhost  
    ServerName mon-super-site.com  
    ServerAlias www.mon-super-site.com

    ```bash
    Documentroot Chemin/test/www/
    ```

    Modifier les noms des 2 logs

8.  Activer le virtualhost

    ```bash
    a2ensite nom-du-virtual-host.conf
    ```

9.  Redemarrer apache2

10. configurer le HOST  
    si dns interne on va dans
    ```bash
    C:/Windows/System32/Drivers/etc/ hosts
    ```

```bash
apt install php
```

Télécharger getkirby starterkit, le renommer en wwww dans le user getkirby.  
Créer le dossier media.  
Modifier les droits d'écriture :

```bash
chmod -R 777 media/
```
