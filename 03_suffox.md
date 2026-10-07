# ███████ 🦊 Suffox — Padrão Universal de Nomeação de Arquivos ███████

Este documento define o padrão oficial de nomeação de arquivos do
**Junglapp 2.0**.

O objetivo é permitir que humanos e IAs identifiquem a responsabilidade de um
arquivo **apenas lendo seu nome**.

O Suffox deve garantir:

* consistência;
* previsibilidade;
* navegação rápida;
* fácil localização;
* nomes descritivos;
* independência de linguagem;
* integração com a estratégia de refatoração do Junglapp.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**NOME DO ARQUIVO = CONTEXTO + RESPONSABILIDADE**

O sufixo representa a **responsabilidade principal** daquele arquivo.

Exemplo:

```text
login_form_btn
```

Significa:

```text
login
  ↓
contexto principal

form
  ↓
subcontexto

btn
  ↓
responsabilidade do arquivo
```

A extensão pertence à linguagem.

```text
login_form_btn.dart
login_form_btn.ts
login_form_btn.py
login_form_btn.cs
login_form_btn.kt
```

O nome permanece.

A tecnologia muda apenas a extensão.

---

> ░░░░░░░ Formação Oficial ░░░░░░░

O formato padrão é:

```text
<feature>[_subcontext]_<sufixo>.<extensão>
```

Exemplos:

```text
login_pag.dart
login_form_btn.dart
login_auth_ctl.dart
profile_data_mdl.dart
stock_list_ctn.dart
splash_logo_anm.dart
```

O subcontexto é opcional.

Usar apenas quando realmente ajudar a identificar o arquivo.

---

> ░░░░░░░ Lower Snake Case ░░░░░░░

O padrão oficial do Suffox é:

**lower_snake_case**

Exemplos corretos:

```text
login_pag.dart
login_form_btn.dart
user_profile_mdl.dart
splash_logo_anm.dart
```

Evitar:

```text
LoginPage.dart
loginPage.dart
login-page.dart
LOGIN_PAGE.dart
área_login.dart
```

Utilizar somente:

* letras ASCII minúsculas;
* números quando possuírem significado real;
* `_` para separação.

Evitar:

* espaços;
* acentos;
* hífen;
* camelCase;
* PascalCase no nome físico do arquivo.

---

> ░░░░░░░ Um Sufixo por Arquivo ░░░░░░░

Cada arquivo deve possuir **um único sufixo principal**.

Não:

```text
login_form_btn_wdt.dart
user_data_mdl_str.dart
auth_api_svc.dart
```

Preferir:

```text
login_form_btn.dart
user_data_mdl.dart
auth_svc.dart
```

A pergunta é:

> **Qual é a principal responsabilidade desse arquivo?**

Essa responsabilidade define o sufixo.

---

> ░░░░░░░ Estratégia do Junglapp 2.0 ░░░░░░░

Durante a construção inicial, o Junglapp utiliza arquivos autocontidos.

Exemplo:

```text
login_pag.dart
```

Esse arquivo pode temporariamente possuir vários BLOCOs do Snake:

```text
LOGIN_PAGE

├── AUTENTICAÇÃO
├── VALIDAÇÃO
├── INTERFACE
└── ANIMAÇÃO
```

Esses BLOCOs ainda **não precisam virar arquivos**.

Primeiro:

**FAZER FUNCIONAR.**

---

> ░░░░░░░ Suffox Durante a Refatoração ░░░░░░░

Quando os BLOCOs do Snake forem extraídos, o Suffox define o nome dos novos
arquivos.

Antes:

```text
login_pag.dart

├── BLOCO AUTENTICAÇÃO
├── BLOCO VALIDAÇÃO
├── BLOCO FORMULÁRIO
└── BLOCO ANIMAÇÃO
```

Depois:

```text
login_pag.dart
login_auth_ctl.dart
login_validation_val.dart
login_form_wdt.dart
login_logo_anm.dart
```

Assim:

**SNAKE identifica o que pode ser extraído.**

**SUFFOX define como o novo arquivo será chamado.**

---

> ░░░░░░░ Regra de Extração ░░░░░░░

Ao transformar um BLOCO em arquivo:

```text
BLOCO
  ↓
IDENTIFICAR RESPONSABILIDADE
  ↓
ESCOLHER SUFIXO
  ↓
CRIAR NOME
  ↓
EXTRAIR
```

Exemplo:

```text
BLOCO: VALIDAÇÃO DO LOGIN
```

vira:

```text
login_validation_val.dart
```

---

> ░░░░░░░ Sufixos Oficiais — Interface ░░░░░░░

| Sufixo | Significado | Usado para                         |
| -----: | ----------- | ---------------------------------- |
|  `pag` | Page        | Página, tela ou destino principal  |
|  `ctn` | Container   | Agrupador visual ou seção          |
|  `wdt` | Widget      | Componente visual reutilizável     |
|  `btn` | Button      | Botão com responsabilidade própria |

Exemplos:

```text
home_pag.dart
stock_list_ctn.dart
user_avatar_wdt.dart
login_submit_btn.dart
```

`wdt` representa conceitualmente um **componente visual reutilizável**.

Mesmo quando a tecnologia não utiliza o termo "Widget", o significado do
Suffox permanece.

---

> ░░░░░░░ Sufixos Oficiais — Controle e Lógica ░░░░░░░

| Sufixo | Significado | Usado para                                 |
| -----: | ----------- | ------------------------------------------ |
|  `ctl` | Controller  | Coordenação e controle de comportamento    |
|  `svc` | Service     | Serviço ou regra operacional reutilizável  |
|  `val` | Validator   | Validações                                 |
|  `hlp` | Helper      | Função auxiliar com responsabilidade clara |

Exemplos:

```text
login_ctl.dart
auth_svc.dart
login_validation_val.dart
date_format_hlp.dart
```

Evitar:

```text
utils.dart
helpers.dart
functions.dart
```

Preferir dizer **o que o helper realmente faz**.

```text
date_format_hlp.dart
password_strength_val.dart
```

---

> ░░░░░░░ Sufixos Oficiais — Dados e Estado ░░░░░░░

| Sufixo | Significado          | Usado para                            |
| -----: | -------------------- | ------------------------------------- |
|  `mdl` | Model                | Estrutura ou modelo de dados          |
|  `str` | Store                | Estado compartilhado da aplicação     |
|  `rep` | Repository           | Acesso e abstração de fontes de dados |
|  `dto` | Data Transfer Object | Estrutura de transferência de dados   |

Exemplos:

```text
user_mdl.dart
cart_str.dart
product_rep.dart
login_response_dto.dart
```

O sufixo `str` representa **estado compartilhado**, não persistência.

Exemplo:

```text
cart_str
    ↓
estado atual do carrinho
```

Se esse estado precisar sobreviver ao fechamento da aplicação:

```text
CROCROLLER
    ↓
cart_str
    ↓
DATABEEZZE
    ↓
PERSISTÊNCIA
```

Portanto:

**`str` → ESTADO COMPARTILHADO**

**DataBeezze → PERSISTÊNCIA**

Criar esses arquivos somente quando a responsabilidade realmente existir.

---

> ░░░░░░░ Sufixos Oficiais — Comunicação ░░░░░░░

| Sufixo | Significado | Usado para                       |
| -----: | ----------- | -------------------------------- |
|  `api` | API         | Comunicação direta com API       |
|  `svc` | Service     | Serviço ou integração            |
|  `rep` | Repository  | Intermediação de fontes de dados |

Exemplos:

```text
user_api.dart
payment_svc.dart
product_rep.dart
```

Não criar:

```text
api_api.dart
service_svc.dart
```

O contexto precisa continuar descritivo.

---

> ░░░░░░░ Sufixos Oficiais — Animação ░░░░░░░

O Suffox mantém a separação do padrão original.

| Sufixo | Significado          | Usado para                          |
| -----: | -------------------- | ----------------------------------- |
|  `anm` | Animation            | Parte visual da animação            |
| `actl` | Animation Controller | Controle e orquestração da animação |

`anm` representa:

* efeitos;
* transições;
* transformações visuais;
* elementos animados.

`actl` representa:

* duração;
* curvas;
* estados;
* sequência;
* controle da animação.

Exemplos:

```text
splash_logo_anm.dart
logo_fade_actl.dart
```

---

> ░░░░░░░ Sufixos Oficiais — Configuração ░░░░░░░

| Sufixo | Significado   | Usado para                          |
| -----: | ------------- | ----------------------------------- |
|  `cfg` | Configuration | Configuração dedicada de um sistema |

Exemplo:

```text
server_cfg.py
database_cfg.ts
build_cfg.cs
```

Porém, lembre-se:

**Configurações locais devem permanecer dentro do próprio BLOCO sempre que
possível.**

Criar um arquivo `cfg` apenas quando a configuração realmente precisar ser
independente.

---

> ░░░░░░░ Arquivos Especiais do Junglapp ░░░░░░░

Alguns padrões possuem identidade própria e não precisam obrigatoriamente
utilizar um sufixo genérico.

Exemplos conceituais:

```text
Kolors
Navgator
```

Esses arquivos possuem responsabilidade definida por um padrão Junglapp.

O Suffox não deve forçar um sufixo desnecessário quando outro padrão já define
claramente a responsabilidade.

---

> ░░░░░░░ Sufixos Oficiais ░░░░░░░

Resumo atual:

| Sufixo | Responsabilidade               |
| -----: | ------------------------------ |
|  `pag` | Página / tela principal        |
|  `ctn` | Agrupador visual               |
|  `wdt` | Componente visual reutilizável |
|  `btn` | Botão                          |
|  `ctl` | Controle / coordenação         |
|  `svc` | Serviço                        |
|  `val` | Validação                      |
|  `hlp` | Helper específico              |
|  `anm` | Animação visual                |
| `actl` | Controle de animação           |
|  `mdl` | Modelo de dados                |
|  `str` | Estado compartilhado / Store   |
|  `rep` | Repository                     |
|  `dto` | Transferência de dados         |
|  `api` | Comunicação com API            |
|  `cfg` | Configuração dedicada          |

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

Renderiza uma página ou tela principal?

→ `pag`

É um agrupador visual?

→ `ctn`

É um componente visual reutilizável?

→ `wdt`

É especificamente um botão?

→ `btn`

Coordena comportamento ou comandos?

→ `ctl`

Executa um serviço reutilizável?

→ `svc`

Valida dados?

→ `val`

É uma função auxiliar específica?

→ `hlp`

É uma animação visual?

→ `anm`

Controla animações?

→ `actl`

Representa dados?

→ `mdl`

Mantém estado compartilhado?

→ `str`

Precisa persistir esse estado?

→ **DataBeezze**

Abstrai acesso a dados?

→ `rep`

Transporta dados entre sistemas?

→ `dto`

Comunica diretamente com uma API?

→ `api`

Possui configuração independente?

→ `cfg`

---

> ░░░░░░░ Não Confundir Estado com Persistência ░░░░░░░

Estado e persistência são responsabilidades diferentes.

Exemplo:

```text
currentUser
```

pode existir apenas durante a execução.

Seu gerenciamento pertence ao:

**Crocroller**

Se precisar ser salvo:

```text
ESTADO
   ↓
DATABEEZZE
   ↓
PERSISTÊNCIA
```

O arquivo `str` não se torna responsável por banco, arquivo ou storage apenas
porque contém um estado que posteriormente será persistido.

A regra é:

**STORE CONTROLA ESTADO.**

**DATABEEZZE CONTROLA PERSISTÊNCIA.**

---

> ░░░░░░░ Não Confundir Papel com Tecnologia ░░░░░░░

O sufixo representa **o que o arquivo faz**.

Não necessariamente **como ele foi implementado**.

Exemplo:

Um arquivo que utiliza HTTP internamente, mas cuja responsabilidade é fornecer
um serviço de autenticação, pode ser:

```text
auth_svc.dart
```

e não obrigatoriamente:

```text
auth_api.dart
```

Se sua responsabilidade principal for comunicação direta com a API:

```text
auth_api.dart
```

A pergunta sempre é:

> **Qual é o papel principal deste arquivo?**

---

> ░░░░░░░ Exemplos Bons ░░░░░░░

```text
login_pag.dart

login_form_btn.dart

login_auth_ctl.dart

login_validation_val.dart

splash_logo_anm.dart

splash_logo_actl.dart

home_header_ctn.dart

user_avatar_wdt.dart

user_mdl.dart

session_str.dart

product_rep.dart

payment_svc.dart

login_api.dart

date_format_hlp.dart
```

---

> ░░░░░░░ Exemplos Ruins ░░░░░░░

```text
utils.dart

file.dart

functions.dart

stuff.dart

misc.dart

login2.dart

login_controller_final.dart

widget-helper.dart

SplashLogo.dart

área_login.dart

login_btn_wdt.dart

auth_api_svc_ctl.dart
```

---

> ░░░░░░░ Números ░░░░░░░

Evitar números usados apenas para diferenciar arquivos.

Não:

```text
login1.dart
login2.dart
button3.dart
```

Se os arquivos são diferentes, o nome deve explicar a diferença.

Preferir:

```text
login_email_btn.dart
login_google_btn.dart
login_apple_btn.dart
```

Números são permitidos quando fazem parte real do conceito.

---

> ░░░░░░░ Testes ░░░░░░░

Arquivos de teste devem espelhar o arquivo testado sempre que a tecnologia
permitir.

Arquivo:

```text
login_ctl.dart
```

Teste:

```text
login_ctl_test.dart
```

Outro exemplo:

```text
user_mdl.py
user_mdl_test.py
```

A convenção nativa da tecnologia pode ser usada quando obrigatória.

---

> ░░░░░░░ Arquivos Obrigatórios da Tecnologia ░░░░░░░

O Suffox não deve renomear arquivos que uma linguagem, framework ou ferramenta
exige com um nome específico.

Exemplos conceituais:

```text
main
index
package
manifest
configuração nativa
```

A regra é:

**REQUISITO DA TECNOLOGIA TEM PRIORIDADE SOBRE O SUFFOX.**

O Suffox controla os arquivos que pertencem ao projeto e podem ser nomeados
livremente.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao criar ou extrair um arquivo, uma IA deve:

1. identificar a feature;
2. identificar a responsabilidade principal;
3. verificar se um arquivo realmente precisa existir;
4. escolher somente um sufixo;
5. utilizar `lower_snake_case`;
6. evitar nomes genéricos;
7. evitar números sem significado;
8. respeitar nomes obrigatórios da tecnologia;
9. verificar se um padrão Junglapp já define aquele arquivo;
10. renomear o arquivo se sua responsabilidade mudar;
11. utilizar `str` somente para estado compartilhado;
12. encaminhar persistência para o DataBeezze.

---

> ░░░░░░░ Relação com o Crocroller ░░░░░░░

O **Crocroller** determina:

**QUEM POSSUI O ESTADO E COMO ELE MUDA**

Quando esse estado precisar de um Store próprio, o Suffox pode nomeá-lo:

```text
cart_str.dart
```

Portanto:

**CROCROLLER → DEFINE O ESTADO**

**SUFFOX → NOMEIA O ARQUIVO DE ESTADO**

---

> ░░░░░░░ Relação com o DataBeezze ░░░░░░░

O **DataBeezze** determina como os dados são persistidos.

Exemplo:

```text
cart_str
   ↓
estado atual
   ↓
cart_rep
   ↓
banco / API / armazenamento
```

Portanto:

**STORE ≠ PERSISTÊNCIA**

O Store pode solicitar persistência.

Mas não substitui a camada responsável pelos dados.

---

> ░░░░░░░ Relação com o Snake ░░░░░░░

O **Snake** identifica um BLOCO:

```text
BLOCO AUTENTICAÇÃO
```

O **Suffox** transforma essa responsabilidade em um nome:

```text
login_auth_ctl.dart
```

Portanto:

**SNAKE → IDENTIFICA A FRONTEIRA**

**SUFFOX → DEFINE O NOME DO ARQUIVO**

---

> ░░░░░░░ Relação com o Order of Lion ░░░░░░░

O **Order of Lion** determina quando o arquivo deve existir.

O **Suffox** determina como ele será chamado.

Isso significa que o Suffox **não é autorização para criar arquivos
antecipadamente**.

Primeiro:

**NECESSIDADE**

Depois:

**ARQUIVO**

Depois:

**NOME CORRETO**

---

> ░░░░░░░ Observações Finais ░░░░░░░

Se a responsabilidade do arquivo mudar:

**RENOMEAR O ARQUIVO.**

Se um arquivo possuir responsabilidades demais:

**IDENTIFICAR BLOCOs COM O SNAKE.**

Se chegar o momento da refatoração:

**EXTRAIR OS BLOCOs E APLICAR O SUFFOX.**

Se o nome precisar de vários sufixos para explicar o arquivo:

**A RESPONSABILIDADE PROVAVELMENTE NÃO ESTÁ CLARA.**

---

> ░░░░░░░ Regra Final ░░░░░░░

Um bom nome deve permitir responder:

**DE QUAL FEATURE ESTE ARQUIVO É?**

**QUAL É A RESPONSABILIDADE DELE?**

sem precisar abrir o arquivo.

A filosofia do Suffox é:

**NOMEAR PELO QUE FAZ.**

**UM ARQUIVO.**

**UMA RESPONSABILIDADE PRINCIPAL.**

**UM SUFIXO.**

# ███████ 🦊 FIM — SUFFOX ███████
