# ███████ 🐍 Snake — Padrão de Comentários ███████

Este documento estabelece o padrão visual e hierárquico de comentários do
**Junglapp 2.0**, garantindo legibilidade, consistência, organização e facilidade
de refatoração.

O Snake foi desenvolvido para ser facilmente compreendido tanto por **humanos**
quanto por **IAs**.

O padrão é universal e pode ser adaptado à sintaxe de comentários da linguagem
utilizada.

> ░░░░░░░ Filosofia do Snake ░░░░░░░

O Junglapp 2.0 trabalha inicialmente com **arquivos autocontidos**.

Primeiro fazemos a funcionalidade funcionar.

Depois, durante a refatoração, partes desse arquivo poderão ser extraídas para
arquivos próprios.

Por isso, o Snake precisa mostrar claramente:

* onde cada responsabilidade começa;
* onde cada responsabilidade termina;
* quais partes poderão virar arquivos;
* quais partes pertencem umas às outras.

A estrutura oficial é:

**BLOCO → SOBRE → SEÇÃO → SUBSEÇÃO → ESCOPO**

---

> ░░░░░░░ Regra dos 88 Caracteres ░░░░░░░

Todos os comentários devem respeitar a régua de:

**88 caracteres por linha.**

As quebras devem ser feitas manualmente quando necessário, mantendo alinhamento
e legibilidade.

No VS Code:

```json
"editor.rulers": [88]
```

Sempre que tecnicamente possível, o próprio código também deve permanecer dentro
dessa régua.

---

> ░░░░░░░ Níveis de Comentário ░░░░░░░

| Nível | Nome         | Formato visual               | Finalidade      |
| ----: | ------------ | ---------------------------- | --------------- |
|   0️⃣ | **BLOCO**    | `╔══════╗`                   | Futuro arquivo  |
|   1️⃣ | **SOBRE**    | `/* ///// SOBRE ///// */`    | Explica o bloco |
|   2️⃣ | **SEÇÃO**    | `/* ***** SEÇÃO ***** */`    | Área principal  |
|   3️⃣ | **SUBSEÇÃO** | `/* ----- SUBSEÇÃO ----- */` | Divisão interna |
|   4️⃣ | **ESCOPO**   | `// comentário`              | Ação pontual    |

---

> ░░░░░░░ 0️⃣ BLOCO ░░░░░░░

O **BLOCO** é o maior nível do Snake.

Ele representa uma responsabilidade que poderá futuramente ser extraída e
transformada em outro arquivo.

Visualmente, deve chamar atenção imediatamente.

Exemplo:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ AUTENTICAÇÃO                                                            ║
   ║ FUTURO ARQUIVO: authentication                                          ║
   ║ RESPONSABILIDADE: autenticar o usuário                                  ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */
```

A regra é:

**1 BLOCO = 1 possível arquivo futuro**

Durante a refatoração:

**BLOCO → RECORTAR → NOVO ARQUIVO → CONECTAR**

---

> ░░░░░░░ 1️⃣ SOBRE ░░░░░░░

O **SOBRE** aparece imediatamente depois do BLOCO.

Ele explica aquela responsabilidade.

Deve informar, quando necessário:

* **Contexto**
* **Objetivo**
* **Pode**
* **Não pode**

Exemplo:

```dart
/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: controla o processo de autenticação do usuário.
   Objetivo: validar as credenciais e realizar a autenticação.
   Pode: estado, validação, lógica e comunicação com autenticação.
   Não pode: responsabilidades relacionadas ao perfil do usuário.
///////////////////////////////////////////////////////////////////////////// */
```

Quando o BLOCO for extraído, seu SOBRE vai junto.

---

> ░░░░░░░ 2️⃣ SEÇÃO ░░░░░░░

A **SEÇÃO** organiza as grandes áreas internas de um BLOCO.

Exemplos:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */


/* ************************ ESTADO ******************************************* */


/* ************************ VALIDAÇÃO **************************************** */


/* ************************ LÓGICA ******************************************* */


/* ************************ SERVIÇOS ***************************************** */


/* ************************ INTERFACE **************************************** */
```

Nem todo BLOCO precisa possuir todas essas seções.

Criamos somente as necessárias.

---

> ░░░░░░░ Configurações Centralizadas ░░░░░░░

Quando um BLOCO possuir valores que provavelmente serão alterados no futuro,
sua primeira SEÇÃO deve ser, quando necessário:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

const maxLoginAttempts = 5;
const loginTimeout = 30;
const minPasswordLength = 8;
```

Isso permite alterar valores importantes sem precisar procurá-los no código.

Essas configurações pertencem ao próprio BLOCO.

Quando o BLOCO virar outro arquivo, elas vão junto.

**Secrets não pertencem aqui.**

Nunca colocar diretamente:

* senha;
* token;
* API key;
* private key;
* credencial.

Secrets seguem as regras do **Tiger**.

---

> ░░░░░░░ 3️⃣ SUBSEÇÃO ░░░░░░░

A **SUBSEÇÃO** divide partes menores dentro de uma SEÇÃO.

Exemplo:

```dart
/* ------------------------------- EMAIL ------------------------------------ */


/* ------------------------------- SENHA ------------------------------------ */


/* ----------------------------- REQUISIÇÃO --------------------------------- */


/* ------------------------------- ERROS ------------------------------------ */
```

Ela deve existir somente quando realmente melhorar a organização.

---

> ░░░░░░░ 4️⃣ ESCOPO ░░░░░░░

O **ESCOPO** é o comentário pontual.

Exemplos:

```dart
// valida o formato do e-mail

// impede outra tentativa enquanto o login estiver processando

// atualiza o estado após autenticação

// exibe a mensagem de erro
```

Evitar comentários óbvios.

Exemplo desnecessário:

```dart
// adiciona 1 ao contador
counter++;
```

---

> ░░░░░░░ Exemplo Visual Completo ░░░░░░░

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ AUTENTICAÇÃO                                                            ║
   ║ FUTURO ARQUIVO: authentication                                          ║
   ║ RESPONSABILIDADE: autenticar o usuário                                  ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: controla o processo de autenticação.
   Objetivo: validar e enviar as credenciais.
   Pode: configurações, estado, validação e autenticação.
   Não pode: interface ou responsabilidades relacionadas ao perfil.
///////////////////////////////////////////////////////////////////////////// */

/* ************************ CONFIGURAÇÕES ************************************ */

const maxLoginAttempts = 5;
const loginTimeout = 30;

/* ************************ ESTADO ******************************************* */

bool isLoading = false;
String? errorMessage;

/* ************************ VALIDAÇÃO **************************************** */

/* ------------------------------- EMAIL ------------------------------------ */

// verifica se o e-mail possui formato válido

/* ------------------------------- SENHA ------------------------------------ */

// verifica se a senha possui o tamanho mínimo

/* ************************ LÓGICA ******************************************* */

/* ----------------------------- AUTENTICAR --------------------------------- */

// bloqueia novas tentativas durante o processamento

// envia as credenciais

// atualiza o estado conforme o resultado
```

---

> ░░░░░░░ Regra de Extração ░░░░░░░

O **BLOCO é a fronteira oficial de extração**.

Tudo que pertence ao BLOCO deve poder ser identificado visualmente.

Na refatoração:

1. Identificar o BLOCO.
2. Recortar seu conteúdo.
3. Criar o arquivo definitivo.
4. Colar o conteúdo.
5. Ajustar imports e conexões.
6. Testar.

O objetivo é **mover**, não reconstruir.

---

> ░░░░░░░ Boas Práticas ░░░░░░░

* Usar somente o Snake no projeto.
* Não misturar estilos de comentários.
* Respeitar a hierarquia dos níveis.
* Evitar comentários redundantes.
* Não criar divisões vazias.
* Utilizar somente os níveis necessários.
* Manter valores ajustáveis centralizados.
* Preparar BLOCOs para futura extração.
* Explicar **motivo, contexto e objetivo** quando necessário.
* Respeitar a régua de **88 caracteres**.

---

> ░░░░░░░ Hierarquia Final ░░░░░░░

**0️⃣ BLOCO**
↳ futuro arquivo

**1️⃣ SOBRE**
↳ explica o bloco

**2️⃣ SEÇÃO**
↳ grande responsabilidade interna

**3️⃣ SUBSEÇÃO**
↳ divisão da seção

**4️⃣ ESCOPO**
↳ comentário pontual

---

# ███████ 🐍 FIM — SNAKE ███████
