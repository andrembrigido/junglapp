# ███████ 🎨 Kolors — Padrão Universal de Cores ███████

Este documento define o padrão universal de cores do **Junglapp 2.0**.

Todo projeto deve possuir uma **paleta centralizada de cores**, independentemente
da linguagem, framework, engine ou plataforma utilizada.

O objetivo é evitar cores espalhadas pelo código e garantir:

* consistência visual;
* facilidade de manutenção;
* facilidade de alteração;
* reutilização;
* leitura simples;
* padronização entre projetos;
* maior autonomia para humanos e IAs.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**COR UTILIZADA PELO PROJETO → KOLORS → COMPONENTE**

Evitar:

```dart
color: Color(0xFF1560FD)
```

Preferir:

```dart
color: Kolors.blue3
```

Assim, se a cor mudar futuramente, ela é alterada em **um único lugar**.

---

> ░░░░░░░ Regra Universal ░░░░░░░

Todo projeto Junglapp deve possuir um arquivo, módulo, classe, objeto ou estrutura
equivalente responsável pelas cores.

O nome conceitual será:

**Kolors**

A implementação depende da tecnologia.

Exemplos possíveis:

```text
Flutter      → app_colors.dart
Python       → colors.py
JavaScript   → colors.js
TypeScript   → colors.ts
C#           → Colors.cs
Kotlin       → Colors.kt
Swift        → Colors.swift
CSS          → colors.css
Unity        → Colors.cs
```

O nome físico do arquivo pode ser adaptado.

A responsabilidade não muda.

---

> ░░░░░░░ Regra de Centralização ░░░░░░░

Cores reutilizadas não devem ser declaradas diretamente dentro de:

* páginas;
* widgets;
* componentes;
* botões;
* serviços;
* funções;
* telas.

Elas devem ser declaradas primeiro no **Kolors**.

A regra é:

**UMA COR → UMA FONTE OFICIAL**

---

> ░░░░░░░ Sistema Numérico ░░░░░░░

As cores principais utilizam cinco intensidades.

| Número | Nome      | Significado   |
| -----: | --------- | ------------- |
|    `1` | **Soft**  | Muito claro   |
|    `2` | **Light** | Claro         |
|    `3` | **Pure**  | Cor principal |
|    `4` | **Dark**  | Escuro        |
|    `5` | **Hard**  | Muito escuro  |

Exemplo:

```text
blue1 → Soft
blue2 → Light
blue3 → Pure
blue4 → Dark
blue5 → Hard
```

O número `3` deve representar, sempre que possível, a versão principal da cor.

---

> ░░░░░░░ Cores Oficiais ░░░░░░░

O conjunto básico do Junglapp deve considerar somente cores fundamentais:

* branco;
* preto;
* cinza;
* vermelho;
* laranja;
* amarelo;
* verde;
* azul;
* roxo;
* rosa;
* marrom.

Não é necessário criar cores como:

* cyan;
* magenta;
* teal;
* indigo;
* lime;
* cores intermediárias desnecessárias.

Caso um projeto realmente precise delas, elas podem ser adicionadas depois.

---

> ░░░░░░░ BasicScale ░░░░░░░

O grupo básico contém cores estruturais que não precisam seguir a escala `1–5`.

```text
/* ************************ BASIC SCALE ************************************* */

white       = #FFFFFF
whiteEdge   = #FCFCFD

light       = branco com transparência
transparent = transparente
shadow      = preto com transparência

black       = #000000
```

Essas cores são usadas para necessidades estruturais gerais.

---

> ░░░░░░░ GrayScale ░░░░░░░

```text
/* ************************ GRAY SCALE ************************************** */

gray1 = #EAEAEA    // Soft
gray2 = #C8C8C8    // Light
gray3 = #7A7A7A    // Pure
gray4 = #484848    // Dark
gray5 = #1C1C1C    // Hard
```

---

> ░░░░░░░ RedScale ░░░░░░░

```text
/* ************************ RED SCALE *************************************** */

red1 = #FFE0E0    // Soft
red2 = #FF9A9A    // Light
red3 = #F44336    // Pure
red4 = #C62828    // Dark
red5 = #7F0000    // Hard
```

---

> ░░░░░░░ OrangeScale ░░░░░░░

```text
/* ************************ ORANGE SCALE ************************************ */

orange1 = #FFE5CC    // Soft
orange2 = #FFC27A    // Light
orange3 = #FF9800    // Pure
orange4 = #EF6C00    // Dark
orange5 = #9A4300    // Hard
```

---

> ░░░░░░░ YellowScale ░░░░░░░

```text
/* ************************ YELLOW SCALE ************************************ */

yellow1 = #FFF4CC    // Soft
yellow2 = #FFE082    // Light
yellow3 = #FFC107    // Pure
yellow4 = #D49B00    // Dark
yellow5 = #8A6500    // Hard
```

---

> ░░░░░░░ GreenScale ░░░░░░░

```text
/* ************************ GREEN SCALE ************************************* */

green1 = #D9F5E3    // Soft
green2 = #8ED8A8    // Light
green3 = #22A447    // Pure
green4 = #187A36    // Dark
green5 = #0D4D22    // Hard
```

---

> ░░░░░░░ BlueScale ░░░░░░░

```text
/* ************************ BLUE SCALE ************************************** */

blue1 = #DCE8FF    // Soft
blue2 = #8FB3FF    // Light
blue3 = #1560FD    // Pure
blue4 = #1148C8    // Dark
blue5 = #0D2F80    // Hard
```

---

> ░░░░░░░ PurpleScale ░░░░░░░

```text
/* ************************ PURPLE SCALE ************************************ */

purple1 = #E9DDFB    // Soft
purple2 = #C4A1F3    // Light
purple3 = #7E57C2    // Pure
purple4 = #5E35B1    // Dark
purple5 = #3B1E78    // Hard
```

---

> ░░░░░░░ PinkScale ░░░░░░░

```text
/* ************************ PINK SCALE ************************************** */

pink1 = #FFE0EC    // Soft
pink2 = #FFA6C8    // Light
pink3 = #EC407A    // Pure
pink4 = #C2185B    // Dark
pink5 = #7A0D3A    // Hard
```

---

> ░░░░░░░ BrownScale ░░░░░░░

```text
/* ************************ BROWN SCALE ************************************* */

brown1 = #EADDD4    // Soft
brown2 = #C8A78E    // Light
brown3 = #8D6E63    // Pure
brown4 = #5D4037    // Dark
brown5 = #3E2723    // Hard
```

---

> ░░░░░░░ Estrutura Recomendada ░░░░░░░

Independentemente da linguagem, a ordem deve ser:

```text
BASIC SCALE

GRAY SCALE

RED SCALE

ORANGE SCALE

YELLOW SCALE

GREEN SCALE

BLUE SCALE

PURPLE SCALE

PINK SCALE

BROWN SCALE
```

Isso também facilita para uma IA localizar rapidamente uma cor.

---

> ░░░░░░░ Exemplo Flutter ░░░░░░░

Em Flutter, uma implementação poderia continuar seguindo este formato:

```dart
import 'package:flutter/material.dart';

/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ KOLORS                                                                  ║
   ║ RESPONSABILIDADE: paleta central de cores do projeto                    ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: fonte central de todas as cores reutilizáveis do projeto.
   Objetivo: impedir valores de cor espalhados pela aplicação.
   Pode: cores, escalas e aliases visuais.
   Não pode: estilos, tamanhos, espaçamentos ou lógica de interface.
///////////////////////////////////////////////////////////////////////////// */

class Kolors {
  /* ************************ BASIC SCALE *********************************** */

  static const Color white = Color(0xFFFFFFFF);
  static const Color whiteEdge = Color(0xFFFCFCFD);
  static const Color light = Color(0x66FFFFFF);
  static const Color transparent = Colors.transparent;
  static const Color shadow = Color(0x66000000);
  static const Color black = Color(0xFF000000);

  /* ************************ GRAY SCALE ************************************ */

  static const Color gray1 = Color(0xFFEAEAEA);
  static const Color gray2 = Color(0xFFC8C8C8);
  static const Color gray3 = Color(0xFF7A7A7A);
  static const Color gray4 = Color(0xFF484848);
  static const Color gray5 = Color(0xFF1C1C1C);

  /* ************************ RED SCALE ************************************* */

  static const Color red1 = Color(0xFFFFE0E0);
  static const Color red2 = Color(0xFFFF9A9A);
  static const Color red3 = Color(0xFFF44336);
  static const Color red4 = Color(0xFFC62828);
  static const Color red5 = Color(0xFF7F0000);

  /* ************************ ORANGE SCALE ********************************** */

  static const Color orange1 = Color(0xFFFFE5CC);
  static const Color orange2 = Color(0xFFFFC27A);
  static const Color orange3 = Color(0xFFFF9800);
  static const Color orange4 = Color(0xFFEF6C00);
  static const Color orange5 = Color(0xFF9A4300);

  /* ************************ YELLOW SCALE ********************************** */

  static const Color yellow1 = Color(0xFFFFF4CC);
  static const Color yellow2 = Color(0xFFFFE082);
  static const Color yellow3 = Color(0xFFFFC107);
  static const Color yellow4 = Color(0xFFD49B00);
  static const Color yellow5 = Color(0xFF8A6500);

  /* ************************ GREEN SCALE *********************************** */

  static const Color green1 = Color(0xFFD9F5E3);
  static const Color green2 = Color(0xFF8ED8A8);
  static const Color green3 = Color(0xFF22A447);
  static const Color green4 = Color(0xFF187A36);
  static const Color green5 = Color(0xFF0D4D22);

  /* ************************ BLUE SCALE ************************************ */

  static const Color blue1 = Color(0xFFDCE8FF);
  static const Color blue2 = Color(0xFF8FB3FF);
  static const Color blue3 = Color(0xFF1560FD);
  static const Color blue4 = Color(0xFF1148C8);
  static const Color blue5 = Color(0xFF0D2F80);

  /* ************************ PURPLE SCALE ********************************** */

  static const Color purple1 = Color(0xFFE9DDFB);
  static const Color purple2 = Color(0xFFC4A1F3);
  static const Color purple3 = Color(0xFF7E57C2);
  static const Color purple4 = Color(0xFF5E35B1);
  static const Color purple5 = Color(0xFF3B1E78);

  /* ************************ PINK SCALE ************************************ */

  static const Color pink1 = Color(0xFFFFE0EC);
  static const Color pink2 = Color(0xFFFFA6C8);
  static const Color pink3 = Color(0xFFEC407A);
  static const Color pink4 = Color(0xFFC2185B);
  static const Color pink5 = Color(0xFF7A0D3A);

  /* ************************ BROWN SCALE *********************************** */

  static const Color brown1 = Color(0xFFEADDD4);
  static const Color brown2 = Color(0xFFC8A78E);
  static const Color brown3 = Color(0xFF8D6E63);
  static const Color brown4 = Color(0xFF5D4037);
  static const Color brown5 = Color(0xFF3E2723);
}
```

---

> ░░░░░░░ Cores do Projeto ░░░░░░░

A paleta básica não impede um projeto de possuir cores próprias.

Se um projeto utilizar uma cor de marca específica, ela deve ser adicionada ao
Kolors de forma organizada.

Exemplo:

```text
BRAND SCALE

brand1
brand2
brand3
brand4
brand5
```

A cor principal normalmente deve ser:

```text
brand3
```

---

> ░░░░░░░ Cores Semânticas ░░░░░░░

Quando necessário, um projeto pode criar aliases semânticos que apontam para
cores já existentes.

Exemplo:

```text
success → green3

warning → yellow3

danger → red3

info → blue3
```

Isso permite mudar posteriormente o significado visual sem alterar todos os
componentes.

O alias não deve duplicar o valor.

Ele deve **referenciar a paleta existente**.

---

> ░░░░░░░ Nunca Fazer ░░░░░░░

Evitar cores espalhadas:

```dart
Container(
  color: Color(0xFF1560FD),
)
```

Evitar:

```dart
Text(
  'Erro',
  style: TextStyle(
    color: Color(0xFFF44336),
  ),
)
```

Preferir:

```dart
Container(
  color: Kolors.blue3,
)
```

e:

```dart
Text(
  'Erro',
  style: TextStyle(
    color: Kolors.red3,
  ),
)
```

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao trabalhar em um projeto Junglapp, uma IA deve:

1. verificar o Kolors antes de criar uma nova cor;
2. reutilizar uma cor existente quando apropriado;
3. não espalhar HEX/RGB diretamente pelos componentes;
4. adicionar uma nova cor ao Kolors quando ela for realmente necessária;
5. manter o padrão `1–5`;
6. utilizar `3` como tom principal;
7. evitar criar cores intermediárias sem necessidade;
8. manter somente cores utilizadas ou planejadas como base oficial.

---

> ░░░░░░░ Relação com Configurações Centralizadas ░░░░░░░

Kolors é uma aplicação direta da filosofia de **Configurações Centralizadas**.

Em vez de:

```text
TELA A → #1560FD
TELA B → #1560FD
BOTÃO → #1560FD
ÍCONE → #1560FD
```

utilizamos:

```text
                    ┌→ TELA A
                    │
Kolors.blue3 ───────┼→ TELA B
                    │
                    ├→ BOTÃO
                    │
                    └→ ÍCONE
```

Uma alteração no Kolors atualiza todos os locais que dependem daquela cor.

---

> ░░░░░░░ Regra Final ░░░░░░░

**Uma cor não deve precisar ser procurada dentro do projeto.**

Ela deve possuir um endereço conhecido.

Esse endereço é:

**KOLORS**

A filosofia é:

**DEFINIR UMA VEZ.**

**REUTILIZAR SEMPRE.**

**ALTERAR EM UM ÚNICO LUGAR.**

# ███████ 🎨 FIM — KOLORS ███████
