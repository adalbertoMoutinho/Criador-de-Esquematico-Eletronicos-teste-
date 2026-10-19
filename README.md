# Criador de Esquemáticos Eletrônicos

> Protótipo experimental para testar a viabilidade de uma ferramenta de apoio à engenharia reversa de placas eletrônicas, antes de iniciar o desenvolvimento em linguagem C.

## Sobre o projeto

Durante a manutenção e a engenharia reversa de placas eletrônicas, muitas vezes é necessário identificar componentes, mapear seus terminais e reconstruir manualmente as conexões de um circuito.

Este projeto nasceu como um **teste de viabilidade (prova de conceito / PoC)**: antes de investir no desenvolvimento de uma aplicação em C, resolvi experimentar a ideia com **HTML, CSS e JavaScript**, utilizando o Canvas do navegador para representar o esquemático.

A intenção nesta etapa não é substituir softwares profissionais de CAD eletrônico, mas testar a interação, a organização dos componentes e a representação de suas conexões. **O projeto ainda está em fase experimental.**

## Funcionalidades atuais

- Inserção de resistores, capacitores, diodos, transistores e símbolos VCC/GND.
- Criação de circuitos integrados e blocos personalizados com pinos identificados.
- Posicionamento dos componentes com mouse ou coordenadas X/Y, com alinhamento à grade.
- Rotação de componentes em incrementos de 90°.
- Conexão entre terminais pelo mouse ou por comandos de texto.
- Réguas horizontal e vertical e navegação pela área de trabalho.
- Seleção e exclusão de componentes ou conexões.
- Exportação e reabertura do projeto em arquivo JSON.

## Como executar

1. Baixe o arquivo `criadordeesquematico.html` deste repositório.
2. Abra-o em um navegador moderno.
3. Utilize o campo **PROMPT CLI >**, na parte inferior da interface, para inserir comandos. Digite um comando por vez e pressione **Enter** ou clique em **Executar**.

O protótipo funciona diretamente no navegador, sem necessidade de instalar dependências ou configurar um servidor.

## Mini tutorial

### 1. Adicionar componentes

```text
add[R1,10k]
add[C1,100uF]
add[D1,1N4007]
add[Q1,NPN]
```

Cada comando adiciona um componente. O identificador indica o tipo: `R` (resistor), `C` (capacitor), `D` (diodo) e `Q` (transistor).

### 2. Organizar e rotacionar

```text
move[R1,200,200]
move[Q1,400,200]
rotate[R1,90]
```

O comando `move` posiciona um componente nas coordenadas X/Y. Também é possível arrastá-lo com o mouse. `rotate` gira o componente pelo ângulo informado (90°, 180° ou 270°); sem ângulo, gira 90°.

### 3. Criar um componente personalizado

```text
createcomponente[U1,2left,2right,left[pin 1=VCC,pin 2=IN],right[pin 1=OUT,pin 2=GND]]
```

O exemplo cria um bloco `U1` com dois terminais à esquerda e dois à direita, identificados pelos rótulos fornecidos. Outra forma de criar um circuito integrado é:

```text
create[U2,4left,4right]
```

### 4. Conectar os terminais

Ative **Modo Fiação** e clique nos pontos vermelhos dos dois terminais que deseja ligar. Ou use o comando:

```text
connect[R1.2,Q1.B]
```

O exemplo conecta o terminal `2` do resistor `R1` à base (`B`) do transistor `Q1`. Para componentes personalizados, é possível usar referências como `U1.L1` e `U1.R1`.

### 5. Navegar, excluir e salvar

- **Mover tela:** ative o botão correspondente e arraste o fundo; também é possível usar Shift + arrastar no modo normal.
- **Centralizar tela:** retorna ao início da área de trabalho.
- **Excluir componente / Excluir linha:** selecione o item e use o botão correspondente ou a tecla Delete fora do campo de texto.
- **Salvar Projeto:** exporta os componentes, posições, metadados e conexões para `circuito.json`.
- **Abrir Projeto:** seleciona um arquivo JSON anteriormente salvo para restaurar o trabalho.
- **Limpar Tudo:** esvazia a área de trabalho atual.

## Referência rápida dos comandos

| Comando | Exemplo | Finalidade |
| --- | --- | --- |
| `add` | `add[R1,10k]` | Adicionar componente comum |
| `create` | `create[U1,4left,4right]` | Criar bloco de circuito integrado |
| `createcomponente` | `createcomponente[U1,1left,1right,left[pin 1=IN],right[pin 1=OUT]]` | Criar bloco com pinos nomeados |
| `move` | `move[R1,400,200]` | Posicionar por coordenadas |
| `rotate` | `rotate[R1,90]` | Rotacionar componente |
| `connect` | `connect[R1.2,Q1.B]` | Conectar dois terminais |
| `delete` | `delete[R1]` | Excluir componente e seus fios |
| `deletewire` | `deletewire[1]` | Excluir conexão pelo índice (a partir de 1) |

Os comandos são digitados individualmente no prompt da aplicação.

## Limitações desta versão

Esta é uma ferramenta de **desenho e documentação experimental**, não um simulador elétrico. O protótipo ainda não implementa simulação de circuitos, verificação elétrica das conexões, roteamento avançado ou exportação para formatos profissionais de CAD eletrônico. As conexões são representadas graficamente entre terminais, com segmentos ortogonais.

## Próximos passos (ideias para desenvolvimento)

- Reestruturar o projeto para uma implementação em **C**.
- Separar o núcleo de componentes/conexões, o interpretador de comandos, a interface gráfica e a persistência.
- Evoluir a representação de conexões para nós elétricos (*nets*), incluindo múltiplos terminais.
- Ampliar a biblioteca de símbolos e a edição dos componentes.
- Melhorar as ferramentas de navegação, desenho e documentação de placas analisadas.

Esses itens são objetivos futuros, não funcionalidades já concluídas.

## Motivação

O objetivo deste experimento é responder a uma pergunta simples: **vale a pena desenvolver uma ferramenta própria para apoiar a reconstrução de esquemáticos durante a engenharia reversa de placas eletrônicas?**

Este protótipo é o primeiro passo para testar a proposta, encontrar dificuldades e aprender antes de começar a versão em C.

---

**Tecnologias do protótipo:** HTML · CSS · JavaScript · Canvas · JSON  
**Estado:** Prova de conceito / Em desenvolvimento
