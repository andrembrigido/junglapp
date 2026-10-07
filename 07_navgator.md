# ███████ 🐱 Navgator — Padrão Universal de Rotas ███████

Este documento define o padrão universal de navegação e rotas do
**Junglapp 2.0**.

O objetivo é garantir que todos os caminhos da aplicação estejam:

* centralizados;
* organizados;
* fáceis de localizar;
* fáceis de alterar;
* protegidos quando necessário;
* independentes da tecnologia utilizada.

O Navgator pode ser aplicado em:

* apps mobile;
* sites;
* desktop;
* jogos;
* APIs;
* sistemas internos;
* qualquer projeto que possua navegação entre destinos.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**ROTA → NAVGATOR → DESTINO**

Evitar espalhar caminhos diretamente pelo projeto.

Não:

```dart
context.go('/profile');
```

em vários lugares diferentes.

Preferir:

```dart
context.go(AppRoutes.profile);
```

ou o equivalente da linguagem utilizada.

Assim, se o caminho mudar:

**alteramos em um único lugar.**

---

> ░░░░░░░ Responsabilidade do Navgator ░░░░░░░

O Navgator deve centralizar, quando aplicável:

* caminhos;
* nomes das rotas;
* destinos;
* rota inicial;
* parâmetros;
* rotas protegidas;
* redirecionamentos;
* rota de erro;
* rota não encontrada;
* regras básicas de acesso.

O Navgator não deve conter lógica de negócio da tela.

---

> ░░░░░░░ Regra Universal ░░░░░░░

Toda aplicação com navegação deve possuir um local oficial para declarar
suas rotas.

O nome conceitual é:

**Navgator**

A implementação física depende da tecnologia.

Exemplos:

```text
Flutter      → app_router.dart
React        → routes.ts
JavaScript   → routes.js
Python       → routes.py
C#           → Routes.cs
Kotlin       → Routes.kt
Swift        → Routes.swift
Unity        → SceneRouter.cs
Web          → router.ts
```

O nome do arquivo pode variar.

A responsabilidade permanece.

---

> ░░░░░░░ Configurações Centralizadas ░░░░░░░

Os caminhos devem ser definidos antes da configuração do roteador.

Exemplo conceitual:

```text
SPLASH  = /splash
LOGIN   = /login
HOME    = /home
PROFILE = /profile
```

Isso evita repetir strings pelo projeto.

---

> ░░░░░░░ Caminhos Centralizados ░░░░░░░

Exemplo Flutter:

```dart
/* ************************ CONFIGURAÇÕES ************************************ */

abstract class AppRoutes {
  static const splash = '/splash';
  static const login = '/login';
  static const home = '/home';
  static const profile = '/profile';
}
```

Depois:

```dart
context.go(AppRoutes.profile);
```

Em vez de:

```dart
context.go('/profile');
```

---

> ░░░░░░░ Estrutura Básica de uma Rota ░░░░░░░

Toda rota deve possuir, quando necessário:

| Campo          | Função                         |
| -------------- | ------------------------------ |
| **Nome**       | Identificação interna          |
| **Caminho**    | Endereço da rota               |
| **Destino**    | Tela, página, cena ou recurso  |
| **Parâmetros** | Informações recebidas          |
| **Acesso**     | Quem pode entrar               |
| **Fallback**   | O que acontece em caso de erro |

Nem toda tecnologia utiliza todos esses campos.

---

> ░░░░░░░ Rota Inicial ░░░░░░░

A aplicação deve possuir um ponto inicial claramente identificado.

Exemplo:

```text
INITIAL_ROUTE = SPLASH
```

ou:

```text
INITIAL_ROUTE = LOGIN
```

A rota inicial não deve ficar escondida dentro de uma configuração difícil
de localizar.

---

> ░░░░░░░ Organização das Rotas ░░░░░░░

As rotas devem seguir uma ordem previsível.

Sugestão:

```text
INICIAL

AUTENTICAÇÃO

PRINCIPAL

USUÁRIO

CONFIGURAÇÕES

ROTAS ESPECIAIS

ERRO / NOT FOUND
```

Essa ordem pode mudar conforme o projeto.

O importante é manter consistência.

---

> ░░░░░░░ Rotas Públicas ░░░░░░░

Rotas públicas podem ser acessadas sem autenticação.

Exemplos:

```text
/splash
/login
/register
/recovery
```

---

> ░░░░░░░ Rotas Protegidas ░░░░░░░

Rotas privadas devem verificar permissão antes de permitir acesso.

Exemplos:

```text
/home
/profile
/settings
/admin
```

Fluxo:

```text
SOLICITA ROTA
      ↓
VERIFICA ACESSO
      ↓
 ┌────┴────┐
SIM        NÃO
 ↓          ↓
ENTRA    REDIRECIONA
```

Essa proteção deve respeitar o padrão de segurança do Junglapp.

---

> ░░░░░░░ Nunca Confiar Apenas na Rota ░░░░░░░

Bloquear uma página no Navgator melhora o fluxo da aplicação.

Mas isso não substitui autorização real.

Exemplo:

```text
USUÁRIO NÃO PODE ABRIR /admin
```

não significa que a API administrativa está protegida.

A proteção real também deve existir no backend quando aplicável.

---

> ░░░░░░░ Parâmetros ░░░░░░░

Rotas podem receber parâmetros.

Exemplo:

```text
/profile/:userId
```

O parâmetro recebido deve ser tratado como entrada externa.

Nunca assumir:

```text
userId = 10
```

significa:

```text
USUÁRIO ATUAL TEM ACESSO AO USUÁRIO 10
```

Permissões continuam sendo verificadas pelo sistema responsável.

---

> ░░░░░░░ Rotas Nomeadas ░░░░░░░

Quando a tecnologia permitir, rotas podem possuir:

```text
NOME
+
CAMINHO
```

Exemplo:

```text
profile
/profile
```

Isso permite que o projeto navegue utilizando uma identificação estável,
mesmo se o caminho mudar futuramente.

---

> ░░░░░░░ Rotas de Erro ░░░░░░░

Todo sistema que permita navegação inválida deve possuir um comportamento
definido.

Exemplos:

```text
NOT FOUND

ERRO

ACESSO NEGADO
```

Nunca deixar a aplicação em estado indefinido.

---

> ░░░░░░░ Regra de Fallback ░░░░░░░

Quando uma rota não existir:

```text
ROTA INVÁLIDA
     ↓
FALLBACK
```

O fallback pode ser:

* página não encontrada;
* tela inicial;
* login;
* página de erro.

A escolha depende do projeto.

---

> ░░░░░░░ Exemplo Universal ░░░░░░░

Conceitualmente:

```text
ROUTES

splash
    path: /splash
    access: public
    destination: Splash

login
    path: /login
    access: public
    destination: Login

home
    path: /home
    access: authenticated
    destination: Home

profile
    path: /profile
    access: authenticated
    destination: Profile
```

A linguagem apenas traduz essa estrutura.

---

> ░░░░░░░ Exemplo Flutter ░░░░░░░

```dart
import 'package:go_router/go_router.dart';

/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ NAVGATOR                                                                ║
   ║ RESPONSABILIDADE: centralizar as rotas e navegação do aplicativo        ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: centraliza todas as rotas principais da aplicação.
   Objetivo: evitar caminhos espalhados e organizar a navegação.
   Pode: caminhos, destinos, redirecionamentos e regras de acesso.
   Não pode: lógica de negócio das páginas.
///////////////////////////////////////////////////////////////////////////// */

/* ************************ CONFIGURAÇÕES ************************************ */

abstract class AppRoutes {
  static const splash = '/splash';
  static const login = '/login';
  static const home = '/home';
  static const profile = '/profile';
}

/* ************************ ROTEADOR **************************************** */

GoRouter createAppRouter() {
  return GoRouter(
    initialLocation: AppRoutes.splash,

    routes: [
      /* ------------------------------- SPLASH ----------------------------- */

      // GoRoute(
      //   path: AppRoutes.splash,
      //   builder: (context, state) => const SplashPage(),
      // ),

      /* -------------------------------- LOGIN ----------------------------- */

      // GoRoute(
      //   path: AppRoutes.login,
      //   builder: (context, state) => const LoginPage(),
      // ),

      /* -------------------------------- HOME ------------------------------ */

      // GoRoute(
      //   path: AppRoutes.home,
      //   builder: (context, state) => const HomePage(),
      // ),
    ],
  );
}
```

---

> ░░░░░░░ Um Único Lugar ░░░░░░░

O objetivo é evitar:

```text
LoginPage      → '/home'
Menu           → '/home'
Profile        → '/home'
Splash         → '/home'
```

E utilizar:

```text
                     ┌→ LoginPage
                     │
AppRoutes.home ──────┼→ Menu
                     │
                     ├→ Profile
                     │
                     └→ Splash
```

Assim:

**1 ROTA = 1 FONTE OFICIAL**

---

> ░░░░░░░ Navegação Não é Rota ░░░░░░░

Existe uma diferença importante.

**ROTA**

Define onde o destino existe.

**NAVEGAÇÃO**

Define quando alguém vai para aquele destino.

O Navgator pode centralizar a estrutura de navegação.

Mas regras como:

> "Depois de concluir uma compra, vá para confirmação."

pertencem à lógica da funcionalidade, não necessariamente ao arquivo de rotas.

---

> ░░░░░░░ Regra do Mínimo ░░░░░░░

Não criar rotas que ainda não existem apenas porque poderão existir no futuro.

Adicionar a rota quando o destino realmente existir ou estiver sendo criado.

Evitar:

```text
/shop
/admin
/chat
/friends
/marketplace
```

se essas funcionalidades ainda não fazem parte do projeto atual.

---

> ░░░░░░░ Rotas e Refatoração ░░░░░░░

Durante a estratégia de arquivo único do Junglapp, o Navgator pode começar
simples.

À medida que o projeto crescer, grupos de rotas podem ser separados.

Exemplo:

```text
ANTES

Navgator

├── autenticação
├── principal
├── usuário
└── configurações
```

Depois:

```text
DEPOIS

routes/
├── auth
├── main
├── user
└── settings
```

Essa separação só deve acontecer quando trouxer benefício real.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao trabalhar em um projeto Junglapp, uma IA deve:

1. verificar o Navgator antes de criar uma rota;
2. evitar caminhos repetidos diretamente no código;
3. centralizar novos caminhos;
4. definir claramente a rota inicial;
5. identificar rotas públicas e protegidas;
6. tratar parâmetros como dados não confiáveis;
7. não confundir proteção visual com autorização real;
8. criar fallback quando necessário;
9. evitar rotas futuras sem necessidade;
10. manter a estrutura simples enquanto o projeto for pequeno.

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO CRIAR E CONECTAR AS ROTAS**

O **Snake** define:

**COMO ORGANIZAR O NAVGATOR**

O padrão de segurança define:

**COMO PROTEGER ACESSOS E PARÂMETROS**

O **Navgator** define:

**ONDE CADA DESTINO EXISTE E COMO ELE É ALCANÇADO**

---

> ░░░░░░░ Regra Final ░░░░░░░

Uma rota nunca deve precisar ser descoberta procurando pelo projeto.

Ela deve possuir um endereço oficial.

Esse endereço pertence ao:

**NAVGATOR**

A filosofia é:

**DEFINIR UMA VEZ.**

**REFERENCIAR SEMPRE.**

**PROTEGER QUANDO NECESSÁRIO.**

**ALTERAR EM UM ÚNICO LUGAR.**

# ███████ 🐱 FIM — NAVGATOR ███████
