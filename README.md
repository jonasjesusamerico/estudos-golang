# **APRENDENDO SOBRE Golang**
 
## **TOUR PELA LINGUAGEM**
* ### **PACOTES, VARIÁVEIS E FUNÇÕES**.
   * Os programas em GO, é composto por pacotes
   * Por convenção, o nome do pacote tem que ser igual ao último elemento do caminho da impostação. Por exemplo:  `math/rand`, compreende arquivos que começam com `package rand`
   * #### **IMPORTAÇÕES**
       * As importações podem ser feitas de duas maneiras, a primeira seria: `import "fmt"`, que poderia ser feito dessa forma repetidamente para outros pacotes. Mas o recomendado é utilizar `import ("fmt")`, que nesse caso, você poderá adicionar todos os seus importes dentro de um mesmo local, deixando o código mais simplificado
   * #### **EXPORTAÇÕES**
       * Para que se consiga exportar a função criada, é necessário que a mesma contenha a primeira letra MAIÚSCULA, que se comparado a outra linguagem, seria os metodos público, já quando declarado com a primeira letra minuscula, será considerado método privado.
   * #### **FUNÇÕES**
       * As funções em Go suportam zero ou mais argumentos.
       * O tipo do argumento sempre será declarado após o nome, por exemplo: `add(x int, y int) int {}`, assim como para o seu tipo de retorno.
       * Se todos o parâmetros tiverem o mesmo tipo, existe a opção de declarar apenas o tipo para a última propriedade, por exemplo: `func add(x, y int) int {}`
       * As funções em Go, tem a possibilidade de retornar múltiplos resultado, por exemplo:
           ```go
               package main
 
               import "fmt"
 
               func swap(x, y string) (string, string) {
                   return y, x
               }
 
               func main() {
                   a, b := swap("hello", "world")
                   fmt.Println(a, b)
               }
           ```
   * #### **VARIÁVEIS**
       * `var`, utilizado para declarar uma lista de variáveis, como em lista de argumentos de função, o tipo é o último a ser passado.
           * Pode ser declarado a nível de pacto ou a nível de função.
           * Pode conter inicializadores, se for adicionado um inicializador, o seu tipo pode ser omitido, por exemplo:
               ```go
                   package main
 
                   import "fmt"
 
                   var i, j int = 1, 2
 
                   func main() {
                       var c, python, java = true, false, "no!" // Tipos omitidos
                       fmt.Println(i, j, c, python, java)
                   }
               ```
       * `:=`, pode ser utilizado no lugar do `var`. Dessa forma, ela faz a declaração do tipo implicitamente.
           * Só será permitido utilizar em escopo de funções
       * Tipos de variáveis básica disponível em Go
           ```go
               bool
 
               string
 
               int  int8  int16  int32  int64
               uint uint8 uint16 uint32 uint64 uintptr
 
               byte // pseudônimo para uint8
 
               rune // pseudônimo para int32
                   // representa um ponto de código Unicode
 
               float32 float64
 
               complex64 complex128
           ```
           * Os tipos `int, uint` e `uintptr`, são geralmente 32 bits em sistema de 32, e 64 em sistema 64 bits. Geralmente quando preciso utilizar um inteiro, usar `int`. Somente em casos específicos utilizar inteiro com tamanho especificado ou sem sinal.
       * Quando não especificado valores para as variáveis, valores "zero" serão atribuído por default, por exemplo: Para int, será 0. booleanos será false e para string será ""
       * **Conversões de tipos**É possível converter um inteiro para float, de forma simples. Basta passar na forma o valor inteiro no "construtor" do tipo float desejado. Por exemplo:
           ```go
               package main
 
               import (
                   "fmt"
               )
 
               func main() {
                   var x, y int = 3, 4
                   fmt.Println(float64(x), float64(y)) // conversão do tipo
               }
           ```
       * **Inferência de tipo**Quando declarado uma variável se indicar o seu tipo, por exemplo utilizando da forma `:=`, o tipo da variável será baseado no tipo do valor que foi atribuído ao seu lado direito. Por exemplo:
           ```go
               package main
 
               import "fmt"
 
               func main() {
                   var a int
                   fmt.Printf("A é um tipo: %T\n", a) // A é um tipo: int
                   b := a
                   fmt.Printf("B é um tipo: %T\n", b) // B é um tipo: int. Pois o valor atribuído ao lado direito que seria o "a" é um inteiro
                   c := 1.1
                   fmt.Printf("C é um tipo: %T\n", c) // V é um tipo: float.
               }
           ```
           * Quando atribuído ao lado direito uma constante numérica não tipificada, ele poderá ser: `int`, `float64`, ou `complex128` dependendo da precisão da constante.
       * **Constantes**: São declaradas como variáveis, e com a palavra chave `cost`
           * Elas não podem ser declarada usando a sintaxe `:=`
       * **Constantes numéricas**Constantes numéricas também são valores de alta-precisão. Uma constante sem tipo pega o tipo necessário pelo seu contexto.
 
* ### **ESTRUTURAS DE CONTROLE DE FLUXO: FOR, IF, ELSE E SWITCH**
   * O Go tem apenas uma estrutura de laço de repetição, o **`for`**
   * #### **LAÇO DE REPETIÇÃO**
       * ##### **For**
           * Seu funcionamento é semelhante a outras linguagens.
               * Não há necessidade de adicionar os parentes ao lado da expressão e as chaves são obrigatórias.
               ```go
                   package main
 
                   import "fmt"
 
                   func main() {
                       sum := 0
                       for i := 0; i < 10; i++
                           sum += i
 
                       fmt.Println(sum)
                   }
               ```
               * A instrução que faz a declaração do **I** e sua continuação **i++**, são opcionais
               ```go
                   package main
 
                   import "fmt"
 
                   func main() {
                       sum := 1
                       for ; sum < 1000; {
                           sum += sum
                       }
                       fmt.Println(sum)
                   }
               ```
       * ##### **While**
           * No Go, não existe explicitamente o laço **while**. Para conseguir simular um **while**, basta remover o inicializador e o contador do laço for, por exemplo:
           ```go
               package main
 
               import "fmt"
 
               func main() {
                   sum := 1
                   for sum < 1000 {
                       sum += sum
                   }
                   fmt.Println(sum)
               }
 
           ```
   * #### **CONDICIONAIS**
       * **if**: Não precisa ser cercada com os **`()`**  mas as chaves **`{}`** são obrigatórios.
           * Na expressão, é possível que seja declarado uma variável atribuído o valor, e se atender a determinada condição e entrar no **`if`**, essa variável é acessível no escopo do **`if`**, por exemplo:
           ```go
               package main
 
               import (
                   "fmt"
                   "math"
               )
 
               func pow(x, n, lim float64) float64 {
                   if variavel := math.Pow(x, n); variavel < lim {
                       return variavel // Permitido acesso no escopo do IF
                   }
                   return lim
               }
 
               func main() {
                   fmt.Println(
                       pow(3, 2, 10),
                       pow(3, 3, 20),
                   )
               }
 
           ```
       * **if e else**: Funciona semelhante ao contexto do **`if`**, complementando que o acesso a **variavel** também está no escopo do else
       * **Switch**Seu funcionamento é semelhante ao de outras linguagens. Não é necessário declarar o **`break`** ao final de cada **`case`**, pois o **Go** fornece o mesmo automaticamente.
           * Funciona semelhante ao if, pode-se declarar a variável dentro da estrutura e ter acesso ao escopo do **`switch`**, exemplo:
           ```go
               package main
 
               import (
                   "fmt"
               )
 
               func main() {
                   fmt.Print("O valor da variável: ")
                  
                   switch variavel := 10 ; variavel {
                   case 1:
                       fmt.Println("1.")
                   case 2:
                       fmt.Println("2.")
                   default:
                       // Qualquer outro...
                       fmt.Println(variavel)
                   }
               }
           ```
           * Pode também utilizar ele sem condições, utilizado para simplificar a escrita de **`if-else`**
       * **defer**: Tem como funcionamento adiar a execução de uma função qualquer até que a função de origem termine. Por exemplo:
           ```go
               package main
 
               import "fmt"
 
               func main() {
                   defer fmt.Println("world") // imprimir por último. Segura a execução até que termine o restante
 
                   fmt.Println("hello") // imprimir primeiro
               }
           ```
           * É possível que seja empilhada **`if-else`**, o último entrar será o primeiro a sair.