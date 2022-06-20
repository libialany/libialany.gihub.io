---
title:  "PortScanner en Go"
subtitle: "Learning Go By Doing"
author: "Melany Estevez C."
avatar: "img/authors/wferr.png"
image: "img/flor.jpg"
date:   2022-05-15 
---



<p style="font-size: 15px;">Vamos aprender un poco de <i>Go</i> enfocandonos en la Capa 4 del modelo TCP/IP y el cual entra en esa categoria  un Port Scanner.El S.O que estoy usando es Fedora. 👀</p>



_Intro_ 

Como este proyecto se va enfocado a la capa 4,se me toparon nuevos conceptos importantes y relevantes, tratare de resumirlos ,creo que fueron los suficiente para entender como estaba funcionando todo.

_Teoria_

**Debemos saber que es el Protocolo tcp**

```
net.DialTimeout("tcp",....)
//more code
```

El protocolo TCP de la capa de trasporte nos confirma que un paquete ha alcanzado su destino ,este ha estableciendo una conexión de punto a punto entre los hosts de envío y recepción. 


**Goroutines**

Un goroutine es una función que es capaz de ejecutarse simultáneamente con otras funciones.

`go` es la invocacion a una funcion,algo importante ,debe ejecutarse una funcion para que una goroutina responda o se ejecute.

```
func hello(s string){
	fmt.Println(s)
}
func main(){
	go hello("1")
	//Para que funcione
	//(1) ejecutas la funcion hello 
	//hello("2")
	//(2) ejecutas la funcion Sleep
 	//time.Sleep(time.Millisecond*200)
```

__Analogia__

Cocinar lo primero el agua hirviendo.

Despues vas agregando la papa, el arroz estarian siendo cocidas al mismo tiempo.



**Channel**

Los canales son medio de comunicacion entre una goroutina y un programa principal.

Gracias a esperar una respuesta o a comunicarse, podemos limitar un canal (decirle que no se pase de una cantidad).



__Analogia__

El Agua si esta hirviendo a gran temperatura empezara a crear vapor  o sonido es un medio que nos informa.

```
// Creas un canal
sem:= make(chan bool, 10)
	for i := 0; i < 100; i++ {
		// le fijas un valor
		sem <- true
		go func(i int){
			defer wg.Done()
			// la goroutina le comunica al canal
			defer func() { <-sem }()
			//more code
		}(i)
//more code
```

Un canal puede ser varios tipos:int,string ,struct,etc.Debes inicializarle un valor.En Go si tienes una variable debes usarla por eso si tienes un canal debes devolverlo con valores **no puedes abrirlo y dejarlo**.


**Sync**

La Sincronizacion ,cuando ejecutamos una goroutina no esperamos a que acabe , si  usamo __sync__   la libreria podemos asegurar que 
nuestras goroutines acaben.

Son 4 palabras clave son un ciclo no pueden ser omitidas.

```

	// crea un sync
	var wg sync.WaitGroup
	// adicionas una goroutina
	wg.Add(1)
	go func(){
			// more code
			// restas una goroutina
			wg.Done()
		}()
	}
	// acabas  con el sync por que deberi tener valor de 0
	wg.Wait()
```

__Analogia__

Para asegurarnos de no quemar o falta de coccion de nuestro comida podemos poner un timer(alarma).



**PortScanner**

_Prerequisitos_

1. Golang instalado.

_Pasos_

  <p> 1. Lo primero es ingresa una IP </p>

  <p> 2. Tratar de conectarte por tcp con un puerto x (65535>x>1).</p>

  <p> 3. Manejar las respuestas.</p>

_Ejecucion_

clonas el repo 

```
git clone [URL]

```

dentro del directorio

```
|-> README.md
|-> main.go
```
lo inicializas.
```
go mod init main.go
```
lo ejecutas con 
```
go run main.go -ip [IP]
```

Scanear tu propio localhost

```
go run main.go
```

_Mejoras_ 

Cree un script enfocado a resolver el dns para asi tener una funcionalidad mas pero el Codigo debe ser mas estructurado ,debo mejorarlo con Programacion Orientada a Objetos. 


Un PortScanner
<a href="https://tutorialedge.net/projects/building-security-tools-in-go/building-port-scanner-go/" style="color: red; text-decoration: underline;text-decoration-style: dotted;">Sincrono </a> 😁.

si  quieres el <a href="https://github.com/libialany/portscanner/blob/timeout/main.go" style="color: red; text-decoration: underline;text-decoration-style: dotted;"> portscanner </a>.



**EXTRA**

Lear by doing 🔥,thanks.
