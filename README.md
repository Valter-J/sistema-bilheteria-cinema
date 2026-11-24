# Sistema de Bilheteria de Cinema

Sistema de bilheteria desenvolvido em **linguagem C** para o projeto prático da disciplina Bases da Computação 1 — Algoritmos.

O sistema permitirá consultar filmes, visualizar assentos, reservar e comprar ingressos, consultar bilhetes, cancelar compras, simular reembolsos e emitir relatórios de vendas.

## Objetivos do projeto

- Aplicar modularização por meio de funções e procedimentos.
- Trabalhar com passagem de parâmetros e escopo de variáveis.
- Utilizar vetores unidimensionais, matrizes e strings.
- Aplicar estruturas condicionais (`if/else` e `switch/case`).
- Aplicar estruturas de repetição (`for`, `while` e `do/while`).
- Validar entradas e impedir operações inconsistentes.

## Regras e restrições

O desenvolvimento seguirá as regras do enunciado:

- Linguagem C.
- Não utilizar `struct`.
- Não utilizar alocação dinâmica (`malloc`, `calloc`, `realloc` ou `free`).
- Não declarar nem manipular ponteiros explicitamente.
- Não utilizar listas encadeadas.
- Não inserir comentários no código-fonte; a organização e os nomes devem tornar a lógica compreensível.
- Utilizar vetores e matrizes de capacidade previamente definida.
- Manter os registros em memória durante a execução; persistência em arquivos não é obrigatória.

> A passagem convencional de vetores e matrizes como parâmetros é permitida pelo enunciado.

## Funcionalidades do sistema

O menu principal terá as opções:

1. Consultar filmes disponíveis.
2. Visualizar assentos.
3. Reservar assento e comprar ingresso.
4. Consultar e exibir bilhete.
5. Cancelar compra e realizar reembolso.
6. Exibir relatório de vendas.
7. Sair do sistema.

O menu deverá permanecer ativo até que o usuário escolha a opção de encerramento.

## Arquitetura e hierarquia de funções

A função `main()` será responsável por inicializar o sistema, exibir o menu, obter a opção escolhida e encaminhar a execução para o módulo correspondente. As regras de cada operação ficarão em funções específicas.

```text
main()
├── inicializarSistema()
│   ├── inicializarAssentos()
│   └── inicializarContadores()
├── exibirMenu()
├── obterOpcaoMenu()
└── switch (opcao)
    ├── consultarFilmes()
    │   └── exibirDadosFilme()
    ├── visualizarAssentos()
    │   ├── selecionarFilme()
    │   └── exibirMatrizAssentos()
    ├── reservarIngresso()
    │   ├── selecionarFilme()
    │   ├── exibirMatrizAssentos()
    │   ├── solicitarAssento()
    │   ├── validarAssento()
    │   ├── solicitarNomeCliente()
    │   ├── selecionarTipoIngresso()
    │   ├── selecionarCombo()
    │   ├── calcularValorCompra()
    │   ├── gerarNumeroBilhete()
    │   └── registrarBilhete()
    │       ├── atualizarMatrizAssentos()
    │       └── atualizarEstatisticas()
    ├── consultarBilhete()
    │   ├── solicitarNumeroBilhete()
    │   ├── localizarBilhete()
    │   └── exibirBilhete()
    ├── cancelarCompra()
    │   ├── solicitarNumeroBilhete()
    │   ├── localizarBilhete()
    │   ├── verificarSituacaoBilhete()
    │   ├── exibirBilhete()
    │   ├── confirmarCancelamento()
    │   └── processarReembolso()
    │       ├── atualizarSituacaoBilhete()
    │       ├── liberarAssento()
    │       └── atualizarEstatisticas()
    ├── gerarRelatorio()
    │   ├── calcularEstatisticas()
    │   └── exibirRelatorio()
    └── encerrarSistema()
```

As funções compartilhadas — por exemplo, `selecionarFilme()`, `exibirMatrizAssentos()` e `localizarBilhete()` — deverão ser implementadas uma única vez e reutilizadas pelos módulos.

## Estruturas de dados previstas

A proposta inicial é utilizar vetores e matrizes de tamanho fixo. Os tamanhos poderão ser ajustados em conjunto antes da implementação.

| Estrutura | Finalidade |
|---|---|
| `filmes[3][100]` | Títulos dos filmes |
| `horarios[3]` | Horários das sessões |
| `precos[3]` | Preços dos ingressos inteiros |
| `assentos[3][5][6]` | Assentos de cada sessão |
| `numeroBilhete[100]` | Identificadores dos bilhetes |
| `nomeCliente[100][100]` | Nomes dos clientes |
| `filmeBilhete[100]` | Filme associado à compra |
| `linhaBilhete[100]` | Linha do assento |
| `colunaBilhete[100]` | Coluna do assento |
| `tipoIngresso[100]` | Tipo de ingresso |
| `combo[100]` | Indicação de combo |
| `valorPago[100]` | Valor total da compra |
| `situacao[100]` | Situação do bilhete |

**Atenção:** os dados de um mesmo bilhete ocuparão a mesma posição nos respectivos vetores. O limite inicial previsto é de 100 registros. O contador de numeração dos bilhetes deverá ser independente da quantidade de bilhetes ativos, para que um número cancelado nunca seja reutilizado durante a execução.

## Organização de diretórios planejada

```text
sistema-bilheteria-cinema/
├── README.md
├── .gitignore
└── src/
    └── main.c
```

Inicialmente, o projeto poderá ficar em um único arquivo `.c`, organizado em protótipos, funções e `main()`. A separação em vários arquivos só deverá ser adotada se o grupo e o professor concordarem que ela é adequada ao conteúdo trabalhado.

## Estratégia de branches

Trabalharemos com **5 branches no total**: uma principal e quatro de desenvolvimento.

| Branch | Responsabilidade |
|---|---|
| `main` | Versão estável e integrada do projeto |
| `develop/menu-inicializacao` | Menu, inicialização e consulta de filmes |
| `develop/assentos` | Matrizes, seleção de filme e visualização de assentos |
| `develop/reservas-bilhetes` | Reservas, compras, geração, registro e consulta de bilhetes |
| `develop/cancelamento-relatorios` | Cancelamentos, reembolsos e relatórios |

### Fluxo de trabalho

1. Atualizar a branch de trabalho com a versão mais recente da `main`.
2. Implementar e testar a funcionalidade na branch correspondente.
3. Registrar as alterações com commits pequenos e objetivos.
4. Abrir um Pull Request para `main`.
5. Revisar e testar a integração.
6. Fazer o merge somente quando a funcionalidade estiver funcionando.

A `main` não deverá receber desenvolvimento direto. A branch `develop` não será criada neste planejamento para manter o total em cinco branches.

## Checklist de implementação

### 1. Estrutura inicial e menu

- [ ] Definir constantes e capacidades máximas.
- [ ] Declarar os vetores e matrizes necessários.
- [ ] Criar os protótipos das funções.
- [ ] Implementar `inicializarSistema()`.
- [ ] Implementar `inicializarAssentos()`.
- [ ] Implementar `inicializarContadores()`.
- [ ] Implementar `exibirMenu()`.
- [ ] Implementar `obterOpcaoMenu()`.
- [ ] Implementar o laço principal com `do/while`.
- [ ] Implementar o `switch/case` do menu.
- [ ] Tratar opções inválidas.

### 2. Consulta de filmes

- [ ] Definir pelo menos três filmes.
- [ ] Armazenar títulos em strings.
- [ ] Definir horário e preço de cada sessão.
- [ ] Implementar `consultarFilmes()`.
- [ ] Implementar `exibirDadosFilme()`.
- [ ] Implementar `selecionarFilme()` com validação.

### 3. Assentos

- [ ] Criar uma matriz própria para cada sessão.
- [ ] Inicializar todos os assentos com `D`.
- [ ] Implementar `visualizarAssentos()`.
- [ ] Implementar `exibirMatrizAssentos()`.
- [ ] Identificar linhas e colunas na exibição.
- [ ] Validar limites de linha e coluna.
- [ ] Impedir reserva de assento ocupado.
- [ ] Garantir que sessões diferentes não compartilhem ocupação.

### 4. Reservas e compras

- [ ] Implementar `reservarIngresso()`.
- [ ] Implementar `solicitarAssento()`.
- [ ] Implementar `validarAssento()`.
- [ ] Implementar `solicitarNomeCliente()`.
- [ ] Implementar `selecionarTipoIngresso()`.
- [ ] Calcular meia-entrada como 50% do ingresso inteiro.
- [ ] Implementar `selecionarCombo()`.
- [ ] Definir o preço do combo.
- [ ] Implementar `calcularValorCompra()`.
- [ ] Implementar `gerarNumeroBilhete()`.
- [ ] Implementar `registrarBilhete()`.
- [ ] Implementar `atualizarMatrizAssentos()`.
- [ ] Implementar `atualizarEstatisticas()`.
- [ ] Impedir novas compras quando os 100 registros forem preenchidos.

### 5. Consulta de bilhetes

- [ ] Implementar `solicitarNumeroBilhete()`.
- [ ] Implementar `localizarBilhete()`.
- [ ] Implementar `consultarBilhete()`.
- [ ] Implementar `exibirBilhete()`.
- [ ] Exibir todos os dados exigidos no enunciado.
- [ ] Informar quando o bilhete não for encontrado.
- [ ] Exibir corretamente a situação ativo/cancelado.

### 6. Cancelamento e reembolso

- [ ] Implementar `cancelarCompra()`.
- [ ] Verificar se o bilhete existe.
- [ ] Verificar se o bilhete está ativo.
- [ ] Implementar `verificarSituacaoBilhete()`.
- [ ] Apresentar os dados antes da confirmação.
- [ ] Implementar `confirmarCancelamento()`.
- [ ] Implementar `processarReembolso()`.
- [ ] Implementar `atualizarSituacaoBilhete()`.
- [ ] Implementar `liberarAssento()`.
- [ ] Atualizar as estatísticas financeiras.
- [ ] Impedir cancelamento duplicado.
- [ ] Manter o registro do bilhete cancelado.

### 7. Relatórios

- [ ] Implementar `gerarRelatorio()`.
- [ ] Contabilizar ingressos ativos.
- [ ] Contabilizar ingressos inteiros.
- [ ] Contabilizar meias-entradas.
- [ ] Contabilizar combos vendidos.
- [ ] Contabilizar bilhetes cancelados.
- [ ] Calcular arrecadação com ingressos.
- [ ] Calcular arrecadação com combos.
- [ ] Calcular total de reembolsos.
- [ ] Calcular arrecadação líquida.
- [ ] Implementar `exibirRelatorio()`.
- [ ] Conferir consistência dos valores após cancelamentos.

### 8. Encerramento e testes finais

- [ ] Implementar `encerrarSistema()`.
- [ ] Exibir relatório final ao sair.
- [ ] Exibir mensagem de encerramento.
- [ ] Testar todas as opções do menu.
- [ ] Testar entradas inválidas.
- [ ] Testar assento ocupado.
- [ ] Testar limite de registros.
- [ ] Testar cancelamento e liberação do assento.
- [ ] Testar tentativa de cancelar duas vezes.
- [ ] Testar numeração única após cancelamentos.
- [ ] Testar os cálculos do relatório.
- [ ] Compilar e executar o programa sem erros.

## Critérios de conclusão

O projeto será considerado pronto quando:

- Todas as funcionalidades obrigatórias estiverem implementadas.
- Os dados dos bilhetes permanecerem consistentes entre os vetores.
- As matrizes de assentos forem atualizadas em reservas e cancelamentos.
- O relatório distinguir compras, reembolsos e arrecadação líquida.
- As entradas inválidas forem tratadas.
- O código respeitar as restrições do enunciado.
- O grupo conseguir demonstrar e explicar a implementação.

## Compilação

Com GCC instalado, o comando inicial de compilação será:

```bash
gcc src/main.c -o bilheteria
```

Para executar no Linux/macOS:

```bash
./bilheteria
```

No Windows:

```bash
bilheteria.exe
```

---

**Projeto acadêmico — Bases da Computação 1: Algoritmos**

O planejamento poderá ser atualizado conforme as decisões do grupo e a evolução da implementação.
