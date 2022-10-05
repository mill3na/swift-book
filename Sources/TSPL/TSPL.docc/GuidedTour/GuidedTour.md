

# A Swift Tour



Tradition suggests that the first program in a new language
should print the words “Hello, world!” on the screen.
In Swift, this can be done in a single line:



```swift
print("Hello, world!")
// Prints "Hello, world!"
```




If you have written code in C or Objective-C,
this syntax looks familiar to you ---
in Swift, this line of code is a complete program.
You don't need to import a separate library for functionality like
input/output or string handling.
Code written at global scope is used
as the entry point for the program,
so you don't need a `main()` function.
You also don't need to write semicolons
at the end of every statement.

This tour gives you enough information
to start writing code in Swift
by showing you how to accomplish a variety of programming tasks.
Don’t worry if you don’t understand something ---
everything introduced in this tour
is explained in detail in the rest of this book.

## Valores Simples

Use `let` para criar uma constante e `var` para criar uma variável.
O valor de uma constante não precisa ser sabido no momento do código ser compilado. mas você deve atribuí-la um valor somente uma vez. Isso significa que você pode usar constantes para nomear um valor que você determinou uma vez, mas utiliza em muitos lugares.

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```




A constante ou variável deve ser do mesmo tipo do valor que você quer atribuir a ela.  Entretanto, você nem sempre precisa atribuir o tipo de forma explícita. 
Dar um valor à constante ou variável no momento de sua criação faz com que o compilador infira qual o seu tipo.  No exemplo acima, o compilador irá inferir que a `myVariable` é um inteiro, pois o seu valor inicial é um inteiro.   Se o valor inicial não entrega informação suficiente (ou se não foi atribuído nenhum valor inicial), especifique o tipo escrevendo-o logo depois da variável, separado por dois pontos. 

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```




> Experimente: Crie uma constante com o tipo `Float` explícito e de valor `4`.

Valores nunca são implicitamente convertidos para outro tipo. Se você precisar converter um valor para um tipo diferente, faça uma instância explicitamente do tipo desejado. 

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```




> Experimente: Tente remover a conversão para `String` da última linha
> Que tipo de erro dá?



Existe uma forma ainda mais simples de incluir valores em uma string: escreva o valor em parênteses com uma barra invertida (`\`) antes do primeiro parêntese. Por exemplo:

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```




> Experimente: Use `\()` para incluir um cálculo de floating-point em uma string e para incluir o nome de alguém em uma saudação.

Use três aspas duplas para strings que pegam múltiplas linhas.  A indentação no começo de cada linha de texto será removida, caso seja a mesma das aspas fechando. 
Por exemplo:

```swift
let quotation = """
I said "I have \(apples) apples."
And then I said "I have \(apples + oranges) pieces of fruit."
"""
```






Crie arrays e dicionários usando colchetes (`[]`), e acesse seus elementos escrevendo o índex ou chave também entre colchetes. A vírgula após o último elemento é permitida. 





```swift
var fruits = ["strawberries", "limes", "tangerines"]
fruits[1] = "grapes"

var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
 ]
occupations["Jayne"] = "Public Relations"
```




Os Arrays crescem automaticamente quando você adiciona elementos a eles. 

```swift
fruits.append("blueberries")
print(fruits)
```




Para criar um array ou dicionário vazio, use a sintaxe de inicialização.  
```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```




Se o tipo da informação pode ser inferido, você pode escrever um array vazio com `[]` e um dicionário vazio com `[:]`. Por exemplo, quando você configura um novo valor para uma variável ou passa um argumento para uma função.




```swift
fruits = []
occupations = [:]
```




## Controle de Fluxo

`## Controle de Fluxo

Use `if` e `switch` para fazer condicionais,
e use `for`-`in`, `while`, e `repeat`-`while`
para criar loops.
É opcional inserir as condicionais ou variáveis de loop entre parênteses. 
É obrigatório inserir o texto _body_ entre chaves.

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Prints "11"
```








Em uma declaração `if`,
a condicional deve ser uma expressão booleana ---
isso significa que o código como `if score { ... }` é um erro,
não é uma comparação implicita à zero.

Você pode usar ‘if’ e ‘let’ juntos
para trabalhar com valores que podem estar ausentes.
Esses valores são representados como opcionais.
Um valor opcional contém um valor
ou contém `nil`para indicar um valor ausente.
Insira um ponto de interrogação, em seguida, digite um valor
para marcá-lo como opcional.





```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Prints "false"

var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```




> Experimente: Altere `optionalName` para `nil`.
> Qual saudação você recebe?
> Insira `else` para definir uma saudação diferente
> Se `optionalName` é `nil`.

Se o valor opcional é `nil`,
a condicional é ‘false’ e o código nas chaves são pulados
Caso contrário, o valor opcional é desempacotado e atribuído,
para a constant edepois de ‘let’
o que faz o valor desempacotado ficar disponível
dentro do bloco de código.

Outra maneira de lidar com os valores opcionais
é provendo um valor padrão usando o operador ‘??’.
Se o valor opcional está ausente,
o valor padrão é usado como substituto. 

```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```




You can use a shorter spelling to unwrap a value,
using the same name for that unwrapped value.

```swift
if let nickname {
    print("Hey, \(nickname)")
}
```




Switches suporta todos os tipos de dados
e uma grande variedade de operações de comparação —
sem limitação de inteiros
e testes para igualdade.



```swift
let vegetable = "red pepper"
switch vegetable {
    case "celery":
        print("Add some raisins and make ants on a log.")
    case "cucumber", "watercress":
        print("That would make a good tea sandwich.")
    case let x where x.hasSuffix("pepper"):
        print("Is it a spicy \(x)?")
    default:
        print("Everything tastes good in soup.")
}
// Prints "Is it a spicy red pepper?"
```




> Experimente: tente remover a  _default case_
> Qual o erro que foi percebido?

Perceba como ‘let’ pode ser usado em um padrão
para determinar o valor que combina o padrão
com a constante.

Depois de executar o código dentro do ’switch case’



Você usa `for`-`in`para integrar os itens em um dicionário
provendo um par names para usar
para cada par de chave de valor.
Dicionários são uma coleção não-ordenada
então, suas chaves e valores são integrados
em uma ordem arbritária



```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (_, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Prints "25"
```




> Experimente: Substitua `_` com o nome de uma variável,
> e acompanhe qual tipo de número foi maior.

Use `while` para repetir um bloco de código até a condição mudar.
As condições de um loop podem estar no final
assegurando que o loop será executado pelo menos uma vez.



```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Prints "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Prints "128"
```




Você pode manter um _index_ em loop
usando `..<` para criar uma série de _indexes_.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Prints "6"
```




Use `..<` para criar um intervalo que omite seu maior valor,
e use `...` para usar um intervalo que inclui ambos valores.

## Funções e *Closures*

Use `func` para declarar uma função.
Crie uma função seguindo seu nome
com uma lista de argumentos entre parênteses.
Use `->` para separar os nomes e tipos de parâmetros do tipo de retorno da função.



```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```




> Experimente: tente remover o parâmetro `day`.
> Adicione um parâmetro que inclua o almoço especial de hoje na saudação.

Por padrão,
funções usam seus nomes de parâmetros
como rótulos para seus argumentos.
Escreva um rótulo de argumento personalizado antes do nome do parâmetro,
ou escreva `_` para não usar nenhum rótulo de argumento.


```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```





Use uma tupla para fazer um valor composto ---
por exemplo, para retornar vários valores de uma função.
Os elementos de uma tupla podem ser referenciados pelo
nome ou pelo número.




```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0

    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }

    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Imprime "120"
print(statistics.2)
// Imprime "120"
```




Funções podem ser aninhadas.
Funções aninhadas têm acesso a variáveis
que foram declaradas na função externa.
Você pode usá-las para organizar o código em funções
que são longas ou complexas.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```





As funções são um tipo de primeira classe, o que significa que podem ter outra função como seu valor de retorno.

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```




Uma função pode ter outra função como um de seus argumentos.

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```




As funções são, na verdade, um caso especial de closures:
blocos de código que podem ser chamados posteriormente.
O código em uma *closure* tem acesso a coisas como variáveis e funções que estavam disponíveis no escopo de sua criação, ainda que a *clusore* esteja em um escopo diferente quando for executada, --- você viu um exemplo disso já com funções aninhadas.
Você pode escrever uma *closure* sem um nome, envolvendo o código com chaves (`{}`).
Use `in` para separar os argumentos e o tipo de retorno do corpo da *closure*.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```




> Experimente: Reescreva essa *closure* para retornar zero para todos os números ímpares.

Você tem várias opções para escrever *closures* de forma mais concisa.
Quando o seu tipo já é conhecido,
como o retorno de uma chamada para um *delegate*,
você pode omitir o tipo de seus parâmetros,
seu tipo de retorno, ou ambos.
*Closures* de instrução única retornam implicitamente o valor
de sua única instrução.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Imprime "[60, 57, 21, 36]"
```




Você pode se referir a parâmetros por número em vez de por nome ---
essa abordagem é especialmente útil em *closures* muito curtas.
Uma *closure* passada como o último argumento para uma função
pode aparecer logo após os parênteses.
Quando uma *closure* é o único argumento para uma função,
você pode omitir os parênteses.

```swift
let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Imprime "[20, 19, 12, 7]"
```










## Objects and Classes

Use `class` followed by the class's name to create a class.
A property declaration in a class is written the same way
as a constant or variable declaration,
except that it's in the context of a class.
Likewise, method and function declarations are written the same way.



```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```




> Experiment: Add a constant property with `let`,
> and add another method that takes an argument.

Create an instance of a class
by putting parentheses after the class name.
Use dot syntax to access
the properties and methods of the instance.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```




This version of the `Shape` class is missing something important:
an initializer to set up the class when an instance is created.
Use `init` to create one.

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String

    init(name: String) {
       self.name = name
    }

    func simpleDescription() -> String {
       return "A shape with \(numberOfSides) sides."
    }
}
```




Notice how `self` is used to distinguish the `name` property
from the `name` argument to the initializer.
The arguments to the initializer are passed like a function call
when you create an instance of the class.
Every property needs a value assigned ---
either in its declaration (as with `numberOfSides`)
or in the initializer (as with `name`).

Use `deinit` to create a deinitializer
if you need to perform some cleanup
before the object is deallocated.

Subclasses include their superclass name
after their class name,
separated by a colon.
There's no requirement for classes to subclass any standard root class,
so you can include or omit a superclass as needed.

Methods on a subclass that override the superclass's implementation
are marked with `override` ---
overriding a method by accident, without `override`,
is detected by the compiler as an error.
The compiler also detects methods with `override`
that don't actually override any method in the superclass.

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() -> Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```




> Experiment: Make another subclass of `NamedShape`
> called `Circle`
> that takes a radius and a name
> as arguments to its initializer.
> Implement an `area()` and a `simpleDescription()` method
> on the `Circle` class.

In addition to simple properties that are stored,
properties can have a getter and a setter.

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }

    var perimeter: Double {
        get {
             return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }

    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Prints "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Prints "3.3000000000000003"
```




In the setter for `perimeter`,
the new value has the implicit name `newValue`.
You can provide an explicit name in parentheses after `set`.

Notice that the initializer for the `EquilateralTriangle` class
has three different steps:

- Setting the value of properties that the subclass declares.
- Calling the superclass's initializer.
- Changing the value of properties defined by the superclass.
   Any additional setup work that uses methods, getters, or setters
   can also be done at this point.

If you don't need to compute the property
but still need to provide code that's run before and after setting a new value,
use `willSet` and `didSet`.
The code you provide is run any time the value changes outside of an initializer.
For example, the class below ensures
that the side length of its triangle
is always the same as the side length of its square.



```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// Prints "10.0"
print(triangleAndSquare.triangle.sideLength)
// Prints "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Prints "50.0"
```






When working with optional values,
you can write `?` before operations like methods, properties, and subscripting.
If the value before the `?` is `nil`,
everything after the `?` is ignored
and the value of the whole expression is `nil`.
Otherwise, the optional value is unwrapped,
and everything after the `?` acts on the unwrapped value.
In both cases,
the value of the whole expression is an optional value.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```




## Enumerations and Structures

Use `enum` to create an enumeration.
Like classes and all other named types,
enumerations can have methods associated with them.



```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king

    func simpleDescription() -> String {
        switch self {
            case .ace:
                return "ace"
            case .jack:
                return "jack"
            case .queen:
                return "queen"
            case .king:
                return "king"
            default:
                return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```




> Experiment: Write a function that compares two `Rank` values
> by comparing their raw values.

By default, Swift assigns the raw values starting at zero
and incrementing by one each time,
but you can change this behavior by explicitly specifying values.
In the example above, `Ace` is explicitly given a raw value of `1`,
and the rest of the raw values are assigned in order.
You can also use strings or floating-point numbers
as the raw type of an enumeration.
Use the `rawValue` property to access the raw value of an enumeration case.

Use the `init?(rawValue:)` initializer
to make an instance of an enumeration from a raw value.
It returns either the enumeration case matching the raw value
or `nil` if there's no matching `Rank`.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```




The case values of an enumeration are actual values,
not just another way of writing their raw values.
In fact,
in cases where there isn't a meaningful raw value,
you don't have to provide one.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs

    func simpleDescription() -> String {
        switch self {
            case .spades:
                return "spades"
            case .hearts:
                return "hearts"
            case .diamonds:
                return "diamonds"
            case .clubs:
                return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```




> Experiment: Add a `color()` method to `Suit` that returns "black"
> for spades and clubs, and returns "red" for hearts and diamonds.



Notice the two ways that the `hearts` case of the enumeration
is referred to above:
When assigning a value to the `hearts` constant,
the enumeration case `Suit.hearts` is referred to by its full name
because the constant doesn't have an explicit type specified.
Inside the switch,
the enumeration case is referred to by the abbreviated form `.hearts`
because the value of `self` is already known to be a suit.
You can use the abbreviated form
anytime the value's type is already known.

If an enumeration has raw values,
those values are determined as part of the declaration,
which means every instance of a particular enumeration case
always has the same raw value.
Another choice for enumeration cases
is to have values associated with the case ---
these values are determined when you make the instance,
and they can be different for each instance of an enumeration case.
You can think of the associated values
as behaving like stored properties of the enumeration case instance.
For example,
consider the case of requesting
the sunrise and sunset times from a server.
The server either responds with the requested information,
or it responds with a description of what went wrong.



```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}

let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")

switch success {
    case let .result(sunrise, sunset):
        print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
    case let .failure(message):
        print("Failure...  \(message)")
}
// Prints "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```




> Experiment: Add a third case to `ServerResponse` and to the switch.

Notice how the sunrise and sunset times
are extracted from the `ServerResponse` value
as part of matching the value against the switch cases.

Use `struct` to create a structure.
Structures support many of the same behaviors as classes,
including methods and initializers.
One of the most important differences
between structures and classes is that
structures are always copied when they're passed around in your code,
but classes are passed by reference.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```




> Experiment: Write a function that returns an array containing
> a full deck of cards,
> with one card of each combination of rank and suit.

## Concurrency

Use `async` to mark a function that runs asynchronously.

```swift
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}
```




You mark a call to an asynchronous function by writing `await` in front of it.

```swift
func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}
```




Use `async let` to call an asynchronous function,
letting it run in parallel with other asynchronous code.
When you use the value it returns, write `await`.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```




Use `Task` to call asynchronous functions from synchronous code,
without waiting for them to return.

```swift
Task {
    await connectUser(to: "primary")
}
// Prints "Hello Guest, user ID 97"
```




## Protocols and Extensions

Use `protocol` to declare a protocol.

```swift
protocol ExampleProtocol {
     var simpleDescription: String { get }
     mutating func adjust()
}
```




Classes, enumerations, and structures can all adopt protocols.



```swift
class SimpleClass: ExampleProtocol {
     var simpleDescription: String = "A very simple class."
     var anotherProperty: Int = 69105
     func adjust() {
          simpleDescription += "  Now 100% adjusted."
     }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription

struct SimpleStructure: ExampleProtocol {
     var simpleDescription: String = "A simple structure"
     mutating func adjust() {
          simpleDescription += " (adjusted)"
     }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```




> Experiment: Add another requirement to `ExampleProtocol`.
> What changes do you need to make
> to `SimpleClass` and `SimpleStructure`
> so that they still conform to the protocol?

Notice the use of the `mutating` keyword
in the declaration of `SimpleStructure`
to mark a method that modifies the structure.
The declaration of `SimpleClass` doesn't need
any of its methods marked as mutating
because methods on a class can always modify the class.

Use `extension` to add functionality to an existing type,
such as new methods and computed properties.
You can use an extension to add protocol conformance
to a type that's declared elsewhere,
or even to a type that you imported from a library or framework.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
 }
print(7.simpleDescription)
// Prints "The number 7"
```




> Experiment: Write an extension for the `Double` type
> that adds an `absoluteValue` property.

You can use a protocol name just like any other named type ---
for example, to create a collection of objects
that have different types
but that all conform to a single protocol.
When you work with values whose type is a protocol type,
methods outside the protocol definition aren't available.

```swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// Prints "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Uncomment to see the error
```




Even though the variable `protocolValue`
has a runtime type of `SimpleClass`,
the compiler treats it as the given type of `ExampleProtocol`.
This means that you can't accidentally access
methods or properties that the class implements
in addition to its protocol conformance.

## Error Handling

You represent errors using any type that adopts the `Error` protocol.



```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```




Use `throw` to throw an error
and `throws` to mark a function that can throw an error.
If you throw an error in a function,
the function returns immediately and the code that called the function
handles the error.

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```




There are several ways to handle errors.
One way is to use `do`-`catch`.
Inside the `do` block,
you mark code that can throw an error by writing `try` in front of it.
Inside the `catch` block,
the error is automatically given the name `error`
unless you give it a different name.

```swift
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// Prints "Job sent"
```




> Experiment: Change the printer name to `"Never Has Toner"`,
> so that the `send(job:toPrinter:)` function throws an error.





You can provide multiple `catch` blocks
that handle specific errors.
You write a pattern after `catch` just as you do
after `case` in a switch.



```swift
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// Prints "Job sent"
```




> Experiment: Add code to throw an error inside the `do` block.
> What kind of error do you need to throw
> so that the error is handled by the first `catch` block?
> What about the second and third blocks?

Another way to handle errors
is to use `try?` to convert the result to an optional.
If the function throws an error,
the specific error is discarded and the result is `nil`.
Otherwise, the result is an optional containing
the value that the function returned.

```swift
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```




Use `defer` to write a block of code
that's executed after all other code in the function,
just before the function returns.
The code is executed regardless of whether the function throws an error.
You can use `defer` to write setup and cleanup code next to each other,
even though they need to be executed at different times.

```swift
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]

func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }

    let result = fridgeContent.contains(food)
    return result
}
fridgeContains("banana")
print(fridgeIsOpen)
// Prints "false"
```




## Generics

Write a name inside angle brackets
to make a generic function or type.



```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
         result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```




You can make generic forms of functions and methods,
as well as classes, enumerations, and structures.

```swift
// Reimplement the Swift standard library's optional type
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```




Use `where` right before the body
to specify a list of requirements ---
for example,
to require the type to implement a protocol,
to require two types to be the same,
or to require a class to have a particular superclass.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
   return false
}
anyCommonElements([1, 2, 3], [3])
```




> Experiment: Modify the `anyCommonElements(_:_:)` function
> to make a function that returns an array
> of the elements that any two sequences have in common.

Writing `<T: Equatable>`
is the same as writing `<T> ... where T: Equatable`.



