---
title:  "Makefile y Docker"
subtitle: "Conociendo un poco de makefile"
author: "Melany Estevez C."
avatar: "img/authors/wferr.png"
image: "img/torre.jpg"
date:   2022-05-15 
---



<p style="font-size: 15px;">Vamos aprender un poco mas sobre archivos makefile.El S.O que estoy usando es Fedora. 👀</p>


_Intro_ 

El uso de un makefile nos puede ayudar en el caso de actualizaciones de versiones de archivos,por que los makefiles tienen tasks(tareas|comandos) que  deseas ejecutar.

`make` es el comando, el `makefile` es el archivo que se ejecutara.


```
make ....
```

**Ejemplo**

_Makefile para Docker_ 

_Prerequisitos_

Tener docker y  docker-compose instalado.

_Estructura_

Vamos a cambiar la version de la imagen a descargar de  alpine y señalaremos el path del archivo.

_Estructura_

```
|-> Makefile 
|-> v1       --> clean.sh
|-> Dockerfile
```
  <p> 1. Makefile es donde pondremos las instrucciones para el contenedor.</p>

  <p> 2. El Dockerfile va a copiar  v1 folder dentro de  la imagen .</p>

  <p> 3. Dockerfile el objetivo es ejecutar un programa (clean.sh)</p>


Setear los argumentos en Dockerfile:

```
nano Dockerfile 
```

La seccion importante son **FROM** y **ADD**.

```
ARG alp_ver
FROM alpine:$alp_ver
ARG fil_ver
ADD $fil_ver/clean.sh /usr/local/bin/clean.sh
RUN chmod +x /usr/local/bin/clean.sh
ENTRYPOINT ["clean.sh"]
```
**ARG** el uso es obligado.

Ahora creamos nuestro `Makefile`.

- Fijamos nuestras variables.

```
alpver=3.12
filver=v1
name=${alpver}/${filver}
....more code
```

- Fijamos nuestra etiqueta de entrada.

```
build: 
```
- Fijamos nuestro comando.

```
build:
      @docker build . -t ${name} --build-arg alp_ver=${alpver} --build-arg fil_ver=${filver}
```

- Antes de la etiqueta debemos poner la bandera .PHONY.

```
.PHONY: build
```

fijamos .PHONY ,si hay un file llamado build y ejecutamos `make build` no va ejecutar , para evitar que el make comando se confunda, se utiliza .PHONY.

```
alpver=3.12
filver=v1
name=${alpver}/${filver}

.PHONY: help build push all
help:
	@echo "Makefile arguments:"
	@echo "alpver - Alpine Version"
	@echo "filver - File Version"
	@echo "Makefile commands:"
	@echo "build"
	@echo "all"
.DEFAULT_GOAL := all
build: 
	@docker build . -t ${name} --build-arg alp_ver=${alpver} --build-arg fil_ver=${filver}
all: build push
```

0_o el help para recordar,ayuda.

por ultimo.

```
make build
```
<a href="https://opensource.com/article/18/8/what-how-makefile#:~:text=The%20make%20utility%20requires%20a,be%20installed%20using%20make%20install%20." style="color: red; text-decoration: underline;text-decoration-style: dotted;">mas sobre Makefile</a> 😁.

si  quieres el <a href="https://github.com/libialany/scripts_in_bash/blob/main/makefile/Makefile/Dockerfile" style="color: red; text-decoration: underline;text-decoration-style: dotted;"> Dockerfile </a>.



**EXTRA**

nota es importante saber algo de makefile 🔥,thanks.
