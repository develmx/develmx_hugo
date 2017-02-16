+++
banner = ""
date = "2017-02-15T23:40:03-06:00"
title = "Actualización a Dart 1.22"
menu = ""
description = ""
categories = ["Dart"]
tags = ["news"]
images = []
slug = "actualización-a-dart-1_22"
draft = true
+++
( Post traducido de http://news.dartlang.org/2017/02/dart-122-faster-tools-assert-messages.html )

Como caracteristica de un lenguage vivo, de vez en cuando un lenguage tiene modificaciones que mejoran la calidad del lenguage

## Inicio mas rapidio de herramientass
Los archivos compilados de Dart tienen la peculiaridad de inicar mucho muy rapido por que tienen implementada una funcionalidad llamada _snapshots_,
la cual consiste en que el estado inicial de la aplicacion queda en el compilado al inicio del coidgo asi al leerlo por el interprete automaticamente puede inicar la ejecucion.
 
Y ahora han portado esta funcionalidad para las herramientas del SDK como el dart2js, el analyzer, y el pub. Y el resultado es increible.
 
Comparacion de los tiempo despues de la mejora:
![alt text](/images/chart001.png "Chart de las mejoras")

[![Mas informacion sobre AOT compilling](http://img.youtube.com/vi/lqE4u8s8Iik/0.jpg)](http://www.youtube.com/watch?v=lqE4u8s8Iik)

## Mensages de Assert
El principio de falla rapido es fundamental para hacer software de alta calidad y en dart, [Assert](https://www.dartlang.org/guides/language/language-tour#assert) 
es la mejor manera de falllar rapido. Pero hasta ahora no era posible agregar un mensage a los aserts, al menos que se tubieran que hacer una secuencia de `Throw` errors
pero ahora son mucho mas faciles, como se puede ver a continuacion:

```javascript
num measureDistance(List<Place> waypoints) {
  assert(waypoints.any((point) => point.isInaccessible),
         'At least one waypoint is inaccessible.');
  // ...
}
```

Y lo mejor al momento ejecutar en produccion los Asserts no son evaluados lo que hace el proceso mas rapido
![Asert Covariant example](/images/realease-1.22.gif "Asert Covariant example")

## El tipo `Null` ahora es un subtipo de cualquier tipo de datos
 
Osea se a modido el Tipo `Null` a la base de la jerarquia de todas las clases. Antes el `null` estaba en el fondo de los tipos ahora la clase `Null` tambien.

```javascript
final empty = <Null>[];

String concatenate(List<String> parts) => parts.join();
int sum(List<int> numbers) => numbers.fold(0, (sum, n) => sum + n);

concatenate(empty); // OK.
sum(empty); // OK.
```

Y mas cambios que se pueden consultar en el post original.