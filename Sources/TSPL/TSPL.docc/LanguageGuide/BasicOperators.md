

# Operadores básicos

Um operador é um símbolo ou frase que você pode usar para verificar, mudar ou combinar valores.
Por exemplo, o operador de adição (`+`) soma dois números,
como em `let i = 1 + 2`,
e o operador lógico E (*AND* - `&&`) combina dois valores booleanos,
como em `if enteredDoorCode && passedRetinaScan`.

Swift suporta os operadores que você já conhece de linguagens como C,
e melhora vários recursos para eliminar erros comuns de codificação.
O operador de atribuição (`=`) não retorna um valor,
para evitar que seja usado erroneamente quando
o operador igual a (`==`) é pretendido.
Operadores aritméticos (`+`, `-`, `*`, `/`, `%` e assim por diante)
detectam e desabilitam estouros de valor,
para evitar resultados inesperados quando estamos trabalhando com números que se tornam muito maiores ou muito menores do que o intervalo permitido nos tipos que os armazenam.
Você pode ativar o comportamento de estouro de valor
usando os operadores de estouro do Swift,
conforme descrito em <doc:OperadoresAvançados#Operadores-de-estouro>.

Swift também fornece operadores de intervalo que não são encontrados em C,
como `a..<b` e `a...b`, como um atalho para expressar um intervalo de valores.
Este capítulo descreve os operadores comuns em Swift.
<doc:OperadoresAvançados> abrange os operadores avançados do Swift,
e descreve como definir seus próprios operadores personalizados
e implementar os operadores padrão para seus próprios tipos personalizados.

## Terminologia

Os operadores são unários, binários ou ternários:

- Operadores **unários** operam em um único alvo (como `-a`).
  Operadores unários **pré-fixados** aparecem imediatamente antes de seu destino (como `!b`),
  e operadores unários **pós-fixados** aparecem imediatamente após seu destino (como `c!`).
- Operadores **binários** operam com dois alvos (como `2 + 3`)
  e são **infixos** porque aparecem entre seus dois alvos.
- Operadores **ternários** operam em três alvos.
  Como C, Swift tem apenas um operador ternário,
  o operador condicional ternário (`a ? b : c`).
  
Os valores que os operadores afetam são **operandos**.
Na expressão `1 + 2`, o símbolo `+` é um operador infixo
e seus dois operandos são os valores `1` e `2`.

## Operador de atribuição
O **operador de atribuição** (`a = b`)
inicializa ou atualiza o valor de `a` com o valor de `b`:

```swift
let b = 10
var a = 5
a = b
// 'a' agora é igual a 10
```


@Comment {
  - test: `assignmentOperator`
  
  ```swifttest
  -> let b = 10
  -> var a = 5
  -> a = b
  /> a is now equal to \(a)
  </ a is now equal to 10
  ```
}

Se o lado direito da atribuição for uma tupla com vários valores,
seus elementos podem ser decompostos em várias constantes ou variáveis de uma só vez:

```swift
let (x, y) = (1, 2)
// 'x' é igual a 1, e 'y' é igual a 2
```


@Comment {
  - test: `assignmentOperator`
  
  ```swifttest
  -> let (x, y) = (1, 2)
  /> x is equal to \(x), and y is equal to \(y)
  </ x is equal to 1, and y is equal to 2
  ```
}

@Comment {
  - test: `tuple-unwrapping-with-var`
  
  ```swifttest
  >> var (x, y) = (1, 2)
  ```
}

@Comment {
  Isso ainda permite a atribuição para variáveis,
  mesmo que os padrões var tenham sido removidos,
  porque é analisado como uma declaração de variável,
  usando a primeira alternativa onde (x, y) é um padrão,
  mas `var` vem da *variable-declaration-head*
  em vez do padrão.
  
}

Ao contrário do operador de atribuição em C e Objective-C,
o operador de atribuição em Swift não retorna um valor.
A seguinte declaração não é válida:

```swift
if x = y {
   // Isso não é válido, pois 'x = y' não retorna um valor.
}
```


@Comment {
  - test: `assignmentOperatorInvalid`
  
  ```swifttest
  -> if x = y {
        // This isn't valid, because x = y doesn't return a value.
     }
  !$ error: cannot find 'x' in scope
  !! if x = y {
  !!    ^
  !$ error: cannot find 'y' in scope
  !! if x = y {
  !!        ^
  ```
}

Este recurso evita que o operador de atribuição (`=`) seja usado acidentalmente
quando o operador igual a (`==`) é o que se pretende.
Tornando `if x = y` inválido,
O Swift ajuda você a evitar esses tipos de erros em seu código.

@Comment {
  TODO: Devemos mencionar que (`x = y = z`) também não é válido?
  Em caso afirmativo, há um argumento convincente sobre por quê isso é uma coisa boa?
  
}

## Operadores aritméticos

O Swift suporta os quatro **operadores aritméticos** padrão para todos os tipos de números:

- Adição (`+`)
- Subtração (`-`)
- Multiplicação (`*`)
- Divisão (`/`)

```swift
1 + 2       // igual a 3
5 - 3       // igual a 2
2 * 3       // igual a 6
10.0 / 2.5  // igual a 4.0
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  >> let r0 =
  -> 1 + 2       // equals 3
  >> assert(r0 == 3)
  >> let r1 =
  -> 5 - 3       // equals 2
  >> assert(r1 == 2)
  >> let r2 =
  -> 2 * 3       // equals 6
  >> assert(r2 == 6)
  >> let r3 =
  -> 10.0 / 2.5  // equals 4.0
  >> assert(r3 == 4.0)
  ```
}

Ao contrário dos operadores aritméticos em C e Objective-C,
os operadores aritméticos do Swift não permitem que os valores estourem por padrão.
Você pode optar por avaliar o comportamento de estouro usando os operadores de estouro do Swift
(como em `a &+ b`). Consulte <doc:OperadoresAvançados#Operadores-de-Estouro>.

O operador de adição também é pode ser usado para fazer concatenação de `String`:

```swift
"hello, " + "world"  // igual a "hello, world"
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  >> let r4 =
  -> "hello, " + "world"  // equals "hello, world"
  >> assert(r4 == "hello, world")
  ```
}

### Operador de resto de divisão

O **operador de resto de divisão** (`a % b`)
calcula quantos múltiplos de `b` caberão dentro de `a`
e retorna o valor que sobrou
(conhecido como **resto**).

> Nota: O operador de resto (`%`) também é conhecido como
> um **operador de módulo** em outras linguagens.
> No entanto, seu comportamento em Swift para números negativos significa que,
> estritamente falando, é um resto e não uma operação de módulo.

@Comment {
  - test: `percentOperatorIsRemainderNotModulo`
  
  ```swifttest
  -> for i in -5...0 {
        print(i % 4)
     }
  << -1
  << 0
  << -3
  << -2
  << -1
  << 0
  ```
}

Veja como o operador de resto funciona.
Para calcular `9 % 4`, você primeiro calcula quantos `4`s caberão dentro de `9`:

![](remainderInteger)

Você pode colocar dois `4`s dentro de um `9`, e o resto é `1`.

Em Swift, isso seria escrito como:

```swift
9 % 4    // igual a 1
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  >> let r5 =
  -> 9 % 4    // equals 1
  >> assert(r5 == 1)
  ```
}

Para determinar a resposta para `a % b`,
o operador `%` calcula a seguinte equação
e retorna `restante` como sua saída:

`a` = (`b` x `some multiplier`) + `remainder`

onde `some multiplier` é o maior número de múltiplos de `b`
que caberão dentro de `a`.

Inserir `9` e `4` nesta equação produz:

`9` = (`4` x `2`) + `1`

O mesmo método é aplicado ao calcular o restante para um valor negativo de `a`:

```swift
-9 % 4   // igual a -1
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  >> let r6 =
  -> -9 % 4   // equals -1
  >> assert(r6 == -1)
  ```
}

Inserir `-9` e `4` na equação produz:

`-9` = (`4` x `-2`) + `-1`

dando para o resto um valor de `-1`.

O sinal de `b` é ignorado para valores negativos de `b`.
Isso significa que `a % b` e `a % -b` sempre dão a mesma resposta.

### Operador Unário: Menos

O sinal de um valor numérico pode ser alternado usando um prefixo `-`,
conhecido como o **operador de menos unário**:

```swift
let three = 3
let minusThree = -three       // 'minusThree' é igual a -3
let plusThree = -minusThree   // 'plusThree' é igual a 3, or "menos menos 'three' "
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  -> let three = 3
  -> let minusThree = -three       // minusThree é igual a -3
  -> let plusThree = -minusThree   // plusThree é igual a, or "menos menos 'three' "
  ```
}

O operador de menos unário (`-`) é prefixado diretamente antes do valor em que opera,
sem nenhum espaço em branco.

### Operador Unário: Soma

O **operador unário de soma** (`+`) simplesmente retorna
o valor em que opera, sem qualquer alteração:

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // 'alsoMinusSix' é igual a -6
```


@Comment {
  - test: `arithmeticOperators`
  
  ```swifttest
  -> let minusSix = -6
  -> let alsoMinusSix = +minusSix  // 'alsoMinusSix' é igual a -6
  >> assert(alsoMinusSix == minusSix)
  ```
}

Embora o operador unário de soma não faça nada,
você pode usá-lo para fornecer simetria em seu código para números positivos
ao usar também o operador de menos unário para números negativos.

## Operadores de atribuição composta

Assim como C, Swift fornece **operadores de atribuição composta** que combinam atribuição (`=`) com outra operação.
Um exemplo é o **operador de atribuição de adição** (`+=`):

```swift
var a = 1
a += 2
// 'a' agora é igual a 3
```


@Comment {
  - test: `compoundAssignment`
  
  ```swifttest
  -> var a = 1
  -> a += 2
  /> a is now equal to \(a)
  </ a is now equal to 3
  ```
}

A expressão `a += 2` é um atalho para `a = a + 2`.
Efetivamente, a adição e a atribuição são combinadas em um operador
que executa as duas tarefas ao mesmo tempo.

> Nota: Os operadores de atribuição compostos não retornam um valor.
> Por exemplo, você não pode escrever `let b = a += 2`.

Para obter informações sobre os operadores fornecidos pela biblioteca padrão Swift,
consulte [Operadores de Declaração](https://developer.apple.com/documentation/swift/operator_declarations).

## Operadores de Comparação

Swift suporta os seguintes operadores de comparação:

- Igual a (`a == b`)
- Diferente de (`a != b`)
- Maior que (`a > b`)
- Menor que (`a < b`)
- Maior ou igual a (`a >= b`)
- Menor ou igual a (`a <= b`)

> Nota: Swift também fornece dois **operadores de referência** (`===` e `!==`),
> que você usa para testar se duas referências de objeto se referem à mesma instância de objeto.
> Para obter mais informações, consulte <doc:ClassesEStructs#Operadores-de-Referência>.

Cada um dos operadores de comparação retorna um valor `Bool` para indicar se a declaração é verdadeira ou não:

```swift
1 == 1   // true porque 1 é igual a 1
2 != 1   // true porque 2 não é igual a 1
2 > 1    // true porque 2 é maior que 1
1 < 2    // true porque 1 é menor que 2
1 >= 1   // true porque 1 é maior ou igual a 1
2 <= 1   // false porque 2 não é menor ou igual a 1
```


@Comment {
  - test: `comparisonOperators`
  
  ```swifttest
  >> assert(
  -> 1 == 1   // true porque 1 é igual a 1
  >> )
  >> assert(
  -> 2 != 1   // true porque 2 não é igual a 1
  >> )
  >> assert(
  -> 2 > 1    // true porque 2 é maior que 1
  >> )
  >> assert(
  -> 1 < 2    // true porque 1 é menor que 2
  >> )
  >> assert(
  -> 1 >= 1   // true porque 1 é maior ou igual a 1
  >> )
  >> assert( !(
  -> 2 <= 1   // false porque 2 não é menor ou igual a 1
  >> ) )
  ```
}

Operadores de comparação são frequentemente usados em declarações condicionais,
como a instrução `if`:

```swift
let name = "world"
if name == "world" {
   print("hello, world")
} else {
   print("I'm sorry \(name), but I don't recognize you")
}
// Imprime "hello, world", porque 'name' é, de fato, igual a "world".
```


@Comment {
  - test: `comparisonOperators`
  
  ```swifttest
  -> let name = "world"
  -> if name == "world" {
        print("hello, world")
     } else {
        print("I'm sorry \(name), but I don't recognize you")
     }
  << hello, world
  // Imprime "hello, world", porque 'name' é, de fato, igual a "world".
  ```
}

Para saber mais sobre a instrução `if`, veja <doc:ControleDeFluxo>.

Você pode comparar
duas tuplas se elas tiverem o mesmo tipo e o mesmo número de valores.
As tuplas são comparadas da esquerda para a direita,
um valor de cada vez,
até que a comparação encontre dois valores
que não são iguais.
Esses dois valores são comparados,
e o resultado dessa comparação
determina o resultado geral da comparação de tuplas.
Se todos os elementos forem iguais,
então as próprias tuplas são iguais. 
Por exemplo:

```swift
(1, "zebra") < (2, "apple")   // true porque 1 é menor que 2; "zebra" e "apple" não são comparados
(3, "apple") < (3, "bird")    // true porque 3 é igual a 3 e "apple" é menor que "bird"
(4, "dog") == (4, "dog")      // true porque 4 é igual a 4 e "dog" é igual a "dog"
```


@Comment {
  - test: `tuple-comparison-operators`
  
  ```swifttest
  >> let a =
  -> (1, "zebra") < (2, "apple")   //  true porque 1 é menor que 2; "zebra" e "apple" não são comparados
  >> let b =
  -> (3, "apple") < (3, "bird")    // true porque 3 é igual a 3 e "apple" é menor que "bird"
  >> let c =
  -> (4, "dog") == (4, "dog")      // true porque 4 é igual a 4 e "dog" é igual a "dog"
  >> print(a, b, c)
  << true true true
  ```
}

No exemplo acima,
você pode ver o comportamento de comparação da esquerda para a direita na primeira linha.
Como `1` é menor que `2`,
`(1, "zebra")` é considerado menor que `(2, "apple")`,
independentemente de quaisquer outros valores nas tuplas.
Não importa que `"zebra"` não seja menor que `"apple"`,
porque a comparação já é determinada pelos primeiros elementos das tuplas.
No entanto,
quando os primeiros elementos das tuplas são os mesmos,
seus segundos elementos **são** comparados ---
isso é o que acontece na segunda e terceira linha.

Tuplas podem ser comparadas com um determinado operador somente se o operador
pode ser aplicado a cada valor nas respectivas tuplas. Por exemplo,
conforme demonstrado no código abaixo, você pode comparar
duas tuplas do tipo `(String, Int)` porque
ambos os valores `String` e `Int` podem ser comparados
usando o operador `<`. Em contrapartida,
duas tuplas do tipo `(String, Bool)` não podem ser comparadas
com o operador `<` porque o operador `<` não pode ser aplicado a
valores `Bool`.

```swift
("blue", -1) < ("purple", 1)        // OK, avalia como true
("blue", false) < ("purple", true)  // Erro, pois < não pode ser usado para valores Booleanos

```


@Comment {
  - test: `tuple-comparison-operators-err`
  
  ```swifttest
  >> _ =
  -> ("blue", -1) < ("purple", 1)        // OK, avalia como true
  >> _ =
  -> ("blue", false) < ("purple", true)  // Erro, pois < não pode ser usado para valores Booleanos
  !$ error: type '(String, Bool)' cannot conform to 'Comparable'
  !! ("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
  !!                 ^
  !$ note: only concrete types such as structs, enums and classes can conform to protocols
  !! ("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
  !!                 ^
  !$ note: required by referencing operator function '<' on 'Comparable' where 'Self' = '(String, Bool)'
  !! ("blue", false) < ("purple", true)  // Error because < can't compare Boolean values
  !!                 ^
  ```
}

@Comment {
  - test: `tuple-comparison-operators-ok`
  
  ```swifttest
  >> let x = ("blue", -1) < ("purple", 1)        // OK, avalia como true
  >> print(x)
  << true
  ```
}

> Nota: A biblioteca padrão do Swift inclui operadores de comparação de tuplas
> para tuplas com menos de sete elementos.
> Para comparar tuplas com sete ou mais elementos,
> você mesmo deve implementar os operadores de comparação.

@Comment {
  TODO: em quais tipos eles operam por padrão?
  Como eles trabalham com *strings*?
  E com seus próprios tipos?
}

## Operador Condicional Ternário

The *ternary conditional operator* is a special operator with three parts,
which takes the form `question ? answer1 : answer2`.
It's a shortcut for evaluating one of two expressions
based on whether `question` is true or false.
If `question` is true, it evaluates `answer1` and returns its value;
otherwise, it evaluates `answer2` and returns its value.

The ternary conditional operator is shorthand for the code below:

```swift
if question {
   answer1
} else {
   answer2
}
```


@Comment {
  - test: `ternaryConditionalOperatorOutline`
  
  ```swifttest
  >> let question = true
  >> let answer1 = true
  >> let answer2 = true
  -> if question {
        answer1
     } else {
        answer2
     }
  !! /tmp/swifttest.swift:5:4: warning: expression of type 'Bool' is unused
  !! answer1
  !! ^~~~~~~
  !! /tmp/swifttest.swift:7:4: warning: expression of type 'Bool' is unused
  !! answer2
  !! ^~~~~~~
  ```
}

@Comment {
  FIXME This example has too much hand waving.
  Swift doesn't have 'if' expressions.
}

Here's an example, which calculates the height for a table row.
The row height should be 50 points taller than the content height
if the row has a header, and 20 points taller if the row doesn't have a header:

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```


@Comment {
  - test: `ternaryConditionalOperatorPart1`
  
  ```swifttest
  -> let contentHeight = 40
  -> let hasHeader = true
  -> let rowHeight = contentHeight + (hasHeader ? 50 : 20)
  /> rowHeight is equal to \(rowHeight)
  </ rowHeight is equal to 90
  ```
}

The example above is shorthand for the code below:

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight: Int
if hasHeader {
   rowHeight = contentHeight + 50
} else {
   rowHeight = contentHeight + 20
}
// rowHeight is equal to 90
```


@Comment {
  - test: `ternaryConditionalOperatorPart2`
  
  ```swifttest
  -> let contentHeight = 40
  -> let hasHeader = true
  -> let rowHeight: Int
  -> if hasHeader {
        rowHeight = contentHeight + 50
     } else {
        rowHeight = contentHeight + 20
     }
  /> rowHeight is equal to \(rowHeight)
  </ rowHeight is equal to 90
  ```
}

The first example's use of the ternary conditional operator means that
`rowHeight` can be set to the correct value on a single line of code,
which is more concise than the code used in the second example.

The ternary conditional operator provides
an efficient shorthand for deciding which of two expressions to consider.
Use the ternary conditional operator with care, however.
Its conciseness can lead to hard-to-read code if overused.
Avoid combining multiple instances of the ternary conditional operator into one compound statement.

## Nil-Coalescing Operator

The *nil-coalescing operator* (`a ?? b`)
unwraps an optional `a` if it contains a value,
or returns a default value `b` if `a` is `nil`.
The expression `a` is always of an optional type.
The expression `b` must match the type that's stored inside `a`.

The nil-coalescing operator is shorthand for the code below:

```swift
a != nil ? a! : b
```


@Comment {
  - test: `nilCoalescingOperatorOutline`
  
  ```swifttest
  >> var a: Int?
  >> let b = 42
  >> let c =
  -> a != nil ? a! : b
  >> print(c)
  << 42
  ```
}

The code above uses the ternary conditional operator and forced unwrapping (`a!`)
to access the value wrapped inside `a` when `a` isn't `nil`,
and to return `b` otherwise.
The nil-coalescing operator provides a more elegant way to encapsulate
this conditional checking and unwrapping in a concise and readable form.

> Note: If the value of `a` is non-`nil`,
> the value of `b` isn't evaluated.
> This is known as *short-circuit evaluation*.

The example below uses the nil-coalescing operator to choose between
a default color name and an optional user-defined color name:

```swift
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
```


@Comment {
  - test: `nilCoalescingOperator`
  
  ```swifttest
  -> let defaultColorName = "red"
  -> var userDefinedColorName: String?   // defaults to nil
  ---
  -> var colorNameToUse = userDefinedColorName ?? defaultColorName
  /> userDefinedColorName is nil, so colorNameToUse is set to the default of \"\(colorNameToUse)\"
  </ userDefinedColorName is nil, so colorNameToUse is set to the default of "red"
  ```
}

The `userDefinedColorName` variable is defined as an optional `String`,
with a default value of `nil`.
Because `userDefinedColorName` is of an optional type,
you can use the nil-coalescing operator to consider its value.
In the example above, the operator is used to determine
an initial value for a `String` variable called `colorNameToUse`.
Because `userDefinedColorName` is `nil`,
the expression `userDefinedColorName ?? defaultColorName` returns
the value of `defaultColorName`, or `"red"`.

If you assign a non-`nil` value to `userDefinedColorName`
and perform the nil-coalescing operator check again,
the value wrapped inside `userDefinedColorName` is used instead of the default:

```swift
userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName isn't nil, so colorNameToUse is set to "green"
```


@Comment {
  - test: `nilCoalescingOperator`
  
  ```swifttest
  -> userDefinedColorName = "green"
  -> colorNameToUse = userDefinedColorName ?? defaultColorName
  /> userDefinedColorName isn't nil, so colorNameToUse is set to \"\(colorNameToUse)\"
  </ userDefinedColorName isn't nil, so colorNameToUse is set to "green"
  ```
}

## Range Operators

Swift includes several *range operators*,
which are shortcuts for expressing a range of values.

### Closed Range Operator

The *closed range operator* (`a...b`)
defines a range that runs from `a` to `b`,
and includes the values `a` and `b`.
The value of `a` must not be greater than `b`.

@Comment {
  - test: `closedRangeStartCanBeLessThanEnd`
  
  ```swifttest
  -> let range = 1...2
  >> print(type(of: range))
  << ClosedRange<Int>
  ```
}

@Comment {
  - test: `closedRangeStartCanBeTheSameAsEnd`
  
  ```swifttest
  -> let range = 1...1
  ```
}

@Comment {
  - test: `closedRangeStartCannotBeGreaterThanEnd`
  
  ```swifttest
  -> let range = 1...0
  xx assertion
  ```
}

The closed range operator is useful when iterating over a range
in which you want all of the values to be used,
such as with a `for`-`in` loop:

```swift
for index in 1...5 {
   print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```


@Comment {
  - test: `rangeOperators`
  
  ```swifttest
  -> for index in 1...5 {
        print("\(index) times 5 is \(index * 5)")
     }
  </ 1 times 5 is 5
  </ 2 times 5 is 10
  </ 3 times 5 is 15
  </ 4 times 5 is 20
  </ 5 times 5 is 25
  ```
}

For more about `for`-`in` loops, see <doc:ControlFlow>.

### Half-Open Range Operator

The *half-open range operator* (`a..<b`)
defines a range that runs from `a` to `b`,
but doesn't include `b`.
It's said to be *half-open*
because it contains its first value, but not its final value.
As with the closed range operator,
the value of `a` must not be greater than `b`.
If the value of `a` is equal to `b`,
then the resulting range will be empty.

@Comment {
  - test: `halfOpenRangeStartCanBeLessThanEnd`
  
  ```swifttest
  -> let range = 1..<2
  >> print(type(of: range))
  << Range<Int>
  ```
}

@Comment {
  - test: `halfOpenRangeStartCanBeTheSameAsEnd`
  
  ```swifttest
  -> let range = 1..<1
  ```
}

@Comment {
  - test: `halfOpenRangeStartCannotBeGreaterThanEnd`
  
  ```swifttest
  -> let range = 1..<0
  xx assertion
  ```
}

Half-open ranges are particularly useful when you work with
zero-based lists such as arrays,
where it's useful to count up to (but not including) the length of the list:

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
   print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```


@Comment {
  - test: `rangeOperators`
  
  ```swifttest
  -> let names = ["Anna", "Alex", "Brian", "Jack"]
  -> let count = names.count
  >> assert(count == 4)
  -> for i in 0..<count {
        print("Person \(i + 1) is called \(names[i])")
     }
  </ Person 1 is called Anna
  </ Person 2 is called Alex
  </ Person 3 is called Brian
  </ Person 4 is called Jack
  ```
}

Note that the array contains four items,
but `0..<count` only counts as far as `3`
(the index of the last item in the array),
because it's a half-open range.
For more about arrays, see <doc:CollectionTypes#Arrays>.

### One-Sided Ranges

The closed range operator
has an alternative form for ranges that continue
as far as possible in one direction ---
for example,
a range that includes all the elements of an array
from index 2 to the end of the array.
In these cases, you can omit the value
from one side of the range operator.
This kind of range is called a *one-sided range*
because the operator has a value on only one side.
For example:

```swift
for name in names[2...] {
    print(name)
}
// Brian
// Jack

for name in names[...2] {
    print(name)
}
// Anna
// Alex
// Brian
```


@Comment {
  - test: `rangeOperators`
  
  ```swifttest
  -> for name in names[2...] {
         print(name)
     }
  </ Brian
  </ Jack
  ---
  -> for name in names[...2] {
         print(name)
     }
  </ Anna
  </ Alex
  </ Brian
  ```
}

The half-open range operator also has
a one-sided form that's written
with only its final value.
Just like when you include a value on both sides,
the final value isn't part of the range.
For example:

```swift
for name in names[..<2] {
    print(name)
}
// Anna
// Alex
```


@Comment {
  - test: `rangeOperators`
  
  ```swifttest
  -> for name in names[..<2] {
         print(name)
     }
  </ Anna
  </ Alex
  ```
}

One-sided ranges can be used in other contexts,
not just in subscripts.
You can't iterate over a one-sided range
that omits a first value,
because it isn't clear where iteration should begin.
You *can* iterate over a one-sided range that omits its final value;
however, because the range continues indefinitely,
make sure you add an explicit end condition for the loop.
You can also check whether a one-sided range contains a particular value,
as shown in the code below.

```swift
let range = ...5
range.contains(7)   // false
range.contains(4)   // true
range.contains(-1)  // true
```


@Comment {
  - test: `rangeOperators`
  
  ```swifttest
  -> let range = ...5
  >> print(type(of: range))
  << PartialRangeThrough<Int>
  >> let a =
  -> range.contains(7)   // false
  >> let b =
  -> range.contains(4)   // true
  >> let c =
  -> range.contains(-1)  // true
  >> print(a, b, c)
  << false true true
  ```
}

## Logical Operators

*Logical operators* modify or combine
the Boolean logic values `true` and `false`.
Swift supports the three standard logical operators found in C-based languages:

- Logical NOT (`!a`)
- Logical AND (`a && b`)
- Logical OR (`a || b`)

### Logical NOT Operator

The *logical NOT operator* (`!a`) inverts a Boolean value so that `true` becomes `false`,
and `false` becomes `true`.

The logical NOT operator is a prefix operator,
and appears immediately before the value it operates on,
without any white space.
It can be read as “not `a`”, as seen in the following example:

```swift
let allowedEntry = false
if !allowedEntry {
   print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```


@Comment {
  - test: `logicalOperators`
  
  ```swifttest
  -> let allowedEntry = false
  -> if !allowedEntry {
        print("ACCESS DENIED")
     }
  <- ACCESS DENIED
  ```
}

The phrase `if !allowedEntry` can be read as “if not allowed entry.”
The subsequent line is only executed if “not allowed entry” is true;
that is, if `allowedEntry` is `false`.

As in this example,
careful choice of Boolean constant and variable names
can help to keep code readable and concise,
while avoiding double negatives or confusing logic statements.

### Logical AND Operator

The *logical AND operator* (`a && b`) creates logical expressions
where both values must be `true` for the overall expression to also be `true`.

If either value is `false`,
the overall expression will also be `false`.
In fact, if the *first* value is `false`,
the second value won't even be evaluated,
because it can't possibly make the overall expression equate to `true`.
This is known as *short-circuit evaluation*.

This example considers two `Bool` values
and only allows access if both values are `true`:

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```


@Comment {
  - test: `logicalOperators`
  
  ```swifttest
  -> let enteredDoorCode = true
  -> let passedRetinaScan = false
  -> if enteredDoorCode && passedRetinaScan {
        print("Welcome!")
     } else {
        print("ACCESS DENIED")
     }
  <- ACCESS DENIED
  ```
}

### Logical OR Operator

The *logical OR operator*
(`a || b`) is an infix operator made from two adjacent pipe characters.
You use it to create logical expressions in which
only *one* of the two values has to be `true`
for the overall expression to be `true`.

Like the Logical AND operator above,
the Logical OR operator uses short-circuit evaluation to consider its expressions.
If the left side of a Logical OR expression is `true`,
the right side isn't evaluated,
because it can't change the outcome of the overall expression.

In the example below,
the first `Bool` value (`hasDoorKey`) is `false`,
but the second value (`knowsOverridePassword`) is `true`.
Because one value is `true`,
the overall expression also evaluates to `true`,
and access is allowed:

```swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```


@Comment {
  - test: `logicalOperators`
  
  ```swifttest
  -> let hasDoorKey = false
  -> let knowsOverridePassword = true
  -> if hasDoorKey || knowsOverridePassword {
        print("Welcome!")
     } else {
        print("ACCESS DENIED")
     }
  <- Welcome!
  ```
}

### Combining Logical Operators

You can combine multiple logical operators to create longer compound expressions:

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```


@Comment {
  - test: `logicalOperators`
  
  ```swifttest
  -> if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
        print("Welcome!")
     } else {
        print("ACCESS DENIED")
     }
  <- Welcome!
  ```
}

This example uses multiple `&&` and `||` operators to create a longer compound expression.
However, the `&&` and `||` operators still operate on only two values,
so this is actually three smaller expressions chained together.
The example can be read as:

If we've entered the correct door code and passed the retina scan,
or if we have a valid door key,
or if we know the emergency override password,
then allow access.

Based on the values of `enteredDoorCode`, `passedRetinaScan`, and `hasDoorKey`,
the first two subexpressions are `false`.
However, the emergency override password is known,
so the overall compound expression still evaluates to `true`.

> Note: The Swift logical operators `&&` and `||` are left-associative,
> meaning that compound expressions with multiple logical operators
> evaluate the leftmost subexpression first.

### Explicit Parentheses

It's sometimes useful to include parentheses when they're not strictly needed,
to make the intention of a complex expression easier to read.
In the door access example above,
it's useful to add parentheses around the first part of the compound expression
to make its intent explicit:

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
   print("Welcome!")
} else {
   print("ACCESS DENIED")
}
// Prints "Welcome!"
```


@Comment {
  - test: `logicalOperators`
  
  ```swifttest
  -> if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
        print("Welcome!")
     } else {
        print("ACCESS DENIED")
     }
  <- Welcome!
  ```
}

The parentheses make it clear that the first two values
are considered as part of a separate possible state in the overall logic.
The output of the compound expression doesn't change,
but the overall intention is clearer to the reader.
Readability is always preferred over brevity;
use parentheses where they help to make your intentions clear.


@Comment {
This source file is part of the Swift.org open source project

Copyright (c) 2014 - 2022 Apple Inc. and the Swift project authors
Licensed under Apache License v2.0 with Runtime Library Exception

See https://swift.org/LICENSE.txt for license information
See https://swift.org/CONTRIBUTORS.txt for the list of Swift project authors
}
