# Classes e objetos

Existem vários tipos de paradigmas de programação que diferentes linguagens seguem para fornecer recursos diferentes. 
Os principais paradigmas de programação são:

- Imperativo
- Lógico
- Funcional
- Orientado a Objetos

O que iremos estudar nesse tutorial é Programação Orientada a Objetos (POO). Kotlin também fornece recursos POO como abstração , encapsulamento , herança , etc. na forma de classes, objetos, interfaces, etc, mas Kotlin não é uma linguagem POO pura, pois também fornece recursos de programação funcional como lambdas , função de ordem superior , etc. Portanto, o Kotlin suporta programação funcional e orientada a objetos.

# Classes e Objetos

No mundo real, podemos encontrar diferentes objetos do mesmo tipo, mas com propriedades diferentes. Tomemos o exemplo de um celular. 
Cada celular tem algumas propriedades como modelo, preço, cor, tamanho, RAM, etc. Para poder definir diferentes configurações móveis, devemos ter algum tipo de espaço em branco para ser arquivado, como um blueprint, com o qual podemos criar vários objetos de dispositivos móveis. 
Podemos conseguir isso usando uma classe.

A classe é usada para criar um blueprint de um objeto. Então vamos continuar com este exemplo por todo o capítulo, abaixo vamos definir uma classe chamada Mobile na qual vamos definir todas as suas propriedades e métodos, e então vamos criar objetos dessa classe, com valores diferentes para essas propriedades. 
Considere os objetos como telefones celulares fornecidos por diferentes empresas, ou diferentes modelos de celulares, como o iPhone 11 Pro pode ser um objeto, o Samsung Galaxy S 20 pode ser outro objeto com configuração própria, depois o One Plus 7 e assim por diante.


# Classe Kotlin

Uma classe é definida usando a palavra-chave `class`. A sintaxe para criar uma classe é:

```kotlin
class nomeDaClasse { // cabeçalho da classe
    // corpo da classe
}
```

Uma classe Kotlin tem duas partes principais:

- **Cabeçalho da classe**: contém o nome da classe, construtor primário, construtor pai, etc. 
- **Corpo da classe**: O corpo da classe contém propriedades, métodos, construtores secundários, bloco de inicialização, etc.

Vamos começar criando uma classe simples chamada `Mobile`. Ela contém as seguintes propriedades e métodos:

Propriedades:
- Marca
- Modelo
- Preco (o preço)
- Desconto

Métodos:
- getActualPrice(): Retornará o preço com desconto do celular.
- printDetails(): Esta função imprimirá detalhes do celular.

```kotlin runnable
class Celular {
    var marca: String = ""   // marca de tipo String
    var modelo: String = ""  // modelo de tipo String
    var preco: Double = 0.0    // preço de tipo float
    var desconto: Double = 0.0 // desconto de tipo float

    fun precoComDesconto():Float{
        return preco - desconto
    }

    fun imprimeDetalhes(){
        println("Detalhes do celular:")
        println("Marca: $marca")
        println("Modelo: $modelo")
        println("Preço: $preco")
        println("Desconto: $desconto")

    }
}
```

Nesse exemplo, estamos criamos uma classe básica com propriedades e métodos.


Pontos importantes sobre as classes Kotlin são:

- As propriedades devem ser inicializadas no momento da criação do objeto. Inicializamos `marca` e `modelo` como uma string vazia e `preco` e `desconto` como 0, como valores padrão.
- Por padrão, as classes são públicas em Kotlin.

# Objeto de classe em Kotlin

Objeto é a entidade do mundo real. Ele tem todas as propriedades e métodos declarados em uma classe. A sintaxe para declarar um objeto de uma classe é:

```kotlin
var nomedoNovoObjeto = NomeDaClasse()
```

Podemos acessar as propriedades e métodos de uma classe usando o operador `.` (ponto). Após o nome do objeto, adicione o ponto `.` e o nome da propriedade/método:

```kotlin 
var nomeDoNovoObjeto = NomeDaClasse()
nomeDoNovoObjeto.propriedade = 0
nomeDoNovoObjeto.nomeDoMetodo()
```

Vamos criar um objeto da classe Mobile e chamar seus métodos abaixo:

```kotlin runnable
fun main() {
    val novoCelular = Celular()
    novoCelular.marca = "iPhone"
    novoCelular.modelo = "11 pro"
    novoCelular.preco = 10000.00
    novoCelular.desconto = 900.00

    println("O preço com desconto é: ${novoCelular.precoComDesconto()}")

    novoCelular.imprimeDetalhes()
}
```

Explicação:

- Na linha nº 2, é criado o objeto da classe `Mobile`.
- Da linha 3 à linha 6, são fornecidos valores para todas as propriedades de classe.
- Na linha 8, o preço com desconto é impresso usando a função `getActualPrice()`.
- Na linha 10, a função printDetails() é chamada.

# Construtor Primário e Secundário

Um construtor é usado para inicializar as propriedades da classe quando um objeto da classe é criado. Pode ser considerada como uma função especial. 
O construtor chama a si mesmo no momento da criação do objeto. Sempre que criamos um objeto de uma classe, o construtor é chamado automaticamente.

Existem dois tipos de construtores em Kotlin:

- Construtor primário
- Construtor Secundário

Pode haver apenas um construtor primário e muitos construtores secundários.

### Construtor primário

Uma das características mais importantes do Kotlin é sua concisão. Ela pode ser visto na declaração do construtor primário. 
O construtor primário é uma parte do cabeçalho da classe. Todas as propriedades da classe também se tornam parte do construtor primário.

O construtor primário é criado adicionando `constructor()` no final do nome da classe:

```kotlin
class NomeDaClasse constructor(){
}
```

A palavra-chave `constructor` também pode ser removida:

```kotlin
class NomeDaClasse(){
}
```

Isso significa que, quando definimos uma classe normal, o construtor primário é criado.

Vamos criar um construtor primário para a classe `Mobile` que criamos nesse capítulo:

```kotlin runnable
class Celular (var marca: String, var modelo: String, var preco: Double, var desconto: Double) {

    // class methods
    fun precoComDesconto():Double{
        return mrp - discount
    }

    fun imprimeDetalhes(){
        println("Detalhes do celular:")
        println("Marca: $marca")
        println("Modelo: $modelo")
        println("Preco: $preco")
        println("Desconto: $desconto")

    }
}
```

Aqui todas as propriedades de classe são definidas como os parâmetros do construtor primário.


Agora, vamos criar um objeto desta classe:

```kotlin runnable
fun main() {
    val novoCelular: Celular = Celular("iPhone", "11 pro", 100000f, 1000f)
    println("O preço com desconto é: ${novoCelular.precoComDesconto()}")
    novoCelular.imprimeDetalhes()
}
```

Agora as variáveis ​​são inicializadas pelo construtor primário.

Mas torna-se necessário fornecer todos os valores para propriedades de classe. Para isso, também podemos fornecer valores padrão para o construtor primário:

```kotlin
class Celular (var marca: String = "", var modelo: String = "", var preco: Double = 0.0, var desconto: Double = 0.0)
```

### Construtor primário com bloco `init`

No construtor primário, os valores fornecidos são atribuídos diretamente às propriedades da classe. 
Se quisermos alterar os valores antes de atribuí-los ou adicionar alguma lógica ao construtor primário, podemos usar o bloco `init`.

Aqui está um exemplo de código,

```kotlin runnable
class Celular constructor(marca: String, modelo: String, preco: Float, desconto: Float) {
    var marca: String
    var modelo: String
    var preco: Float
    var desconto: Float

    // init function
    init {
        println("In init")
        this.marca = marca.toUpperCase()
        this.modelo = modelo.toUpperCase()
        this.preco = preco
        this.desconto = desconto
    }

    fun precoComDesconto():Double{
        return preco - desconto
    }

    fun imprimeDetalhes(){
        println("Detalhes do celular:")
        println("Marca: $marca")
        println("Modelo: $modelo")
        println("Preço: $preco")
        println("Desconto: $desconto")

    }
}
```

Agora podemos criar o objeto e imprimir os detalhes:

```kotlin runnable
fun main() {
    val celular1: Celular = Celular("iPhone", "11 pro", 100000f, 1000f)
    println("O preço com desconto é: ${celular1.precoComDesconto()}")
    mobile.imprimeDetalhes()
}
```

Pontos importantes sobre o bloco init:

- O bloco init é sempre chamado após o construtor primário.
- Uma classe pode ter vários blocos init.


### Construtor Secundário Kotlin

Um construtor secundário é usado para inicializar um grupo de valores. Os construtores secundários são criados usando a palavra-chave `constructor`. 
Uma classe pode ter um ou mais construtores secundários.

Vamos criar dois construtores na classe `Celular`:

```kotlin runnable
class Celular {
    var marca: String = ""
    var modelo: String = ""
    var preco: Float = 0f
    var desconto: Float = 0f

    // first secondary constructor
    constructor(_marca: String, _modelo: String){
        this.parca = _marca
        this.modelo = _modelo
    }

    // second secondary constructor
    constructor(_preco: Float, _desconto: Float){
        this.preco = _preco
        this.desconto = _desconto
    }

    fun precoComDesconto():Float{
        return preco - desconto
    }

    fun imprimeDetalhes(){
        println("Detalhes do celular:")
        println("Marca: $marca")
        println("Modelo: $modelo")
        println("Preço: $preco")
        println("Desconto: $desconto")

    }
}
```

Agora podemos criar um objeto passando valores de acordo com os construtores:

```kotlin runnable
fun main() {
    val celular1: Celular = Celular("iPhone", "11 pro")
    println("O preço com desconto é: ${celular1.precoComDesconto()}")
    celular1.imprimeDetalhes()
}
```

Alguns pontos sobre o construtor secundário:

Construtores secundários não são tão comuns. Eles geralmente são evitados, os blocos `init` podem ser usados ​​para executar qualquer tarefa específica antes da criação do objeto.

Se o construtor primário já estiver presente, cada construtor secundário deve chamar o construtor primário. Ele é chamado usando `this()`:

```kotlin
constructor(_marca: String, _modelo: String): this()
```

**Exemplo:**

```kotlin runnable
class Celular (_modelo: String, _preco: Float){
    var marca: String = ""
    var modelo: String = ""
    var preco: Float = 0f
    var desconto: Float = 0f

    init {
        this.modelo = _modelo.toUpperCase()
        this.preco = _preco
    }

    // first secondary constructor
    constructor(_marca: String, _modelo: String, _preco: Float, _desconto: Float):this(_modelo, _preco){
        this.marca = _marca.toUpperCase()
        this.modelo = _modelo.toUpperCase()
        this.preco = _preco
        this.desconto = _desconto
    }

    // second secondary constructor
    constructor(_modelo: String, _preco: Float, _desconto: Float):this(_modelo, _preco){
        this.modelo = _modelo.toUpperCase()
        this.preco = _preco
        this.desconto = _desconto
    }

    fun precoComDesconto():Float{
        return preco - (preco * desconto)/100
    }

    fun imprimeDetalhes(){
        println("Detalhes do celular:")
        println("Marca: $marca")
        println("Modelo: $modelo")
        println("Preço: R\$$preco")
        println("Desconto: ${desconto}%")
    }
}

fun main(args: Array<String>) {
    val celular1: Celular = Celular("iPhone 11 pro", 6500.00f)
    celular1.imprimeDetalhes()
    println("O preço com desconto é: ${celular1.precoComDesconto()}")

    println()
    
    celular1.marca = "Apple"
    celular1.desconto = 15f
    celular1.imprimeDetalhes()
    println("O preço com desconto é: ${celular1.precoComDesconto()}")

    println()

    val celular2: Celular = Celular("Nokia", "3310", 100.00f, 25f)
    celular2.imprimeDetalhes()
    println("O preço com desconto é: ${celular2.precoComDesconto()}")

    println()

    val celular3: Celular = Celular("Redmi 9", 955.00f, 7f)
    celular3.imprimeDetalhes()
    println("O preço com desconto é: ${celular3.precoComDesconto()}")
}
```

Também podemos chamar um construtor secundário de outro construtor secundário usando this():

```kotlin
constructor(_marca: String, _modelo: String): this(10.00,1.00)
```

Esse construtor está chamando outros construtores com valores 10.00 e 1.00 para `preco` e `desconto`.

Também podemos chamar o construtor da classe pai (no caso de herança) usando super(). 

```
Fonte:
https://www.studytonight.com/kotlin/kotlin-class-and-object
https://www.studytonight.com/kotlin/kotlin-constructor-primary-and-secondary-constructor
```
