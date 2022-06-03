# Classe abstrata

Suponha que temos uma classe chamada `Shape`. Essa classe tem uma função `area()` para calcular a área da forma. Agora queremos que cada classe filha implemente esta função `area()` para calcular suas respectivas áreas. Em vez de fornecer o corpo do método `area()` na classe `Shape`, podemos marcá-lo como `abstract`.

Ao marcá-lo como abstrato , garantimos o seguinte:

- Agora, não há necessidade de fornecer o corpo da definição da função area() na classe Shape.
- A classe filha deve substituir esta função `area()` e fornecer sua própria implementação, caso contrário o compilador dará erro.

Então, se classes como `Square`, `Rectangle`, `Circle`, etc herdam a classe `Shape`, essas classes devem substituir a função `area()`, caso contrário o compilador lançará um erro.


## Classe abstrata

Se qualquer função de uma classe estiver marcada com a palavra-chave `abstract`, a classe também deve ser marcada com a palavra-chave `abstract`. Vamos primeiro ver um exemplo básico de uma classe abstrata:

```kotlin runnable
abstract class Shape{
    abstract fun area()
}

class Square: Shape() {
    override fun area() {
        println("Área do quadrado: side*side")
    }
}

class Circle: Shape() {
    override fun area() {
        println("Área do círculo: 3.14*r*r")
    }
}

fun main() {
    val square = Square()
    val circle = Circle()
    square.area()
    circle.area()
}
```

Neste exemplo, criamos uma classe abstrata `Shape`. A classe `Square` e a classe `Circle` herdam a classe `Shape` e sobrepõem o método `area()`.

Vamos discutir alguns pontos importantes sobre a classe abstrata:

- Se uma classe tem uma propriedade abstrata ou função abstrata, então a classe deve ser marcada como abstrata.
- Uma classe abstrata não pode ser instanciada. Isso significa que não podemos criar objeto de uma classe abstrata.
- Não há necessidade de adicionar a palavra-chave `open` em classes abstratas, pois elas devem ser herdadas e, portanto, abertas por padrão.
- Uma classe abstrata pode ter funções e propriedades abstratas e não abstratas (normalmente definidas).
- Uma função abstrata não tem corpo.
- Na classe abstrata, por padrão, todos os membros são não abstratos. Precisamos adicionar a palavras-chave `abstract` para torná-los abstratos.

Vejamos um exemplo ilustrando os pontos acima:

```kotlin runnable
abstract class Shape{
    abstract var sides: Int
    abstract fun area()

    fun sayShape(){
        println("É uma forma...")
    }
}

class Square: Shape() {
    override var sides: Int = 4
    override fun area() {
        println("Área do quadrado: side*side")
    }
}

class Circle: Shape() {
    override var sides: Int = 0
    override fun area() {
        println("Área do círculo: 3.14*r*r")
    }
}

fun main() {
    val square = Square()
    val circle = Circle()
    println("Lado do quadrado: ${square.sides}")
    println(Lado do círculo: ${circle.sides}")
    square.area()
    circle.area()
    square.sayShape()
    circle.sayShape()
}
```

# Interface Kotlin

As interfaces no Kotlin são semelhantes às classes abstratas com algumas diferenças importantes.

Uma interface pode ser considerada como uma classe totalmente abstrata. Isso significa que, por padrão, todas as funções e propriedades de uma interface são abstratas.

Uma interface é usada para definir o blueprint de uma classe, o que significa que podemos fornecer os nomes da função junto com a declaração completa da função, incluindo seus argumentos e tipo de retorno em uma Interface e quando qualquer classe implementar essa Interface, então essa classe terá que fornecer a definição para essas funções.

Antes do Java 8, apenas a declaração de função era permitida em interfaces. Não era possível definir o corpo de funções nas interfaces. Mas a partir do Java 8, temos a funcionalidade de adicionar o corpo da função também. Kotlin por padrão fornece esse recurso. Assim, em Kotlin, funções também podem ter um corpo em interfaces.

Isso torna as interfaces e classes abstratas muito semelhantes. A principal diferença entre classe abstrata e interface é: uma classe pode herdar apenas uma classe abstrata, mas pode herdar muitas interfaces. Se houver necessidade de herdar mais de uma classe, podemos optar por interfaces.

## Interface Kotlin

A sintaxe para definir uma interface em Kotlin é:

```kotlin
interface A{
    var x:Int       // abstract property
    fun sayHello()  // asbtract method
    fun sayBye(){   
        // Default implementation of sayBye()
    }
}
```

Por padrão, todas as propriedades e funções das interfaces são abstratas, a menos que forneçamos sua implementação.

## Implementando interfaces

As interfaces também são herdadas usando o mesmo `:` operador que é usado para herdar uma classe. Vamos criar uma classe `C` que herda as interfaces `A`e `B`:

```kotlin runnable
// first interface
interface A{
    fun sayHelloByA()
    fun sayByeByA(){
        println("Bye from A....")
    }
}
// second interface
interface B{
    fun sayHelloByB()
    fun sayByeByB(){
        println("Bye from B....")
    }
}
// class implementing first and second interface
class C: A,B{
    override fun sayHelloByA() {
        println("Hello from overridden A....")
    }

    override fun sayHelloByB() {
        println("Hello from overridden B....")
    }
}
```

Neste exemplo, ambas as interfaces `A` e `B`possuem duas funções: uma é abstrata e outra com implementação padrão. A classe `C` herda ambas as interfaces e substitui suas funções abstratas.

Vamos criar o objeto da classe `C`e chamar suas funções:

```kotlin runnable
fun main() {
    val c = C()
    c.sayHelloByA()
    c.sayHelloByB()
    c.sayByeByA()
    c.sayByeByB()
}
```

## E se duas interfaces têm a mesma função?

Suponha que interface `A` e interface `B` tenham uma função nomeada `sayHello()` com implementações padrão. Agora, se a classe `C` herdar ambas as interfaces `A` e `B`, haverá um conflito. A classe `C` dará um erro:

```kotlin runnable
interface A{
    fun sayHello(){
        println("Hello from A....")
    }
}
interface B{
    fun sayHello(){
        println("Hello from B....")
    }
}
class C: A,B {      // Error
    
}
```

É porque a classe `C` obteve implementações do método `sayHello()` da interface `A` e do `B`. Para resolver esse conflito, a classe `C` deve substituir o método `sayHello()` e fornecer sua implementação:

```kotlin runnable
interface A{
    fun sayHello(){
        println("Olá de A....")
    }
}
interface B{
    fun sayHello(){
        println("Olá de B....")
    }
}
class C: A,B {
    override fun sayHello() {
        println("Olá de C....")
    }
}

fun main() {
    val c = C()
    c.sayHello()
}
```

## Chamar a implementação de A ou B:

Em vez de fornecer nossa própria implementação, se quisermos chamar a implementação de `A` ou de `B` de `sayHello()`, podemos chamá-la usando a palavra-chave `super` e o nome da interface, assim:

```kotlin runnable
interface A{
    fun sayHello(){
        println("Olá de A....")
    }
}
interface B{
    fun sayHello(){
        println("Olá de B....")
    }
}
class C: A,B {
    override fun sayHello() {
        super<A>.sayHello()
        super<B>.sayHello()
    }
}

fun main() {
    val c = C()
    c.sayHello()
}
```
