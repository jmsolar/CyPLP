# Conceptos y paradigmas de lenguajes de programación

## Integrantes del grupo

* Franceschi Luis, legajo 4343/2
* Otero Llambay Mariano, legajo 11335/5
* Solar Jonatan Matias, legajo 8396/0

## Lenguajes asignados

* Python
* Processing

### Bibliografía utilizada

* https://docs.python.org/3.9/reference/index.html
* https://entrenamiento-python-basico.readthedocs.io/es/latest/
* https://nedbatchelder.com/text/names.html
* https://processing.org/reference/
* Processing: A programming handbook for visual designers and artists, de Casey Reas y Ben Fry - The MIT Press
* Programming 101: The How and Why of Programming Revealed Using the Processing Programming Language, de Jeanine Meyer - Apress

<div style="page-break-after: always;"></div>

**A. Enuncie y compare distintas caracteristicas (o criterios de evaluación) de cada uno
de los lenguajes asignados funcamentando cada uno con ejemplos de código.**

* **Processing** es un framework basado en Java, orientado a diseño grafico que brinda la posibilidad de crear código basado en otros lenguajes como Javascript, Python y Ruby.
Sin embargo es importante mencionar que en la misma documentación de este framework se hace hincapié a tratar
de no usar librerías externas dado que podrían producirse errores con el mismo.
* **Python** es un lenguaje de programación de alto nivel, interpretado, de propósito general. Puede utilizarse como lenguaje procedural, orientado a objetos y en menor medida funcional.

#### Simplicidad y legibilidad

Python hace hincapié en la legibilidad del código, se siguen reglas de PEP8 para que todos escribamos de la misma manera.
El equivalente en Processing al "Hello World" es dibujar una línea simple:
```processing
line(15, 25, 70, 90);
```

En python un “Hello World” se vería de esta forma:
```python
print(“Hello World”)
```

Podemos nombrar a Processing como un lenguaje menos simple que Python, al tratarse de un 
lenguaje con mayor cantidad de palabras reservadas así como reglas sintácticas a seguir,
como puede ser el uso de ";" para finalizar la línea, llaves de apertura y cierre de bloques,
la definición del tipo retornado por una función (void en caso de no retornar nada), entre otros.

* **Processing**
```processing
float y = 100;
void setup() {
  size(640, 360);  // Size should be the first statement
  stroke(255);     // Set stroke color to white
  noLoop();
  
  y = height * 0.5;
}

void draw() { 
  background(0);   // Set the background to black
  line(0, y, width, y);  
  
  y = y - 1; 
  if (y < 0) { 
    y = height; 
  } 
} 

void mousePressed() {
  loop();
}
```

<div style="page-break-after: always;"></div>

* **Python**
```python
y = 100

def setup()
  size(640, 360)
  stroke(255)
  noLoop()
  y = height * 0.5

def draw()
  background(0)
  line(0, y, width, y)
  y = y - 1 

  if y < 0:
    y = height

def mousePressed()
  loop()
```

#### Claridad en los bindings
* **Python**

Acorde a lo mencionado en el punto anterior sobre las reglas en las que se basa el lenguaje,
vemos que no hay complejidad operativa que conlleve al programador a cometer errores en la escritura de sus programas.
Dando como ejemplo las operaciones aritméticas la escritura del programa es aún clara
para los casos donde se construyen operaciones complejas. En este mismo sentido,
la interpretación de los programas se realizan de forma sencilla procesando de izquierda a derecha
teniendo en cuenta la prioridad de operadores.
Además de esto para distintos “tipos” de datos pueden utilizarse los mismos símbolos del lenguaje pero
con diferente fin, siendo de fácil entendimiento, como lo es el uso de “+” en operaciones aritméticas,
concatenación de cadenas de texto o incremento de valores

```python
suma = (2 + num5) * (2/(num1 * num2 * num3))
```

* **Processing**

Siendo Processing un framework para desarrollo visual o gráfico es claro que la mayor parte de las operaciones realizadas en él son a través de métodos, es decir, haciendo el llamado a funciones con un propósito específico. Pueden como cualquier otra función recibir parámetros en caso que el método lo permita y de esta forma tener sobrecarga de métodos.
Al resumirse mayormente en la utilización de métodos o funciones la complejidad simplemente es reducida y la curva de aprendizaje de la herramienta es cómoda para quien este interesado.
Ahora bien, no todo se realiza mediante funciones sino que es posible utilizar comparadores (mayor que, mayor o igual que, menor, igual, etc) y los mismos símbolos no son utilizados para realizar otras operaciones. Esto está acotado dado que el propósito del framework no es general sino para un ambiente de desarrollo de artes visuales.

#### Confiabilidad
* **Python**

Siendo un lenguaje interpretado, la detección de los errores es llevada a cabo al momento de la ejecución de las sentencias,
el compilador se encarga de interpretar instrucción a instrucción y en caso de por ejemplo intentar sumar a un valor
numérico el valor almacenado en otra variable sin esta haber sido inicializada producirá un error. 
Por tanto, la detección de los errores y el soporte de confiabilidad que provee el lenguaje están estrictamente
ligados a la ejecución del programa y su correción por parte del desarrollador.
El lenguaje provee mecanismos para poder evitar ciertos errores basandose en la utilización de lo que llamamos excepciones.
De esta forma, podríamos evitar la interrupción del programa o al menos poder realizar acciones adicionales antes de que esto suceda.
Este soporte también debe ser implicitamente incluido por el desarrollador en cada sección que considere podría sucederse algún error.
Por ej: intentar abrir archivos en un directorio que el usuario ingresa para copiarlo a otra ubicación,
podría sucederse que el archivo de origen no exista o aún el path no exista.
Entonces en estás situaciones el desarrollador puede agregar implicitamente la “validación” de si existe el directorio/archivo y de esta forma manejar el error producido.

* **Processing**

Al igual que Python, es posible realizar de forma implícita el tratamiento de errores.

```processing
// Ejemplo
BufferedReader reader;
String line;
 
void setup() {
  // Open the file from the createWriter() example
  reader = createReader("positions.txt");    
}
 
void draw() {
  try {
    line = reader.readLine();
  } catch (IOException e) {
    e.printStackTrace();
    line = null;
  }
  if (line == null) {
    // Stop reading because of an error or file is empty
    noLoop();  
  } else {
    String[] pieces = split(line, TAB);
    int x = int(pieces[0]);
    int y = int(pieces[1]);
    point(x, y);
  }
}
```
Se presenta aquí un ejemplo de apertura de un archivo no existente. Similar a lo que realiza Python, se tiene un bloque de código encerrado en una sección “try” y en “catch” la/s posible/s solución/es según el error ocurrido. Esto nos permite continuar la ejecución del programa sin detenerlo abruptamente.
En cuanto a los tipos y su declaración, es necesario realizar esto antes de darles uso, en este aspecto el lenguaje se apoya en el soporte que brinda el lenguaje Java donde el programa al compilarse es puesto a prueba en su sintaxis y semántica para de esta forma poder descubrir los errores antes que el mismo sea ejecutado.

#### Soporte
* **Python**

Es administrado por la Python Software Foundation. Posee una licencia de código abierto,
denominada "Python Software Foundation License", que es compatible con la Licencia pública general de GNU.
En el sitio oficial se encuentra disponible el codigo fuente asi como "releases" para la gran mayoría
de los sistemas operativos: Linux, Windows, Mac OS X, y diversas versiones de UNIX.
También esta disponible la documentación oficial, clasificada según varios criterios:
nivel, idioma, tipo (escrito o audiovisual). Además de la implementación oficial en C, que es la más ampliamente usada,
existen otras implementaciones en otros lenguajes por ejemplo: .NET (IronPython), java (Jython), python (PyPy)

* **Processing**

Es administrado por la Processing Foundation, que desarrolla y distribuye bajo una licencia LGPL,además existen varias implementaciones en distintos lenguajes: Processing (Java), p5.js (JavaScript) y Processing.py (Python)
El código fuente se encuentra disponible en Github y en el sitio oficial podemos descargar el ejecutable y
al estar desarrollado en Java es multiplataforma.
El sitio cuenta con documentación oficial y referencias a libros que ahondan en distintos aspectos del lenguaje.

> **Si bien hasta aquí el soporte de ambos lenguajes es similar, Python cuenta con una comunidad de usuarios mucho más grande que Processing**

#### Abstracción

Ambos lenguajes tienen soporte para abstracción mediante el uso de clases abstractas,
las cuales tienen uno o más métodos abstractos, es decir sin implementación.
Subclases de la clase abstracta proveen la implementación de los métodos abstractos.

#### Ortogonalidad

Se refiere al significado de las palabras reservadas o simbolos.
Si una palabra reservada siempre tiene el mismo significado independientemente del
contexto en que se use el lenguaje tiene una mayor ortogonalidad.
Un ejemplo es el signicado de "+" si siempre representa la suma aritimetica es ortogonal,
pero si representa a la suma para variables numéricas y concatenación para strings entonces
es menos ortogonal.
Un lenguaje con caracteristicas ortogonales, nos da la facilidad de aprenderlo mas rapido, ya que existen menos excepciones y casos
especiales para tener en cuenta
* Ortogonalidad en Python.
**Python** y **Processing** provee una gran cantidad de palabras reservadas que nos permite utilizarlas en cualquier momento
y siempre tener el mismo resultado, aunque posee algunas excepciones como en caso mencionado con el caracter "+"

**B. Defina y compare diferentes aspectos de la sintáxis que Ud. considere. Ejemplifique.**

A continuación vamos a comparar los tipos de sintáxis entre los lenguajes utilizando de ejemplo una iteración, donde
se almacene el resultado de la suma entre los 10 primeros números, comenzando por el 1.

Ejemplo de for en Python
```python
suma = 0
for numero in range(1, 10+1):
  suma += numero
```

Ejemplo de for en Processing
```processing
int suma = 0;
for(int numero = 1; numero <= 10; numero++) {
  suma += numero
}
```
En Python se utiliza la palabra reservada **for** al igual que en Processing,
las diferencias radican en cómo se contruye la condicion de fin y de la forma en que
estos lenguajes identifican el bloque de iteración.

En el primer ejemplo el for se construye de la forma
"**para cada** elemento **dentro** de una coleccion **repetir bloque**", los 
dos puntos luego de la condición marcan el comienzo del bloque
a ejecutar, si cuenta con más de una línea esta se escribe 
indentado por 4 espacios una debajo de la otra. Mientras que en el
segundo ejemplo la condición la podemos dividir en 3 pasos: 
el primero se declara una variable de inicio al loop, en el segundo
paso se encuentra la verificación de la condición (si nuestra variable
de inicio cumple con el valor de corte) y por último se incrementa la 
variable de inicio. La condición siempre se encuentra entre paréntesis
y el bloque de cédigo entre llaves **{ bloque }**
al loop 

**Tipos de sintáxis:**

* Abstracta: Mismas estructuras donde ambos lenguajes tienen la misma
estructura **for** condición bloque.

* Concreta: Diferencias léxicas. La condicion en Python se define entre
la palabra reservada **for** y los dos puntos mientras que en Processing debe estar dentro de los paréntesis, la suma y asignación se
escribe de la misma manera y por último se puede observar que en Processing
es necesario definir el tipo de la variable mientras que en Python no.

* Pragmática: Dentro del contexto de estos ejemplos planteados se comprende
mejor el primer ejemplo donde vemos que el bloque for se itera dentro de un rango,
mientras que en el segundo depende de una condición de corte.

**C. Enuncie y compare distintos aspectos semánticos (tanto de la semántica estática y dinámica)
de cada uno de los lenguajes asignados.**

Analizaremos los siguientes puntos desde la perspectiva semántica estática y dinámica,
recurriendo a ejemplos para brindar mayor entendimiento de lo evaluado.

*  Indentación
*  Declaración de variables
*  Tratamiento de excepciones
*  Comentarios
*  Expresiones condicionales (IF)

Teniendo presente el siguiente ejemplo escrito en Python explicaremos los puntos antes mencionados. 

```python
# INICIO PROGRAMA
pares = 0  # linea 1
impares = 0  # linea 2
lista_numeros = [1, 2, 4, 8, 15]  # linea 3
for num in lista_numeros:  # linea 4
  if num % 2 == 0:  # linea 5
    print("Es par")  # linea 6
    pares += 1  # linea 7
  else:  # linea 8
    print("Es Impar")  # linea 9
    impares += 1  # linea 10
print(f"Cantidad de numeros pares: {pares}")  # linea 11
print(f"Cantidad de numeros impares: {impares}")  # linea 12
# FIN PROGRAMA
```

#### Indentación
Dentro del lenguaje Python deben agregarse espacios en blanco (4) al
comienzo de una línea lógica (línea 6), agrupando así un conjunto
de sentencias (líneas 7 y 8 o líneas 9 y 10). 
De esta forma al asociarlas se ejecutarán conjuntamente. Por ejemplo si
fuesen agrupadas dentro de una sentencia **if** (línea 5) teniendo 
un significado durante ejecución diferente si no estuviesen indentadas;
caso donde se produciría un error al interpretar el código.
La escritura incorrecta de una indentación (línea 10) podría cambiar el sentido
lógico de un programa definido dando como resultado números impares tantos como
hayan definidos en la variable "lis", por lo tanto en este sentido la 
característica de indentación en el lenguaje puede tener
efecto tanto en semántica estática como dinámica. 
Estática ya que como bien mencionamos el significado no es el mismo
y dinámico porque el resultado en ejecución en caso del ejemplo presentado,
no produciría una correcta salida de la intención propuesta en la lógica del programa.

En Processing la indentación y los espacios en blanco en general no tiene ningun
efecto sintactico ni semantico, los siguientes dos ejemplos de código
producen exactamente el mismo resultado:

```processing
// ejemplo a:
int x = 50;
if (x > 100) {
    line(20, 20, 80, 80);
} else {
    line(80, 20, 20, 80);
}

// ejemplo b:
int x = 50;
if (x > 100) {
line(20, 20, 80, 80);
} else {                    
line(80, 20, 20, 80);
}
```

Python no aplica esta característica al ser un lenguaje dinámicamente tipado,
es decir, que una variable puede cambiar su tipo de dato almacenado sin restricción.
No hay una sintaxis definida para tal característica.
Podemos destacar que al cambiar el tipo de valor almacenado en ejecución sucede
una modificación a nivel puntero de la zona de memoria que contendrá este valor.

Processing es fuertemente tipado, además el tipado es estático, es decir, 
una vez que se le asigna un tipo a una variable no puede ser modificado
en subsiguientes líneas de código.

#### Tratamiento de excepciones
* Manejo de excepciones en Python.
```python
try:
  numero1 = input("Numero 1")
  numero2 = input("Numero 2")
  division = numero1 % numero2
  print(f"Resultado de dividir {numero1} % {numero2} es {division}")
except ZeroDivisionError:
  print("Division por cero erronea")
finally:
  print("finalizó el programa")
```
	
Son construidas en base a la característica de la indentación tratada anteriormente.
Su implicancia en la semántica estática se produce por la generación de indentaciones construidas
correctamente para dar sentido lógico al programa.
En otro caso en tiempos de ejecución se obtendría el resultado o efecto (semántica dinámica) no deseado,
como ser una operación matemática no necesaria.

Processing también utiliza la sentencia **try** para definir el bloque de código dentro del
cual se quiere manejar la excepción, y **catch** para definir el código que debe
ejecutarse si la excepción se ocurre.

* Manejo de excepciones en Processing
```processing
BufferedReader reader;
String line;
 
void setup() {
  // Open the file from the createWriter() example
  reader = createReader("positions.txt");    
}
 
void draw() {
  try {
    line = reader.readLine();
  } catch (IOException e) {
    e.printStackTrace();
    line = null;
  }
  if (line == null) {
    // Stop reading because of an error or file is empty
    noLoop();  
  } else {
    String[] pieces = split(line, TAB);
    int x = int(pieces[0]);
    int y = int(pieces[1]);
    point(x, y);
  }
}
```

#### Comentarios

* Comentarios en Python

Dentro del lenguaje Python simplemente tendrán significado semántico pudiendo
ser de ayuda para el lector del código fuente, sin embargo su agregado
no produce ningún impacto a nivel ejecución lógico del programa ya que su
definición misma le indica al intérprete que no debe ser ejecutada como parte del programa.

```python
# Comentario para una sola lina
contador = 0  # inicializa variable contador

"""
Esto es un Comentario de muchas lineas
generalemte se utillizan como docstrings
de las funciones como una minuma ayuda de que parametros recibe y 
que parametros retorna...
"""
```

* Comentarios en Processing

Los comentarios funcionan de la misma manera y se pueden incluir de tres formas: 
```processing
// para comentar el resto de la linea.

/* 
 para abrir y cerrar un comentario de varias líneas.
 COMENTARIO
 COMENTARIO
*/
/**
 para abrir y cerrar un comentario de documentación.
*/
```

#### Expresiones condicionales (IF)
En **Python** se evalúan tanto los operadores como operandos involucrados en la sentencia,
tomando un camino u otro según el resultado lógico obtenido.
Su impacto puede apreciarse en ambas semánticas tal como vimos con
el ejemplo anterior de números pares/impares.
Las formas válidas de construir una expresión condicional nos permitirán
tener complejas evaluaciones que en tiempo de ejecución nos permitirán ejecutar
ciertas porciones de código específico llegando muy posiblemente a un final de
programa diferente según el camino tomado.

En **Processing** el condicional IF funciona de la misma manera,
pero requiere que el valor a evaluar esté entre paréntesis.

**D. Defina una porción de código donde pueda apreciarse las características más relevantes de las variables en cuanto a sus atributos. Elija alguno de los lenguajes asignados que presente mayores posibilidades para mostrar estas características y desarrolle el ejercicio de la misma forma que se realiza en la práctica. Luego, si es necesario realice las explicaciones que permitan una mayor comprensión del ejercicio.**

COMPLETARRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRR

**E. Mencione y compare entre ambos lenguajes los diferentes tipos de parámetros y características de su implementación**

#### Python

Por omisión los parámetros se pasan de forma posicional aunque también se pueden usar parámetros nombrados.
Son objetos los que se pasan como parámetro, los objetos simples, "inmutables", se pasan por valor y los objetos complejos, "mutables", por referencia.

#### Pasaje por valor

Cuando se pasa un objeto simple o inmutable, se pasa una copia del parámetro actual, los cambios que se hagan dentro de la función no afecta a la copia original. Ejemplo:

```python
def doble(numero):
    numero *= 2
    print(numero)

i=1
doble(i)
print(i)
```

> **Salida: 2 1**

El tipo del parámetro formal no se declara, se confía en que el objeto que se pasa a la función va a poder responder a los métodos que se especifican dentro de la función.

#### Pasaje por referencia

Cuando se pasa un objeto complejo o mutable, se envía por referencia el objeto que está en el ambiente del llamador, los cambios dentro de la función se hacen sobre el mismo objeto. Ejemplo:

```python
def doble(numeros):
    for i,n in enumerate(numeros):
        numeros[i] *= 2
    print(numeros)
        
numeros=[1,2,3]
doble(numeros)
print(numeros)
```

> **Salida: [2,4,6] [2,4,6]**

#### Pasaje nombrados

```python
def saludo(mensaje, nombre):
     print(mensaje + " " + nombre)
   
saludo(nombre="Juan", mensaje="Hola")
```

> **Salida: Hola Juan**

#### Pasaje por omisión

En la definición de la función, primero deben declararse los parámetros comunes, y luego los parámetros por omisión.

```python
def saludo(mensaje, nombre="Juan"):
     print(mensaje + " " + nombre)
   
saludo("hola")
```

> **Salida: Hola Juan**

#### Processing

Tiene las mismas limitaciones que tiene Java al respecto del pasaje de parámetros. El pasaje de parámetros se hace de forma posicional. No existen los parámetros nombrados o por omisión.
La declaración de los parámetros formales requieren que se especifique el tipo. Los tipos de los parámetros actuales tienen que coincidir con los tipos de los parámetros formales, de lo contrario da error.
Además el único mecanismo contemplado es el paso por copia de valor pero como las variables de tipos no primitivos son todas referencias a variables anónimas en la heap, el paso por valor de una de estas variables constituye en realidad un paso por referencia de la variable.

* Parámetro de tipo primitivo, el pasaje es por valor
```processing
void tripleDiameter(float diam) {
  diam *=3;
}

void setup(){
size(300, 300);
background(0, 200, 0);
int circleX = 50;
int circleY = 50;
int diameter = 50;
fill(255, 0, 0);
ellipse(circleX, circleY, diameter, diameter);
tripleDiameter(diameter);
ellipse(circleX+100, circleY+100, diameter, diameter);
}
```

* Parámetro de tipo no primitivo (arreglo), el pasaje es por referencia
```processing
void tripleDiameter(float args[]) {
  args[2] *=3;
}

void setup(){
size(300, 300);

background(0, 200, 0);
float[] params= new float[3];
params[0] = 50;
params[1] = 50;
params[2] = 50;
fill(255, 0, 0);
ellipse(params[0], params[1], params[2], params[2]);
tripleDiameter(params);
ellipse(params[0]+100, params[1]+100, params[2], params[2]);
}
```

**F. Analice y explique la fortaleza del sistema de tipos de cada uno de los lenguajes asignados**

#### Python

Al almacenar datos en una variable lo que podemos hacer con ella dependerá del tipo de dato al cual pertenezca. Ejemplificando esto:

```python
10 + 25
"10" + "25"
```

> **Salida: 35 '1025'**

Podemos notar que la diferencia radica en la utilización de las comillas, es decir, el lenguaje detecta esto y procesa los datos de forma tal que las operaciones que pueden realizar son dependientes de este símbolo. 
Conocer los tipos de datos que provee cada lenguaje entonces es útil para conocer las diferentes operaciones que podamos realizar con ellos.
Python es un lenguaje de tipado dinámico (a cada variable o identificador se le asocia o liga en tiempo de ejecución un tipo de dato) y fuerte (cada tipo define un conjunto restrictivo de operaciones posibles que puede realizarse con ellos). En este último caso en Python no es necesario declarar el tipo de dato de forma explícita sino que se infiera dentro del contexto.
Siendo fuertemente tipado permite reducir los errores generados por parte del desarrollador, por ejemplo al querer obtener por consola el resultado de una operación aritmética sin convertir este valor a una cadena de texto se producirá un error en compilación. Por otra parte al ser dinámico no solo permite escribir programas a mayor velocidad (dado que no es necesario declarar tipos, tanto sea en las variables como en las firmas de métodos) sino que es posible comprobar en tiempo de ejecución el tipo de dato de la línea en ejecución y así “asociar” a ella el conjunto de operaciones posibles. 
Respecto a la conversión de datos en tanto que el programa funcione de forma correcta es necesario realizarlo de manera explícita por el desarrollador ya que de otra forma esto producirá un error y posteriormente la finalización del programa si es que no se cuenta con ningún manejador de excepciones, el ejemplo clásico de esta situación es la salida por consola de un valor numérico sin antes convertirlo en una cadena de caracteres.
Los tipos básico del lenguaje en sus distintas versiones (2.x o 3.x) son:

#### Estándar
*  Booleano
*    Numéricos
*    Cadena de caracteres
*    Secuencias
*    Diccionarios
*    Conjuntos
#### Definidos por el usuario
*    Clases

Pueden crearse tipos donde uno incluya a otro, es decir, tener lo siguiente:

```python
fichas = ['negro', 'blanco']
col_primarios = ['azul','amarillo','rojo']
col_secundarios = ['verde','naranja']
for numero in range(7):
    fichas.append(numero)
fichas.append(True)
fichas.append(col_secundarios)
print(fichas)
```
> **Salida: ['negro', 'blanco', 0, 1, 2, 3, 4, 5, 6, True, ['verde', 'naranja']]**

Si bien el ejemplo plantea la versatilidad de un tipo de dato específico como lo son las listas, podemos notar que este no está definido por el usuario sino que su característica o extensibilidad nos permite almacenar en él cualquier otro tipo de dato. En contraposición a este caso las clases si son datos definidos por el usuario basándose en tipos de datos primitivos o estándares como los mencionados, aunque bien podrían contener datos pertenecientes a otras clases y así sucesivamente, pero en definitiva y en última instancia habrá un dato estándar. Las clases también nos brindan la posibilidad de realizar operaciones mediante la utilización de métodos, los cuales accediendo a sus datos realizan lo necesario por cada funcionalidad. Por ejemplo:

```python
class Persona:
    def __init__(self, n, a, e):
        self.nombre = n
        self.apellido = a
        self.edad = e
     
    def print_minombre(self):
        print(self.nombre)
         
    def print_miedad(self):
        print(self.edad)

juan = Persona("Juan", "Perez", 23)
juan.print_minombre()
juan.print_miedad()
```
> **Salida: Juan 23**

#### Processing

Los tipos de datos se encuentran divididos en dos grandes categorías: primitivos y compuestos

#### Primitivos
*    Booleano
*    Numéricos (enteros, flotantes, bytes, etc)
#### Compuestos
*    Arreglos
*    Objetos
*    Tablas
*    Cadena de caracteres
*    etc

Al igual que Python y siendo Processing un framework basado principalmente en el lenguaje Java comparte muchas de sus características en cuanto a restricciones en las operaciones posibles que pueden aplicarse sobre cada tipo.
Además de lo mencionado también se reconoce al lenguaje como de tipado fuerte y estático. Esta última característica es quizás una de las diferencias más notables sobre lenguajes como Python. Como ya hemos mencionado, que sea fuertemente tipado indica que es necesario declarar el tipo de dato para cada variable y en este lenguaje debe ser explícita esta declaración. Por ejemplo:

```processing
boolean puertaAbierta = false;
```

Como bien se sabe esta característica reserva en una porción de la memoria de datos un espacio de tamaño predeterminado por el tipo de dato declarado, además de mantener el identificador asociado al valor actual en el momento que se lo invoque (al instanciar la variable sin asignar valor, seguramente contenga “null”, “nil” o cualquier representación que indique “basura” dentro del programa)
En el tipado estático la comprobación de los tipos se realiza al momento de la compilación, capacidad que difiere respecto a Python que realiza esto al momento de ejecución.

Ejemplo de declaración de un objeto y un posible uso

```processing
HLine h1 = new HLine(20, 2.0); 
HLine h2 = new HLine(50, 2.5); 
 
void setup() 
{
  size(200, 200);
  frameRate(30);
}

void draw() { 
  background(204);
  h1.update(); 
  h2.update();  
} 
 
class HLine { 
  float ypos, speed; 
  HLine (float y, float s) {  
    ypos = y; 
    speed = s; 
  } 
  void update() { 
    ypos += speed; 
    if (ypos > height) { 
      ypos = 0; 
    } 
    line(0, ypos, width, ypos); 
  } 
}
```

Podemos concluir que Python con su dinamismo en cuanto a tipado es más lento en ejecución ya que debe interpretar instrucción por instrucción para conocer las restricciones que se aplican a los elementos o variables implicadas en una sentencia, pero tiene como ventaja la velocidad de escritura por parte del programador ya que no necesita indicar los tipos a los que pertenecen sus datos. Por otra parte Processing lleva ventaja en el tiempo de ejecución final de un programa al realizar una sola compilación y luego ejecución de lo compilado (cuestión que trae aparejado el necesitar espacio adicional donde almacenar el código compilado) y es más restrictivo al tener que declarar por cada tipo a que clase de dato pertenece.

**G. Enuncie las características más importantes del manejo de excepciones que presentan los lenguajes asignados

Una excepción es un acontecimiento que ocurre durante la ejecución de un programa y que interrumpe el flujo normal de las instrucciones del programa. Algunos lenguajes no presentan mecanismos para el manejo de excepciones como Pascal, en estos casos se pueden simular este manejo de excepciones con otros recursos.
Ejemplo de excepciones:
  
*  Abrir un archivo que no existe
*  Acceder a una clave de un diccionario que no existe
*  Invocar un método que no existe
*  Dividir por cero

#### Python

* Manejo de excepciones

```python
try:
  sentencia 1
  ...
  sentencia n
except nombre-de-la-except-1:
  sentencias
except nombre-de-la-except-2:
  sentencias
else:
  sentencias
finally:
  sentencias
```
Dentro de la cláusula **except** se pueden manejar varias excepciones *except(exp-1, exp-2)*. Las cláusulas **else** y **finally** son opcionales, si no aparece ninguna excepción para ser manejada se ejecuta el código dentro de la sección **else** y si existe declarado **finally** sea cual sea el flujo siempre se ejecutará el código dentro de esta cláusula.
Es importante indagar sobre la forma de propagación que utilizan los lenguajes, es decir, qué sucede cuando no se encuentra un manejador para la excepción levantada, ¿dónde se busca quién maneje la excepción?. En Python primero se busca estáticamente, termina el bloque interno y busca en el bloque que lo contiene. Ejemplo:

```python
dic = {1: 'Mariano', 2: 'Juan', 3: 'pedro'}
y = 0
try:
  try:
    for x in range(1, 6):
      print(dict[z])
  except(KeyError):
    dict[x] = "agregado"

  y = y + 1
  print("el valor de y es:" + str(y))

except(NameError):
  print("se esta usando una variable que no existe')

print('se sigue con la siente sentencia del programa')
```

Este código produce un error de tipo **NameError** variable no definida que no es manejada por el bloque try interno pero **si es manejado** por el bloque try que lo contiene.
En el siguiente ejemplo vamos a demostrar que Python aplica el mecanismo de terminación.

```python 
def elemento(x):
  dic = {'art1': "mesa", 'art2': "silla", 'art4': "sillon"}
  try:
    return dict[x]
  except NameError:
    x = 'art1'

elem = input('ingrese clave para acceder al diccionario:')
try:
  print("el valor del elemento : "+ str(elem) + "es: " + str(elemento(elem)))
except KeyError:
  print('ojo! : entro una clave inexistente. pruebe de nuevo!')
```
Ingresando una clave que no tiene el diccionario se produce un error dentro de la función **elemento** y al no manejarse allí la excepcion y al no encontrar un manejador para esa excepción bajo dinamicamente a quien lo llamó, i no se encuentra un manejador se aborta el programa en este caso particular.
En Python también es posible levantar excepciones explícitamente. Ejemplo:

```python
try:
  for x in range(1,6):
    if x == 2 or x == 3:
      raise KeyError
    else:
      print(dic[x])
except(KeyError)
  dict[x] = 'nuevo'
```
El programa controla que exista la clave y en caso contrario explícitamente levanta la excepción con la sentencia **raise**

Excepciones predefinidas (Built-in Python)
* EOFError: errores de EOF
* ImportError: error con importaciones de módulos
* IndexError: error por índice fuera de rango
* KeyError: error por nombre no encontrado
* SyntaxError: error por problemas sintácticos
* ZeroDivisionError: error por división por cero

También se pueden definir nuevas excepciones definiendo clases que deriven de **Exception**.

#### Processing

```processing
try {
  tryStatements
} catch (exception) {
  catchStatements
}
```

tryStatements si el codigo puede llegar a lanzar una excepcion, despues se ejecuta las líneas dentro de "catch"
exception exception java que fue raiseada
catchStatement código que maneja la excepción

**H. Conclusión sobre los lenguajes: Realice una entrevista a un usuario/s experimentado de los lenguajes asignados con el fin de obtener una opinión acerca del lenguaje respecto de los temas tratados en el trabajo. Esta conclusión no debe superar una carilla**

#### Processing

**  ¿Considera que la sintaxis del lenguaje permite mantener un buen grado de legibilidad de código?
**  ¿Qué ventajas/desventajas puede nombrar sobre la utilización de variables globales dentro de su código fuente?
**  ¿Los tipos de datos ofrecidos en el lenguaje pueden ser extendidos fácilmente y así crear nuevos?
**  ¿Qué dificultades o desventajas frente a otros lenguajes encuentra al momento de realizar pasaje de parámetros?
**  ¿Considera como concepto de seguridad el hecho de que una variable conozca su tipo de dato antes de la ejecución del programa?

> **Sin respuesta**

#### Python

**  ¿Que ventajas/desventajas tiene el lenguaje al ser interpretado contra los lenguajes compilados?
**  ¿Al ser un lenguaje de tipado dinámico el código es menos legible?
**  ¿Encuentra alguna dificultad o desventaja con que sea fuertemente tipado?
**  ¿Cuando empezó a trabajar en Python que fue lo que más le intereso del lenguaje?
**  A la hora de encarar un nuevo proyecto con más personas de distintos niveles (desde principiantes a avanzados) ¿elegiría éste u otro lenguaje, ¿porque?
**  ¿Considera una desventaja que el lenguaje sea multiparadigma?

> **Sin respuesta**

**I. Conclusión sobre el trabajo: Realice una conclusión mencionando los aportes que le generó la realización del trabajo en comparación con sus conocimientos previos de los lenguajes asignados**

COMPLETARRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRRR
