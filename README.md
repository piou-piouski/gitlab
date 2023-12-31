# gitlab
- Formateur : thomas Saquet (thomas@solution-libre.fr)  
- Chaine youtube : Qu'est-ce que tu GEEKes ?
- GitHub : https://github.com/tsaquet/gitlab  
- Outil : bisect  
- https://git.goffinet.org/  
- GitLab peut servir de registry pour Docker  
- Reset password : gitlab-rake "gitlab:password:reset[root]"
- echo $?  
- terraform => opentofu (fork de terraform)
- Template de .gitlab-ci.yml : https://gitlab.com/gitlab-org/gitlab-foss/-/tree/master/lib/gitlab/ci/templates

# docker
- Lance un docker : docker run hello-world  
- Options du run : -i pour connecter le clavier et -t pour ouvrir un terminal  
- Lister les containers : docker ps  
- Quitter un container : exit ou ctrl+d
- Stopper un service : gitlab-ctl stop nginx
- Vérifier l'état d'un service : gitlab-ctl status  
- Démarrer un service : gitlab-ctl start nginx  
- Redémarrer l'ensemble des services : gitlab-ctl restart

## Logs
- Permet d'ouvrir un shell dans un container : docker exec -it idContainer bash  
- Permet de lister les process avec leurs status : gitlab-ctl status

### Logs de gitlab
- docker inspect idContainer  
- cd /srv/gitlab/logs  
- cd nginx/  
- gitlab-access.log  
- gitlab-error.log

## API
- Lien vers la doc API : https://docs.gitlab.com/ee/api/rest/  
- Liste les projets, le |jq permet de mettre en forme le retour json : curl --header "Authorization: Bearer glpat-5-xW5WL3HpDUL7Jw938e" "http://localhost/api/v4/projects" | jq  
- Liste les groups : curl --header "Authorization: Bearer glpat-5-xW5WL3HpDUL7Jw938e" "http://localhost/api/v4/groups" | jq  
- Ajout d'un groupe : curl --request POST --header "Authorization: Bearer glpat-5-xW5WL3HpDUL7Jw938e" --header "Content-Type: application/json" --data '{"path":"mon-groupe", "name":"Mon-Groupe"}' "http://localhost/api/v4/groups"

## Backup
- Lien vers la doc backup : https://docs.gitlab.com/omnibus/settings/backups.html
- Lien vers la doc backup : https://docs.gitlab.com/ee/administration/backup_restore/  
- Permet de générer un backup du container : docker exec -t idContainer gitlab-backup  
- Permet de restore un backup : docker exec -t idContainer gitlab-backup restore

## Runner
- Lien vers la doc : https://docs.gitlab.com/runner/install/linux-repository.html
- curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.rpm.sh" | sudo bash
- sudo yum install gitlab-runner
- lister les runners : sudo nano /etc/gitlab-runner/config.toml  
- Depuis le gitLab -> CI/CD -> Runners  

## DockerFile
- nano Dockerfile  
FROM alpine  

CMD ["echo", "Hello World"]  
- Permet de construire une image du nom 'hello' avec le contenu du répertoire courant '.' : docker build -t hello .  
- Permet de lister les images docker : docker images  
- Permet de lancer une image 'hello' version 1, de la run : docker run hello:V1
- Permet de push une image docker vers le registry sur gitlab : docker push hello  

## Install gitlab runner in the docker
- Doc : https://docs.gitlab.com/runner/install/docker.html#option-1-use-local-system-volume-mounts-to-start-the-runner-container \
- docker run -d --name gitlab-runner --restart always \
  -v /srv/gitlab-runner/config:/etc/gitlab-runner \
  -v /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest \
- docker exec -it gitlab-runner bash \
- gitlab-runner register \


## Install nginx
- docker pull nginx \

## Créer une image nginx
- nano imageDocker/nginx/Dockerfile  
- FROM nginx  
  COPY static-html-directory /usr/share/nginx/html
- cd imageDocker/nginx/Dockerfile  
- docker build -t nginx .  
