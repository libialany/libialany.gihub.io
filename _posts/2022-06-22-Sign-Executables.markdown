---
title:  "Learnig Something About OpenSSL"
subtitle: "Exploring Certificates"
author: "Melany Estevez C."
avatar: "img/authors/wferr.png"
image: "img/flor.jpg"
date:   2022-06-22
---



<p style="font-size: 15px;">Sector <i>Researcher</i> es algo rebuscado que se me aparecio. 👀</p>



_Intro_ 

Este post va enfocado a conocer un poco de como funciona la seguridad en windows a nivel de executables.

_Marco Teorico_

**Como Windows podria detectar que un programa es sospechoso**

_Resumen Express_


**IBM Says**


`SAP` (Software, Application and Product)  en windows debe tener un digital certificate.

Un usuario deberia percatarse de esto mediante:

1) Su conocimiento de instalacion de algun Software(Programa .exe .dll).

2) Certificado de un `Trusted Publishers certificate store`.

*) La firma digital se puede ver desde la pestaña Firma digital de Propiedades del archivo firmado(.exe).


**Sign Executable Files and Why It’s Important**


El certificado firmado de un codigo utiliza un hash criptografico que valida la integridad del archivo ejecutable.

Los CA pueden ser DigiCert o Sectigo.

No puede ser un Publisher de confianza sin un certificado.

__Demo__


**Signing Executables Files**

.... &lt; This will continue &gt;


_Mejoras_ 

Este es un post que trata un nivel basico de Signing Executables Files(Archivos Ejecutables Firmados).

__Links__

<a href="https://www.ibm.com/docs/en/spferp/8.1.0?topic=planning-digital-signing-executable-files-windows" style="color: red; text-decoration: underline;text-decoration-style: dotted;">IBM Says</a> 😁.

<a href="https://codesigningstore.com/how-to-digitally-sign-executable-files" style="color: red; text-decoration: underline;text-decoration-style: dotted;"> How to Digitally Sign Executable Files and Why It’s Important </a>.



**EXTRA**

Dont trust in win... 🔥,thanks.
