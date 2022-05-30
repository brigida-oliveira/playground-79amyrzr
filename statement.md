# Classes

As classes em Kotlin são declaradas usando a palavra-chave class:

class Person { /*...*/ }
A declaração de classe consiste no nome da classe, no cabeçalho da classe (especificando seus parâmetros de tipo, o construtor primário e algumas outras coisas) e o corpo da classe entre chaves. Tanto o cabeçalho quanto o corpo são opcionais; se a classe não tiver corpo, as chaves podem ser omitidas.

class Empty
Construtores﻿
Uma classe em Kotlin pode ter um construtor primário e um ou mais construtores secundários . O construtor primário faz parte do cabeçalho da classe e segue o nome da classe e os parâmetros de tipo opcionais.

class Person constructor(firstName: String) { /*...*/ }
Se o construtor primário não tiver anotações ou modificadores de visibilidade, a palavra- constructorchave poderá ser omitida:

class Person(firstName: String) { /*...*/ }
O construtor primário não pode conter nenhum código. O código de inicialização pode ser colocado em blocos inicializadores prefixados com a palavra- initchave.

Durante a inicialização de uma instância, os blocos inicializadores são executados na mesma ordem em que aparecem no corpo da classe, intercalados com a propriedade inicializadores:

class  InitOrderDemo ( nome : String ) {
    val  firstProperty  =  "Primeira propriedade: $name" . também (:: println )
    
    inicializar {
        println ( "Primeiro bloco inicializador que imprime $name" )
    }
    
    val  secondProperty  =  "Segunda propriedade: ${name.length}" . também (:: println )
    
    inicializar {
        println ( "Segundo bloco inicializador que imprime ${name.length}" )
    }
}
Abrir no Playground →
Destino: JVM
Executando na v. 1.6.21
Os parâmetros do construtor primário podem ser usados ​​nos blocos inicializadores. Eles também podem ser usados ​​em inicializadores de propriedades declarados no corpo da classe:

class Customer(name: String) {
    val customerKey = name.uppercase()
}
Kotlin tem uma sintaxe concisa para declarar propriedades e inicializá-las a partir do construtor primário:

class Person(val firstName: String, val lastName: String, var age: Int)
Tais declarações também podem incluir valores padrão das propriedades da classe:

class Person(val firstName: String, val lastName: String, var isEmployed: Boolean = true)
Você pode usar uma vírgula à direita ao declarar propriedades de classe:

class Person(
    val firstName: String,
    val lastName: String,
    var age: Int, // trailing comma
) { /*...*/ }
Assim como as propriedades regulares, as propriedades declaradas no construtor primário podem ser mutáveis ​​( var) ou somente leitura ( val).

Se o construtor tiver anotações ou modificadores de visibilidade, a constructorpalavra-chave é necessária e os modificadores vêm antes dela:

class Customer public @Inject constructor(name: String) { /*...*/ }
Saiba mais sobre modificadores de visibilidade .

Construtores secundários﻿
Uma classe também pode declarar construtores secundários , que são prefixados com constructor:

class Person(val pets: MutableList<Pet> = mutableListOf())

class Pet {
    constructor(owner: Person) {
        owner.pets.add(this) // adds this pet to the list of its owner's pets
    }
}
Se a classe tiver um construtor primário, cada construtor secundário precisará delegar ao construtor primário, direta ou indiretamente por meio de outro(s) construtor(es) secundário(s). A delegação para outro construtor da mesma classe é feita usando a thispalavra-chave:

class Person(val name: String) {
    val children: MutableList<Person> = mutableListOf()
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
O código em blocos inicializadores efetivamente se torna parte do construtor primário. A delegação para o construtor primário acontece como a primeira instrução de um construtor secundário, portanto, o código em todos os blocos inicializadores e inicializadores de propriedade é executado antes do corpo do construtor secundário.

Mesmo que a classe não tenha construtor primário, a delegação ainda acontece implicitamente e os blocos inicializadores ainda são executados:

 Construtores de classe {
    inicializar {
        println ( "Bloco de inicialização" )
    }
​
    construtor ( i : Int ) {
        println ( "Construtor $i" )
    }
}
Abrir no Playground →
Destino: JVM
Executando na v. 1.6.21
Se uma classe não abstrata não declarar nenhum construtor (primário ou secundário), ela terá um construtor primário gerado sem argumentos. A visibilidade do construtor será pública.

Se você não quiser que sua classe tenha um construtor público, declare um construtor primário vazio com visibilidade não padrão:

class DontCreateMe private constructor () { /*...*/ }
Na JVM, se todos os parâmetros do construtor primário tiverem valores padrão, o compilador gerará um construtor sem parâmetros adicional que usará os valores padrão. Isso facilita o uso do Kotlin com bibliotecas como Jackson ou JPA que criam instâncias de classe por meio de construtores sem parâmetros.

class Customer(val customerName: String = "")
Criando instâncias de classes﻿
Para criar uma instância de uma classe, chame o construtor como se fosse uma função regular:

val invoice = Invoice()

val customer = Customer("Joe Smith")
Kotlin não tem uma palavra- newchave.

O processo de criação de instâncias de classes internas aninhadas, internas e anônimas é descrito em Classes aninhadas .

Membros da classe﻿
As aulas podem conter:

Construtores e blocos inicializadores

Funções

Propriedades

Classes aninhadas e internas

Declarações de objetos

Herança﻿
As classes podem ser derivadas umas das outras e formar hierarquias de herança. Saiba mais sobre herança em Kotlin .

Aulas abstratas﻿
Uma classe pode ser declarada abstract, juntamente com alguns ou todos os seus membros. Um membro abstrato não tem uma implementação em sua classe. Você não precisa anotar classes ou funções abstratas com open.

abstract class Polygon {
    abstract fun draw()
}

class Rectangle : Polygon() {
    override fun draw() {
        // draw the rectangle
    }
}
Você pode substituir um openmembro não abstrato por um abstrato.

open class Polygon {
    open fun draw() {
        // some default polygon drawing method
    }
}

abstract class WildShape : Polygon() {
    // Classes that inherit WildShape need to provide their own
    // draw method instead of using the default on Polygon
    abstract override fun draw()
}
Objetos complementares﻿
Se você precisar escrever uma função que possa ser chamada sem ter uma instância de classe, mas que precise de acesso aos componentes internos de uma classe (como um método de fábrica), você pode escrevê-la como um membro de uma declaração de objeto dentro dessa classe.

Ainda mais especificamente, se você declarar um objeto complementar dentro de sua classe, poderá acessar seus membros usando apenas o nome da classe como qualificador.

```kotlin runnable
fun main(args: Array<String>) {
    println("Hello, World!")
}
```
