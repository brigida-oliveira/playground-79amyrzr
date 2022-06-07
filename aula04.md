# Classe aninhada Kotlin
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
