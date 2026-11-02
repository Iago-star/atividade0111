# Relatório — Um algoritmo, diferentes linguagens: listas, arrays e repetições

**Unidade curricular:** Algoritmos e Programação
**Professor:** Alexandre de Oliveira — Montanha
**Dupla:**

| Nome completo | RA |
|---|---|
| [PREENCHER: nome do integrante 1] | [PREENCHER: RA] |
| [PREENCHER: nome do integrante 2] | [PREENCHER: RA] |

> **Como usar este rascunho:** tudo que está entre `[PREENCHER: ...]` precisa ser completado pela dupla, porque depende de coisas que só vocês podem informar (minutos da gravação, páginas do livro, prints, parágrafos pessoais). O restante é um rascunho: leiam, entendam, testem e reescrevam com as palavras de vocês onde achar necessário. Apaguem este aviso antes de entregar.

---

## 1. Análise da aula

Aula gravada: https://youtu.be/JzwH1EVyO1Q

**1. Por que utilizamos laços de repetição?**

Usamos laços de repetição para executar o mesmo trecho de código várias vezes sem precisar escrever o código repetido. No nosso caso, em vez de escrever um `println` para cada time, usamos um `for` que percorre a coleção inteira. Isso também faz o programa funcionar para qualquer quantidade de times: quando entrou o Tombense, não precisamos mudar os laços, só a coleção. (Minuto da gravação: [PREENCHER: mm:ss])

**2. Qual é a diferença entre `while` e `do-while`? Exemplo em que essa diferença é importante.**

No `while` a condição é testada **antes** de executar o bloco, então o bloco pode não executar nenhuma vez. No `do-while` a condição é testada **depois**, então o bloco executa **pelo menos uma vez**.

Exemplo em que isso importa: pedir uma senha ao usuário e repetir enquanto ela estiver errada. Precisamos pedir a senha pelo menos uma vez antes de saber se está certa, então o `do-while` é o mais adequado:

```java
String senha;
do {
    senha = leitor.nextLine();   // pede a senha pelo menos uma vez
} while (!senha.equals("1234"));
```

Com `while`, teríamos que ler a senha antes do laço também, repetindo código. (Minuto da gravação: [PREENCHER: mm:ss])

**3. No exemplo dos times em C#, por que são necessários dois laços?**

Porque cada confronto envolve **dois** times: o mandante e o visitante. O laço de fora escolhe o mandante (índice `i`) e, para cada mandante, o laço de dentro percorre todos os times para escolher o visitante (índice `j`). Com um laço só conseguiríamos percorrer os times um por um, mas não combinar um time com todos os outros.

**4. Qual é a função do `if` que impede confrontos de um time contra ele mesmo?**

Os dois laços percorrem a coleção inteira, então em algum momento `i` e `j` apontam para o mesmo time (ex.: Cruzeiro x Cruzeiro). O `if (i != j)` só deixa exibir e contar o jogo quando os índices são diferentes, descartando essas combinações.

**5. Comparando Java, C# e Rust: duas diferenças de sintaxe e um conceito lógico que permanece igual.**

- Diferença 1: a forma de saber o tamanho da coleção. Em Java é `times.length` (sem parênteses, array), em C# é `times.Count` e em Rust é `times.len()` (método).
- Diferença 2: o `for`. Em Java e C# usamos `for (int i = 0; i < n; i++)`, e em Rust usamos `for i in 0..n`, com `println!` (macro, com `!`) para imprimir e `let mut` para variáveis que mudam.
- O que permanece igual: o raciocínio. Dois laços aninhados percorrendo os índices, um `if` comparando `i` com `j`, e um contador que soma a cada jogo exibido.

(Minuto da gravação: [PREENCHER: mm:ss])

> **Atenção:** o enunciado pede que pelo menos duas respostas indiquem o minuto:segundo da gravação. Assistam ao vídeo, conferam se as respostas acima batem com o que o professor explica e preencham os minutos. Se o professor mostrou algo diferente do que está aqui, ajustem o texto.

---

## 2. Leitura e relação com o livro

**Referência consultada:** BHARGAVA, Aditya. *Entendendo Algoritmos: um guia ilustrado para programadores e outros curiosos*. Capítulo 2.
**Edição:** [PREENCHER: edição/ano do exemplar consultado]
**Seções consultadas:** [PREENCHER: títulos das seções do capítulo 2 lidas — memória, arrays, listas encadeadas, inserção e exclusão]
**Páginas:** [PREENCHER: ex. pp. XX–YY]

**1. Como os elementos de um array são organizados e acessados?**

Os elementos de um array ficam em posições de memória **vizinhas** (contíguas), uma logo depois da outra. Por isso o computador consegue calcular a posição de qualquer elemento a partir do endereço inicial e do índice, e acessar direto, sem passar pelos anteriores. É o que fazemos com `times[2]`. O livro compara a memória a uma fileira de gavetas e explica que, por isso, ler um elemento de um array é rápido.

**2. Como os elementos de uma lista encadeada são organizados? Desenho simples.**

Os elementos podem ficar **espalhados** pela memória. Cada elemento guarda o seu valor e o endereço do próximo. Para chegar no terceiro, é preciso começar no primeiro e seguir os endereços.

```
Array (posições vizinhas na memória, acesso direto pelo índice):

 índice:   0             1            2             3
        +-------------+------------+-------------+-------------+
        | Atlético-MG | Cruzeiro   | América-MG  | Villa Nova  |
        +-------------+------------+-------------+-------------+

Lista encadeada (cada nó aponta para o próximo):

 +-----------------+      +-------------+      +--------------+      +--------------+
 | Atlético-MG | * |----->| Cruzeiro | * |----->| América-MG | *|----->| Villa Nova |X|
 +-----------------+      +-------------+      +--------------+      +--------------+
   (X = fim da lista)
```

**3. Por que inserir ou excluir elementos pode exigir operações diferentes nessas duas estruturas?**

No array, como os elementos estão lado a lado, inserir ou excluir no meio obriga a **deslocar** os elementos seguintes para abrir ou fechar espaço. Além disso, o tamanho de um array é fixo: se não há espaço, é preciso criar outro maior e copiar tudo (foi o que fizemos em Java). Na lista encadeada, para inserir ou excluir basta **mudar os ponteiros** dos nós vizinhos, sem mover os outros elementos. Em compensação, para chegar até a posição desejada é preciso percorrer a lista a partir do começo, e ler um elemento no meio é mais lento do que no array.

**4. Uma coleção chamada "lista" em uma linguagem é necessariamente uma lista encadeada? (`List<string>` de C# e `Vec<String>` de Rust)**

Não. O nome "lista" não garante a estrutura por trás:

- **`List<T>` do C#:** pela documentação da Microsoft, ela guarda os elementos em um **array interno** e, quando enche, aloca um array maior e copia os elementos. É uma lista dinâmica baseada em array. A lista encadeada em C# é outra classe, a `LinkedList<T>`.
- **`Vec<T>` do Rust:** é um vetor dinâmico que guarda os elementos em um bloco **contíguo** de memória, com um tamanho (`len`) e uma capacidade (`capacity`). Quando a capacidade acaba, ele realoca para um bloco maior. A lista encadeada do Rust é a `LinkedList<T>`, em `std::collections`.

Em resumo: array, lista dinâmica e lista encadeada não são sinônimos. `List<string>` e `Vec<String>` são listas dinâmicas apoiadas em arrays.

Fontes pesquisadas: [PREENCHER: confirmar e colar os links consultados — documentação da Microsoft sobre `List<T>` e documentação do Rust (doc.rust-lang.org) sobre `Vec`]

**5. Para guardar os times e percorrê-los repetidamente, quais vantagens vocês identificam em uma estrutura baseada em array?**

- Acesso direto pelo índice (`times[i]`), que é exatamente o que os dois laços usam o tempo todo.
- Como os elementos estão em sequência, percorrer do início ao fim é simples e eficiente.
- O tamanho conhecido (`length`, `Count`, `len()`) deixa fácil definir os limites dos laços.
- Os índices permitiram resolver o turno único sem coleção auxiliar, só começando o laço interno em `i + 1`.

Relação com o trabalho: o problema precisa ler vários times várias vezes pelos índices, e isso é o ponto forte da estrutura baseada em array. Já a inserção do Tombense mostrou a limitação do array puro (tamanho fixo).

---

## 3. Desafio prático — Gerador de confrontos

Código-fonte nas pastas `java/`, `csharp/` e `rust/`. As três versões atendem aos requisitos:

| Requisito | Onde está no código |
|---|---|
| RF-01 exibir os times com índices | método/função `exibirTimes` / `ExibirTimes` / `exibir_times` |
| RF-02 ida e volta com dois laços aninhados | `idaEVolta` / `IdaEVolta` / `ida_e_volta` |
| RF-03 impedir time contra ele mesmo | `if (i != j)` |
| RF-04 contar os confrontos | variável `jogos` |
| RF-05 turno único sem coleção auxiliar | laço interno começando em `i + 1` |
| RF-06 contar os jogos do turno único | variável `jogos` em `turnoUnico` / `TurnoUnico` / `turno_unico` |

Estruturas usadas: Java com `String[]`, C# com `List<string>` e Rust com `Vec<String>` (inicializado com `vec!`).

**Evidências de execução**

- Java: [PREENCHER: print da execução da dupla] (saída de referência em `evidencias/saida_java.txt`)
- C#: [PREENCHER: print da execução da dupla com `dotnet run`]
- Rust: [PREENCHER: print da execução da dupla] (saída de referência em `evidencias/saida_rust.txt`)

---

## 4. Alteração da coleção (inclusão do Tombense)

Depois das duas tabelas com 4 times, cada versão acrescenta o Tombense e gera as tabelas novamente.

- **Java:** cria `novoArray` com 5 posições, copia os 4 times com um `for` e coloca o Tombense na posição 4.
- **C#:** `times.Add("Tombense");`
- **Rust:** `times.push(String::from("Tombense"));`

**1. Por que o array de Java exigiu a criação de outro array?**

Porque um array em Java tem tamanho fixo, definido na criação. O array original tem 4 posições e não dá para aumentá-lo. Para ter espaço para o quinto time foi preciso criar um array novo de tamanho 5 e copiar os 4 elementos antigos.

**2. O que ficou mais simples com `List<string>` e `Vec<String>`?**

Adicionar o elemento: uma única chamada (`Add` ou `push`) resolve. Não precisamos criar outra coleção nem escrever o laço de cópia, porque a própria estrutura cuida de aumentar o espaço quando necessário.

**3. A facilidade de adicionar um elemento significa que essas estruturas são listas encadeadas?**

Não. Como pesquisamos na seção 2, `List<string>` e `Vec<String>` são listas dinâmicas apoiadas em arrays: quando o espaço acaba, elas alocam um bloco maior e copiam os elementos por baixo dos panos. A facilidade vem dessa automação, não de ponteiros entre nós. Prova disso é que continuamos acessando por índice (`times[i]`), o que é característico de array.

---

## 5. Comparação das sintaxes

| Operação | Java | C# | Rust |
|---|---|---|---|
| Criar a coleção | `String[] times = {"Atlético-MG", "Cruzeiro", "América-MG", "Villa Nova"};` | `List<string> times = new List<string> { "Atlético-MG", "Cruzeiro", "América-MG", "Villa Nova" };` | `let mut times: Vec<String> = vec![String::from("Atlético-MG"), String::from("Cruzeiro"), String::from("América-MG"), String::from("Villa Nova")];` |
| Consultar a quantidade de elementos | `times.length` | `times.Count` | `times.len()` |
| Acessar um elemento pelo índice | `times[i]` | `times[i]` | `times[i]` |
| Escrever um laço para percorrer a coleção | `for (int i = 0; i < times.length; i++) { ... }` | `for (int i = 0; i < times.Count; i++) { ... }` | `for i in 0..times.len() { ... }` |
| Escrever dois laços aninhados | `for (int i = 0; i < times.length; i++) { for (int j = 0; j < times.length; j++) { ... } }` | `for (int i = 0; i < times.Count; i++) { for (int j = 0; j < times.Count; j++) { ... } }` | `for i in 0..times.len() { for j in 0..times.len() { ... } }` |
| Impedir confronto contra o próprio time | `if (i != j) { ... }` | `if (i != j) { ... }` | `if i != j { ... }` |
| Acrescentar o quinto time | `String[] novoArray = new String[5]; for (...) { novoArray[i] = times[i]; } novoArray[4] = "Tombense"; times = novoArray;` | `times.Add("Tombense");` | `times.push(String::from("Tombense"));` |

**O que mudou na escrita dos programas e o que permaneceu igual no raciocínio?**

Mudou a sintaxe: a forma de declarar a coleção, o nome da propriedade ou método do tamanho (`length`, `Count`, `len()`), o formato do `for` em Rust (`for i in 0..n`), o `println!` com `!` e as chaves `{}` do Rust, o `let mut` para variáveis que mudam, e principalmente a forma de acrescentar um elemento. Em Java, a coleção é um array de tamanho fixo e precisou de cópia manual.

Permaneceu igual o raciocínio: guardar os times em uma coleção indexada, percorrer com dois laços aninhados pelos índices, comparar `i` com `j` para evitar o confronto contra si mesmo, começar o laço interno em `i + 1` para o turno único e contar os jogos exibidos. O algoritmo é o mesmo nas três linguagens, e as saídas foram idênticas.

---

## 6. Teste de mesa e validação

**Teste de mesa da tabela de ida e volta com Atlético-MG (0), Cruzeiro (1) e América-MG (2):**

| Índice do primeiro time | Índice do segundo time | Combinação examinada | Exibe o jogo? Por quê? |
|---|---|---|---|
| 0 | 0 | Atlético-MG x Atlético-MG | Não: `i == j`, o time contra ele mesmo |
| 0 | 1 | Atlético-MG x Cruzeiro | Sim: `i != j` |
| 0 | 2 | Atlético-MG x América-MG | Sim: `i != j` |
| 1 | 0 | Cruzeiro x Atlético-MG | Sim: `i != j` (mandos invertidos) |
| 1 | 1 | Cruzeiro x Cruzeiro | Não: `i == j` |
| 1 | 2 | Cruzeiro x América-MG | Sim: `i != j` |
| 2 | 0 | América-MG x Atlético-MG | Sim: `i != j` |
| 2 | 1 | América-MG x Cruzeiro | Sim: `i != j` |
| 2 | 2 | América-MG x América-MG | Não: `i == j` |

Foram 9 combinações examinadas e 6 jogos exibidos, o que bate com a execução dos programas (3 times).

**Resultados obtidos nos programas:**

| Quantidade de times | Jogos de ida e volta | Jogos em turno único |
|---|---|---|
| 3 | 6 | 3 |
| 4 | 12 | 6 |
| 5 | 20 | 10 |

**1. Por que a quantidade de combinações examinadas pode ser maior que a quantidade de jogos exibidos?**

Porque os laços examinam **todas** as combinações de índices, inclusive as em que `i == j`, e o `if` descarta essas. Com 3 times, são 9 combinações examinadas (3 × 3) e 6 jogos exibidos; as 3 diferenças são os times contra eles mesmos. Com n times, examinamos n² combinações e exibimos n × (n − 1).

**2. O que acontece com a quantidade de confrontos quando acrescentamos um time?**

Ela cresce mais do que proporcionalmente. Na ida e volta o total é n × (n − 1): 6, 12 e 20 jogos para 3, 4 e 5 times. Ao passar de 4 para 5 times, foram 8 jogos a mais (o novo time joga em casa contra 4 e fora contra 4). No turno único o total é n × (n − 1) / 2: 3, 6 e 10, ou seja, 4 jogos a mais ao chegar no quinto time (um contra cada time que já existia).

**3. As três linguagens produziram os mesmos jogos e totais? Caso contrário, identifiquem e corrijam a diferença.**

Sim. Comparamos as saídas e os jogos, a ordem e os totais foram idênticos nas versões em Java e em Rust (a comparação foi feita com `diff` nos arquivos de `evidencias/`). A versão em C# deve ser executada pela dupla para confirmar os mesmos totais. [PREENCHER: confirmar que a saída do C# é igual e anotar aqui o resultado]

---

## 7. Organização e participação da dupla

**Evidências de execução das três versões:** ver seção 3. [PREENCHER: prints]

**Um erro encontrado e como foi corrigido**

Ao rodar a versão em Java no terminal, os acentos apareceram trocados por `?` (por exemplo, `Atl?tico-MG` e `Combina??es`), enquanto a versão em Rust mostrava os acentos corretamente. A lógica estava certa; o problema era a codificação de caracteres da saída do terminal. Corrigimos executando o Java com `java -Dfile.encoding=UTF-8 -Dstdout.encoding=UTF-8 Campeonato` (no Windows também ajuda usar `chcp 65001`). Depois disso a saída ficou idêntica à do Rust. Esse comando está registrado no `README.md`.

> Se a dupla encontrou outro erro durante os testes, troque este texto pelo erro de vocês.

**Contribuição de cada integrante**

[PREENCHER: Integrante 1 — um parágrafo explicando o que você fez (programação, revisão, testes, relatório) e qual foi seu principal aprendizado.]

[PREENCHER: Integrante 2 — um parágrafo explicando o que você fez (programação, revisão, testes, relatório) e qual foi seu principal aprendizado.]

**Uso de IA**

- **Ferramenta utilizada:** Claude (Anthropic).
- **Como foi utilizada:** a ferramenta gerou a primeira versão do código das três linguagens, o rascunho das respostas deste relatório, o README e a estrutura do repositório. A ferramenta executou as versões em Java e em Rust e comparou as saídas; a versão em C# não pôde ser executada no ambiente dela e precisa ser testada pela dupla.
- **O que a dupla fez:** [PREENCHER: descrevam com sinceridade o que vocês fizeram — assistiram à aula, leram o capítulo 2, executaram o C#, conferiram as respostas, reescreveram trechos, tiraram os prints, etc.]
- O uso de IA não substitui a responsabilidade de compreender, testar e explicar o código.

**Referências consultadas**

- BHARGAVA, Aditya. *Entendendo Algoritmos: um guia ilustrado para programadores e outros curiosos*. Capítulo 2. [PREENCHER: edição, editora e ano]
- Aula gravada do professor Alexandre de Oliveira: https://youtu.be/JzwH1EVyO1Q
- Documentação do C#/.NET sobre `List<T>` e `LinkedList<T>`. [PREENCHER: link consultado]
- Documentação do Rust sobre `Vec<T>` e `LinkedList<T>`. [PREENCHER: link consultado]
- Documentação do Java sobre arrays. [PREENCHER: link, se consultado]
