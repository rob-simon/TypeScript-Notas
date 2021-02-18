# TypeScript

## Índice de contenidos
* [Instalación TypeScript](#instalaci%C3%B3n-typescript)
* [Tipado de Variables](#tipado-de-variables)
* [Variables y Constantes (let & const)](#variables-y-constantes-let--const)
* [Creación de variables](#creaci%C3%B3n-de-variables)
  * [Reestructuración de un Array](#reestructuraci%C3%B3n-de-un-array)
  * [Reestructuración de un Objeto](#reestructuraci%C3%B3n-de-un-objeto)
  * [Template de texto](#template-de-texto)
  * [Operador Spread y Rest](#operador-spread-y-rest)
* [Opciones de compilación (tsconfig.json)](#opciones-de-compilaci%C3%B3n-tsconfigjson)
* [Funciones](#funciones)
  * [Funciones declaradas con una flecha](#funciones-declaradas-con-una-flecha)
  * [Parámetros con valor por defecto](#parámetros-con-valor-por-defecto)
* [Clases](#Clases)
  * [Herencia de clases](#herencia-de-clases)
  * [Getters y Setters](#getters-y-setters)
  * [Propiedades y métodos estáticos](#propiedades-y-métodos-estáticos)
  * [Clases Abstractas](#clases-abstractas)
* [Conocimientos extra](#conocimientos-extra)

## Instalación TypeScript
Abrimos una consola de comandos.
Debemos tener el paquete nodeJS (npm) instalado para poder instalar nuestros paquetes de JS externos.
Cuando tengamos NodeJS instalado ejecutaremos el siguiente comando:
```powershell
npm -g install typescript
```

## Tipado de Variables
En typeScript te permite especificar el tipo de las propiedades, esto significa, qué, al igual que sucede en muchos lenguajes de programación, cada variable tiene un único tipo de dato asignado, no como pasa con *JavaScript*, que el tipado es dinámico y puedes reasignar un tipo diferente a una variable una vez inicializada.
```typescript
let bienvenido: string = "Welcome home!";

function Welcome(bienvenido: string) {
  this.bienvenido = bienvenido;
}

console.log(Welcome(bienvenido));
```

## Variables y Constantes (let & const)
Cuando tengamos variables que no vayan a cambiar su valor, podemos crearlas como constantes. De esta manera tendremos controlado que no se modifique el calor de esa constante en ningún momento, ya que nos devolvería un error de compilación.
```typescript
//let & const
let variable = "Test";
console.log(variable);
variable = "Test modificado";
console.log(variable);

const maxLevels = 100;
console.log(maxLevels);
// maxLevels = 99; //Error de compilación
```

## Creación de variables
Para crear una variable utilizaremos el comando “let”, al cual, una vez le asignemos un valor de un tipo de dato, no se le podrá asignar un valor de tipo diferente, a diferencia de javascript, que las variables son dinámicas y puedes reasignar el tipo de una variable.
```typescript
//string
let myString = 'Test';
myString = 99;  //esta línea provocaría un error al compilar

//number
let myNumber = 50;
myNumber = 'Test'; //esta línea provocaría un error al compilar

//boolean
let myBoolean = false;
myBoolean = 1; //esta línea también provocaría un error al compilar
```

Si no asignamos un valor en la inicialización de la variable, podremos asignar diferentes tipos a esta variable, pero siempre cogerá el último tipo asignado:
```typescript
//assign types
let myTypeNumber;
myTypeNumber = 50;
myTypeNumber = 'Test'; //esta línea NO provocaría un error al compilar
```

Para asignar un tipo de dato a una variable, se lo especificamos añadiendo “: {tipo_dato}” justo después del nombre de nuestra variable:
```typescript
//assign types
let myTypeNumber: number;
myTypeNumber = 50;
myTypeNumber = 'Test'; //esta línea SÍ provocaría un error al compilar
```

Para la asignación de valores en un array, funcionaría de la misma manera, pero también podemos asignar un valor “any” al array, de forma que pueda añadir datos de cualquier tipo.
```typescript
//array
let myArray: any[] = ["Test1", "Test2"];
myArray = [50]; //esta línea NO provocaría un error
```

Para crear una tuple y sabemos que valores tendrá cada posición se lo podemos asignar de la siguiente forma:
```typescript
//tuples
let mytuple: [string, number] = ["Test1", 50];
```

Para los enumeradores vamos a ver cómo se le asignan los valores por defecto y como modificarlos. Por defecto, si tenemos una lista de valores de un enum y no le asignamos valores, estos tendrán un valor de 0 a X. Para modificar el valor de uno de ellos simplemente le asignamos el número que queramos a ese valor del enum, pero teniendo en cuenta que el siguiente valor del enum seguiré el orden de la asignación anterior.
```typescript
//enum
enum Color {
  Gray, //valor 0
  Green = 100, //valor 100
  Blue, //valor 101
  Yellow = 2 //valor 2
};
```

Para declarar un objeto es importante definir sus propiedades y el tipo de estas propiedades.
```typescript
//objects
let userData: { name: string, age: number} = {
  Name: "Max",
  Age: 27
};
```

Las propiedades de un objeto no tienen por qué ser tipos primarios, también podemos asignarle una función como una de sus propiedades.
```typescript
//complex object
let complex: {data: number[], output: (all: boolean) => number[]} = {
  data: [100, 3.99, 10],
  output: function (all: boolean): number[] {
    return this.data;
    }
};
```

Algo que nos permite Typescript es definir un alias para un tipo que queramos definir.
```typescript
//type alias
type Complex = {data: number[], output: (all: boolean) => number[]};
//complex object
let complex: Complex = {
  data: [100, 3.99, 10],
  output: function (all: boolean): number[] {
    return this.data;
  }
};
```

También es posible definir múltiples tipos a una variable.
```typescript
//union types
let multipleType: number | string = 27;
multipleType = "27";
```

Podemos comprobar el tipo de una variable utilizando "typeof":
```typescript
//Check types
let finalValue = 30;
if (typeof finalValue == "number") {
  console.log(“Es un número”);
}
```

Existe el tipo "never" el cual significa que tu función no devolverá absolutamente nada, ni pintará nada por consola.
```typescript
//never
function neverReturns(): never {
  Throw new Error("Un error!");
}
```

Para declarar variables que admitan valores "null" se puede definir de la misma forma que la asignación de multiple tipos o asignarle un type "any", pero este último no es muy recomendable, ya que pierde sentido el tipado de variables.
```typescript
//Nullable Types
tet canBeNull: number | null = 12;
canBeNull = null;
```

  ### Reestructuración de un Array
Para reasignar las posiciones de un array dentro de variables independientes lo realizaremos de esta forma:
```typescript
const myHobbies = ["Cooking", "Sports"];
const [hobby1, hobby2] = myHobbies; // esta asignación colocará cada posición dentro de la lista de nombres que definamos
console.log(hobby1, hobby2); // de esta forma podemos llamar cada posición con el nombre de la variable que tenga asignado.
```

  ### Reestructuración de un Objeto
De la misma forma que hemos reaisgnado los valores de un array en el ejemplo anterior, con los objetos funcionaría de una forma muy similar.
```typescript
const userData = [userName: "Max", age: 25];
const [userName, age] = userData; // como las propiedades de un objeto tienen su propio nombre asignado, podemos usar eso como key, y él mismo sabrá reconocer cada valor.
console.log(userName, age);

//Tabmién es posible asignar un alias al nombre de la nueva asignación
const userData = [userName: "Max", age: 25];
const [userName: myName, age: myAge] = userData; // como las propiedades de un objeto tienen su propio nombre asignado, podemos usar eso como key, y él mismo sabrá reconocer cada valor.
console.log(myName, myAge);
```

  ### Template de texto
Vamos a ver como crear un template de multilínea y como se le concatenan variables. Para crear el template usaremos las comillas simples invertidas ``. Para asignar una variable utilizaremos el signo del dolar seguido de llaves. ${}
```typescript
const userName = "Max";
const greeting = `This is a heading!
I'm ${userName}.
This is cool!`;
console.log(greeting);
```

  ### Operador Spread y Rest
Una forma de pasar multiples argumentos utilizando un array sería la siguiente.
```typescript
// Spread
const numbers = [1, 10, 99, -5];
console.log(Math.max(33, 99, 10, -3)); // la función .max() pide como argumentos pasar cada número como un argumento.
console.log(Math.max(...numbers)); // si le pasásemos un array de números fallaría al no ser el tipo de argumentos esperado, de esta forma funcionaría igual que el ejemplo anterior.

// Rest
function makeArray(...args number[]) {
  return args;
}

//es posible realizar multiples variantes de argumentos, aunque el siguiente ejemplo no debería ser muy correcto:
const numbers [5, 10, 60]
function multiplesArgs(name: string, number1: number, number2: number, number3: number) {
  return name;	
}
console.log(multiplesArgs("Test",...numbers))
```

## Opciones de compilación (tsconfig.json)
Ref: [https://www.typescriptlang.org/docs/handbook/compiler-options.html](https://www.typescriptlang.org/docs/handbook/compiler-options.html)
* **compilerOptions**
  * **module**: Especifica la generación de código del módulo: "None", "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015" or "ESNext".
  * **target**: Especifica la versión de destino de ECMAScript.
  * **noImplicitAny**: Genera error en expresiones y declaraciones si se asigna el tipo “any”.
  * **sourceMap**: Genera el archivo .map con el cual podremos debuggear directamente en la consola del navegador en nuestro archivo “.ts”.
  * **noEmitOnError**: No emite salidas si se informa de algún error.
  * **strictNullChecks**: Verifica los valores null y undefined los cuales solo se pueden asignar a sí mismos o al tipo “any”.
  * **noUnusedParameters**: Genera un error si una función tiene parámetros que no utiliza.

## Funciones
A la hora de crear una función, es conveniente especificar el tipo de dato que va a retornar, o "void" en caso de que no devuelva nada.
```typescript
//return string
function returnString(): string {
  return "test";
}
//void
function sayHallo(): void {
  console.log("test");
}
//tipado de argumentos
function calcula(value1: number, value2: number): number {
  return value1 * value2;
}
```

  ### Funciones declaradas con una flecha
Otra forma de declarar las funciones; si vamosa asignar su valor a una variable/constante, sería utilizando la flecha de la siguiente forma:
```typescript
//si nuestra función únicamente va tener una línea de código, podemos definirlo todo en la misma línea
const addNumber = (number1: number, number2: number) => number1 * number2;
console.log(addNumber(10,3)); // Pintaría por consola -> 13

//si en cambio, nuestra función tendrá más de una línea utilizaríamos las llaves después de la flecha
const multiplyNumber = (number1: number, number2: number) => {
  let suma: number = number1 + number2;
  return suma * 2;
}
console.log(multiplyNumber(10,2)); // Pintaría por consola -> 24

// si solo usa 1 argumento, no sería necesario añadir los paréntesis
const unParam = number1 => number1 * 2;
console.log(unParam(2)); // Pintaría por consola -> 4

//si no tiene argumentos, se añaden los paréntesis vacíos
const saludo = () => console.log("Hello!");
```

  ### Parámetros con valor por defecto
Podemos asignar un valor por defecto en los argumentos de una función.
```typescript
//Default parameter
const countDown = (start: number = 10): void => {
  console.log(start);
  while (start > 0) {
    start--;
  }
  console.log("Done!", start);
}
```

## Clases
De la misma forma que trabajamos en otros lenguajes con programación orientada a objetos, aquí también es posible, aquí vamosa ver como crear clases y como asignarle sus propiedades públicas; por defecto, privadas y protegidas.

```typescript
class Person {
  name: string;
  private type: string;
  protected age: number = 25;
  
  // aquí vemos como podemos definir una propiedad más del objeto directamente en el contructor.
  constructor(name: string, public username: string) { 
    this.name = name;
  }
  
  //si creamos una función privada, no será accesible fuera de la clase, pero sí dentro de la misma
  private printAge() {
    console.log(this.age)
  }
  
  setType(type: string) {
    this.type = type;
    console.log(this.type);
    printAge(); // podemos llamar a la función privada
  }
}

const person = new Person("Max", "max");
console.log(person);
console.log(person.name, person.username);
// person.printAge(); // Error al llamar un método privado
person.setType("Cool");
```

  ### Herencia de clases
Otra de las características que tenemos es la de poder heredar una clase utilizando la función extends al crear nuestra clase y especificarle de quien debe heredar.
```typescript
//Herencia - como vemos aquí, es posible llamar la propiedad de Person dentro de la clase Max 
// añadiendo la extensión de Person a nuestra clase.
class Max extends Person {
  //name = "Max";
  
  // A la hora de definir el constructor, llámamos a super para hacer referencia al constructor de la clase heredada
  constructor(username: string) {
    super("Max", username);
    // veamos como podemos acceder a la propiedad heredada Age
    this. age = 31;
    // pero no podemos acceder a la propiedad heredada type, por ser privada, por lo que solo es accesible desde la clase heredada
  }
}

const max = new Max("max");
console.log(max);
```

  ### Getters y Setters
  Vamos a ver como definir los getters y setters de nuestra clase, para que se pueda acceder a las propiedades que necesitemos.
  ```typescript
  //Getters & Setters
  class Plant {
    private _species: string = "Default";
    
    get species() {
      return this._species;
    }
    
    set species(value: string) {
      if (value.length > 3) {
        this._species = value;
      } else {
        this._species = "Default";
      }
    }
  }
  
  let plant = new Plant();
  console.log(plant.species);
  plant.species = "AB";
  console.log(plant.species);
  plant.species = "Green Plant";
  console.log(plant.species);
  ```

  ### Propiedades y métodos estáticos
  En algún caso nos puede interesar crear clases estáticas, las cuales no necesitemos instanciar para acceder a ellas. Eso también es posible aquí:
  ```typescript
  class Helpers {
    static PI: number = 3.14;
    static calcCircumference(diameter: number): number {
      return this.PI * diameter;
    }
  }
  console.log(2 * Helpers.PI);
  console.log(Helpers.calcCircumference(8))
  ```
  
  ### Clases Abstractas
  También es crear clases abstractas.
  ```typescript
  //Abstract Classes
  abstract class Project {
    projectName: string = "Default";
    budget: number;
    
    abstract changeName(name: string): void;
    
    calcBudged() {
      return this.budget * 2;
    }
  }
  
  class ITProject extends Project {
    // como la clase abstracta tiene definida la función changeName, es necesario implementarla en la clase que la hereda.
    changeName(name: string): void {
      this.projectName = name;
    }
  }
  
  let newProject = new IRProject();
  console.log(newProject);
  newProject.changeName("Final Project");
  console.log(newProject);
  ```

## Conocimientos extra
La extensión de los ficheros de Typescript es “.ts”, pero como el navegador no sabe interpretar typescript, cuando se importe un archivo “.ts” en nuestro código HTML lo llamaremos como si fuese Javascript:
```html
<script src="./script.js"></script>
```

**Instrucciones**
- npm init
- npm install lite-server --save-dev
- npm start
- tsc --init
- tsc
