https://docs.docker.com/install/linux/docker-ce/centos/#install-using-the-repository

fintecheando@localhost ~]$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
[sudo] password for fintecheando: 
Complementos cargados:fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.cenac.ipn.mx
 * extras: mirror.cenac.ipn.mx
 * updates: mirror.cenac.ipn.mx
El paquete device-mapper-persistent-data-0.7.0-0.1.rc6.el7_4.1.x86_64 ya se encuentra instalado con su versión más reciente
El paquete 7:lvm2-2.02.171-8.el7.x86_64 ya se encuentra instalado con su versión más reciente
Resolviendo dependencias
--> Ejecutando prueba de transacción
---> Paquete yum-utils.noarch 0:1.1.31-42.el7 debe ser instalado
--> Procesando dependencias: python-kitchen para el paquete: yum-utils-1.1.31-42.el7.noarch
--> Procesando dependencias: libxml2-python para el paquete: yum-utils-1.1.31-42.el7.noarch
--> Ejecutando prueba de transacción
---> Paquete libxml2-python.x86_64 0:2.9.1-6.el7_2.3 debe ser instalado
---> Paquete python-kitchen.noarch 0:1.1.1-5.el7 debe ser instalado
--> Procesando dependencias: python-chardet para el paquete: python-kitchen-1.1.1-5.el7.noarch
--> Ejecutando prueba de transacción
---> Paquete python-chardet.noarch 0:2.2.1-1.el7_1 debe ser instalado
--> Resolución de dependencias finalizada

Dependencias resueltas

======================================================================================================================
 Package                         Arquitectura            Versión                          Repositorio           Tamaño
======================================================================================================================
Instalando:
 yum-utils                       noarch                  1.1.31-42.el7                    base                  117 k
Instalando para las dependencias:
 libxml2-python                  x86_64                  2.9.1-6.el7_2.3                  base                  247 k
 python-chardet                  noarch                  2.2.1-1.el7_1                    base                  227 k
 python-kitchen                  noarch                  1.1.1-5.el7                      base                  267 k

Resumen de la transacción
======================================================================================================================
Instalar  1 Paquete (+3 Paquetes dependientes)

Tamaño total de la descarga: 857 k
Tamaño instalado: 4.3 M
Downloading packages:
(1/4): yum-utils-1.1.31-42.el7.noarch.rpm                                                      | 117 kB  00:00:00     
(2/4): libxml2-python-2.9.1-6.el7_2.3.x86_64.rpm                                               | 247 kB  00:00:00     
(3/4): python-chardet-2.2.1-1.el7_1.noarch.rpm                                                 | 227 kB  00:00:00     
(4/4): python-kitchen-1.1.1-5.el7.noarch.rpm                                                   | 267 kB  00:00:01     
----------------------------------------------------------------------------------------------------------------------
Total                                                                                 654 kB/s | 857 kB  00:00:01     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Instalando    : python-chardet-2.2.1-1.el7_1.noarch                                                             1/4 
  Instalando    : python-kitchen-1.1.1-5.el7.noarch                                                               2/4 
  Instalando    : libxml2-python-2.9.1-6.el7_2.3.x86_64                                                           3/4 
  Instalando    : yum-utils-1.1.31-42.el7.noarch                                                                  4/4 
  Comprobando   : libxml2-python-2.9.1-6.el7_2.3.x86_64                                                           1/4 
  Comprobando   : yum-utils-1.1.31-42.el7.noarch                                                                  2/4 
  Comprobando   : python-kitchen-1.1.1-5.el7.noarch                                                               3/4 
  Comprobando   : python-chardet-2.2.1-1.el7_1.noarch                                                             4/4 

Instalado:
  yum-utils.noarch 0:1.1.31-42.el7                                                                                    

Dependencia(s) instalada(s):
  libxml2-python.x86_64 0:2.9.1-6.el7_2.3  python-chardet.noarch 0:2.2.1-1.el7_1  python-kitchen.noarch 0:1.1.1-5.el7 

¡Listo!
[fintecheando@localhost ~]$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
Complementos cargados:fastestmirror
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
[fintecheando@localhost ~]$ sudo yum install docker-ce
Complementos cargados:fastestmirror
docker-ce-stable                                                                               | 2.9 kB  00:00:00     
docker-ce-stable/x86_64/primary_db                                                             |  11 kB  00:00:00     
Loading mirror speeds from cached hostfile
 * base: mirror.cenac.ipn.mx
 * extras: mirror.cenac.ipn.mx
 * updates: mirror.cenac.ipn.mx
Resolviendo dependencias
--> Ejecutando prueba de transacción
---> Paquete docker-ce.x86_64 0:17.12.0.ce-1.el7.centos debe ser instalado
--> Procesando dependencias: container-selinux >= 2.9 para el paquete: docker-ce-17.12.0.ce-1.el7.centos.x86_64
--> Procesando dependencias: libcgroup para el paquete: docker-ce-17.12.0.ce-1.el7.centos.x86_64
--> Ejecutando prueba de transacción
---> Paquete container-selinux.noarch 2:2.36-1.gitff95335.el7 debe ser instalado
--> Procesando dependencias: policycoreutils-python para el paquete: 2:container-selinux-2.36-1.gitff95335.el7.noarch
---> Paquete libcgroup.x86_64 0:0.41-13.el7 debe ser instalado
--> Ejecutando prueba de transacción
---> Paquete policycoreutils-python.x86_64 0:2.5-17.1.el7 debe ser instalado
--> Procesando dependencias: setools-libs >= 3.3.8-1 para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libsemanage-python >= 2.5-5 para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: audit-libs-python >= 2.1.3-4 para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: python-IPy para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libqpol.so.1(VERS_1.4)(64bit) para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libqpol.so.1(VERS_1.2)(64bit) para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libapol.so.4(VERS_4.0)(64bit) para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: checkpolicy para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libqpol.so.1()(64bit) para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Procesando dependencias: libapol.so.4()(64bit) para el paquete: policycoreutils-python-2.5-17.1.el7.x86_64
--> Ejecutando prueba de transacción
---> Paquete audit-libs-python.x86_64 0:2.7.6-3.el7 debe ser instalado
---> Paquete checkpolicy.x86_64 0:2.5-4.el7 debe ser instalado
---> Paquete libsemanage-python.x86_64 0:2.5-8.el7 debe ser instalado
---> Paquete python-IPy.noarch 0:0.75-6.el7 debe ser instalado
---> Paquete setools-libs.x86_64 0:3.3.8-1.1.el7 debe ser instalado
--> Resolución de dependencias finalizada

Dependencias resueltas

======================================================================================================================
 Package                          Arquitectura     Versión                           Repositorio                Tamaño
======================================================================================================================
Instalando:
 docker-ce                        x86_64           17.12.0.ce-1.el7.centos           docker-ce-stable            30 M
Instalando para las dependencias:
 audit-libs-python                x86_64           2.7.6-3.el7                       base                        73 k
 checkpolicy                      x86_64           2.5-4.el7                         base                       290 k
 container-selinux                noarch           2:2.36-1.gitff95335.el7           extras                      31 k
 libcgroup                        x86_64           0.41-13.el7                       base                        65 k
 libsemanage-python               x86_64           2.5-8.el7                         base                       104 k
 policycoreutils-python           x86_64           2.5-17.1.el7                      base                       446 k
 python-IPy                       noarch           0.75-6.el7                        base                        32 k
 setools-libs                     x86_64           3.3.8-1.1.el7                     base                       612 k

Resumen de la transacción
======================================================================================================================
Instalar  1 Paquete (+8 Paquetes dependientes)

Tamaño total de la descarga: 32 M
Tamaño instalado: 128 M
Is this ok [y/d/N]: y
Downloading packages:
(1/9): audit-libs-python-2.7.6-3.el7.x86_64.rpm                                                |  73 kB  00:00:00     
(2/9): libsemanage-python-2.5-8.el7.x86_64.rpm                                                 | 104 kB  00:00:00     
(3/9): container-selinux-2.36-1.gitff95335.el7.noarch.rpm                                      |  31 kB  00:00:00     
(4/9): checkpolicy-2.5-4.el7.x86_64.rpm                                                        | 290 kB  00:00:00     
(5/9): python-IPy-0.75-6.el7.noarch.rpm                                                        |  32 kB  00:00:00     
(6/9): libcgroup-0.41-13.el7.x86_64.rpm                                                        |  65 kB  00:00:00     
(7/9): policycoreutils-python-2.5-17.1.el7.x86_64.rpm                                          | 446 kB  00:00:00     
(8/9): setools-libs-3.3.8-1.1.el7.x86_64.rpm                                                   | 612 kB  00:00:08     
warning: /var/cache/yum/x86_64/7/docker-ce-stable/packages/docker-ce-17.12.0.ce-1.el7.centos.x86_64.rpm: Header V4 RSA/SHA512 Signature, key ID 621e9f35: NOKEY
No se ha instalado la llave pública de docker-ce-17.12.0.ce-1.el7.centos.x86_64.rpm 
(9/9): docker-ce-17.12.0.ce-1.el7.centos.x86_64.rpm                                            |  30 MB  00:00:26     
----------------------------------------------------------------------------------------------------------------------
Total                                                                                 1.2 MB/s |  32 MB  00:00:26     
Obteniendo clave desde https://download.docker.com/linux/centos/gpg
Importando llave GPG 0x621E9F35:
 Usuarioid  : "Docker Release (CE rpm) <docker@docker.com>"
 Huella       : 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 Desde      : https://download.docker.com/linux/centos/gpg
Está de acuerdo [s/N]:s
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Instalando    : libcgroup-0.41-13.el7.x86_64                                                                    1/9 
  Instalando    : setools-libs-3.3.8-1.1.el7.x86_64                                                               2/9 
  Instalando    : checkpolicy-2.5-4.el7.x86_64                                                                    3/9 
  Instalando    : python-IPy-0.75-6.el7.noarch                                                                    4/9 
  Instalando    : audit-libs-python-2.7.6-3.el7.x86_64                                                            5/9 
  Instalando    : libsemanage-python-2.5-8.el7.x86_64                                                             6/9 
  Instalando    : policycoreutils-python-2.5-17.1.el7.x86_64                                                      7/9 
  Instalando    : 2:container-selinux-2.36-1.gitff95335.el7.noarch                                                8/9 
  Instalando    : docker-ce-17.12.0.ce-1.el7.centos.x86_64                                                        9/9 
  Comprobando   : libsemanage-python-2.5-8.el7.x86_64                                                             1/9 
  Comprobando   : audit-libs-python-2.7.6-3.el7.x86_64                                                            2/9 
  Comprobando   : python-IPy-0.75-6.el7.noarch                                                                    3/9 
  Comprobando   : policycoreutils-python-2.5-17.1.el7.x86_64                                                      4/9 
  Comprobando   : libcgroup-0.41-13.el7.x86_64                                                                    5/9 
  Comprobando   : docker-ce-17.12.0.ce-1.el7.centos.x86_64                                                        6/9 
  Comprobando   : checkpolicy-2.5-4.el7.x86_64                                                                    7/9 
  Comprobando   : 2:container-selinux-2.36-1.gitff95335.el7.noarch                                                8/9 
  Comprobando   : setools-libs-3.3.8-1.1.el7.x86_64                                                               9/9 

Instalado:
  docker-ce.x86_64 0:17.12.0.ce-1.el7.centos                                                                          

Dependencia(s) instalada(s):
  audit-libs-python.x86_64 0:2.7.6-3.el7                      checkpolicy.x86_64 0:2.5-4.el7                         
  container-selinux.noarch 2:2.36-1.gitff95335.el7            libcgroup.x86_64 0:0.41-13.el7                         
  libsemanage-python.x86_64 0:2.5-8.el7                       policycoreutils-python.x86_64 0:2.5-17.1.el7           
  python-IPy.noarch 0:0.75-6.el7                              setools-libs.x86_64 0:3.3.8-1.1.el7                    

¡Listo!
[fintecheando@localhost ~]$ sudo systemctl start docker
[fintecheando@localhost ~]$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
ca4f61b1923c: Pull complete 
Digest: sha256:083de497cff944f969d8499ab94f07134c50bcf5e6b9559b27182d3fa80ce3f7
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
 
[fintecheando@localhost ~]$ sudo groupadd docker
groupadd: el grupo «docker» ya existe
[fintecheando@localhost ~]$ sudo usermod -aG docker $USER
[fintecheando@localhost ~]$ id
uid=1000(fintecheando) gid=1000(fintecheando) grupos=1000(fintecheando),10(wheel) contexto=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
[fintecheando@localhost ~]$ exit
logout
Connection to 192.168.188.129 closed.
victor@centauro:kubernetes$ ssh fintecheando@192.168.188.129
fintecheando@192.168.188.129's password: 
Last login: Mon Feb 19 18:19:11 2018 from 192.168.188.1
[fintecheando@localhost ~]$ docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

[fintecheando@localhost ~]$ wget https://github.com/openshift/origin/releases
-bash: wget: no se encontró la orden
[fintecheando@localhost ~]$ sudo yum install wget
Complementos cargados:fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.cenac.ipn.mx
 * extras: mirror.cenac.ipn.mx
 * updates: mirror.cenac.ipn.mx
Resolviendo dependencias
--> Ejecutando prueba de transacción
---> Paquete wget.x86_64 0:1.14-15.el7_4.1 debe ser instalado
--> Resolución de dependencias finalizada

Dependencias resueltas

======================================================================================================================
 Package                Arquitectura             Versión                              Repositorio               Tamaño
======================================================================================================================
Instalando:
 wget                   x86_64                   1.14-15.el7_4.1                      updates                   547 k

Resumen de la transacción
======================================================================================================================
Instalar  1 Paquete

Tamaño total de la descarga: 547 k
Tamaño instalado: 2.0 M
Is this ok [y/d/N]: y
Downloading packages:
wget-1.14-15.el7_4.1.x86_64.rpm                                                                | 547 kB  00:00:01     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Instalando    : wget-1.14-15.el7_4.1.x86_64                                                                     1/1 
  Comprobando   : wget-1.14-15.el7_4.1.x86_64                                                                     1/1 

Instalado:
  wget.x86_64 0:1.14-15.el7_4.1                                                                                       

¡Listo!
[fintecheando@localhost ~]$ wget https://github.com/openshift/origin/releases/download/v3.9.0-alpha.3/openshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz
--2018-02-19 18:47:27--  https://github.com/openshift/origin/releases/download/v3.9.0-alpha.3/openshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz
Resolviendo github.com (github.com)... 192.30.253.112, 192.30.253.113
Conectando con github.com (github.com)[192.30.253.112]:443... conectado.
Petición HTTP enviada, esperando respuesta... 302 Found
Localización: https://github-production-release-asset-2e65be.s3.amazonaws.com/22442668/0e98efec-0c0e-11e8-8053-e959c7f25e0d?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20180219%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20180219T234727Z&X-Amz-Expires=300&X-Amz-Signature=0bec626743a0aeec83ff720dd67fa5a12c09756bb30ce96cc0508e71cc9381ed&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment%3B%20filename%3Dopenshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz&response-content-type=application%2Foctet-stream [siguiendo]
--2018-02-19 18:47:27--  https://github-production-release-asset-2e65be.s3.amazonaws.com/22442668/0e98efec-0c0e-11e8-8053-e959c7f25e0d?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20180219%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20180219T234727Z&X-Amz-Expires=300&X-Amz-Signature=0bec626743a0aeec83ff720dd67fa5a12c09756bb30ce96cc0508e71cc9381ed&X-Amz-SignedHeaders=host&actor_id=0&response-content-disposition=attachment%3B%20filename%3Dopenshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz&response-content-type=application%2Foctet-stream
Resolviendo github-production-release-asset-2e65be.s3.amazonaws.com (github-production-release-asset-2e65be.s3.amazonaws.com)... 52.216.130.155
Conectando con github-production-release-asset-2e65be.s3.amazonaws.com (github-production-release-asset-2e65be.s3.amazonaws.com)[52.216.130.155]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 43775984 (42M) [application/octet-stream]
Grabando a: “openshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz”

100%[============================================================================>] 43 775 984   748KB/s   en 42s    

2018-02-19 18:48:09 (1.00 MB/s) - “openshift-origin-client-tools-v3.9.0-alpha.3-78ddc10-linux-64bit.tar.gz” guardado [43775984/43775984]

[fintecheando@localhost ~]$ 
