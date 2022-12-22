<p align="center">
  <img height="200" src="t4face.jpg" alt="Twyn">
</p>

<p align="center">
    <b>Your digital Identity</b>
</p>

<p align=center>
    <a href="./docs/license/LICENSE.txt"><img src="https://img.shields.io/badge/License-Apache%202.0-success" alt="Apache 2.0 License"></a>
    <a href="./docs/roadmap/README.md"><img src="https://img.shields.io/badge/Roadmap-v1.0-bc1439.svg" alt="Roadmap v1.0"></a>
</p>

## T4-Face

T4-Face Docker Version is the [T4ISB](https://www.t4isb.com) Face engine that allows authentication, identification and image comparision.

Our aim is to protect the user identity and give him the total control of his biometric data and SSI identity.

### Self Sovereign Identity (SSI)

As defined by [WIKIPEDIA](https://en.wikipedia.org/wiki/Self-sovereign_identity), SSI is an approach to digital identity that gives individuals control of their digital identities. We want to help people protect their data and their identity.

### Install Docker
To run our T4-Face Dokcer version you need to install the following :<br/>
1. **Docker Engine**: Docker CE is a free and open-source version available for users. 
2. **Docker Compose**: Docker Compose is a utility that permits you to run multi-container application setups based on YAML definitions

Below an example of how to install Docker CE on ubutnu
```
snap remove docker
rm -R /var/lib/docker
sudo apt-get remove docker docker-engine docker.io

sudo apt update
sudo apt upgrade
sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
apt-cache policy docker-ce
sudo apt install docker-ce
sudo systemctl status docker
```
Once the Docker engine is intalled, all you need is to create a docker-compose.yml file:

```
version: '3.4'
services:
 t4face:
   container_name: t4face-server-docker
   image: t4isb/t4face:t4face-server-v1.4.7
   ports:
     - 8004:8004
   environment:
     - PORT=8004
   depends_on:
     - mysql-db
     - index-server
   restart: always
   expose:
      - 8004
    
 mysql-db:
   container_name: frs_db_server
   image: t4isb/t4face:mysql-frs-db
   ports:
     - 3306:3306
   environment:
     - MYSQL_ROOT_PASSWORD=<Password>
     - MYSQL_DATABASE=<database>
 index-server:
   container_name: index-server
   image: t4isb/t4face:index-grpc-server-V1.0.2
   command: 'server.py --dim 512 --save_path "/data/" --debug true --log logs/index-server.log'
   ports:
       - 50051:50051
   volumes:
       - ./data:/data
    
```

To run our T4-Face engine, just run the follwoing command:

```
docker-compose -f docker-compose.yml up [-d to run in background]
```
This command will pull t4isb/t4face:t4face-server-v1.4.7, t4isb/t4face:mysql-frs-db and t4isb/t4face:index-grpc-server-V1.0.2 docker images and launch the containers. Our images are private and you need to get a username/password to be able to pull them.

Please contact our support to get your user/password.


### Support or Contact

Having trouble ?  [contact support](https://www.t4isb.com) and we’ll help you sort it out.


## Contributors ✨

Thanks to the people who contributed to T4-Face Docker Version:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/nizarelouaer"><img src="https://avatars.githubusercontent.com/u/57862776?v=4" width="50px;" alt=""/><br /><sub><b>Nizar Elouaer</b></sub></a><br /><a href="https://github.com/nizarelouaer/t4-face/commits?author=nizarelouaer" title="Code">💻</a></td>
    
  <tr>
   
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

## License

T4-Face Docker is licensed under the Apache License, Version 2.0. View a copy of the [License file](LICENSE).
