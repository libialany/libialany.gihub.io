---
title:  "Load Balancer con Nginx y Docker"
subtitle: "Conociendo un poco de Nginx"
author: "Melany Estevez C."
avatar: "img/authors/wferr.png"
image: "img/f.jpg"
date:   2022-05-12 
---



<p style="font-size: 15px;">Vamos aprender un poco mas sobre Nginx.El S.O que estoy usando es Fedora. </p>


_Prerequisitos_ 

tener instalado docker **puedes ir al sitio de Docker donde ellos te guian como instalar.**
tener instalado docker-compose.

```
sudo dfn install docker-compose
```

para verificar:

```
which docker-compose
```
:| puedes omitir dfn por apt,etc.

_Estructura_

El plan a seguir es configurar nginx para que balancee la carga entre 2 aplicaciones.

_Estructura_

```
|-> app1 --> Dockerfile
|        --> app1.py
|-> app2 --> Dockerfile
|        --> app2.py
|-> nginx--> default.conf
|        --> nginx.conf
| docker-compose.yml
```
  1. app1/Dockerfile construye la aplicacion app1.py

  2. app2/Dockerfile construye la aplicacion app2.py

  3. Ahora si explicamos la configuracion de Nginx

```
nano nginx/default.conf 
```

la seccion importante son **upstream** y **proxy_pass**.


```
upstream loadbalancer {
server 172.17.0.1:5001 weight=6;
server 172.17.0.1:5002 weight=4;
}
server {
location / {
proxy_pass http://loadbalancer;
}}
```
**upstream** significa que todas las solicitudes de **http://loadbalancer** van a cualquiera de los servidores : : :**172.17.0.1** en el puerto 5001 (es la app1 ), **172.17.0.1**  en el puerto 5002 (es la app2).
**weight** proporcion de trafico que debe dirigirse a cada servidor.

```
sudo nano /etc/nginx/nginx.conf
```
ahora configuramos dentro de la etiqueta http{}.

```
events {
# todo el codigo normal
}
http{
   #todo el codigo
   #ponlo al final 
   server_tokens off;
}
```
__off-topic__ :**server_tokens** para ocultar la version de Nginx que usas.


0_o la ip **172.27.0.1** es el gateway de la red bridge asignada por default ,tambien lo puedes ver en tu maquina:

```
ip a | grep docker0
```
<a href="https://argus-sec.com/docker-networking-behind-the-scenes/" style="color: red; text-decoration: underline;text-decoration-style: dotted;">mas sobre networking en docker</a> 😁.


 4.  **docker-compose.yml**, en el contenedor de nginx solo le pasaremos nuestro archivos por volumenes 😅.

```
  nginx:
    image: nginx:latest
    container_name: webserver
    ports:
      - 80:80
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - app1
      - app2
```
esto es solo un fragmento del docker-compose.yml , si quieres todo <a href="https://github.com/libialany/load-balancer/blob/main/docker-compose.yml" style="color: red; text-decoration: underline;text-decoration-style: dotted;">mas del codigo de este mini-tutorial</a>.

Por ultimo ,levantemos todo nuestros contenedores.

```
docker-compose up 
```
verificar entrando a...

```
 curl localhost #verificamos
```

**EXTRA**

nota es importante conocer de networking con docker 👀,thanks.
