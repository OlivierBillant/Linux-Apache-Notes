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
/var/www/html/
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
cd /etc/apache2/site-available
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
