# Machine Virtuelles

Le NAS Production accueille différentes machines virtuelles via "Virtual Machine Manager"

## Machines Windows

Deux machines virtuelles WIN 10 sont utilisées et hébergées sur le NAS Production, sur le Volume 2 avec SSD

### TECH
### PLAYLIST

## Machines Linux

### UBUNTU AUTOMATOR 

Une machine virtuelle dédiée aux automatisations : 

- mise à jour des horodatages des titres pour remonter 2 nouveaux titres en playlist par nuit // TODO
- mise à jour de la base de données musicales avec les playlists musicales toutes les nuits
    - le script https://github.com/scaphandroid/vostok-auto-playlist est exécuté toutes les nuits à 1h
    - et à 3h le dossier de ce script est copié vers le dossier de la playlist (en écrasant les fichiers déjà existants)
    - détail des cronjob : 
    ```
    0 1 * * * /home/vostok_admin/ANTENNE/vostok-auto-playlist/vostok-auto-playlist
    0 3 * * * cp -r -f /home/vostok_admin/ANTENNE/vostok-auto-playlist/* /home/vostok_admin/ANTENNE/DATABASE/MUSIQUE\ DB/
    ```
