# ███████ 🦁 Order of Lion — Ordem de Construção ███████

Este documento define a ordem oficial de construção de projetos no
**Junglapp 2.0**.

O objetivo é permitir que humanos e IAs saibam:

* o que fazer primeiro;
* o que pode esperar;
* quando testar;
* quando conectar;
* quando refatorar;
* quando aplicar segurança;
* como evitar complexidade prematura;
* quando uma decisão pode ser tomada de forma autônoma.

O Order of Lion é **universal**.

Ele não depende de:

* linguagem;
* framework;
* engine;
* plataforma;
* tipo de aplicação.

Cada tecnologia pode possuir necessidades próprias, mas a filosofia e a ordem
do Junglapp permanecem.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A ordem principal é:

**ENTENDER → PROTEGER → CRIAR O MÍNIMO → CONSTRUIR → TESTAR → COMPLETAR →
REFATORAR**

A filosofia pode ser resumida em:

**Faça funcionar primeiro.
Faça funcionar corretamente.
Complete.
Separe e organize no final.**

Existe uma exceção importante:

**Segurança não espera a refatoração.**

---

> ░░░░░░░ Relação com os Outros Padrões ░░░░░░░

O Order of Lion não trabalha sozinho.

### 🦁 Order of Lion

Define:

**QUANDO FAZER.**

### 🐯 Tiger

Define:

**COMO NÃO COMPROMETER A SEGURANÇA.**

### 🐍 Snake

Define:

**COMO ORGANIZAR O ARQUIVO.**

A relação é:

```text
ORDER OF LION
      ↓
    TIGER
      ↓
    SNAKE
      ↓
 IMPLEMENTAÇÃO
```

Nenhum desses padrões substitui o outro.

Eles trabalham juntos.

---

> ░░░░░░░ Ordem Oficial ░░░░░░░

Todo projeto deve seguir, sempre que possível:

| Ordem | Etapa                | Objetivo                                  |
| ----: | -------------------- | ----------------------------------------- |
|    01 | **Entender**         | Compreender o que será construído         |
|    02 | **Mapear riscos**    | Aplicar o Tiger                           |
|    03 | **Definir**          | Escolher apenas o necessário para começar |
|    04 | **Criar o mínimo**   | Criar somente estrutura obrigatória       |
|    05 | **Criar componente** | Um componente autocontido                 |
|    06 | **Configurar**       | Centralizar valores ajustáveis            |
|    07 | **Construir**        | Fazer a funcionalidade funcionar          |
|    08 | **Testar**           | Validar comportamento e segurança         |
|    09 | **Conectar**         | Integrar componentes funcionais           |
|    10 | **Repetir**          | Construir a próxima parte                 |
|    11 | **Completar**        | Terminar as funcionalidades               |
|    12 | **Validar**          | Confirmar o projeto completo              |
|    13 | **Refatorar**        | Extrair os BLOCOs                         |
|    14 | **Finalizar**        | Revisar e testar novamente                |

---

> ░░░░░░░ 01 — Entender ░░░░░░░

Antes de criar código, entender o suficiente para começar.

Identificar:

* o que o projeto é;
* o que ele precisa fazer;
* quem vai usar;
* qual é o fluxo principal;
* qual resultado é esperado.

Não é necessário definir todo o futuro do projeto.

A regra é:

**Planejar o suficiente para começar corretamente.**

Não:

**Planejar tanto que o projeto nunca começa.**

---

> ░░░░░░░ 02 — Mapear Riscos ░░░░░░░

Antes de construir uma funcionalidade, verificar o **Tiger**.

Perguntar se ela envolve:

* usuário;
* login;
* senha;
* permissão;
* dados privados;
* dados sensíveis;
* banco de dados;
* API;
* internet;
* upload;
* download;
* secret;
* pagamento;
* serviço externo.

Se envolver risco relevante, a proteção deve fazer parte da implementação
desde o início.

A regra é:

**SEGURANÇA NECESSÁRIA = PARTE DA FUNCIONALIDADE**

Pode esperar:

* separação de arquivos;
* arquitetura final;
* organização definitiva;
* otimização.

Não pode esperar:

* autenticação necessária;
* autorização;
* proteção de senhas;
* proteção de secrets;
* controle de acesso;
* validação de segurança.

---

> ░░░░░░░ 03 — Definir ░░░░░░░

Definir somente o necessário para começar.

Escolher:

* tecnologia;
* componentes principais;
* funcionalidades principais;
* fluxo principal;
* arquivos obrigatórios da tecnologia.

Não decidir antecipadamente tudo que **talvez** seja necessário no futuro.

---

> ░░░░░░░ 04 — Criar o Mínimo ░░░░░░░

Criar somente:

**OBRIGATÓRIO PELA TECNOLOGIA + NECESSÁRIO PELO PROJETO**

Evitar:

* pastas vazias;
* arquivos vazios;
* services sem uso;
* repositories sem necessidade;
* managers sem responsabilidade;
* abstrações prematuras;
* dependências preventivas.

Antes de criar algo, perguntar:

> **Isso precisa existir agora?**

Se a resposta for não:

**não criar ainda.**

---

> ░░░░░░░ 05 — Componente Autocontido ░░░░░░░

Durante a construção, utilizar:

**1 COMPONENTE = 1 ARQUIVO PRINCIPAL**

sempre que tecnicamente possível.

Esse arquivo pode temporariamente conter:

* configurações;
* dados;
* estado;
* validação;
* lógica;
* serviços;
* interface;
* helpers.

A separação interna deve ser feita utilizando o **Snake**.

O objetivo não é manter tudo no mesmo arquivo para sempre.

O objetivo é:

**fazer funcionar primeiro e deixar preparado para separar depois.**

---

> ░░░░░░░ BLOCOs do Snake ░░░░░░░

Dentro do arquivo principal, responsabilidades que futuramente poderão virar
arquivos devem ser separadas como **BLOCOs**.

Exemplo:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ AUTENTICAÇÃO                                                            ║
   ║ FUTURO ARQUIVO: authentication                                          ║
   ║ RESPONSABILIDADE: autenticar o usuário                                  ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */
```

Depois:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ INTERFACE                                                               ║
   ║ FUTURO ARQUIVO: login_interface                                         ║
   ║ RESPONSABILIDADE: interface do login                                    ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */
```

A regra é:

**1 BLOCO = 1 possível arquivo futuro**

---

> ░░░░░░░ 06 — Configurações Centralizadas ░░░░░░░

Valores que provavelmente poderão mudar futuramente não devem ficar perdidos
no meio do código.

Eles devem ficar centralizados.

Exemplos:

* tamanhos;
* limites;
* tempos;
* quantidades;
* espaçamentos;
* valores padrão;
* textos configuráveis;
* comportamentos ajustáveis.

Exemplo:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

const maxLoginAttempts = 5;
const loginTimeout = 30;
const minPasswordLength = 8;
```

Assim, quando um valor precisar ser alterado:

**não é necessário procurar dentro da lógica.**

---

> ░░░░░░░ Configurações por BLOCO ░░░░░░░

Cada BLOCO deve possuir suas próprias configurações quando necessário.

Exemplo:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ AUTENTICAÇÃO                                                            ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ************************ CONFIGURAÇÕES ************************************ */

const maxLoginAttempts = 5;
const loginTimeout = 30;
```

Outro BLOCO:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ INTERFACE                                                               ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ************************ CONFIGURAÇÕES ************************************ */

const formSpacing = 16;
const buttonHeight = 48;
```

A configuração deve ficar próxima da responsabilidade que utiliza aquele valor.

---

> ░░░░░░░ Local Primeiro, Global Depois ░░░░░░░

Configurações devem começar **locais ao BLOCO**.

Somente quando várias partes realmente precisarem do mesmo valor, avaliar uma
configuração compartilhada.

A regra é:

**LOCAL PRIMEIRO → COMPARTILHADO SOMENTE QUANDO NECESSÁRIO**

Não criar um arquivo gigante de configurações globais antecipadamente.

---

> ░░░░░░░ Configuração Não é Secret ░░░░░░░

Configurações centralizadas não devem ser usadas para guardar secrets.

Pode ficar no código:

* tamanho;
* limite;
* tempo;
* espaçamento;
* quantidade;
* comportamento.

Não deve ficar diretamente no código:

* senha;
* token;
* API key;
* private key;
* credencial.

Secrets seguem o **Tiger**.

---

> ░░░░░░░ 07 — Construir ░░░░░░░

Construir **uma funcionalidade por vez**.

O ciclo deve ser:

```text
CONFIGURAR
    ↓
PROTEGER
    ↓
CONSTRUIR
    ↓
TESTAR
    ↓
CORRIGIR
```

Evitar abrir muitas funcionalidades incompletas ao mesmo tempo.

---

> ░░░░░░░ 08 — Testar ░░░░░░░

Depois de construir uma parte:

* testar o caminho normal;
* testar erros prováveis;
* testar estados importantes;
* testar proteções relevantes;
* corrigir antes de avançar.

Não acumular várias partes não testadas.

A funcionalidade só deve ser considerada funcional quando:

**o caminho normal funciona e os principais erros são tratados.**

---

> ░░░░░░░ 09 — Conectar ░░░░░░░

Quando dois componentes estiverem funcionando individualmente:

**CONECTAR → TESTAR → CORRIGIR → VALIDAR**

A integração deve acontecer aos poucos.

Não esperar o projeto inteiro ficar pronto para descobrir que os componentes
não conseguem conversar entre si.

---

> ░░░░░░░ 10 — Repetir ░░░░░░░

Depois:

```text
PRÓXIMO COMPONENTE
      ↓
CONFIGURAÇÕES
      ↓
TIGER
      ↓
SNAKE
      ↓
CONSTRUIR
      ↓
TESTAR
      ↓
CONECTAR
```

Repetir até o projeto possuir todas as funcionalidades necessárias.

---

> ░░░░░░░ 11 — Regra Contra Refatoração Prematura ░░░░░░░

O arquivo crescer não significa automaticamente que ele precisa ser separado.

Antes de refatorar durante a construção, perguntar:

> **A estrutura atual está impedindo o desenvolvimento?**

Se não:

**continuar construindo.**

Se sim:

**refatorar somente o necessário para desbloquear.**

A grande refatoração acontece no final.

---

> ░░░░░░░ 12 — Preparação para Extração ░░░░░░░

Mesmo permanecendo no mesmo arquivo, cada BLOCO deve ser escrito pensando na
extração futura.

O objetivo é chegar a:

```text
IDENTIFICAR BLOCO
       ↓
RECORTAR
       ↓
CRIAR ARQUIVO
       ↓
COLAR
       ↓
AJUSTAR CONEXÕES
       ↓
TESTAR
```

O ideal é **mover código**, não reconstruí-lo.

---

> ░░░░░░░ 13 — Quando Refatorar ░░░░░░░

A refatoração completa começa somente quando:

* o fluxo principal funciona;
* os componentes estão conectados;
* as funcionalidades principais estão completas;
* as proteções do Tiger estão presentes;
* os BLOCOs estão identificados;
* as configurações estão centralizadas;
* não existem bloqueios importantes conhecidos.

---

> ░░░░░░░ 14 — Refatoração Final ░░░░░░░

Na refatoração:

1. identificar os BLOCOs;
2. criar os arquivos definitivos;
3. mover cada BLOCO;
4. levar junto suas configurações;
5. ajustar imports e conexões;
6. organizar pastas;
7. remover duplicações;
8. testar novamente.

Exemplo:

```text
ANTES

login.dart

├── BLOCO AUTENTICAÇÃO
├── BLOCO VALIDAÇÃO
└── BLOCO INTERFACE
```

Depois:

```text
DEPOIS

login/
├── authentication
├── validation
└── interface
```

---

> ░░░░░░░ Autonomia da IA ░░░░░░░

Uma IA trabalhando com Junglapp deve possuir autonomia para decisões pequenas.

Ela não deve interromper o desenvolvimento por decisões simples, reversíveis e
sem impacto importante.

A IA pode decidir sozinha quando a decisão:

* é reversível;
* não altera o objetivo;
* não altera regra de negócio;
* respeita o Tiger;
* respeita o Snake;
* não cria risco relevante;
* possui uma solução claramente mais simples.

Exemplos:

* nomes internos claros;
* posição de helper;
* organização dentro de uma SEÇÃO;
* criação de configuração local necessária;
* pequena escolha técnica equivalente.

---

> ░░░░░░░ Quando a IA Deve Perguntar ░░░░░░░

A IA deve perguntar quando a decisão:

* altera objetivo do produto;
* altera regra de negócio;
* remove funcionalidade;
* exige credencial;
* exige escolha importante do usuário;
* possui impacto difícil de reverter;
* possui alternativas com resultados significativamente diferentes;
* reduz proteção importante do Tiger.

---

> ░░░░░░░ Regra de Continuidade ░░░░░░░

Se existe informação suficiente para continuar:

**CONTINUAR.**

Evitar perguntas como:

> "Quer que eu continue?"

quando a próxima etapa já estiver definida.

Em uma dúvida não bloqueadora:

**escolher a opção segura → escolher a mais simples → registrar → continuar**

Em uma dúvida bloqueadora:

**parar → explicar objetivamente → perguntar**

---

> ░░░░░░░ Regra de Desempate ░░░░░░░

Quando várias soluções forem válidas, priorizar:

1. **Segura**
2. **Simples**
3. **Clara**
4. **Menos arquivos**
5. **Menos dependências**
6. **Fácil de testar**
7. **Fácil de modificar**
8. **Fácil de extrair depois**
9. **Escalável**

Segurança obrigatória vem antes da simplicidade.

Escalabilidade não justifica complexidade que ainda não existe.

---

> ░░░░░░░ Regra do Snake ░░░░░░░

Todo código Junglapp deve seguir o Snake.

A hierarquia é:

**BLOCO → SOBRE → SEÇÃO → SUBSEÇÃO → ESCOPO**

E deve respeitar a régua de:

**88 caracteres por linha**

sempre que tecnicamente possível.

---

> ░░░░░░░ Ciclo Oficial do Junglapp ░░░░░░░

```text
ENTENDER
    ↓
MAPEAR RISCOS
    ↓
DEFINIR
    ↓
CRIAR O MÍNIMO
    ↓
CRIAR COMPONENTE
    ↓
CRIAR BLOCOs
    ↓
CENTRALIZAR CONFIGURAÇÕES
    ↓
APLICAR TIGER
    ↓
ORGANIZAR COM SNAKE
    ↓
CONSTRUIR
    ↓
TESTAR
    ↓
CONECTAR
    ↓
REPETIR
    ↓
COMPLETAR
    ↓
VALIDAR
    ↓
EXTRAIR BLOCOs
    ↓
REFATORAR
    ↓
TESTAR NOVAMENTE
    ↓
FINALIZAR
```

---

> ░░░░░░░ Resumo para IA ░░░░░░░

Ao receber um projeto Junglapp:

1. **Entenda o objetivo.**
2. **Verifique os riscos com o Tiger.**
3. **Crie somente o necessário.**
4. **Use um arquivo principal por componente.**
5. **Separe futuras responsabilidades em BLOCOs.**
6. **Centralize valores ajustáveis dentro de cada BLOCO.**
7. **Não coloque secrets nas configurações.**
8. **Use o Snake para organizar tudo.**
9. **Respeite 88 caracteres.**
10. **Construa uma parte por vez.**
11. **Teste antes de acumular funcionalidades.**
12. **Conecte progressivamente.**
13. **Tome decisões pequenas de forma autônoma.**
14. **Não crie complexidade para problemas que ainda não existem.**
15. **Não faça a grande refatoração antes do projeto funcionar.**
16. **No final, extraia os BLOCOs para seus arquivos definitivos.**

---

> ░░░░░░░ Regra Final ░░░░░░░

**Segurança desde o início.**

**Configuração no lugar certo.**

**Mínimo de estrutura.**

**Máximo de clareza.**

**Funcionar primeiro.**

**Separar depois.**

**Construir o que precisa existir agora.**

**Preparar o presente para que o futuro seja fácil.**

# ███████ 🦁 FIM — ORDER OF LION ███████
