# gitlab

- Formateur : thomas Saquet (thomas@solution-libre.fr)  
- Chaine youtube : Qu'est-ce que tu GEEKes ?  
- Outil : bisect  
- https://git.goffinet.org/  
- GitLab peut servir de registry pour Docker

# docker

- Lance un docker : docker run hello-world  
- Options du run : -i pour connecter le clavier et -t pour ouvrir un terminal  
- Lister les containers : docker ps  
- Quitter un container : exit ou ctrl+d
- Stopper un service : gitlab-ctl stop nginx
- Vérifier l'état d'un service : gitlab-ctl status  
- Démarrer un service : gitlab-ctl start nginx  
- Redémarrer l'ensemble des services : gitlab-ctl restart

## Backup
- Lien vers la doc backup : https://docs.gitlab.com/omnibus/settings/backups.html  
- Permet de générer un backup du container : docker exec -t idContainer gitlab-backup  
- Permet d'ajouter les fichiers secret : docker exec -t idContainer /bin/sh -c 'gitlab-ctl backup-etc && cd /etc/gitlab/config_backup && cp $(ls -t | head -n1) /secret/gitlab/backups/'

## Logs
- Permet d'ouvrir un shell dans un container : docker exec -it idContainer bash  
- Permet de lister les process avec leurs status : gitlab-ctl status

### Logs de gitlab
- docker inspect idContainer  
- cd /srv/gitlab/logs  
- cd nginx/  
- gitlab-access.log  
- gitlab-error.log

