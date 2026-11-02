# Um algoritmo, diferentes linguagens: listas, arrays e repetições

**Unidade curricular:** Algoritmos e Programação
**Professor:** Alexandre de Oliveira — Montanha
**Atividade:** Gerador de confrontos de um pequeno campeonato (Java, C# e Rust)

## Dupla

| Nome completo | RA |
|---|---|
| [PREENCHER: nome do integrante 1] | [PREENCHER: RA] |
| [PREENCHER: nome do integrante 2] | [PREENCHER: RA] |

## Estrutura do repositório

```
.
├── README.md
├── relatorio.md
├── evidencias/
├── java/
│   └── Campeonato.java
├── csharp/
│   ├── Program.cs
│   └── CampeonatoCSharp.csproj
└── rust/
    ├── Cargo.toml
    └── src/main.rs
```

Pastas de compilação (`bin`, `obj`, `target`) não são versionadas (ver `.gitignore`).

## Como executar

### Java (array de `String`)

```bash
cd java
javac Campeonato.java
java Campeonato
```

Se os acentos aparecerem como `?` no terminal (acontece no Windows), use:

```bash
java -Dfile.encoding=UTF-8 -Dstdout.encoding=UTF-8 Campeonato
```

No Windows também ajuda rodar `chcp 65001` antes.

### C# (`List<string>`)

Requer o SDK do .NET (`dotnet --version` para conferir).

```bash
cd csharp
dotnet run
```

### Rust (`Vec<String>`)

Requer o Rust instalado pelo rustup (`rustc --version` e `cargo --version` para conferir).

```bash
cd rust
cargo run
```

## O que cada programa faz

1. Exibe os 4 times com seus índices (Atlético-MG, Cruzeiro, América-MG, Villa Nova).
2. Gera a tabela de **ida e volta** com dois laços aninhados e um `if` que impede um time de jogar contra ele mesmo, e conta os jogos.
3. Gera a tabela de **turno único** só com os índices (o laço interno começa em `i + 1`), sem coleção auxiliar, e conta os jogos.
4. Acrescenta o **Tombense** (Java: cria um novo array de tamanho 5 e copia com laço; C#: `Add`; Rust: `push`) e repete as tabelas.
5. Roda também uma validação com 3 times, usada na seção 6 do relatório.

## Resultados esperados

| Times | Ida e volta | Turno único |
|---|---|---|
| 3 | 6 | 3 |
| 4 | 12 | 6 |
| 5 | 20 | 10 |

## Uso de IA

Foi utilizada a ferramenta **Claude (Anthropic)** para gerar a primeira versão do código, o rascunho do relatório e a estrutura do repositório. Os detalhes estão na seção "Uso de IA" do `relatorio.md`.
