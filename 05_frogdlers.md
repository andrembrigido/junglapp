# ███████ 🐸 Frogdlers — Padrão Universal de Organização de Pastas ███████

Este documento define o padrão oficial de organização de pastas do
**Junglapp 2.0**.

O objetivo é garantir uma estrutura:

* simples;
* previsível;
* fácil de navegar;
* fácil de expandir;
* independente de linguagem;
* organizada por responsabilidade;
* compatível com a estratégia de refatoração do Junglapp.

O Frogdlers não determina uma árvore fixa para todos os projetos.

Ele determina **quando uma pasta deve existir, onde ela deve ficar e o que pode
ser colocado dentro dela**.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**PASTA SÓ EXISTE QUANDO EXISTE ALGO REAL PARA ORGANIZAR.**

Não criar estrutura apenas porque ela poderá ser necessária futuramente.

A ordem é:

**NECESSIDADE → ARQUIVOS → AGRUPAMENTO → PASTA**

Nunca:

**PASTA → TALVEZ UM DIA TENHA ALGUMA COISA**

---

> ░░░░░░░ Filosofia do Junglapp 2.0 ░░░░░░░

No Junglapp 2.0, não começamos pela arquitetura final.

Primeiro:

**FAZER FUNCIONAR.**

Depois:

**COMPLETAR.**

Por último:

**ORGANIZAR E REFATORAR.**

Isso significa que o Frogdlers possui duas fases:

**ESTRUTURA INICIAL**

e

**ESTRUTURA FINAL**

---

> ░░░░░░░ Estrutura Inicial ░░░░░░░

No início, utilizar o **mínimo de pastas possível**.

Criar somente:

* pastas obrigatórias da tecnologia;
* pastas necessárias para execução;
* pastas que já possuem uma responsabilidade real.

Exemplo conceitual:

```text
project/

├── source/
├── assets/
└── arquivos obrigatórios da tecnologia
```

Dependendo da tecnologia, pode ser ainda mais simples.

Exemplo:

```text
project/

├── src/
│   ├── main
│   ├── login
│   └── home
│
└── assets/
```

Não criar antecipadamente:

```text
controllers/
services/
repositories/
models/
stores/
helpers/
widgets/
pages/
```

se essas divisões ainda não são necessárias.

---

> ░░░░░░░ Arquivo Antes da Pasta ░░░░░░░

Durante a construção inicial, uma funcionalidade pode existir como um único
arquivo autocontido.

Exemplo:

```text
src/

├── login_pag
├── home_pag
└── profile_pag
```

O arquivo pode possuir vários BLOCOs do Snake:

```text
LOGIN

├── BLOCO VALIDAÇÃO
├── BLOCO AUTENTICAÇÃO
├── BLOCO ESTADO
└── BLOCO INTERFACE
```

Ainda não é necessário criar:

```text
login/

├── validation/
├── authentication/
├── state/
└── interface/
```

Primeiro a funcionalidade deve funcionar.

---

> ░░░░░░░ BLOCO Antes da Pasta ░░░░░░░

O Snake prepara a futura estrutura de pastas.

Exemplo:

```text
login_pag

├── BLOCO AUTENTICAÇÃO
├── BLOCO VALIDAÇÃO
├── BLOCO FORMULÁRIO
└── BLOCO ANIMAÇÃO
```

Quando chegar a refatoração:

```text
login/

├── login_pag
├── login_auth_ctl
├── login_validation_val
├── login_form_wdt
└── login_logo_anm
```

Portanto:

**SNAKE IDENTIFICA**

**SUFFOX NOMEIA**

**FROGDLERS ORGANIZA**

---

> ░░░░░░░ Quando Criar uma Pasta ░░░░░░░

Criar uma pasta quando existir uma necessidade real de agrupamento.

Exemplos:

* vários arquivos pertencem à mesma feature;
* vários arquivos possuem a mesma responsabilidade;
* a raiz começou a ficar difícil de navegar;
* uma parte do sistema virou claramente independente;
* a tecnologia exige aquela pasta;
* a separação reduz confusão real.

Antes de criar uma pasta, perguntar:

> **O que exatamente esta pasta está organizando?**

Se não existir uma resposta clara:

**não criar.**

---

> ░░░░░░░ Quando NÃO Criar uma Pasta ░░░░░░░

Evitar pastas:

* vazias;
* contendo apenas outra pasta;
* criadas por antecipação;
* sem responsabilidade clara;
* criadas apenas para seguir uma arquitetura genérica;
* que adicionam navegação sem benefício real.

Exemplo desnecessário:

```text
features/
└── login/
    └── pages/
        └── login_pag
```

quando existe apenas um único arquivo.

Preferir inicialmente:

```text
login_pag
```

ou:

```text
features/
└── login_pag
```

dependendo da necessidade real do projeto.

---

> ░░░░░░░ Regra do Menor Caminho ░░░░░░░

Entre duas estruturas igualmente organizadas, preferir aquela que exige menos
níveis para chegar ao arquivo.

Evitar:

```text
src/
└── frontend/
    └── lib/
        └── features/
            └── authentication/
                └── pages/
                    └── login/
                        └── login_pag
```

quando:

```text
src/
└── login/
    └── login_pag
```

resolve o problema com a mesma clareza.

A profundidade deve existir por necessidade, não por estética arquitetural.

---

> ░░░░░░░ Feature First ░░░░░░░

Quando o projeto crescer, o Frogdlers favorece organização por
**funcionalidade**.

Exemplo:

```text
features/

├── login/
├── profile/
├── shop/
└── settings/
```

Cada feature mantém suas próprias responsabilidades próximas.

Isso facilita:

* localização;
* manutenção;
* remoção;
* reutilização;
* trabalho independente.

---

> ░░░░░░░ Feature First Não é Obrigatório no Início ░░░░░░░

O Junglapp não deve criar uma árvore completa de features antes que elas
existam.

Primeiro:

```text
login_pag
home_pag
```

Depois, quando houver necessidade:

```text
features/

├── login/
│   └── login_pag
│
└── home/
    └── home_pag
```

E somente quando a feature crescer:

```text
features/

└── login/
    ├── login_pag
    ├── login_auth_ctl
    ├── login_validation_val
    └── login_form_wdt
```

---

> ░░░░░░░ Organização por Responsabilidade ░░░░░░░

Dentro de uma feature, arquivos podem ser agrupados por responsabilidade quando
a quantidade justificar.

Exemplo:

```text
login/

├── pages/
├── controllers/
├── widgets/
├── models/
└── services/
```

Mas somente criar essas pastas quando realmente existirem arquivos suficientes
para justificar o agrupamento.

Com poucos arquivos:

```text
login/

├── login_pag
├── login_auth_ctl
├── login_form_wdt
└── login_user_mdl
```

é preferível.

---

> ░░░░░░░ Estrutura Cresce com o Projeto ░░░░░░░

A evolução ideal é:

```text
FASE 1

src/
└── login_pag
```

Depois:

```text
FASE 2

src/
└── login/
    ├── login_pag
    ├── login_auth_ctl
    └── login_form_wdt
```

Depois, se realmente necessário:

```text
FASE 3

src/
└── login/
    ├── pages/
    │   └── login_pag
    │
    ├── controllers/
    │   └── login_auth_ctl
    │
    └── widgets/
        └── login_form_wdt
```

A estrutura cresce **junto com a complexidade real**.

---

> ░░░░░░░ Estrutura Universal ░░░░░░░

O Frogdlers não obriga:

```text
backend/
domain/
frontend/
```

em todos os projetos.

Essa divisão continua válida quando o projeto realmente possuir essas camadas.

Exemplo:

```text
project/

├── backend/
├── domain/
└── frontend/
```

Mas um aplicativo simples pode possuir apenas:

```text
project/

├── src/
└── assets/
```

Um jogo pode possuir:

```text
project/

├── scripts/
├── scenes/
└── assets/
```

Uma API pode possuir:

```text
project/

├── src/
└── tests/
```

O conceito é universal.

A árvore depende do projeto.

---

> ░░░░░░░ Separação de Sistemas ░░░░░░░

Quando um projeto realmente possui sistemas independentes, eles devem possuir
pastas próprias.

Exemplo:

```text
project/

├── backend/
├── frontend/
└── shared/
```

ou:

```text
project/

├── server/
├── web/
└── mobile/
```

A separação deve representar uma diferença real de execução ou
responsabilidade.

---

> ░░░░░░░ Domain ░░░░░░░

Uma camada de domínio pode existir quando o projeto possuir regras de negócio
independentes da interface ou infraestrutura.

Exemplo:

```text
domain/

├── entities/
├── rules/
└── contracts/
```

Porém, o Frogdlers não exige uma pasta `domain/` em projetos que não precisam
dela.

A regra é:

**NÃO CRIAR CAMADA SEM RESPONSABILIDADE REAL.**

---

> ░░░░░░░ Core ░░░░░░░

Uma pasta global como:

```text
core/
```

pode existir para elementos realmente fundamentais ao projeto.

Exemplos:

```text
core/

├── Kolors
├── Navgator
└── configurações globais
```

Mas `core/` não deve virar um depósito de arquivos sem lugar definido.

Antes de mover algo para `core/`, perguntar:

> **Isso pertence realmente ao projeto inteiro?**

Se não:

**manter próximo da feature.**

---

> ░░░░░░░ Shared ░░░░░░░

Uma pasta:

```text
shared/
```

deve conter apenas elementos realmente utilizados por diferentes partes do
projeto.

Não promover algo para `shared/` apenas porque existe possibilidade de
reutilização futura.

Primeiro:

**LOCAL**

Depois, quando reutilizado:

**SHARED**

---

> ░░░░░░░ Regra Local Primeiro ░░░░░░░

Uma responsabilidade começa próxima de onde é utilizada.

Exemplo:

```text
login/
└── login_form_wdt
```

Se futuramente o mesmo componente for utilizado por várias features:

```text
shared/
└── form_wdt
```

A promoção acontece quando a reutilização se torna real.

---

> ░░░░░░░ Assets ░░░░░░░

Arquivos estáticos devem ficar organizados conforme as necessidades da
tecnologia.

Exemplos:

```text
assets/

├── images/
├── fonts/
├── audio/
└── videos/
```

Não é obrigatório criar todas essas pastas.

Se o projeto possui somente imagens:

```text
assets/
└── images/
```

é suficiente.

A tecnologia pode exigir outra localização.

Nesse caso:

**REQUISITO DA TECNOLOGIA TEM PRIORIDADE.**

---

> ░░░░░░░ Assets por Feature ░░░░░░░

Quando um projeto grande se beneficiar disso, assets também podem ser
organizados por feature.

Exemplo:

```text
assets/

├── login/
├── profile/
└── shop/
```

Ou por tipo:

```text
assets/

├── images/
├── audio/
└── fonts/
```

Escolher um padrão e manter consistência.

Não misturar organizações sem necessidade.

---

> ░░░░░░░ Pastas Obrigatórias da Tecnologia ░░░░░░░

Frameworks, engines e linguagens podem exigir pastas específicas.

Exemplos conceituais:

```text
src/
lib/
public/
android/
ios/
Assets/
Resources/
```

Essas estruturas devem ser respeitadas.

O Frogdlers atua **dentro da liberdade que a tecnologia permite**.

Nunca quebrar uma convenção obrigatória apenas para obedecer ao Junglapp.

---

> ░░░░░░░ Nomeação de Pastas ░░░░░░░

Pastas devem utilizar nomes:

* curtos;
* descritivos;
* previsíveis;
* semanticamente claros.

Quando a tecnologia não possuir outra convenção, preferir:

**lower_snake_case**

Exemplos:

```text
user_profile/
payment_history/
login/
settings/
```

Evitar:

```text
Stuff/
random/
other/
new_folder/
folder2/
misc/
```

---

> ░░░░░░░ Suffox Dentro do Frogdlers ░░░░░░░

O Frogdlers organiza **onde o arquivo fica**.

O Suffox define **como o arquivo se chama**.

Exemplo:

```text
login/

├── login_pag.dart
├── login_form_wdt.dart
└── login_auth_ctl.dart
```

Portanto:

**FROGDLERS → LOCAL**

**SUFFOX → NOME**

---

> ░░░░░░░ Dependências Entre Features ░░░░░░░

Evitar dependências cruzadas desnecessárias.

Exemplo problemático:

```text
login
  ↓
profile
  ↓
shop
  ↓
login
```

Quando duas features precisam da mesma responsabilidade, avaliar se ela deve
ser promovida para:

```text
shared/
```

ou:

```text
core/
```

Mas somente quando essa reutilização for real.

---

> ░░░░░░░ Nada Solto ░░░░░░░

O Frogdlers antigo possuía a regra:

**Nada solto.**

No Junglapp 2.0, essa regra continua, mas com uma interpretação mais simples.

Um arquivo pode permanecer na raiz permitida enquanto a estrutura ainda for
pequena.

Exemplo válido:

```text
src/

├── login_pag
├── home_pag
└── profile_pag
```

Isso não é considerado desorganizado.

Quando a quantidade começar a prejudicar navegação:

**AGRUPAR.**

---

> ░░░░░░░ Limite de Complexidade ░░░░░░░

Uma pasta não deve existir apenas para deixar a árvore mais bonita.

Uma pasta deve reduzir complexidade.

Se criar a pasta aumenta:

* cliques;
* profundidade;
* caminhos;
* imports;
* dificuldade de localização;

sem trazer organização real:

**não criar.**

---

> ░░░░░░░ Refatoração de Pastas ░░░░░░░

A estrutura definitiva surge durante a refatoração.

Fluxo:

```text
ARQUIVO PRINCIPAL
       ↓
BLOCOs DO SNAKE
       ↓
EXTRAÇÃO
       ↓
ARQUIVOS COM SUFFOX
       ↓
AGRUPAMENTO
       ↓
PASTAS COM FROGDLERS
```

Essa ordem é fundamental.

---

> ░░░░░░░ Exemplo Completo ░░░░░░░

Durante o desenvolvimento:

```text
src/

├── main
├── login_pag
├── home_pag
└── profile_pag
```

Depois da extração:

```text
src/

├── main
│
├── login_pag
├── login_auth_ctl
├── login_validation_val
├── login_form_wdt
│
├── home_pag
└── profile_pag
```

Quando o agrupamento passa a fazer sentido:

```text
src/

├── main
│
├── login/
│   ├── login_pag
│   ├── login_auth_ctl
│   ├── login_validation_val
│   └── login_form_wdt
│
├── home/
│   └── home_pag
│
└── profile/
    └── profile_pag
```

Somente se o projeto crescer ainda mais:

```text
src/

└── features/
    ├── login/
    │   ├── pages/
    │   ├── controllers/
    │   ├── validators/
    │   └── widgets/
    │
    ├── home/
    └── profile/
```

Cada nível é criado quando passa a resolver um problema real.

---

> ░░░░░░░ Estrutura Final Não é Obrigatória ░░░░░░░

Um projeto pequeno pode terminar perfeitamente assim:

```text
src/

├── main
├── login_pag
├── home_pag
└── profile_pag
```

Se a estrutura continua:

* clara;
* pequena;
* fácil de navegar;
* fácil de manter;

não existe motivo para criar mais pastas.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao organizar um projeto Junglapp, uma IA deve:

1. verificar a estrutura obrigatória da tecnologia;
2. criar somente as pastas necessárias;
3. evitar pastas vazias;
4. evitar profundidade sem benefício;
5. manter arquivos próximos da feature;
6. começar local antes de promover para global;
7. usar o Snake antes de separar arquivos;
8. usar o Suffox ao criar os arquivos extraídos;
9. criar pastas somente depois que houver algo para agrupar;
10. preferir a menor estrutura que continue clara;
11. respeitar convenções obrigatórias da tecnologia;
12. reorganizar somente quando a estrutura atual começar a atrapalhar.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

A tecnologia exige a pasta?

→ **CRIAR**

Existem vários arquivos da mesma feature?

→ considerar **PASTA DA FEATURE**

Existe apenas um arquivo?

→ normalmente **NÃO PRECISA DE PASTA**

Vários arquivos possuem a mesma responsabilidade?

→ considerar **SUBPASTA**

Algo é usado somente por uma feature?

→ manter **LOCAL**

Algo é realmente compartilhado?

→ considerar **SHARED**

Algo pertence ao sistema inteiro?

→ considerar **CORE**

Uma pasta está vazia?

→ **REMOVER**

A estrutura está ficando profunda sem motivo?

→ **SIMPLIFICAR**

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO CRIAR E QUANDO REFATORAR**

O **Snake** define:

**QUAIS BLOCOs PODERÃO SER EXTRAÍDOS**

O **Suffox** define:

**COMO OS ARQUIVOS EXTRAÍDOS SERÃO NOMEADOS**

O **Frogdlers** define:

**ONDE ESSES ARQUIVOS SERÃO ORGANIZADOS**

A sequência é:

```text
ORDER OF LION
      ↓
    SNAKE
      ↓
   SUFFOX
      ↓
 FROGDLERS
```

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de criar uma pasta, perguntar:

**ELA ORGANIZA ALGO QUE JÁ EXISTE?**

**ELA FACILITA ENCONTRAR ARQUIVOS?**

**ELA REDUZ COMPLEXIDADE?**

Se não:

**NÃO CRIAR.**

A filosofia do Frogdlers é:

**COMEÇAR PEQUENO.**

**AGRUPAR QUANDO NECESSÁRIO.**

**MANTER PRÓXIMO O QUE PERTENCE JUNTO.**

**NÃO CRIAR ESTRUTURA PARA UM FUTURO QUE AINDA NÃO EXISTE.**

# ███████ 🐸 FIM — FROGDLERS ███████
