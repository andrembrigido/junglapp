# ███████ 🐊 Crocroller — Padrão Universal de Gerenciamento de Estado ███████

Este documento define o padrão oficial de gerenciamento de estado do
**Junglapp 2.0**.

O Crocroller define:

* onde o estado deve existir;
* quem pode alterá-lo;
* quem pode observá-lo;
* quando o estado deve ser local;
* quando deve ser compartilhado;
* quando deve ser persistido;
* quando uma solução mais robusta é realmente necessária.

O objetivo é manter o estado:

* previsível;
* simples;
* rastreável;
* fácil de testar;
* fácil de refatorar;
* independente de linguagem ou framework.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**O ESTADO DEVE VIVER O MAIS PERTO POSSÍVEL DE QUEM PRECISA DELE.**

Começar:

**LOCAL**

Promover somente quando necessário:

**COMPARTILHADO**

Persistir somente quando necessário:

**PERSISTENTE**

A filosofia é:

**MENOR ESCOPO POSSÍVEL → MENOR COMPLEXIDADE POSSÍVEL**

---

> ░░░░░░░ O Que é Estado ░░░░░░░

Estado é qualquer informação que pode mudar durante a execução e alterar o
comportamento do sistema.

Exemplos:

```text
isLoading

selectedUser

currentPage

cartItems

loginStatus

volume

themeMode

currentCharacter
```

Nem toda variável precisa ser tratada como um sistema de estado.

---

> ░░░░░░░ Estado Não é Persistência ░░░░░░░

Estado representa o valor **durante a execução**.

Persistência representa o valor **salvo para uso posterior**.

Exemplo:

```text
volume
   ↓
ESTADO ATUAL
```

Se precisar sobreviver ao fechamento:

```text
volume
   ↓
ESTADO
   ↓
DATABEEZZE
   ↓
PERSISTÊNCIA
```

O Crocroller controla o estado.

O DataBeezze controla sua persistência.

---

> ░░░░░░░ Classificação Oficial ░░░░░░░

O Junglapp divide estado em quatro níveis principais:

| Nível | Tipo              | Uso                           |
| ----: | ----------------- | ----------------------------- |
|     1 | **Local**         | Um componente                 |
|     2 | **Feature**       | Uma funcionalidade            |
|     3 | **Compartilhado** | Várias partes do projeto      |
|     4 | **Persistente**   | Precisa sobreviver à execução |

A complexidade deve aumentar somente quando o estado subir de nível.

---

> ░░░░░░░ 1 — Estado Local ░░░░░░░

Estado local pertence somente a uma pequena parte da aplicação.

Exemplos:

```text
menu aberto

campo selecionado

hover

aba atual

animação ativa

senha visível
```

Se apenas um componente precisa desse estado:

**MANTER LOCAL.**

Não criar controller global, store ou biblioteca externa para uma necessidade
local simples.

---

> ░░░░░░░ Exemplo Conceitual ░░░░░░░

```text
COMPONENTE

isOpen = false

clicou
   ↓
isOpen = true
```

Nenhuma arquitetura adicional é necessária.

---

> ░░░░░░░ 2 — Estado da Feature ░░░░░░░

Quando várias partes da mesma funcionalidade dependem do estado, ele pode subir
para o nível da feature.

Exemplo:

```text
LOGIN

email
password
isLoading
hasError
loginStatus
```

Esses valores pertencem ao fluxo de login.

Não precisam automaticamente existir globalmente.

---

> ░░░░░░░ Estado Dentro do Arquivo Único ░░░░░░░

Durante a construção inicial do Junglapp, o estado pode permanecer dentro do
arquivo principal.

Organizar usando Snake.

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ ESTADO                                                                  ║
   ║ FUTURO ARQUIVO: login_str                                               ║
   ║ RESPONSABILIDADE: controlar o estado do fluxo de login                  ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ************************ CONFIGURAÇÕES ************************************ */


/* ************************ ESTADO ******************************************* */

bool isLoading = false;
bool hasError = false;


/* ************************ AÇÕES ******************************************** */
```

Quando a complexidade justificar:

**EXTRAIR.**

---

> ░░░░░░░ 3 — Estado Compartilhado ░░░░░░░

Estado compartilhado é utilizado por múltiplas partes realmente independentes.

Exemplos:

```text
usuário autenticado

tema

idioma

carrinho

sessão global
```

Não tornar algo global apenas porque talvez seja reutilizado futuramente.

A regra é:

**LOCAL PRIMEIRO → GLOBAL SOMENTE QUANDO NECESSÁRIO**

---

> ░░░░░░░ Estado Global Tem Custo ░░░░░░░

Quanto mais global o estado:

* mais componentes podem alterá-lo;
* mais difícil rastrear mudanças;
* maior o risco de dependências ocultas;
* maior a complexidade de testes.

Portanto:

**ESTADO GLOBAL É UMA FERRAMENTA, NÃO UM PADRÃO AUTOMÁTICO.**

---

> ░░░░░░░ 4 — Estado Persistente ░░░░░░░

Quando o estado precisa sobreviver a:

* fechamento do app;
* reinicialização;
* mudança de dispositivo;
* logout ou login, dependendo da regra;

ele deixa de ser apenas estado em memória.

Fluxo:

```text
CROCROLLER
    ↓
ESTADO
    ↓
DATABEEZZE
    ↓
PERSISTÊNCIA
```

Exemplos:

```text
preferências

configurações do usuário

sessão

progresso

favoritos
```

---

> ░░░░░░░ Um Dono por Estado ░░░░░░░

Todo estado importante deve possuir um responsável claro.

A regra é:

**UM ESTADO → UM DONO PRINCIPAL**

Evitar:

```text
COMPONENTE A altera
COMPONENTE B altera
COMPONENTE C altera
COMPONENTE D altera
```

sem uma regra clara.

Preferir:

```text
           ┌→ COMPONENTE A
           │
ESTADO ← CONTROLLER
           │
           ├→ COMPONENTE B
           │
           └→ COMPONENTE C
```

O controller ou estrutura equivalente controla as alterações.

---

> ░░░░░░░ Leitura e Escrita ░░░░░░░

Sempre que possível, separar conceitualmente:

**OBSERVAR ESTADO**

de:

**ALTERAR ESTADO**

Exemplo:

```text
UI
 ↓
LÊ ESTADO

UI
 ↓
ENVIA AÇÃO
 ↓
CONTROLLER
 ↓
ALTERA ESTADO
```

Isso torna o fluxo mais previsível.

---

> ░░░░░░░ Ações ░░░░░░░

O estado não deve mudar aleatoriamente.

Mudanças importantes devem acontecer através de ações claras.

Exemplos:

```text
login()

logout()

selectUser()

addProduct()

removeProduct()

retry()

reset()
```

Evitar alterações escondidas e difíceis de rastrear.

---

> ░░░░░░░ Estado Derivado ░░░░░░░

Se um valor pode ser calculado a partir de outro estado, avaliar se realmente
precisa ser armazenado.

Exemplo:

```text
price
quantity
```

podem gerar:

```text
total = price × quantity
```

Talvez não seja necessário salvar `total` como outro estado independente.

A regra é:

**NÃO DUPLICAR ESTADO SEM NECESSIDADE.**

---

> ░░░░░░░ Fonte Única de Verdade ░░░░░░░

O mesmo estado não deve possuir várias versões independentes sem necessidade.

Evitar:

```text
userName na UI

userName no controller

userName no store

userName em outra variável
```

se todos representam exatamente a mesma informação.

Preferir:

**UMA FONTE OFICIAL → VÁRIOS LEITORES**

---

> ░░░░░░░ Estados de Fluxo ░░░░░░░

Fluxos importantes devem possuir estados claros.

Exemplo:

```text
IDLE

LOADING

SUCCESS

ERROR
```

Isso é melhor do que múltiplos booleanos contraditórios.

Evitar situações como:

```text
isLoading = true

hasError = true

isSuccess = true
```

ao mesmo tempo sem que isso faça sentido.

---

> ░░░░░░░ Estado Imutável ░░░░░░░

Quando a linguagem e a arquitetura permitirem, estados complexos devem
preferencialmente ser imutáveis.

Em vez de alterar várias propriedades de um mesmo objeto:

```text
ESTADO ANTIGO
    ↓
ALTERA CAMPO A
ALTERA CAMPO B
ALTERA CAMPO C
```

preferir conceitualmente:

```text
ESTADO ANTIGO
    ↓
NOVO ESTADO
```

Isso facilita:

* rastreamento;
* comparação;
* testes;
* histórico;
* reatividade.

Não é obrigatório para estados locais extremamente simples.

---

> ░░░░░░░ Estado e Configurações ░░░░░░░

Não confundir estado com configuração.

Exemplo:

```text
maxLoginAttempts = 5
```

é configuração.

```text
loginAttempts = 2
```

é estado.

Outro exemplo:

```text
defaultVolume = 50
```

é configuração.

```text
currentVolume = 72
```

é estado.

---

> ░░░░░░░ Estado e Modelo ░░░░░░░

Não confundir modelo de dados com estado.

Exemplo:

```text
User
```

é um modelo.

```text
currentUser
```

é um estado que contém um `User`.

O modelo descreve a estrutura.

O Crocroller controla a condição atual.

---

> ░░░░░░░ Estado e Controller ░░░░░░░

Controllers podem ser utilizados quando a lógica de mudança de estado começa a
crescer.

Exemplo:

```text
LOGIN

UI
 ↓
LoginController
 ↓
LoginState
```

O controller pode ser responsável por:

* ações;
* regras;
* transições;
* chamadas;
* atualização do estado.

---

> ░░░░░░░ Controller Não é Obrigatório Sempre ░░░░░░░

Não criar controller para:

```text
bool isOpen
```

que só existe em um único componente simples.

Criar estrutura quando ela resolver uma necessidade real.

A regra é:

**ESTADO SIMPLES → SOLUÇÃO SIMPLES**

**ESTADO COMPLEXO → ESTRUTURA COMPATÍVEL**

---

> ░░░░░░░ Reatividade ░░░░░░░

Frameworks diferentes possuem mecanismos diferentes para observar mudanças.

Exemplos conceituais:

```text
observer

signal

notifier

stream

store

state object

binding

reactive variable
```

O Crocroller não exige uma tecnologia específica.

A regra é:

**A UI DEVE REAGIR SOMENTE AO ESTADO QUE REALMENTE PRECISA OBSERVAR.**

---

> ░░░░░░░ Evitar Atualizações Amplas ░░░░░░░

Uma pequena mudança de estado não deveria obrigar toda a aplicação a atualizar
sem necessidade.

Preferir granularidade adequada.

Exemplo:

```text
CONTADOR MUDA
    ↓
CONTADOR ATUALIZA
```

em vez de:

```text
CONTADOR MUDA
    ↓
APP INTEIRO ATUALIZA
```

quando a tecnologia permitir controle mais preciso.

---

> ░░░░░░░ Ciclo de Vida ░░░░░░░

Estados, controllers, listeners e subscriptions podem possuir ciclo de vida.

Quando a tecnologia exigir:

* criar;
* iniciar;
* pausar;
* cancelar;
* destruir;
* liberar recursos.

Não deixar listeners ou recursos ativos sem necessidade.

---

> ░░░░░░░ Estado Temporário ░░░░░░░

Estados temporários devem desaparecer quando seu contexto deixa de existir.

Exemplos:

```text
hover

loading local

campo em edição

aba selecionada

menu aberto
```

Não promover esse tipo de estado para estruturas globais sem motivo.

---

> ░░░░░░░ Estado Sensível ░░░░░░░

Dados sensíveis mantidos em estado devem seguir o padrão de segurança.

Exemplos:

```text
token

credencial

informação privada

sessão
```

Evitar exposição desnecessária.

Não manter informação sensível na memória por mais tempo que o necessário
quando isso puder ser evitado.

---

> ░░░░░░░ Estratégia Universal de Escolha ░░░░░░░

O Crocroller recomenda subir a complexidade gradualmente.

```text
NÍVEL 1

ESTADO LOCAL
```

Se não for suficiente:

```text
NÍVEL 2

ESTADO DA FEATURE
+
CONTROLLER
```

Se ainda não for suficiente:

```text
NÍVEL 3

ESTADO COMPARTILHADO
+
STORE / SISTEMA REATIVO
```

Quando necessário:

```text
NÍVEL 4

ESTADO
+
PERSISTÊNCIA
+
DATABEEZZE
```

---

> ░░░░░░░ Frameworks e Bibliotecas ░░░░░░░

O Crocroller 2.0 não recomenda uma biblioteca universal.

Cada tecnologia possui soluções próprias.

Exemplos em Flutter podem incluir:

```text
setState

ValueNotifier

Provider

Riverpod

Bloc

MobX
```

Outras tecnologias podem utilizar mecanismos completamente diferentes.

A pergunta correta não é:

> **Qual biblioteca o Junglapp obriga?**

A pergunta é:

> **Qual é a solução mais simples que resolve este estado corretamente?**

---

> ░░░░░░░ Exemplo Flutter — Estado Local ░░░░░░░

```dart
bool isOpen = false;

setState(() {
  isOpen = true;
});
```

Isso pode ser suficiente.

Não existe necessidade automática de uma solução mais complexa.

---

> ░░░░░░░ Exemplo Flutter — Estado da Feature ░░░░░░░

```dart
class CounterController {
  final ValueNotifier<int> _value = ValueNotifier(0);

  ValueListenable<int> get value => _value;

  void increment() {
    _value.value++;
  }

  void dispose() {
    _value.dispose();
  }
}
```

O mecanismo é específico do Flutter.

O princípio é universal:

```text
ESTADO PRIVADO
      ↓
LEITURA CONTROLADA
      ↓
AÇÕES CLARAS
```

---

> ░░░░░░░ Exemplo de Estado de Fluxo ░░░░░░░

```text
LoginState

├── idle
├── loading
├── success
└── error
```

Conceitualmente:

```text
LOGIN
  ↓
LOADING
  ↓
 ┌─────────┐
 ↓         ↓
SUCCESS   ERROR
```

O projeto sabe exatamente em qual fase está.

---

> ░░░░░░░ Durante a Construção ░░░░░░░

Seguindo o Order of Lion, o estado pode permanecer no arquivo principal
enquanto a feature estiver sendo construída.

Exemplo:

```text
login_pag

├── BLOCO CONFIGURAÇÕES
├── BLOCO ESTADO
├── BLOCO VALIDAÇÃO
├── BLOCO LÓGICA
└── BLOCO INTERFACE
```

Não criar vários arquivos antes de existir necessidade.

---

> ░░░░░░░ Durante a Refatoração ░░░░░░░

Se o BLOCO de estado cresceu:

```text
BLOCO ESTADO
```

pode virar:

```text
login_str
```

ou outro arquivo definido pelo Suffox.

Exemplo:

```text
ANTES

login_pag
```

Depois:

```text
login/

├── login_pag
├── login_ctl
└── login_str
```

Somente quando essa separação realmente trouxer benefício.

---

> ░░░░░░░ Regra do Mínimo ░░░░░░░

Não criar automaticamente:

```text
controller

store

provider

event

state class

reducer

observable
```

para toda variável.

Primeiro perguntar:

> **Qual é a menor estrutura necessária para controlar este estado?**

Usar essa.

---

> ░░░░░░░ Regra de Escalada ░░░░░░░

Aumentar a complexidade somente quando existir um problema real.

```text
LOCAL
  ↓
não é suficiente?
  ↓
FEATURE
  ↓
não é suficiente?
  ↓
COMPARTILHADO
  ↓
precisa sobreviver?
  ↓
PERSISTENTE
```

Não começar pelo último nível.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao criar ou modificar estado, uma IA deve:

1. identificar quem realmente precisa do estado;
2. manter o estado no menor escopo possível;
3. identificar um dono principal;
4. evitar duplicar a mesma fonte de verdade;
5. usar nomes definidos pelo Beavar;
6. diferenciar estado de configuração;
7. diferenciar estado de persistência;
8. evitar estruturas globais sem necessidade;
9. utilizar estados claros para fluxos complexos;
10. liberar recursos quando a tecnologia exigir;
11. extrair o estado somente quando a complexidade justificar;
12. escolher a solução mais simples compatível com o problema.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

Só um componente utiliza?

→ **ESTADO LOCAL**

Vários elementos da mesma feature utilizam?

→ **ESTADO DA FEATURE**

Várias features utilizam?

→ considerar **ESTADO COMPARTILHADO**

Precisa sobreviver ao fechamento?

→ **DATABEEZZE**

Existem várias ações e transições?

→ considerar **CONTROLLER**

Existem muitos estados mutuamente exclusivos?

→ considerar **ESTADO DE FLUXO**

O valor pode ser calculado?

→ evitar **DUPLICAR ESTADO**

A solução nativa resolve?

→ **USAR A SOLUÇÃO NATIVA**

Ainda não resolve?

→ subir **UM NÍVEL DE COMPLEXIDADE**

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO CRIAR E QUANDO EXTRAIR O ESTADO**

O **Snake** define:

**ONDE O BLOCO DE ESTADO FICA DURANTE A CONSTRUÇÃO**

O **Suffox** define:

**COMO O ARQUIVO DE ESTADO SERÁ NOMEADO**

O **Frogdlers** define:

**ONDE O ESTADO EXTRAÍDO SERÁ ORGANIZADO**

O **Beavar** define:

**COMO ESTADOS E AÇÕES SERÃO NOMEADOS**

O **DataBeezze** define:

**COMO O ESTADO É PERSISTIDO QUANDO NECESSÁRIO**

O **Crocroller** define:

**QUEM POSSUI O ESTADO E COMO ELE MUDA**

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de criar uma solução de gerenciamento de estado, responder:

**QUEM PRECISA DESSE ESTADO?**

**QUEM PODE ALTERÁ-LO?**

**QUEM PRECISA OBSERVÁ-LO?**

**ELE É LOCAL OU COMPARTILHADO?**

**PRECISA SER PERSISTIDO?**

**EXISTE MAIS DE UMA FONTE DE VERDADE?**

**A SOLUÇÃO MAIS SIMPLES JÁ RESOLVE?**

A filosofia do Crocroller é:

**ESTADO NO MENOR ESCOPO POSSÍVEL.**

**UM DONO PRINCIPAL.**

**UMA FONTE DE VERDADE.**

**AÇÕES CLARAS.**

**COMPLEXIDADE SOMENTE QUANDO NECESSÁRIA.**

**LOCAL PRIMEIRO.**

**GLOBAL SOMENTE QUANDO PRECISAR.**

# ███████ 🐊 FIM — CROCROLLER ███████
