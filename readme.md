# unplasticomenos.com

Generated with https://github.com/dokku-community/dokku-wordpress.

# Update Wordpress

```sh
git remote add wordpress git@github.com:WordPress/WordPress.git
git fetch --tags wordpress

git checkout -b master-old

git checkout 5.7

git checkout master-old composer.json
git checkout master-old composer.lock
git checkout master-old readme.md
git checkout master-old wp-config.php
git checkout master-old .buildpacks
git checkout master-old nginx.conf
git checkout master-old php.ini


git branch -D master
git checkout -b master

git commit -m "Update Wordpress to 5.7"

git push dokku master --force
git push origin master --force
```

# Initial generated installation instructions:

```sh
# adding wp-config.php from gist
# adding .env file to configure buildpack
# ensuring our composer.json loads with php 5.6 and loads the mysql extension
# setting the correct dokku remote for your app and server combination
# retrieving potential salts and writing them to /tmp/wp-salts
# run the following commands on the server to setup the app:

dokku apps:create unplasticomenos

# setup plugins persistent storage

mkdir -p /var/lib/dokku/data/storage/unplasticomenos-plugins
chown 32767:32767 /var/lib/dokku/data/storage/unplasticomenos-plugins
dokku storage:mount unplasticomenos /var/lib/dokku/data/storage/unplasticomenos-plugins:/app/wp-content/plugins

# setup upload persistent storage

mkdir -p /var/lib/dokku/data/storage/unplasticomenos-uploads
chown 32767:32767 /var/lib/dokku/data/storage/unplasticomenos-uploads
dokku storage:mount unplasticomenos /var/lib/dokku/data/storage/unplasticomenos-uploads:/app/wp-content/uploads

# setup languages persistent storage

mkdir -p /var/lib/dokku/data/storage/unplasticomenos-languages
chown 32767:32767 /var/lib/dokku/data/storage/unplasticomenos-languages
dokku storage:mount unplasticomenos /var/lib/dokku/data/storage/unplasticomenos-languages:/app/wp-content/languages

# setup persistent themes

mkdir -p /var/lib/dokku/data/storage/unplasticomenos-themes
chown 32767:32767 /var/lib/dokku/data/storage/unplasticomenos-themes
dokku storage:mount unplasticomenos /var/lib/dokku/data/storage/unplasticomenos-themes:/app/wp-content/themes

# setup your mysql database and link it to your app
# if you're using MariaDB, replace mysql with mariadb

export MYSQL_IMAGE_VERSION="5.6"
dokku mysql:create unplasticomenos_database
dokku mysql:link unplasticomenos_database unplasticomenos

# you will also need to set the proper environment variables for keys and salts
# the following were generated using the wordpress salt api: https://api.wordpress.org/secret-key/1.1/salt/
# and use the following commands to set them up:

dokku config:set unplasticomenos AUTH_KEY='{ZR$A~Nt0X/-Qkam7twmK:3,Fhdw`Kta.+V^AEtZ,.l-(f}RK^)/?/-Cb_+bQ0kD'
dokku config:set unplasticomenos SECURE_AUTH_KEY='TJAe%fo=:+z1w%a]vlb#Il[jYRqH&zanjO7?j_,Qz^^!q}wLuuQOaXW[i-iGI9'
dokku config:set unplasticomenos LOGGED_IN_KEY='{2=KRJ(d^[zb^X-+USsJS]TK|`S`cfKr.a}j/E)e(aaV?J)~,2*|N`yuNK(4$'
dokku config:set unplasticomenos NONCE_KEY='0~_&x~EklHTN}F9c]VrY?=;[I>W:p9x-P*AN-|C=NO%#0Mhq7N_O|XY8}Fw{%qIT'
dokku config:set unplasticomenos AUTH_SALT='Zo>gQr:!+/Mxm^Tv9UnPrfcPCilas07IK}eSKXMw9Yb1-CSrQN+-op=6e9J0:p+'
dokku config:set unplasticomenos SECURE_AUTH_SALT='o>rZm,~{#H8h,d,o:|s-pR!v-%-3-^q@?9TnC+Z8EE^*)=Kda4(,>(jN>-AmMiF'
dokku config:set unplasticomenos LOGGED_IN_SALT='ETD]iabG{$CXj|`_it[Zq--RGD#,=znxF<+yOzH#Rmk-:3/9g!QwAo%GUHM=FJ['
dokku config:set unplasticomenos NONCE_SALT='EY)O/2[Cnzj3vNH.dWzZDbRgfG{Mu-HuT%EH-C-UzV?S_r|-!jZwjd1kF32+xV'

# Set max amount of processes to 4
dokku config:set unplasticomenos WEB_CONCURRENCY=4

# now, on your local machine, change directory to your new wordpress app, and push it up

cd unplasticomenos.com
git push dokku master
```

other initial setup:

```

```
