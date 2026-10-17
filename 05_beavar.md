# ███████ 🦫 Beavar — Padrão Universal de Nomeação ███████

Este documento define o padrão oficial de nomeação de identificadores do
**Junglapp 2.0**.

O Beavar organiza nomes de:

* variáveis;
* constantes;
* funções;
* métodos;
* parâmetros;
* classes;
* estruturas;
* enums;
* callbacks;
* estados;
* coleções.

O objetivo é permitir que humanos e IAs entendam **o significado de um elemento
apenas lendo seu nome**.

O Beavar deve garantir:

* clareza;
* consistência;
* previsibilidade;
* fácil busca;
* melhor autocomplete;
* melhor manutenção;
* independência de linguagem.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**O NOME DEVE EXPLICAR A RESPONSABILIDADE.**

Evitar:

```text
data
value
thing
item2
temp
x
abc
```

quando um nome mais claro puder ser utilizado.

Preferir:

```text
userData
loginTimeout
selectedUser
retryCount
totalPrice
```

A pessoa ou IA não deveria precisar investigar várias linhas de código para
entender o significado de uma variável.

---

> ░░░░░░░ Regra Universal ░░░░░░░

O Beavar define principalmente:

**SIGNIFICADO + CONSISTÊNCIA**

A forma visual pode depender da linguagem.

Por exemplo:

```text
Dart        → lowerCamelCase
JavaScript  → lowerCamelCase
TypeScript  → lowerCamelCase
Java        → lowerCamelCase
Kotlin      → lowerCamelCase
Swift       → lowerCamelCase
Python      → snake_case
C#          → convenções próprias da plataforma
```

Portanto:

**A CONVENÇÃO NATIVA DA LINGUAGEM TEM PRIORIDADE SOBRE A FORMA VISUAL.**

Mas as regras semânticas do Beavar continuam.

---

> ░░░░░░░ Variáveis ░░░░░░░

Variáveis devem descrever claramente o dado armazenado.

Bom:

```text
userName
userAge
totalPrice
retryCount
selectedProduct
```

Ruim:

```text
data
value
number
thing
temp
x
```

Nomes curtos podem ser usados quando o contexto realmente os torna óbvios.

Exemplo:

```text
x
y
```

podem ser perfeitamente válidos em coordenadas matemáticas.

---

> ░░░░░░░ Booleanos ░░░░░░░

Booleanos devem parecer uma pergunta que pode ser respondida com:

**SIM ou NÃO**

Utilizar, quando a linguagem permitir:

```text
is
has
can
should
was
needs
```

Exemplos:

```text
isLoading
isVisible
hasError
hasPermission
canRetry
canEdit
shouldCache
needsUpdate
```

Evitar:

```text
loading
permission
error
visible
```

porque o tipo lógico não fica evidente apenas pelo nome.

---

> ░░░░░░░ Coleções ░░░░░░░

Coleções devem normalmente utilizar nomes no plural.

Exemplo:

```text
user
users

product
products

selectedId
selectedIds
```

A regra é:

**UM ITEM → SINGULAR**

**VÁRIOS ITENS → PLURAL**

---

> ░░░░░░░ Contagens ░░░░░░░

Utilizar nomes claros para quantidades.

Preferir:

```text
userCount
retryCount
totalUsers
itemTotal
```

Evitar:

```text
userNumber
usersValue
userAmountNumber
```

`count` normalmente representa quantidade contada.

`total` normalmente representa um total calculado ou acumulado.

---

> ░░░░░░░ Índices e Posições ░░░░░░░

Para posições em coleções, utilizar:

```text
index
currentIndex
selectedIndex
startIndex
endIndex
```

Evitar redundâncias como:

```text
indexNumber
positionIndexNumber
```

Quando `index` já comunica completamente o significado.

---

> ░░░░░░░ Mínimos e Máximos ░░░░░░░

Utilizar:

```text
min
max
```

como parte clara do nome.

Exemplos:

```text
minPasswordLength
maxLoginAttempts
minWidth
maxHeight
```

Esses nomes combinam diretamente com o padrão de
**Configurações Centralizadas**.

---

> ░░░░░░░ Tempo ░░░░░░░

Nomes relacionados a tempo devem deixar clara sua função e, quando necessário,
a unidade utilizada.

Exemplos:

```text
loginTimeout
fadeDuration
retryDelay
timeoutSeconds
animationMs
```

Evitar:

```text
time
delayValue
durationNumber
```

Se a linguagem possuir um tipo de duração próprio, prefira utilizá-lo em vez de
depender da unidade no nome.

---

> ░░░░░░░ Dimensões ░░░░░░░

Utilizar nomes como:

```text
width
height
radius
padding
spacing
margin
```

Quando necessário, adicionar contexto:

```text
buttonHeight
avatarSize
formSpacing
contentPadding
cardRadius
```

Evitar nomes excessivamente genéricos quando existirem várias dimensões
semelhantes no mesmo escopo.

---

> ░░░░░░░ Unidades ░░░░░░░

Quando a unidade não for evidente pelo tipo, ela pode fazer parte do nome.

Exemplos:

```text
timeoutMs
distanceKm
fileSizeMb
weightKg
```

Não adicionar unidade quando ela já for completamente definida pelo tipo ou
pela abstração utilizada.

---

> ░░░░░░░ Funções e Métodos ░░░░░░░

Funções devem normalmente representar uma **ação**.

Preferir verbos.

Exemplos:

```text
getUserData()
saveProfile()
validateEmail()
calculateTotal()
loadProducts()
sendMessage()
```

Evitar:

```text
user()
data()
thing()
process()
```

quando a função possui uma responsabilidade mais específica.

---

> ░░░░░░░ Funções Booleanas ░░░░░░░

Funções que retornam verdadeiro ou falso devem parecer perguntas.

Exemplos:

```text
isEmailValid()
hasPermission()
canAccessProfile()
shouldRetry()
```

Isso facilita a leitura:

```text
if (hasPermission()) {
  ...
}
```

---

> ░░░░░░░ Callbacks e Eventos ░░░░░░░

Callbacks devem utilizar nomes que indiquem claramente o evento.

Quando apropriado:

```text
onTap
onClick
onSubmit
onChange
onSave
onDelete
onLogin
```

A palavra `on` indica:

**QUANDO ESTE EVENTO ACONTECER**

Funções que executam a lógica interna podem utilizar outro nome.

Exemplo:

```text
onSubmit
    ↓
submitLogin()
```

---

> ░░░░░░░ Classes e Tipos ░░░░░░░

Classes, estruturas e tipos devem utilizar a convenção nativa da linguagem.

Em muitas linguagens:

**PascalCase / UpperCamelCase**

Exemplos:

```text
LoginPage
UserModel
AuthService
ProfileController
```

O nome deve representar claramente aquilo que o tipo é.

---

> ░░░░░░░ Evitar Repetição de Contexto ░░░░░░░

Não repetir desnecessariamente o nome da classe dentro de seus próprios campos.

Ruim:

```dart
class User {
  String userName;
  int userAge;
}
```

Preferir:

```dart
class User {
  String name;
  int age;
}
```

O contexto `User` já está definido pela classe.

---

> ░░░░░░░ Constantes ░░░░░░░

Constantes devem seguir a convenção nativa da linguagem.

Exemplos possíveis:

```text
Dart       → loginTimeout
JavaScript → LOGIN_TIMEOUT ou loginTimeout, conforme contexto
Python     → LOGIN_TIMEOUT
C#         → convenção da plataforma
```

O Beavar não força um formato visual único para constantes.

Ele exige que o nome seja:

* claro;
* específico;
* consistente;
* semanticamente correto.

---

> ░░░░░░░ Configurações Centralizadas ░░░░░░░

Valores ajustáveis devem possuir nomes que indiquem exatamente sua função.

Exemplo:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

const int maxLoginAttempts = 5;
const int minPasswordLength = 8;
const Duration loginTimeout = Duration(seconds: 30);
```

Evitar:

```dart
const int max = 5;
const int length = 8;
const int time = 30;
```

A configuração está centralizada, mas ainda precisa possuir um nome claro.

---

> ░░░░░░░ Imutabilidade ░░░░░░░

O conceito universal é:

**SE O VALOR NÃO PRECISA MUDAR, NÃO DEIXE MUDAR.**

A implementação depende da linguagem.

Exemplo em Dart:

```dart
const int maxLoginAttempts = 5;

final User currentUser;
```

Outras linguagens podem utilizar:

```text
const
readonly
final
immutable
let
```

ou mecanismos equivalentes.

O Beavar não obriga uma palavra-chave específica.

---

> ░░░░░░░ Tipo Explícito ░░░░░░░

Tipos explícitos podem melhorar a clareza em algumas situações.

Exemplo:

```dart
int userCount = 0;
bool isLoading = false;
```

Porém, o Junglapp não deve obrigar tipo explícito quando a linguagem possui
inferência clara e sua convenção recomenda utilizá-la.

A regra é:

**PREFERIR A FORMA MAIS CLARA SEM LUTAR CONTRA A LINGUAGEM.**

---

> ░░░░░░░ Privados ░░░░░░░

Privacidade de identificadores depende da linguagem.

No Dart:

```dart
_retryCount
_fetchUser()
```

Em outras linguagens pode existir:

```text
private
protected
fileprivate
internal
#
```

ou outros mecanismos.

A regra universal é:

**UTILIZAR O MECANISMO NATIVO DA LINGUAGEM.**

Não forçar `_` em linguagens onde ele não representa privacidade.

---

> ░░░░░░░ Enums ░░░░░░░

Enums devem possuir:

**TIPO CLARO + VALORES CLAROS**

Exemplo conceitual:

```text
UserRole

admin
guest
premium
```

A forma visual segue a convenção da linguagem.

Exemplo Dart:

```dart
enum UserRole {
  admin,
  guest,
  premium,
}
```

---

> ░░░░░░░ Abreviações ░░░░░░░

Evitar abreviações obscuras.

Ruim:

```text
usrNm
msgQt
usrCnt
prfImg
```

Preferir:

```text
userName
messageQuantity
userCount
profileImage
```

Abreviações universais e amplamente reconhecidas podem ser utilizadas.

Exemplos:

```text
id
url
api
http
https
json
html
css
ui
db
```

A regra é:

> **Uma pessoa nova no projeto entenderia essa abreviação imediatamente?**

Se não:

**escrever por extenso.**

---

> ░░░░░░░ Números nos Nomes ░░░░░░░

Evitar números usados apenas para diferenciar identificadores.

Ruim:

```text
user1
user2
temp3
button4
```

Preferir:

```text
currentUser
selectedUser
previousUser
submitButton
cancelButton
```

Números podem ser usados quando fazem parte real do conceito.

Exemplo:

```text
player1
player2
```

em um jogo especificamente estruturado para dois jogadores pode ser válido.

---

> ░░░░░░░ Nomes Temporários ░░░░░░░

Durante experimentação, nomes temporários podem surgir.

Antes de considerar o BLOCO concluído:

**RENOMEAR IDENTIFICADORES TEMPORÁRIOS.**

Evitar deixar no código final:

```text
temp
test
thing
stuff
data2
newValue2
```

---

> ░░░░░░░ Consistência de Vocabulário ░░░░░░░

O projeto deve escolher uma palavra para cada conceito e reutilizá-la.

Não misturar:

```text
user
account
member
client
```

para representar a mesma entidade sem uma razão real.

Se o conceito oficial é:

```text
user
```

preferir:

```text
userId
currentUser
userProfile
userData
```

Isso melhora buscas e entendimento por IA.

---

> ░░░░░░░ Mesmo Conceito, Mesmo Nome ░░░░░░░

Quando duas partes representam o mesmo conceito, utilizar o mesmo vocabulário.

Exemplo:

```text
userId
```

não deveria virar:

```text
accountIdentifier
```

em outra parte sem necessidade.

A consistência semântica é mais importante do que inventar nomes diferentes.

---

> ░░░░░░░ Evitar Redundância ░░░░░░░

Evitar nomes como:

```text
userUserName
indexNumber
totalCountTotal
buttonBtn
modelDataModel
```

O nome deve possuir somente as informações necessárias.

---

> ░░░░░░░ Exemplos Corretos ░░░░░░░

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

const int maxLoginAttempts = 5;
const int minPasswordLength = 8;

/* ************************ ESTADO ******************************************* */

bool isLoading = false;
bool hasError = false;

int retryCount = 0;

final List<User> users = [];

/* ************************ FUNÇÕES ***************************************** */

void loadUsers() {
  // ...
}

bool canRetryLogin() {
  // ...
}

/* ************************ CLASSE ****************************************** */

class LoginController {
  void onSubmit() {
    // ...
  }
}

/* ************************ ENUM ******************************************** */

enum UserRole {
  admin,
  guest,
  premium,
}
```

---

> ░░░░░░░ Exemplos Ruins ░░░░░░░

```dart
const max = 5;

bool loading = false;

var a = [];

String data = '';

int indexNumber = 0;

void process() {
  // ...
}

class user_model {
  // ...
}
```

O problema não é apenas estética.

Esses nomes escondem significado.

---

> ░░░░░░░ Convenção da Linguagem ░░░░░░░

O Beavar é universal.

Por isso, não deve tentar transformar todas as linguagens em Dart.

A prioridade é:

```text
SIGNIFICADO CLARO
      ↓
PADRÃO BEAVAR
      ↓
CONVENÇÃO NATIVA DA LINGUAGEM
```

Exemplo:

Um conceito chamado:

```text
max login attempts
```

poderia aparecer como:

```text
Dart       → maxLoginAttempts
JavaScript → maxLoginAttempts
Python     → max_login_attempts
C#         → MaxLoginAttempts ou convenção equivalente
```

O formato muda.

**O significado permanece.**

---

> ░░░░░░░ Relação com o Suffox ░░░░░░░

O **Suffox** define nomes de:

**ARQUIVOS**

Exemplo:

```text
login_auth_ctl.dart
```

O **Beavar** define nomes dentro desse arquivo:

```text
maxLoginAttempts

isLoading

authenticateUser()

LoginController
```

Portanto:

**SUFFOX → FORA DO ARQUIVO**

**BEAVAR → DENTRO DO CÓDIGO**

---

> ░░░░░░░ Relação com o Snake ░░░░░░░

O Snake organiza visualmente:

```text
BLOCO
  ↓
SEÇÃO
  ↓
SUBSEÇÃO
```

O Beavar organiza semanticamente aquilo que existe dentro dessas divisões.

Exemplo:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

const int maxLoginAttempts = 5;

/* ************************ ESTADO ******************************************* */

bool isLoading = false;

/* ************************ LÓGICA ******************************************* */

void authenticateUser() {
  // ...
}
```

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao criar um identificador, uma IA deve:

1. identificar exatamente o que aquele elemento representa;
2. utilizar a convenção nativa da linguagem;
3. escolher um nome que revele sua responsabilidade;
4. usar booleanos com sentido de pergunta;
5. usar coleções no plural;
6. evitar abreviações obscuras;
7. evitar nomes genéricos;
8. evitar números sem significado;
9. preservar o vocabulário já adotado pelo projeto;
10. não repetir contexto desnecessariamente;
11. renomear identificadores se sua responsabilidade mudar;
12. priorizar clareza sobre economia de caracteres.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

É um booleano?

→ nome que responda **SIM/NÃO**

É uma coleção?

→ **plural**

É uma função?

→ normalmente começar com **verbo**

É um callback?

→ normalmente `on...` ou convenção equivalente

É uma contagem?

→ `count` ou `total` conforme significado

É uma posição?

→ `index`

É um limite?

→ `min` ou `max`

É duração?

→ `duration`, `timeout`, `delay` ou unidade quando necessária

É um tipo?

→ convenção de tipo da linguagem

É privado?

→ mecanismo nativo da linguagem

É um arquivo?

→ utilizar **Suffox**

---

> ░░░░░░░ Regra Final ░░░░░░░

Um bom nome deve responder:

**O QUE É?**

**O QUE REPRESENTA?**

**O QUE FAZ?**

sem exigir investigação desnecessária.

A filosofia do Beavar é:

**NOMEAR PARA EXPLICAR.**

**SER ESPECÍFICO SEM SER REDUNDANTE.**

**MANTER O MESMO VOCABULÁRIO.**

**RESPEITAR A LINGUAGEM.**

**CLAREZA PRIMEIRO.**

# ███████ 🦫 FIM — BEAVAR ███████
