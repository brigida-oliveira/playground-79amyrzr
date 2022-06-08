# Classe aninhada e classe interna

## Classe aninhada

Podemos criar uma classe aninhada dentro de outra classe diretamente. Por padrão, as classes aninhadas são estáticas por natureza. Isso significa que podemos usar as propriedades e funções da classe aninhada sem criar um objeto da classe externa. Eles podem ser acessados diretamente usando o operador `.`.

Na classe aninhada:

- Dentro de uma classe aninhada, não podemos acessar membros da classe externa.
- Os membros de classe aninhados são acessados diretamente usando o operador `.` sem criar um objeto da classe externa.

Aqui está a sintaxe para a classe aninhada:

```kotlin
class Exterior{
     // Membros da classe Exterior
     class Aninhada{
         // Membros da classe aninhada
     }
}
```

e a sintaxe para criar um objeto da classe aninhada:

```kotlin
val obj = Exterior.Aninhada()
```

Podemos criar um objeto da classe aninhada usando o nome da classe externa.

**Exemplo de classe aninhada:**

```kotlin runnable
class Animal{
    // outer class property
    val legs = 4
    class Dog{
        // nested class proprty
        val say = "Woof"
        val hasTail = true
        fun tail(){
            println("Cachorro tem rabo: $hasTail")
        }
    }
}

fun main() {
    // Creating object of nested class directly
    val dog = Animal.Dog()
    // Accessing inner class
    dog.tail()
    println("Cachorro diz: ${dog.say}")
}
```

## Classe interna Kotlin

A classe interna é criada usando a palavra-chave ` inner`. Ela pode ser considerada como uma classe aninhada especial.

Em uma classe interna:

- A classe interna mantém uma instância da classe externa. Assim, ela pode acessar membros da classe externa.
- Não podemos declarar uma classe interna dentro de uma interface ou classe não interna.
- Não podemos criar diretamente um objeto da classe interna. Ele pode ser criado usando o objeto de classe externa.

**Sintaxe:**

```kotlin
class Outer{
    // Members of Outer class
    inner class Inner{
        // Members of Inner class
    }
}
```

e para criar o objeto da classe interna,

```kotlin
val outerObj = Outer()
// using outer class object to create inner class object
val innerObj = outerObj.Inner()
```

Como você pode ver na sintaxe acima, primeiro criamos o objeto da classe Externa e depois o usamos para criar o objeto da classe interna.

**Exemplo de classe interna:**

```kotlin
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
```

# Classe de dados 

Em todo projeto precisamos de algumas classes cujo único propósito é armazenar dados. Essas classes são conhecidas como classe de dados ou objetos de acesso a dados ou objetos de transferência de dados, etc.

As classes de dados contêm principalmente:

- variáveis e seus getters e setters,
- construtor,
- algumas funções como `toString()`, `equals()`, `hashCode()`, etc.

Uma classe de dados é criada usando a palavra-chave `data`. A classe de dados em Kotlin por padrão fornece:

- Getters e setters para as propriedades de classe (também verdadeiro no caso de classes normais).
- função `toString()` para imprimir os detalhes do objeto.
- função `copy()`para copiar o conteúdo de um objeto para outro.
- funções `equals()` e `hashCode()` para hashing e comparação.
- funções `componentN()` correspondentes às propriedades em sua ordem de declaração no construtor.

Vamos criar uma classe de dados `Person` em Kotlin:

```kptlin
data class Person(var name: String, var gender: String, var age: Int)
```

E isso é tudo. É um dos grandes exemplos da concisão de Kotlin.

Vamos criar um objeto desta classe e imprimi-lo:

```kotlin runnable
fun main() {
    val man = Person("Ninja", "Male", 18)
    println(man)
}
```

Ao imprimir o objeto, a função `toString()` é chamada. Assim, a partir do exemplo da classe de dados Kotlin, podemos ver como é fácil criar uma classe de dados e usá-la e todas as funções básicas são definidas automaticamente pelo Kotlin.

## Requisitos para uma classe de dados

Para criar uma classe de dados, os seguintes requisitos devem ser atendidos:

- No construtor primário, pelo menos um parâmetro deve estar presente.
- Todos os parâmetros no construtor primário devem ser marcados com `val` ou `var`.
- As classes de dados não podem ser abstratas, abertas, seladas ou internas.


## Copiar propriedades do objeto na classe de dados

Se quisermos criar um novo objeto para qualquer classe de dados em Kotlin, usando algumas propriedades de outro objeto podemos fazer isso usando a função `copy()`:

```kotlin runnable
fun main() {
    val man = Person("Ninja", "Male", 18)
    val woman = man.copy(gender = "Female")
    println(man)
    println(woman)
}
```

Quando usamos uma função `copy()` para copiar um único valor de propriedade de qualquer objeto, devemos usar argumentos nomeados, caso contrário o valor pode ser atribuído a outra variável.

## Classe de dados Kotlin: funções `hashCode` e `equals`

As funções `equals()` e `hashCode()` são usadas para verificar se dois objetos são iguais ou não. O `hashCode()` gera o valor hash de um objeto. Os valores hash de dois objetos são iguais se todos os valores correspondentes de dois objetos forem iguais. A função `equals()` também é usada para verificar se dois objetos são iguais.

Vamos dar um exemplo de código:

```kotlin
fun main() {
    val man = Person("Ninja", "Male", 18)
    val manNew = Person("Ninja", "Male", 18)
    val woman = man.copy(gender = "Female")
    if (man.hashCode() == manNew.hashCode())
        println("man and manNew are equal")
    if (man.hashCode() == woman.hashCode())
        println("It will not be printed")
    if (man.equals(manNew))
        println("man and manNew are equal")
    if (man.equals(woman))
        println("It will not be printed")
}
```

## Desestruturando o objeto da classe de dados - função `componentN()`

Em Kotlin podemos destruir um objeto e obter suas propriedades em variáveis independentes usando a declaração de desestruturação. Vamos destruir o objeto `man` em variáveis independentes:

```kotlin
fun main() {
    val man = Person("Ninja", "Male", 18)
    val (name,gender) = man
    println("Independent variable name: $name")
    println("Independent variable gender: $gender")
}
```

É possível porque o compilador irá gerar funções `componentN()` para cada propriedade como:

```kotlin
man.component1()     // Ninja
man.component2()     // Male
man.component3()     // 18
```

Portanto, se você tiver um objeto de classe de dados com muitos valores de propriedades armazenados nele, podemos usar essa declaração de desestruturação para armazenar o valor das propriedades do objeto de classe de dados em variáveis independentes.

# Classe Selada Kotlin

Uma classe selada é usada para representar hierarquias de classes restritas. Isso significa que o objeto da classe selada pode ter apenas um dos tipos definidos. Vamos entendê-lo com a ajuda de um exemplo.

Suponha que haja a necessidade de declarar classes baseadas em tipos de questões em um exame. O tipo de pergunta pode ser Fácil, Moderado ou Difícil. Agora queremos criar uma classe Question e todo o tipo de pergunta deve herdar esta classe. Também queremos ter certeza de que, além deste caso de uso, nenhuma outra classe deve herdar essa classe Question.

Isso é o que podemos alcançar através das classes seladas. Uma classe pode ter apenas algumas classes filhas especificadas. Isso é útil quando conhecemos todos os subtipos de uma classe pai e não queremos criar uma classe filha a partir do que sabemos.

## Diferença entre a classe Sealed e a classe Enum

A funcionalidade semelhante também é fornecida pelo Enum. No Enum, podemos ter tipos particulares definidos nele. As principais diferenças entre classes Sealed e Enums são:

- Cada instância enum existe apenas como uma única instância, enquanto uma classe filha de uma classe selada pode ter várias instâncias. Isso significa que cada objeto da classe filha (da classe selada) pode ter um estado.
- No Enum, cada instância tem o mesmo conjunto de propriedades e funções. Mas na classe Sealed, diferentes classes filhas podem ter diferentes conjuntos de propriedades e funções.
- As classes filhas de uma classe selada podem ser de diferentes tipos como: dados, objeto ou classe normal.

## Criando a classe Sealed

As classes seladas são criadas usando a palavra-chave `sealed`. É importante observar que todas as subclasses de uma classe selada devem ser declaradas no mesmo arquivo Kotlin. Se tentarmos criar uma subclasse de uma classe selada em outro arquivo Kotlin, receberemos um erro. A classe selada é `abstract` por padrão. Isso significa que não podemos instanciar classes seladas.

Vamos criar uma classe selada chamada Questione criar três subclasses Easy, Moderatee Difficult para ela:

```kotlin runnable
// this is our Kotlin sealed class
sealed class Question{
    // these are child classes
    class Easy(var mark: Int, var time: Int): Question()
    class Moderate(var mark: Int, var time: Int, var hint: String): Question()
    class Difficult(var mark: Int, var time: Int, var hint: String, var solution: String): Question()
}

fun main() {
    val easyQuestion = Question.Easy(1, 1)
    println("The marks and time limit for an easy question is ${easyQuestion.mark} mark and ${easyQuestion.time} min")
}
```

Como você pode ver no exemplo acima, podemos usar classes seladas para casos de uso em que sabemos para o que todas as classes filhas são necessárias e as classes criadas servem estritamente a um único propósito, como no exemplo de código acima, temos uma classe Question que é herdada por 3 classes filhas.

## Classe Kotlin Sealed: expressão `when`

Costumamos usar uma classe selada com uma expressão `when`. É porque a expressão `when` garante que todas as subclasses da classe selada sejam tratadas. Ela dará um erro se esquecermos de lidar com uma subclasse específica da classe selada. Agora não há necessidade de ter um bloco `else`. Mas funcionará apenas se você usar `when` como uma expressão e não como uma declaração.

Vamos modificar o exemplo acima para usar a expressão `when`:

```kotlin
sealed class Question{
    class Easy(var mark: Int, var time: Int): Question()
    class Moderate(var mark: Int, var time: Int, var hint: String): Question()
    class Difficult(var mark: Int, var time: Int, var hint: String, var solution: String): Question()
}

fun questionDetail(question: Question): String {
    return when(question){
        is Question.Easy -> "Easy question Mark: ${question.mark} Time: ${question.time} min"
        is Question.Moderate -> "Moderate question Marks:  ${question.mark} Time: ${question.time} min and Hint: ${question.hint}"
        is Question.Difficult -> "Difficult question Marks:  ${question.mark} Time: ${question.time} min Hint: ${question.hint} and Solution: ${question.solution}"
    }
}
fun main() {
    val easyQuestion = Question.Easy(1, 1)
    val difficultQuestion = Question.Difficult(5,6,"substitution method", "x = 5, y = 3")
    println(questionDetail(easyQuestion))
    println(questionDetail(difficultQuestion))
}
```
