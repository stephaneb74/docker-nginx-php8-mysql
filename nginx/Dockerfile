FROM nginx:1.24-alpine3.17

###
# Mise à jour de l'environnement Alpine.
###
RUN apk update

###
# Installation de paquets supplémentaires.
###
RUN apk --no-cache add nano \
    busybox-extras \
    curl \
    wget

WORKDIR /etc/nginx
COPY conf/nginx.conf .
COPY conf/phpmyadmin.conf .
COPY conf/default.conf .

###
# Défini le répertoire /etc/nginx/conf.d comme répertoire courant.
###
WORKDIR /etc/nginx/conf.d

###
# Copie des fichiers de configuration des hôtes virtuels.
###
COPY ./conf.d/*.conf ./

###
# Copie les certificats SSL.
###
WORKDIR /etc/ssl/certs
COPY ./ssl/*.crt ./

WORKDIR /etc/ssl/private
COPY ./ssl/*.key ./

###
# Changement du répertoire en cours pour /etc/ssl/private
###
WORKDIR /etc/ssl/private

###
# Copie de la clé privé et des certificats SSL.
###
COPY ./ssl/private.key /
COPY ./ssl/*.crt /

###
# Expose les ports 80 et 443 aux autres conteneurs Docker.
###
EXPOSE 80
EXPOSE 443
