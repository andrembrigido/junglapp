# ███████ 🦩 Animacranes — Padrão Universal de Animações ███████

Este documento define o padrão oficial de animações do **Junglapp 2.0**.

O Animacranes determina:

* quando utilizar animação;
* como escolher o nível de complexidade;
* como separar visual de controle;
* onde centralizar configurações;
* quando criar um controller;
* como organizar animações reutilizáveis;
* como preparar animações para futura extração.

O objetivo é manter animações:

* claras;
* previsíveis;
* reutilizáveis;
* fáceis de ajustar;
* fáceis de testar;
* independentes de linguagem;
* separadas da lógica de negócio.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**ANIMAR SOMENTE O QUE PRECISA SER ANIMADO.**

E utilizar:

**A SOLUÇÃO MAIS SIMPLES QUE PRODUZ O RESULTADO CORRETO.**

A evolução deve ser:

**ANIMAÇÃO SIMPLES → CONTROLE MANUAL → SEQUÊNCIA COMPLEXA**

Nunca começar pela solução mais complexa sem necessidade.

---

> ░░░░░░░ Animação Não é Decoração Obrigatória ░░░░░░░

Nem todo elemento precisa ser animado.

Uma animação deve possuir uma função real.

Exemplos:

* indicar mudança de estado;
* mostrar entrada ou saída;
* orientar atenção;
* comunicar progresso;
* melhorar continuidade visual;
* reforçar resposta a uma ação;
* suavizar uma transição.

Evitar animações que:

* atrasam o usuário;
* dificultam leitura;
* escondem ações;
* existem apenas porque são possíveis;
* deixam a interface cansativa.

---

> ░░░░░░░ Classificação Oficial ░░░░░░░

O Animacranes utiliza três níveis principais:

| Nível | Tipo           | Uso                                    |
| ----: | -------------- | -------------------------------------- |
|     1 | **Simples**    | Mudança visual direta                  |
|     2 | **Controlada** | Precisa de controle de tempo ou estado |
|     3 | **Sequencial** | Várias animações coordenadas           |

A complexidade deve subir apenas quando o nível anterior não for suficiente.

---

> ░░░░░░░ 1 — Animação Simples ░░░░░░░

Utilizar para mudanças visuais diretas.

Exemplos:

```text
opacidade

posição

tamanho

cor

escala

rotação

alinhamento
```

Se a própria tecnologia oferece uma solução simples para interpolar entre dois
estados:

**UTILIZAR ESSA SOLUÇÃO.**

Não criar controller apenas para animar uma mudança básica.

---

> ░░░░░░░ Exemplo Conceitual ░░░░░░░

```text
ESTADO A
   ↓
TRANSIÇÃO
   ↓
ESTADO B
```

Exemplo:

```text
isVisible = false
      ↓
fade
      ↓
isVisible = true
```

A animação apenas representa visualmente a mudança.

---

> ░░░░░░░ 2 — Animação Controlada ░░░░░░░

Utilizar quando for necessário controlar explicitamente:

* início;
* pausa;
* retomada;
* reversão;
* duração;
* curva;
* progresso;
* repetição;
* sincronização;
* direção.

Nesse caso, a animação possui duas responsabilidades diferentes:

**CONTROLE**

e

**VISUAL**

Essas responsabilidades devem permanecer separadas.

---

> ░░░░░░░ Controle e Visual ░░░░░░░

A regra principal é:

```text
CONTROLE
   ↓
PROGRESSO DA ANIMAÇÃO
   ↓
VISUAL
```

O controle decide:

* quando começar;
* quanto durar;
* quando parar;
* quando inverter;
* qual etapa está ativa.

O visual decide:

* o que muda;
* como aparece;
* como o elemento reage ao progresso.

---

> ░░░░░░░ Suffox nas Animações ░░░░░░░

O Animacranes mantém os dois sufixos oficiais definidos pelo Suffox:

| Sufixo | Responsabilidade         |
| -----: | ------------------------ |
|  `anm` | Parte visual da animação |
| `actl` | Controle da animação     |

Exemplo:

```text
splash_logo_anm
splash_logo_actl
```

`anm` representa:

**O QUE É ANIMADO**

`actl` representa:

**COMO A ANIMAÇÃO É CONTROLADA**

---

> ░░░░░░░ Durante a Construção ░░░░░░░

No Junglapp 2.0, não é necessário criar dois arquivos imediatamente.

A animação pode permanecer dentro do arquivo principal usando BLOCOs do Snake.

Exemplo:

```text
splash_pag

├── BLOCO INTERFACE
├── BLOCO ANIMAÇÃO VISUAL
└── BLOCO CONTROLE DE ANIMAÇÃO
```

Primeiro:

**FAZER FUNCIONAR.**

Depois:

**EXTRAIR SE NECESSÁRIO.**

---

> ░░░░░░░ Exemplo com Snake ░░░░░░░

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ ANIMAÇÃO VISUAL                                                        ║
   ║ FUTURO ARQUIVO: splash_logo_anm                                        ║
   ║ RESPONSABILIDADE: representar visualmente a animação do logo           ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: animação visual do logo da tela inicial.
   Objetivo: controlar somente transformações visuais do logo.
///////////////////////////////////////////////////////////////////////////// */


/* ************************ CONFIGURAÇÕES ************************************ */

const fadeStart = 0.0;
const fadeEnd = 1.0;


/* ************************ VISUAL ******************************************* */
```

Depois:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ CONTROLE DE ANIMAÇÃO                                                   ║
   ║ FUTURO ARQUIVO: splash_logo_actl                                       ║
   ║ RESPONSABILIDADE: controlar tempo e execução da animação               ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ************************ CONFIGURAÇÕES ************************************ */

const fadeDuration = 800;
const fadeDelay = 200;


/* ************************ CONTROLE **************************************** */
```

---

> ░░░░░░░ Configurações Centralizadas ░░░░░░░

Valores ajustáveis de animação não devem ficar espalhados pelo código.

Centralizar:

* duração;
* delay;
* curva;
* velocidade;
* escala;
* opacidade inicial;
* opacidade final;
* distância;
* número de repetições.

Exemplo conceitual:

```text
fadeDuration = 800
fadeDelay = 200
fadeStart = 0
fadeEnd = 1
```

Assim, a animação pode ser ajustada sem procurar valores dentro da lógica.

---

> ░░░░░░░ Configuração Pertence ao BLOCO ░░░░░░░

Cada animação deve possuir suas próprias configurações quando necessário.

Exemplo:

```text
LOGO

duration
delay
curve
```

Outro BLOCO:

```text
BUTTON

duration
scaleStart
scaleEnd
```

Não criar uma configuração global de animações sem necessidade.

A regra continua:

**LOCAL PRIMEIRO → GLOBAL QUANDO REALMENTE COMPARTILHADO**

---

> ░░░░░░░ Duração ░░░░░░░

Toda animação controlada deve possuir duração clara.

Evitar valores espalhados como:

```text
300
500
800
```

sem contexto.

Preferir:

```text
fadeDuration
buttonPressDuration
pageTransitionDuration
```

seguindo o Beavar.

---

> ░░░░░░░ Delay ░░░░░░░

Delay deve existir somente quando fizer parte real da experiência.

Exemplo:

```text
ANIMAÇÃO A
    ↓
DELAY
    ↓
ANIMAÇÃO B
```

Evitar delays usados apenas para corrigir problemas de sincronização ou lógica.

---

> ░░░░░░░ Curvas e Interpolação ░░░░░░░

Movimentos não precisam ser lineares.

A tecnologia pode oferecer:

* easing;
* curvas;
* interpolação;
* springs;
* física;
* keyframes.

Escolher o comportamento adequado ao objetivo visual.

Não utilizar efeitos exagerados apenas porque estão disponíveis.

---

> ░░░░░░░ 3 — Animação Sequencial ░░░░░░░

Quando múltiplas animações dependem umas das outras, utilizar uma sequência
clara.

Exemplo:

```text
LOGO ENTRA
    ↓
LOGO ESPERA
    ↓
LOGO SOME
    ↓
TELA AVANÇA
```

A ordem deve ser explícita.

Evitar sequências escondidas em vários callbacks desconectados.

---

> ░░░░░░░ Timeline ░░░░░░░

Para animações complexas, pensar em uma linha do tempo.

Exemplo:

```text
0ms        500ms       1000ms       1500ms
│------------│------------│------------│

FADE IN
             ESPERA
                          FADE OUT
                                       FIM
```

Isso facilita entender:

* início;
* duração;
* sobreposição;
* dependência;
* final.

---

> ░░░░░░░ Uma Fonte de Tempo ░░░░░░░

Quando várias partes pertencem à mesma animação coordenada, preferir uma fonte
de progresso compartilhada quando a tecnologia permitir.

Evitar vários timers independentes tentando simular uma única animação.

Preferir:

```text
CONTROLLER
    ↓
PROGRESSO
    ├→ OPACIDADE
    ├→ ESCALA
    └→ POSIÇÃO
```

---

> ░░░░░░░ Estado da Animação ░░░░░░░

Animações complexas podem possuir estados.

Exemplo:

```text
idle
running
paused
completed
reversed
```

Esses estados devem seguir o Crocroller quando realmente fizerem parte do
estado da aplicação.

Nem toda animação simples precisa de um sistema de estado.

---

> ░░░░░░░ Animação Visual Não é Lógica de Negócio ░░░░░░░

Evitar colocar regras importantes dentro da animação.

Ruim:

```text
ANIMAÇÃO TERMINOU
    ↓
SALVA PEDIDO
```

quando salvar o pedido é uma regra de negócio independente.

Preferir:

```text
PEDIDO SALVO
    ↓
ESTADO ATUALIZA
    ↓
ANIMAÇÃO REPRESENTA O RESULTADO
```

A animação deve refletir o comportamento.

Não controlar regras críticas sem necessidade.

---

> ░░░░░░░ Eventos de Animação ░░░░░░░

Eventos como:

```text
onStart
onComplete
onReverse
onCancel
```

podem ser utilizados quando o fluxo realmente depender deles.

Evitar transformar toda animação em uma cadeia complexa de callbacks.

---

> ░░░░░░░ Ciclo de Vida ░░░░░░░

Controllers, listeners, timers ou recursos de animação podem possuir ciclo de
vida.

Quando necessário:

```text
CRIAR
  ↓
INICIAR
  ↓
UTILIZAR
  ↓
PARAR
  ↓
LIBERAR
```

Nunca deixar controllers ou listeners ativos sem necessidade.

A implementação depende da tecnologia.

---

> ░░░░░░░ Animação e Performance ░░░░░░░

Animações devem evitar trabalho desnecessário.

Avaliar:

* quantos elementos atualizam;
* frequência das atualizações;
* quantidade de cálculos;
* quantidade de elementos simultâneos;
* custo de renderização.

Uma animação visual pequena não deveria obrigar a aplicação inteira a
reprocessar sem necessidade.

---

> ░░░░░░░ Animar a Propriedade Correta ░░░░░░░

Quando a tecnologia diferenciar propriedades mais baratas ou mais caras de
animar, escolher a alternativa adequada.

A regra universal é:

**ANIMAR COM O MENOR CUSTO POSSÍVEL SEM SACRIFICAR O RESULTADO.**

---

> ░░░░░░░ Reutilização ░░░░░░░

Uma animação deve ser promovida para algo reutilizável somente quando houver
reutilização real.

Primeiro:

```text
login/
└── login_button_anm
```

Se outras partes começarem a utilizar o mesmo comportamento:

```text
shared/
└── press_scale_anm
```

Não criar biblioteca global de animações preventivamente.

---

> ░░░░░░░ Transições de Navegação ░░░░░░░

Transições entre destinos também pertencem ao Animacranes.

Exemplos:

* fade;
* slide;
* scale;
* combinação simples.

O **Navgator** define:

**PARA ONDE IR**

O Animacranes define:

**COMO A TRANSIÇÃO APARECE**

Não misturar as duas responsabilidades.

---

> ░░░░░░░ Exemplo Conceitual ░░░░░░░

```text
NAVGATOR
    ↓
HOME
```

com:

```text
ANIMACRANES
    ↓
FADE TRANSITION
```

A rota continua funcionando mesmo se a animação mudar ou for removida.

---

> ░░░░░░░ Animações Externas ░░░░░░░

Ferramentas como:

```text
Rive
Lottie
sprites
timeline animation
skeletal animation
CSS animation
engine animation
```

podem ser utilizadas.

O Animacranes não obriga nenhuma delas.

A ferramenta deve ser escolhida conforme a necessidade.

---

> ░░░░░░░ Dependências ░░░░░░░

Antes de adicionar uma biblioteca externa apenas para animação, perguntar:

**A SOLUÇÃO NATIVA JÁ RESOLVE?**

Se sim:

**USAR A NATIVA.**

Se não:

avaliar a dependência conforme:

* necessidade;
* manutenção;
* tamanho;
* compatibilidade;
* segurança;
* benefício real.

---

> ░░░░░░░ Acessibilidade ░░░░░░░

Animações também devem considerar usuários que preferem menos movimento.

Quando a plataforma oferecer uma preferência equivalente a:

```text
REDUCE MOTION
```

o projeto deve considerar respeitá-la.

Isso pode significar:

* remover animação;
* reduzir duração;
* reduzir deslocamento;
* utilizar uma transição mais simples.

---

> ░░░░░░░ Animações Essenciais ░░░░░░░

Se uma animação comunica informação importante, essa informação não deve
depender exclusivamente do movimento.

Exemplo:

Um erro não deve ser indicado somente por:

```text
CAMPO TREME
```

Também deve existir uma indicação compreensível do erro.

---

> ░░░░░░░ Exemplo Flutter — Simples ░░░░░░░

```dart
AnimatedOpacity(
  duration: const Duration(milliseconds: 300),
  opacity: isVisible ? 1.0 : 0.0,
  child: const Text('Animado'),
);
```

O mecanismo é específico do Flutter.

O princípio é:

**MUDANÇA SIMPLES → SOLUÇÃO SIMPLES**

---

> ░░░░░░░ Exemplo Flutter — Controlada ░░░░░░░

```dart
class LogoAnimationController {
  late final AnimationController controller;

  void init(TickerProvider vsync) {
    controller = AnimationController(
      vsync: vsync,
      duration: const Duration(milliseconds: 800),
    );

    controller.forward();
  }

  void dispose() {
    controller.dispose();
  }
}
```

Visual:

```dart
FadeTransition(
  opacity: animation,
  child: Image.asset('assets/images/logo.png'),
);
```

O código Flutter é apenas um exemplo de implementação.

O princípio universal continua:

**CONTROLE ≠ VISUAL**

---

> ░░░░░░░ Durante a Refatoração ░░░░░░░

Antes:

```text
splash_pag

├── BLOCO INTERFACE
├── BLOCO ANIMAÇÃO VISUAL
└── BLOCO CONTROLE DE ANIMAÇÃO
```

Depois:

```text
splash/

├── splash_pag
├── splash_logo_anm
└── splash_logo_actl
```

Se o controle for simples e não justificar outro arquivo:

```text
splash/

├── splash_pag
└── splash_logo_anm
```

também é válido.

A separação só acontece quando traz benefício.

---

> ░░░░░░░ Regra do Mínimo ░░░░░░░

Não criar automaticamente:

```text
controller

timeline

state

sequence

helper

animation service
```

para toda animação.

Perguntar:

> **Qual é a menor solução necessária para produzir este movimento?**

Usar essa solução.

---

> ░░░░░░░ Regra de Escalada ░░░░░░░

```text
ANIMAÇÃO SIMPLES
       ↓
precisa de controle?
       ↓
ANIMAÇÃO CONTROLADA
       ↓
precisa coordenar várias?
       ↓
ANIMAÇÃO SEQUENCIAL
       ↓
precisa de ferramenta especializada?
       ↓
BIBLIOTECA / ENGINE
```

Não pular etapas sem necessidade.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao criar animações, uma IA deve:

1. confirmar que a animação possui uma função real;
2. utilizar a solução mais simples possível;
3. centralizar duração, delay e demais valores ajustáveis;
4. separar controle e visual quando a complexidade exigir;
5. utilizar `anm` para visual e `actl` para controle;
6. evitar lógica de negócio dentro da animação;
7. respeitar o ciclo de vida da tecnologia;
8. evitar dependências externas sem necessidade;
9. considerar performance;
10. considerar redução de movimento;
11. preparar BLOCOs para futura extração;
12. reutilizar somente quando houver reutilização real.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

Só muda uma propriedade visual?

→ **ANIMAÇÃO SIMPLES**

Precisa controlar início, pausa ou reversão?

→ **ANIMAÇÃO CONTROLADA**

Possui várias etapas?

→ **SEQUÊNCIA**

Apenas o visual está animado?

→ `anm`

Existe controle complexo separado?

→ `actl`

A tecnologia nativa resolve?

→ **USAR NATIVO**

Precisa de ferramenta especializada?

→ avaliar **DEPENDÊNCIA EXTERNA**

A animação contém regra de negócio?

→ **SEPARAR**

A animação será reutilizada de verdade?

→ considerar **SHARED**

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO CRIAR E QUANDO EXTRAIR A ANIMAÇÃO**

O **Snake** define:

**COMO SEPARAR VISUAL E CONTROLE DENTRO DO ARQUIVO**

O **Suffox** define:

**`anm` PARA VISUAL E `actl` PARA CONTROLE**

O **Frogdlers** define:

**ONDE OS ARQUIVOS EXTRAÍDOS SERÃO ORGANIZADOS**

O **Beavar** define:

**COMO ESTADOS, CONTROLLERS E CONFIGURAÇÕES SERÃO NOMEADOS**

O **Crocroller** define:

**QUANDO O ESTADO DA ANIMAÇÃO PRECISA SER GERENCIADO**

O **Navgator** define:

**PARA ONDE A NAVEGAÇÃO VAI**

O **Animacranes** define:

**COMO O MOVIMENTO É APRESENTADO**

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de criar uma animação, responder:

**ELA É NECESSÁRIA?**

**O QUE ELA COMUNICA?**

**PODE SER MAIS SIMPLES?**

**PRECISA DE CONTROLE MANUAL?**

**PRECISA DE UM ESTADO PRÓPRIO?**

**CONTROLE E VISUAL ESTÃO SEPARADOS QUANDO NECESSÁRIO?**

**OS VALORES AJUSTÁVEIS ESTÃO CENTRALIZADOS?**

**ELA PRECISA VIRAR OUTRO ARQUIVO?**

A filosofia do Animacranes é:

**MOVIMENTO COM PROPÓSITO.**

**SIMPLES PRIMEIRO.**

**CONTROLE SOMENTE QUANDO NECESSÁRIO.**

**VISUAL E LÓGICA SEPARADOS.**

**CONFIGURAÇÕES CENTRALIZADAS.**

**COMPLEXIDADE NA MEDIDA CERTA.**

# ███████ 🦩 FIM — ANIMACRANES ███████
