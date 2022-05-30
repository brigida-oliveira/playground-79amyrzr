# Classe e objeto Kotlin

Existem vários tipos de paradigmas de programação que diferentes linguagens seguem para fornecer recursos diferentes. 
Os principais paradigmas de programação são:

- Imperativo
- Lógico
- Funcional
- Orientado a Objeto

O paradigma mais popularmente usado é a Programação Orientada a Objetos (POO). 
Kotlin também fornece recursos POO como abstração , encapsulamento , herança , etc. na forma de classes, objetos, interfaces, etc, mas Kotlin não é uma linguagem POO pura, pois também fornece recursos de programação funcional como lambdas , função de ordem superior , etc. 
Portanto, o Kotlin suporta programação funcional e orientada a objetos.

# Classes e Objetos

No mundo real, podemos encontrar diferentes objetos do mesmo tipo, mas com propriedades diferentes. Tomemos o exemplo de um celular. 
Cada celular tem algumas propriedades como modelo, preço, cor, tamanho, RAM, memória, etc. Para poder definir diferentes configurações móveis, devemos ter algum tipo de espaço em branco para ser arquivado, como um blueprint, com o qual podemos criar vários objetos de dispositivos móveis. 
Podemos conseguir isso usando uma classe.

A classe é usada para criar um blueprint de um objeto. Então vamos continuar com este exemplo por todo o capítulo, abaixo vamos definir uma classe chamada Mobile na qual vamos definir todas as suas propriedades e métodos, e então vamos criar objetos dessa classe, com valores diferentes para essas propriedades. 
Considere os objetos como telefones celulares fornecidos por diferentes empresas, ou diferentes modelos de celulares, como o iPhone 11 Pro pode ser um objeto, o Samsung Galaxy S 20 pode ser outro objeto com configuração própria, depois o One Plus 7 e assim por diante.


# Classe Kotlin

Uma classe é definida usando a palavra-chave `class`. A sintaxe para criar uma classe é:

```kotlin
class <class-name> // cabeçalho da classe
{
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
class Mobile {
    var marca: String = ""   // marca de tipo String
    var modelo: String = ""  // modelo de tipo String
    var preco: Float = 0f    // preço de tipo float
    var desconto: Float = 0f // desconto de tipo float

    fun getActualPrice():Float{
        return preco - desconto
    }

    fun printDetails(){
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
var varName = ClassName()
```

Podemos acessar as propriedades e métodos de uma classe usando o operador `.` (ponto). Após o nome do objeto, adicione o ponto `.` e o nome da propriedade/método:

```kotlin 
var varName = ClassName()
varName.property = 0
varName.functionName()
```

Vamos criar um objeto da classe Mobile e chamar seus métodos abaixo:

```kotlin runnable
fun main() {
    val mobile = Mobile()
    mobile.brand = "iPhone"
    mobile.model = "11 pro"
    mobile.mrp = 100000f
    mobile.discount = 1000f

    println("O preço com desconto é: ${mobile.getActualPrice()}")

    mobile.printDetails()
}
```

Explicação:

- Na linha nº 2, é criado o objeto da classe `Mobile`.
- Da linha 3 à linha 6, são fornecidos valores para todas as propriedades de classe.
- Na linha 8, o preço com desconto é impresso usando a função `getActualPrice()`.
- Na linha 10, a função printDetails() é chamada.