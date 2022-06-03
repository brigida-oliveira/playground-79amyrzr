# Classe abstrata Kotlin

No último tutorial discutimos sobre herança. Daremos um passo à frente e discutiremos sobre classes abstratas em Kotlin agora.

Suponha que temos uma classe chamada Shape. Tem uma função area()para calcular a área da forma. Agora queremos que cada classe filha implemente esta area()função para calcular suas respectivas áreas. Em vez de fornecer o corpo do area()método na Shapeclasse, podemos marcá-lo como abstract.

Ao marcá-lo como abstrato , garantimos o seguinte:

Agora, não há necessidade de fornecer o corpo da definição da area()função na Shapeclasse.

A classe filha deve substituir esta area()função e fornecer sua própria implementação, caso contrário o compilador dará erro.

Então, se classes como Square, Rectangle, Circleetc. herdam Shapea classe, essas classes devem substituir area()a função, caso contrário o compilador lançará um erro.


Classe abstrata Kotlin
Se qualquer função de uma classe estiver marcada com abstractpalavra-chave, a classe também deve ser marcada com palavra- abstractchave. Vamos primeiro ver um exemplo básico de uma classe abstrata:

abstract class Shape{
    abstract fun area()
}

class Square: Shape() {
    override fun area() {
        println("Area of square: side*side")
    }
}

class Circle: Shape() {
    override fun area() {
        println("Area of circle: 3.14*r*r")
    }
}

fun main() {
    val square = Square()
    val circle = Circle()
    square.area()
    circle.area()
}

Área do quadrado: lado*lado 
Área do círculo: 3,14*r*r

Neste exemplo, criamos uma classe abstrata Shape. A Squareclasse e Circlea classe herdam a classe Shape e sobrepõem o area()método.

Vamos discutir alguns pontos importantes sobre a classe abstrata:

Se uma classe tem uma propriedade abstrata ou função abstrata, então a classe deve ser marcada como abstrata.

Uma classe abstrata não pode ser instanciada . Isso significa que não podemos criar objeto de uma classe abstrata.

Não há necessidade de adicionar a palavra-chave open em classes abstratas, pois elas devem ser herdadas e, portanto, abertas por padrão.

Um resumo pode ter funções e propriedades abstratas e não abstratas (normalmente definidas).

Uma função abstrata não tem corpo.

Na classe abstrata, por padrão, todos os membros são não abstratos. Precisamos adicionar abstractpalavras-chave para torná-los abstratos.

Vejamos um exemplo ilustrando os pontos acima:

abstract class Shape{
    abstract var sides: Int
    abstract fun area()

    fun sayShape(){
        println("It is a shape...")
    }
}

class Square: Shape() {
    override var sides: Int = 4
    override fun area() {
        println("Area of square: side*side")
    }
}

class Circle: Shape() {
    override var sides: Int = 0
    override fun area() {
        println("Area of circle: 3.14*r*r")
    }
}

fun main() {
    val square = Square()
    val circle = Circle()
    println("Side of square: ${square.sides}")
    println("Side of Circle: ${circle.sides}")
    square.area()
    circle.area()
    square.sayShape()
    circle.sayShape()
}

Lado do quadrado: 4 
Lado do círculo: 0 
Área do quadrado: lado*lado 
Área do círculo: 3,14*r*r 
É uma forma... 
É uma forma...

# Interface Kotlin

Neste tutorial, aprenderemos sobre as Interfaces Kotlin . As interfaces no Kotlin são semelhantes às classes abstratas com algumas diferenças importantes.

Uma interface pode ser considerada como uma classe totalmente abstrata . Isso significa que, por padrão, todas as funções e propriedades de uma interface são abstratas .

Uma interface é usada para definir o blueprint de uma classe , o que significa que podemos fornecer os nomes da função junto com a declaração completa da função, incluindo seus argumentos e tipo de retorno, em uma Interface e quando qualquer classe implementar essa Interface, então isso classe terá que fornecer definição para essas funções.

Antes do Java 8, apenas a declaração de função era permitida em interfaces . Não foi possível definir o corpo de funções nas interfaces. Mas no Java 8 , temos a funcionalidade de adicionar o corpo da função também . Kotlin por padrão fornece esse recurso. Assim, em Kotlin, funções também podem ter um corpo em interfaces .

Isso torna as interfaces e classes abstratas muito semelhantes. A principal diferença entre classe abstrata e interface é: uma classe pode herdar apenas uma classe abstrata, mas pode herdar muitas interfaces . Se houver necessidade de herdar mais de uma classe, podemos optar por interfaces.

Interface Kotlin
A sintaxe para definir uma interface em Kotlin é:


interface A{
    var x:Int       // abstract property
    fun sayHello()  // asbtract method
    fun sayBye(){   
        // Default implementation of sayBye()
    }
}
Por padrão, todas as propriedades e funções das interfaces são abstratas, a menos que forneçamos sua implementação.

Kotlin: implementando interfaces
As interfaces também são herdadas usando o mesmo :operador que é usado para herdar uma classe. Vamos criar uma classe Cque herda interfaces Ae B:

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
Neste exemplo, ambas as interfaces Ae Bpossuem duas funções : uma é abstrata e outra com implementação padrão. A classe Cherda ambas as interfaces e substitui suas funções abstratas.

Vamos criar o objeto da classe Ce chamar suas funções:

fun main() {
    val c = C()
    c.sayHelloByA()
    c.sayHelloByB()
    c.sayByeByA()
    c.sayByeByB()
}

Olá de substituído A.... 
Olá de substituído B.... 
Tchau de A.... 
Tchau de B....

Se duas interfaces têm a mesma função?
Suponha que interface Ae interface Btenham uma função nomeada sayHello()com implementações padrão. Agora, se a classe herdar Cambas as interfaces A, haverá um conflito . A classe dará um erro:BC

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

Erro:(11, 1) Kotlin: A classe 'C' deve substituir a diversão aberta pública sayHello(): Unidade definida em A porque herda vários métodos de interface dela

É porque a classe Cobteve implementações do método sayHello()da interface Ae do B. Para resolver esse conflito, a classe Cdeve substituir o sayHello()método e fornecer sua implementação:

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
class C: A,B {
    override fun sayHello() {
        println("Hello from C....")
    }
}

fun main() {
    val c = C()
    c.sayHello()
}

Olá de C....

Chama a implementação de A ou B:
Em vez de fornecer nossa própria implementação, se quisermos chamar a implementação de A's ou B's sayHello(), podemos chamá-la usando a superpalavra-chave e o nome da interface, assim:

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

Olá de A.... 
Olá de B....
  
# Kotlin aninhado e classe interna

Neste tutorial, discutiremos as duas maneiras de criar uma classe dentro de outra classe em Kotlin, a primeira é a classe Aninhada Kotlin e a outra é a classe Kotlin Inner .

Classe aninhada Kotlin
Podemos criar uma classe aninhada dentro de outra classe diretamente. Por padrão, as classes aninhadas são estáticas por natureza. Isso significa que podemos usar as propriedades e funções da classe aninhada sem criar um objeto da classe externa. Eles podem ser acessados ​​diretamente usando o .operador.

Na classe aninhada:

Dentro de uma classe aninhada, não podemos acessar membros da classe externa (Animal).

Os membros de classe aninhados são acessados ​​diretamente usando .o operador sem criar um objeto da classe externa.

Aqui está a sintaxe para a classe aninhada:

class Outer{
    // Members of Outer class
    class Nested{
        // Members of Nested class
    }
}
e a sintaxe para criar um objeto da classe Nested:


val obj = Outer.Nested()
Podemos criar um objeto da classe aninhada usando o nome da classe externa.

Exemplo de classe aninhada Kotlin:
Vamos dar um exemplo,

class Animal{
    // outer class property
    val legs = 4
    class Dog{
        // nested class proprty
        val say = "Woof"
        val hasTail = true
        fun tail(){
            println("Dog has tail: $hasTail")
        }
    }
}

fun main() {
    // Creating object of nested class directly
    val dog = Animal.Dog()
    // Accessing inner class
    dog.tail()
    println("Dog says: ${dog.say}")
}

Cachorro tem rabo: verdadeiro 
Cachorro diz: Woof

Classe interna Kotlin
A classe Kotlin Inner é criada usando a palavra- innerchave. Ela pode ser considerada como uma classe aninhada especial .

Em uma classe interna:

A classe interna mantém uma instância da classe externa Assim, ela pode acessar membros da classe externa.

Não podemos declarar uma classe interna dentro de uma interface ou classe não interna.


Não podemos criar diretamente um objeto da classe interna. Ele pode ser criado usando o objeto de classe externa.

Aqui está a sintaxe :

class Outer{
    // Members of Outer class
    inner class Inner{
        // Members of Inner class
    }
}
e para criar o objeto da classe interna,

val outerObj = Outer()
// using outer class object to create inner class object
val innerObj = outerObj.Inner()
Como você pode ver na sintaxe acima, primeiro criamos o objeto da classe Outer e depois o usamos para criar o objeto da classe interna.

Exemplo de classe interna Kotlin:
Vamos dar um exemplo,

class Animal{
    // outer class property
    val legs = 4
    inner class Dog{
        // inner class property
        val say = "Woof"
        val hasTail = true
        fun tail(){
            println("Dog has tail: $hasTail")
        }
        fun printLegs(){
            println("No of legs are: $legs")
        }
    }
}

fun main() {
    // Creating object of outer class
    val animal = Animal()
    // Creating object of inner class
    val dog = animal.Dog()
    // Accessing inner class
    dog.tail()
    dog.printLegs()
    println("Dog says: ${dog.say}")

}

Cachorro tem rabo: verdadeiro 
Número de patas são: 4 
Cachorro diz: Woof
