---
title:  "Networking en Linux"
subtitle: "Comandos Basicos"
author: "Melany Estevez C."
avatar: "img/authors/wferr.png"
image: "img/a.jpg"
date:   2022-06-22 
---

<p style="font-size: 15px;">Algo importante en S.0. Linux  en este caso debian es conocer de los comandos de  configuracion  Networking. </p>

_Prerequisitos_ 

tener instalado **vim** o algun editor de texto.

```
sudo apt install vim
```

para verificar:

```
which vim
```
_Intro_

Primero en esta parte veremos los comandos y despues los pondremos en practica en un proyecto: 

_Estructura_

```
|-> proyecto --> config.txt
```

_Conceptos_

🐑🐑  necesitamos cambiar alguna direccion IP de nuestras interfaces **ipconfig**


__Listamos__
```
ifconfig
```

__Cambiar la IP de nuestra interfaz ,el network mask y el maximum transmition unit(unit).__
*_root user_*
```
ifconfig enp0s3 10.0.2.20
ifconfig enp0s3 network 255.255.255.0
```
🐑🐑  adicionar un estatico route ??**ip**

*_root user_*
```
ip route add {NETWORK/MASK} via {GATEWAYIP}
```
🐑🐑  necesito informacion de la configuracion  SCO TCP/IP **kernel routing table**.

*_root user_*
```
kernel routing table 
```

🐑🐑  necesito informacion de la tabla de rutas  **route -n**.

*_root user_*
```
route -n
```

**EXTRA**

Nota es importante conocer el estado y  configuracion de las tablas  de rutas IP  ,nos indican como y a traves de donde se envia un paquete en las distintas redes  👀,thanks.
segunda parte el proyecto.
