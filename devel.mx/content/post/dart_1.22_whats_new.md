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
draft = false
+++
( Post traducido de http://news.dartlang.org/2017/02/dart-122-faster-tools-assert-messages.html )

Como característica de un lenguaje vivo, de vez en cuando un lenguage tiene modificaciones que mejoran la calidad del lenguaje

## Inicio más rápido de herramientas 
Los archivos compilados de Dart tienen la peculiaridad de inicar mucho muy rápido porque tienen implementada una funcionalidad llamada _snapshots_, la cual consiste en que el estado inicial de la aplicación queda en el compilado al inicio del codigo asi al leerlo por el intérprete automáticamente puede iniciar la ejecución. 
 
Y ahora han portado esta funcionalidad para las herramientas del SDK como el dart2js, el analyzer, y el pub. Y el resultado es increíble.
 
Comparación de los tiempo después de la mejora:
![alt text](/images/chart001.png "Chart de las mejoras")

[![Mas informacion sobre AOT compilling](http://img.youtube.com/vi/lqE4u8s8Iik/0.jpg)](http://www.youtube.com/watch?v=lqE4u8s8Iik)

## Mensajes de Assert
El principio de falla rapido es fundamental para hacer software de alta calidad y en dart, [Assert](https://www.dartlang.org/guides/language/language-tour#assert) 
es la mejor manera de fallar rápido. Pero hasta ahora no era posible agregar un mensaje a los aserts, al menos que se tuvieran que hacer una secuencia de `Throw` errors
pero ahora son mucho más fáciles, como se puede ver a continuación:

```javascript
num measureDistance(List<Place> waypoints) {
  assert(waypoints.any((point) => point.isInaccessible),
         'At least one waypoint is inaccessible.');
  // ...
}
```

Y lo mejor al momento ejecutar en producción los Asserts no son evaluados lo que hace el proceso más rápido
![Asert Covariant example](/images/realease-1.22.gif "Asert Covariant example")

## El tipo `Null` ahora es un subtipo de cualquier tipo de datos
 
Osea se a movido el Tipo `Null` a la base de la jerarquía de todas las clases. Antes el `null` estaba en el fondo de los tipos ahora la clase `Null` también.

```javascript
final empty = <Null>[];

String concatenate(List<String> parts) => parts.join();
int sum(List<int> numbers) => numbers.fold(0, (sum, n) => sum + n);

concatenate(empty); // OK.
sum(empty); // OK.
```

Y mÁs cambios que se pueden consultar en el post original.