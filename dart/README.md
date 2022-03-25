# Introducción a Dart

- ¿Por qué Dart?
- Nuestro "Hola Mundo" en Dart
- Tipado de datos en Dart
- Listas
- Mapas
- Funciones
- Clases
- Mixins
- Constructores
- Getters
- Setters
- Extender una clase
- Futures
- Async
- Await

:eye: [Fundamentos de Dart](https://medium.com/@carloslopez_19744/%EF%B8%8F-fundamentos-del-lenguaje-dart-2803fa20556b)

## ¿Por qué Dart?

Google ha creado una nueva plataforma de desarrollo llamada Dart, que permite a los desarrolladores crear aplicaciones móviles de alta calidad.

**Principales características**

- AOT (Ahead of Time): Compilado a un rápido y predecible código nativo. (Totalmente personalizable)
- Puede ser JIT (Just in Time): Compilado apara una velocidad excepcional de desarrollo. (Esto inclute el popular Hot Reload)
- Hace fácil la creación de animaciones y transiciones que corren a 60 fps (frames per seconds)
- Al ser compilado a código nativo, no hay puentes innecesarios para correr el código.
- Dart le permite a Flutter evitar el desarrollo de diseños en archivos independientes como JSX, XML o bien interfaces separadas.
- Dart es relativamente fácil de aprender.

En dart cada uno de sus programas tiene una instrucción principal llamada `main()`.

```dart
void main() {
    // Punto inicial
}
```

[x] Dart es un lenguaje con tipos de datos, también tiene su forma dinámica. Cuando se declara una variable, el valor por defecto es null `String string; // null`

## Hola Mundo

```dart
void main() {
  for (int i = 0; i < 5; i++) {
    print('hello ${i + 1}');
  }
}
```

- [Darpad](https://dartpad.dartlang.org/?)
- [Main Dart](https://github.com/Klerith/dart-basics/blob/master/01-main.dart)

:star: El punto y coma en dark es obligatorio

## Tipos de datos

Dart es de tipado estricto pero tiene inferencia de tipo de datos dependiendo del contenido de la variable, por lo que es flexible.

- **strings** Son cadenas de texto.

```dart
// Strings
var nombre = 'Tony';
var apellido = 'Stark';

final nombreCompleto = 'Este valor no cambia, es inmutable';
const CONSTANTE = 'Este valor no cambia nunca';

// La forma recomendada para las variables
String name = 'Johan';
String lastName = 'Mosquera';

print('$nombre $apellido'); // Usando template string


// Números
int empleados = 10;
double salario = 1856.25;

print(empleados*salario);
```

**const** La variable nunca va a cambiar en tiempo de compilación.
**final** Se mantiene igual al momento de su primero asignación.

## Boolean

```dart
void main() {
    bool isActive = false;

    print(isActive);
}
```

En la últimas versiones de dart, tiene null safety para prevenir errores.
Para indicarle, se debe colocarle el signo de interrogación `?` al final del tipo de dato. `bool? miVariable = null`

## Tipo de datos - Lista

Collección de elementos que tiene un tipo de dato en común.

```dart
List numeros = [1,2,3];
numeros.add(4);
print(numeros);
```

Las listas son en base a cero, es decir las posiciones empiezan con el valor 0.
Dynamic es un tipo especial de datos, permite tener varios tipos de datos en la lista.

`List<dynamic> numeros = [1,2,3, "String"];`

Se recomienda usar un sólo tipo de dato

`List<int> numeros = [1,2,3];`

```dart
// Genera una lista de con 100 valores, de 0 a 100
final masNumeros = List.generate(100, (int index) => index);
print(masNumeros);
```

## Tipo de datos - Mapa

Los mapas son una colección de pares de valores, donde el valor de cada clave es un valor de tipo de dato en común.

```dart
Map<String, dynamic> persona = {
    'nombre': 'Tony',
    'apellido': 'Stark',
    'edad': 45,
    'genero': 'Masculino'
};

persona.addAll({ "estado" : "Soltero" });

print(persona);

```

## Funciones en dart

En dart, los argumentos opcionales se deben colocar dentro de corchetes y deben ir al final de la lista de argumentos.

```dart
void main() {
   saludar('Pacita');
  greeting(name: "Juanito");
}

void saludar(String nombre, [String mensaje = 'No message']) {
  print('Hola $nombre, $mensaje');
}

void greeting({String name: '', String? message}){
  print("Welcome $name");
}

void namedArguments({
    required String name,
    required String message
    }) {
  print("Welcome $name, $message");
}
```

Los argumentos siempre son mandados por valor si son primitivos, booleanos, numeros o strings.
Cualquier objeto es mandado por referencia.

## Clases en Dart

Todo el Flutter son clases pero lucen como funciones.

```dart
void main() {

  var wolverine = new Heroe('Logan', 'Regeneración');

  print(wolverine);

}

class Heroe {

  String nombre;
  String poder;

  // Argumentos posicionales
  Heroe(this.nombre, this.poder);

  // Argumentos por nombre
  /*Heroe({
    required this.nombre,
    required this.poder
  });*/

  @override
  String toString() {
    return 'nombre: ${this.nombre}';
  }

}
```

## Constructores por nombre

En este ejemplo, se muestra como usar los constructores por nombre para recibir parámetros y mapear la información en una clase en dart.

```dart
void main() {

  final rawJson = {
    'nombre': 'Tony Stark',
    'poder': 'Intelligence'
  };

  final ironman = Heroe.fromJson(rawJson);
  print(ironman);

}

class Heroe {

  String nombre;
  String poder;

  // Argumentos por nombre
  Heroe({
    required this.nombre,
    required this.poder
  });

  Heroe.fromJson(Map<String, String> json) :
    this.nombre = json['nombre'] ?? '',
    this.poder = json['poder'] ?? '';

  @override
  String toString() {
    return 'nombre: ${this.nombre} - Poder: ${this.poder}';
  }

}
```

## Getters and Setters

Un **getter** es un método que luce como un método pero se llama como una propiedad.
Un **setter** es un procedimiento en el cual le establecemos el valor a una propiedad.

```dart
import 'dart:math';

void main() {
  final cuadrado = new Cuadrado(3);

  print('Area: ${cuadrado.area}');
  cuadrado.area = 36;
  print('Lado: ${cuadrado.lado}');
}

class Cuadrado {

  double lado; // lado * lado


  Cuadrado(double lado):
    this.lado = lado;

  // Getter
  double get area {
    return this.lado * this.lado;
  }

  // Setter
  set area(double valor) {
    print('Set: $valor');
    this.lado = sqrt(valor);
  }

  double calculaArea() {
    return this.lado * this.lado;
  }

}
```

## Clases abstractas

Son clases que no se pueden instanciar. La clase abstracta sirve para implementar los métodos que se definen. Sirve como un molde para las demás clases.

```dart
void main() {

  final perro = new Perro();
  final gato = new Gato();

  sonidoAnimal(perro);
  sonidoAnimal(gato);

}

void sonidoAnimal(Animal animal) {
  animal.emitirSonido();
}

abstract class Animal {

  int? pata;

  void emitirSonido();

}

class Perro implements Animal {


 int? pata = 4;

 void emitirSonido() {
   print('Guauuuuuuu');
 }

}

class Gato implements Animal {

  int? pata = 4;

  void emitirSonido(){
    print('Miauuuu');
  }
}
```

## Extends

Se usa para la herencia de clases, esto nos permite extender de una clase y usar sus métodos y propiedades.

```dart
void main() {

  final superman = new Heroe('Clark Kent');

  print(superman);

}

abstract class Personaje {

  String? poder;
  String nombre;

  Personaje(this.nombre);

  @override
  String toString() {
    return '$nombre - $poder';
  }

}

class Heroe extends Personaje {

  Heroe(String nombre): super(nombre);

}
```


## Mixins

Esta característica es propia de dart, no hay similitudes con otros lenguajes. Los mixins son clases que se usan para agregar funcionalidades a otras clases. Esto nos permiten ciertas características a unas clases, es cono la implementación de interfaces en una clase.

[¿Qué son lo Mixins?](https://medium.com/flutter-community/dart-what-are-mixins-3a72344011f3)

La palabra reservada **with** se usa para usar mixins.

```dart
void main() {
  
  final flipper = new Dolphin();
  final bat = new Bat();
  
  flipper.nadar();
  bat.caminar();
  bat.volar();
  
}

abstract class Animal {}

abstract class Mammal extends Animal {}
abstract class Bird extends Animal {}
abstract class Fish extends Animal {}


abstract class Volador {
  void volar() => print('Estoy volando');
}

abstract class Caminante {
  void caminar() => print('Estoy caminando');
}

abstract class Nadador {
  void nadar() => print('Estoy nadando');
}

class Dolphin extends Mammal with Nadador {}
class Bat extends Mammal with Caminante, Volador {}
```

## Futures

Los futures son muy importantes en Dart, es como una promesa en javascript. Es una tarea asíncrona.
Un Future, no es más que una tarea asíncrona que se hace a destiempo.

```dart
void main() {
  
  print('Antes de la petición');
  httpGet('https://api.nasa/stars')
    .then((data) {
      print(data);
    });
  
  print('Fin del programa');
  
}

Future<String> httpGet(String url) {
  return Future.delayed(
    Duration(seconds: 3), () {
      return 'Hola mundo - 3 segundos';
    }
  );
}
```

## Async - Await

Si se coloca la palabra reservada **async** dentro de la función, ésta devolverá un Future.
El programa ejecuta todo el programa primero de manera síncrona y luego se ejecutan las tareas asíncronas.

```dart
void main() async {
  
  print('Antes de la petición');
  httpGet('https://api.nasa/stars')
    .then((data) {
      print(data);
    });
  
  // getNombre('001').then(print);
  
  // Usando el await
  final nombre = await getNombre('001');
  print(nombre);
  
  print('Fin del programa');
  
}

Future<String> getNombre(String id) async {
  return '$id - Camilo';
}

Future<String> httpGet(String url) {
  return Future.delayed(
    Duration(seconds: 3), () {
      return 'Hola mundo - 3 segundos';
    }
  );
}
```