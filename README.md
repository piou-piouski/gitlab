# gitlab

Formateur : thomas Saquet (thomas@solution-libre.fr)

Chaine youtube : Qu'est-ce que tu GEEKes ?

Outil : bisect

https://git.goffinet.org/

GitLab peut servir de registry pour Docker

# docker

Lance un docker : docker run hello-world 

Options du run : -i pour connecter le clavier et -t pour ouvrir un terminal

Permet d'ouvrir un shell dans un container : docker exec -it idContainer sh

Permet de lister les 10 derniers log du container : docker logs --teil 10 idContainer

## Backup
Lien vers la doc backup : https://docs.gitlab.com/omnibus/settings/backups.html

Permet de générer un backup du container : docker exec -t idContainer gitlab-backup

Permet d'ajouter les fichiers secret : docker exec -t idContainer /bin/sh -c 'gitlab-ctl backup-etc && cd /etc/gitlab/config_backup && cp $(ls -t | head -n1) /secret/gitlab/backups/'
