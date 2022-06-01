# Funções Getter e Setter

Getters e setters são usados para obter valores de propriedades de classe e definir valores de propriedades de classe. 
No capítulo anterior, vimos que as propriedades declaradas dentro de uma classe são acessadas usando o operador `.`. 
Se tivermos uma classe Empregado com a seguinte definição:

```kotlin
class Empregado{
    var salario: Int = 0
    var nome: String = ""
}
```

Podemos criar um objeto da classe Empregado e acessar as propriedades usando o operador `.` dessa forma:

```kotlin
val employee = Employee()
employee.salary = 340000
employee.name = "Ninja"
println("The salary of ${employee.name} is ${employee.salary}")
```

Sempre que tentamos obter ou definir o valor de uma propriedade, as propriedades não são acessadas diretamente. 
As funções getter e setter são chamadas para obter e definir o valor de uma propriedade.

## O que são getters e setters?

Getter e Setter são as funções que são geradas por padrão para cada propriedade de classe pelo Kotlin. 
Eles são usados para acessar a propriedade.

Se tentarmos chamar `NomeDaClasse.propriedade = valor` a função `set()` é chamada internamente e se tentarmos obter o valor da propriedade usando `NomeDaClasse.propriedade` a função `get()` é chamada internamente.

## Por que a função Getter e Setter?

É uma boa prática não expor as variáveis de uma classe fora dela. 
Se você vem de Java, deve ter declarado propriedades de classe como privadas e criado métodos getter e setter para ela. 
Kotlin por padrão fornece esse recurso.

## Getter e Setter em Kotlin

As funções `get()` e `set()` padrão se parecem com:

```kotlin 
class Pessoa{
    var nome: String = ""
        get() = field
        set(value) {
            field = value
        }
    val idade: Int = 0
        get() = field
}
```

Propriedades declaradas com `var` têm funções `get()` e `set()`. Mas as propriedades declaradas com `val` têm apenas a função `get()`. 
Isso ocorre porque os valores de `val` não podem ser reatribuídos.

A palavra-chave `field` é usada para representar a variável. O `value` é usado para representar o valor a ser atribuído à variável. 
Pode ser alterado também. Essas funções `get()` e `set()` são redundantes, pois o Kotlin as fornece por padrão.

## Definir getters e setters personalizados

Também podemos fornecer funções `get()` e `set()` personalizadas:

```kotlin runnable
class Pessoa{
    var nome: String = ""
        get() {
            println("get() interno de nome")
            return field.toString()
        }
        set(value) {
            println("Dentro do set() de nome")
            if (value.length < 3)
                field = "NOME INVÁLIDO"
            else
                field = value
        }
    val idade: Int = 18
        get(){ 
            println("Dentro do get() de idade")
            return field
        }
}
```
Aqui criamos funções `get()` e `set()` personalizadas para `nome` e função `get()` personalizada para `idade`. 
Vamos criar o objeto desta classe e imprimir a saída:

```kotlin
fun main() {
    val person = Person()
    person.name = "Ninja"       // calls set() function
    println("A idade de ${person.name} é ${person.age}")        // calls get() functions 
} 
```

# Modificadores de acesso

Modificadores de acesso ou modificadores de visibilidade são usados para definir o escopo de uma classe, função, campo, interface etc. 
As palavras-chave do modificador de visibilidade restringem o uso de classes, funções, propriedades etc e informa se estão disponíveis em suas subclasses, em outros arquivos, classes, outros pacotes ou não.

No Kotlin, os modificadores de visibilidade podem ser aplicados a classes, construtores, objetos, interfaces, funções, propriedades e seus setters. 
Os getters têm a mesma visibilidade que a propriedade.

Existem quatro modificadores de visibilidade no Kotlin:

- `private`
- `protected`
- `internal`
- `public`

O modificador de visibilidade padrão é *public*. Isso significa que se não especificamos nenhum modificador de visibilidade para uma classe, função, propriedade etc, por padrão o compilador irá considerá-lo como público.
Os modificadores de visibilidade têm significados diferentes de acordo com o local onde são colocados. Vamos olhar para eles um por um.

## Modificadores de visibilidade em campos de nível superior

Campos de nível superior são aqueles que são colocados fora das classes ou interfaces. 
Eles estão presentes diretamente dentro de qualquer arquivo Kotlin.

Para campos de nível superior, os diferentes modificadores de visibilidade significam:

- `public` - É um modificador padrão e pode ser omitido. Isso significa que as declarações são visíveis em todos os lugares. Eles podem ser usados em diferentes arquivos, classes, pacotes, etc.
- `internal` - Declarações marcadas como internas são visíveis dentro do mesmo módulo. Um módulo significa o conjunto de arquivos Kotlin compilados juntos. Durante o desenvolvimento do projeto podemos ter vários módulos dentro do mesmo projeto. Outros módulos podem ser uma biblioteca ou aplicativo auxiliar que suporta o aplicativo principal.
- `private` - As declarações marcadas com `private` estão disponíveis apenas dentro do mesmo arquivo Kotlin. Eles não podem ser usados fora desse arquivo *.kt*.

O modificador `protected` não está disponível para campos de nível superior.

# Modificadores de visibilidade dentro de classes e interfaces

As funções, propriedades, objetos dentro de uma classe têm acesso a modificadores. Observe que a visibilidade de toda a classe ou interface depende de seu modificador de visibilidade que está no nível superior.


Os modificadores de visibilidade dentro das classes significam:

- `public` - Quem pode ver a classe também pode ver toda a sua declaração pública. Isso significa que as declarações públicas são visíveis em todos os lugares. Eles são visíveis em outros arquivos, classes, pacotes e até módulos.
- `internal` - Igual aos campos de nível superior, eles são visíveis dentro do mesmo módulo.
- `protected` - As declarações marcadas com `protected` são visíveis apenas dentro da classe e sua subclasse. Eles não são visíveis fora da classe. Isso significa que uma função marcada com a palavra-chave `protected` não pode ser usada fora da classe ou de sua subclasse.
- `private` - As declarações marcadas com palavra-chave `private` são visíveis apenas dentro dessa classe. Eles não são visíveis fora da classe, nem mesmo nas subclasses.

Vejamos um exemplo de modificadores de visibilidade em classes:

```kotlin runnable
open class Empregado {
    // Function visible only inside class
    private fun privateFunction(){
    }

    // Function visible in same
    internal fun internalFunction(){
    }

    // Function visible everyWhere
    fun publicFunction(){
    }

    // Function visible only in Employee class and its subclasses
    protected fun protectedFunction(){
    }
}

class Developer: Empregado() {
    // privateFunction() is not visible here
}

fun main() {
    // privateFunction() and protectedFunction() are not visible here
}
```

# Herança Kotlin

## O que é herança?

A herança é uma das características mais importantes da programação orientada a objetos. 
Ele permite que uma classe herde características de outra classe.

Suponha que você criou uma classe Vehicle que possui propriedades e métodos relacionados a veículos. 
Agora precisamos criar outra classe Car que tenha muitas propriedades comuns aos veículos. 
Então, em vez de reescrever o mesmo código, podemos fazer a classe Car herdar a classe Vehicle. 
Da mesma forma, podemos criar uma classe TwoWheeler que novamente pode herdar algumas propriedades comuns básicas da classe Vehicle e pode ter algumas propriedades próprias.

Dessa forma, a Herança pode ser usada para dividir o código adequadamente, permitindo a reutilização do código e fornecendo mais estrutura ao código.

A herança permite que a nova classe herde propriedades e métodos de uma classe existente. 
A classe existente ou a classe da qual a nova classe é herdada é conhecida como classe base ou classe pai ou superclasse. 
A nova classe que herda as características da classe existente é conhecida como classe derivada ou classe filha ou subclasse.

## Herança em Kotlin

Todas as classes em Kotlin são por padrão `final`. Isso significa que essas classes não são herdáveis. 
Para tornar uma classe herdável, adicionamos uma palavra-chave `open` no cabeçalho da classe.

Uma classe filha herda uma classe pai usando o operador `:`. A sintaxe para herdar uma classe é:

```kotlin
open class Parent{
    // Parent class features
}
class Child : Parent(){
    // Child class features
}
```
Vamos criar um exemplo bem básico de herança:

```kotlin runnable
// parent class
open class Vehicle{
    fun run(){
        println("Veículo funciona....")
    }
}
// child class
class Car : Vehicle(){
    fun seats(){
        println("Carro tem 4 lugares")
    }
}

fun main() {
    val car = Car()
    car.seats()
    // calling method defined in parent class
    car.run()
}
```
 
Neste exemplo, marcamos a classe Vehicle como aberta (`open`) para torná-la herdável. 
A classe Car herda a classe Vehicle e, portanto, herda sua função run().

Em Kotlin, uma classe pode herdar apenas uma classe, que é igual a Java. 
Assim, Kotlin não permite herança múltipla. Mas uma classe pode implementar muitas interfaces.

# Construtor primário na herança

Se a classe pai tiver um construtor primário, a classe filha deverá chamar o construtor primário da classe pai. 
No exemplo acima, na classe Car também chamamos o construtor primário da classe Vehicle (o construtor primário foi criado pelo compilador, pois não fornecemos um). 
Vamos passar propriedades para a classe pai e ver como elas funcionam.

```kotlin runnable
/*
  Vehicla class has properties:
     - is the vehicle for carrying passengers
     - no. of tyres
     - fuel capacity of vehicle
*/
open class Vehicle(carryPassenger: Boolean, tyres: Int, fuelCapacity: Int){
    init {
        println("O Veículo transporta passageiros? $carryPassenger")
        println("Pneus no Veículo: $tyres")
        println("Capacidade de Combustível do Veículo: $fuelCapacity")
    }
}

// child class with extra airBags property
class Car(carryPassenger: Boolean, tyres: Int, fuelCapacity: Int, airBags: Int) : Vehicle(carryPassenger, tyres, fuelCapacity){
    // init function for child class
    init {
        println("Nº de air bags no carro: $airBags")
    }
}

fun main() {
    val car = Car(true, 4, 50, 4)
}
```

Neste exemplo, passamos valores ao criar o objeto da classe filha. 
A partir dessas propriedades, passamos carryPassenger, tyres e fuelCapacity para o construtor primário da classe pai Vehicle .

Ao criar o objeto da classe Car, o construtor primário (padrão) da classe filha que é Car é chamado, que chama internamente o construtor primário da classe pai Vehicle primeiro e depois seu bloco `init`. 
Depois disso, o construtor padrão primário da classe filha Car é concluído e, em seguida, o bloco `init` da classe filha Car é executado.

## Construtor secundário na herança

Se a classe base não tiver um construtor primário, mas tiver um construtor secundário, a classe derivada deverá chamar o construtor secundário da classe base usando a palavra-chave `super`.

```kotlin runnable
open class Vehicle{
    // secondary constructor
    constructor(carryPassenger: Boolean, tyres: Int, fuelCapacity: Int){
        println("O veículo transporta passageiros? $carryPassenger")
        println("Pneus no veículo: $tyres")
        println("Capacidade de combustível do veículo: $fuelCapacity")
    }
}
// child class
class Truck: Vehicle{
    // secondary constructor calling super for parent class
    constructor(carryPassenger: Boolean, tyres: Int, fuelCapacity: Int, loadCarryCapacity: Int): super(carryPassenger, tyres, fuelCapacity){
        println("A capacidade de carga é: $loadCarryCapacity")
    }
}

fun main() {
    val truck = Truck(false, 10, 200, 1000)
}
```

Neste exemplo, o construtor secundário de Truckclass chamou o construtor secundário de Vehicleclass usando a palavra-chave super. 
Todos os argumentos necessários para a classe pai são fornecidos durante a chamada super.

## Sobreposição de métodos

Na herança, podemos fornecer implementação específica dos métodos da classe base dentro da classe derivada. 
Isso significa que se existe uma função na classe pai, podemos fornecer uma implementação diferente da mesma função na classe filha. 
É conhecido como sobreposição de métodos.


No Kotlin, os métodos também são `final` por padrão. Para sobrepor um método, ele deve ser marcada como `open` (assim como a classe) na classe pai e na classe filha devemos usar a palavra-chave override em vez de open para especificar que substituímos a função.

O nome da função e os parâmetros devem ser os mesmos .

E o tipo de retorno das funções de classe filha pode ser um subtipo das funções de classe pai.

Vejamos um exemplo no qual substituiremos dois métodos da classe base:

```kotlin runnable
// parent class
open class Vehicle{

    open fun run(){
        println("Vehicle is running")
    }

    open fun drivenBy(name: String){
        println("Vehicle is driven by: $name")
    }
}
// child class
class Jeep: Vehicle(){

    override fun run() {
        println("Dirigindo um Jeep")
    }

    override fun drivenBy(name: String) {
        println("Jeep é dirigido por $name")
    }
}

fun main() {
    val jeep = Jeep()
    jeep.run()
    jeep.drivenBy("Ninja")
}
```

Neste exemplo, sobrescrevemos dois métodos run() e drivenBy() de Vehicleclasse e os sobrescrevemos em Jeepclasse.

Também podemos chamar funções da classe pai dentro da classe filha usando a palavra-chave super.

## Propriedades de sobreposição

Da mesma forma, também podemos sobrepor as propriedades e alterar seu valor dentro da classe filha. 
As propriedades devem ser marcadas open para substituí-las e usar a palavra-chave override na classe filha quando substituirmos a propriedade, assim como fizemos para métodos de classe.

```kotlin runnable
// parent class
open class Vehicle{
    open val color: String = "Preto"
    open fun printColor(){
        println("A cor do veículo é: $color")
    }
}
// child class
class Jeep: Vehicle(){
    override val color: String = "Vermelho"
    override fun printColor(){
        println("A cor do Jeep é: $color")
    }
}

fun main() {
    val jeep = Jeep()
    jeep.printColor()
}
```
 
