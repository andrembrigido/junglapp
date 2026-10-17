# ███████ Git — Padrão de Sincronização do Projeto ███████

Este documento define como o **Git/GitHub** deve ser utilizado dentro do
**Junglapp 2.0** para permitir que humanos e IAs compartilhem uma visão atual
do projeto.

No Junglapp, o Git não serve apenas para versionamento.

Ele também funciona como a ponte entre:

**AMBIENTE LOCAL → GITHUB → IA**

---

> ░░░░░░░ Projeto ░░░░░░░

Nome: NOME_DO_PROJETO

Rep: URL_DO_REPOSITORIO

Branch: BRANCH_DE_REFERENCIA

**Rotinas Rápidas**

| 🟢 START                   | 🟡 BRANCH — CRIAR                | 🔵 PUSH               | 🟠 PULL   | 🟣 BRANCH — TROCA      | ⚪ CLON           |
|----------------------------|-----------------------------------|------------------------|-----------|-------------------------|-------------------|
|git init                    |git switch -c nome-da-branch       |git status              |git status |git branch               |git clone URL      |
|git add .                   |git push -u origin nome-da-branch  |git add .               |git pull   |git switch nome-da-branch|cd nome-do-projeto |
|git commit -m "first commit"|                                   |git commit -m "mensagem"|           |                         |                   |
|git branch -M main          |                                   |git push                |           |                         |                   |
|git remote add origin URL   |                                   |                        |           |                         |                   |
|git push -u origin main     |                                   |                        |           |                         |                   |

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**ANTES DE CONTINUAR UM PROJETO → VERIFICAR O GIT**

Quando a IA não possui acesso direto ao computador do desenvolvedor:

```text
PC LOCAL
   ↓
PUSH
   ↓
GITHUB
   ↓
IA
```

O GitHub representa o estado do projeto disponível para a IA.

---

> ░░░░░░░ Fonte Atual do Projeto ░░░░░░░

Quando houver acesso ao repositório, a IA deve evitar trabalhar apenas com:

* memória;
* conversas anteriores;
* versões antigas do código;
* suposições sobre a estrutura atual.

Preferir:

```text
REPOSITÓRIO
     ↓
BRANCH DE REFERÊNCIA
     ↓
CÓDIGO ATUAL
```

A regra é:

**LER O QUE EXISTE ANTES DE ALTERAR.**

---

> ░░░░░░░ Branch de Referência ░░░░░░░

A IA deve utilizar a branch declarada no início deste arquivo.

Se a branch de referência for:

```text
dev
```

não assumir automaticamente:

```text
main
```

Fluxo:

```text
URL DO REPOSITÓRIO
       ↓
BRANCH DE REFERÊNCIA
       ↓
ESTADO ATUAL
```

Se futuramente a branch de referência mudar, alterar essa informação no início
deste arquivo.

---

> ░░░░░░░ Git e Estado Local ░░░░░░░

Existem dois estados diferentes:

```text
ESTADO LOCAL
```

e:

```text
ESTADO NO GITHUB
```

O estado local pode possuir alterações ainda não enviadas.

A IA somente consegue considerar aquilo que está disponível para ela.

Portanto:

```text
ALTERAÇÃO LOCAL
      ↓
SEM PUSH
      ↓
NÃO ESTÁ NO GITHUB
      ↓
IA NÃO CONSEGUE VER
```

A regra é:

**O ÚLTIMO PUSH É O ÚLTIMO ESTADO COMPARTILHADO.**

---

> ░░░░░░░ Antes de Continuar o Projeto ░░░░░░░

Quando o usuário pedir para:

```text
continuar o projeto

analisar o projeto

ver como está

descobrir o próximo passo

alterar uma funcionalidade existente
```

a IA deve, quando possuir acesso ao GitHub:

```text
LOCALIZAR REPOSITÓRIO
        ↓
VERIFICAR BRANCH DE REFERÊNCIA
        ↓
ANALISAR ESTRUTURA NECESSÁRIA
        ↓
LER ARQUIVOS RELEVANTES
        ↓
ENTENDER IMPLEMENTAÇÃO ATUAL
        ↓
CONTINUAR
```

Não pedir ao usuário para explicar novamente código que já pode ser consultado
no repositório.

---

> ░░░░░░░ Ler Antes de Criar ░░░░░░░

Antes de criar uma nova implementação, verificar se ela já existe.

Evitar:

```text
PEDIDO
  ↓
CRIAR NOVA SOLUÇÃO
```

Preferir:

```text
PEDIDO
  ↓
PROCURAR IMPLEMENTAÇÃO ATUAL
  ↓
ENTENDER
  ↓
ALTERAR OU COMPLETAR
```

Isso reduz:

* duplicação;
* conflitos;
* arquivos desnecessários;
* perda de código existente;
* regressões.

---

> ░░░░░░░ Estrutura Primeiro ░░░░░░░

Quando a localização de uma funcionalidade ainda não for conhecida, começar
pela estrutura do projeto.

```text
REPOSITÓRIO
     ↓
PASTAS
     ↓
ARQUIVOS
     ↓
RESPONSABILIDADES
     ↓
CÓDIGO NECESSÁRIO
```

A estrutura ajuda a identificar onde procurar antes de abrir arquivos
desnecessários.

---

> ░░░░░░░ Ler Somente o Necessário ░░░░░░░

A IA não precisa analisar o repositório inteiro para cada alteração.

Aplicar a filosofia Junglapp:

**LER O MÍNIMO NECESSÁRIO PARA ENTENDER CORRETAMENTE.**

Exemplo:

```text
ALTERAR LOGIN
     ↓
LOCALIZAR LOGIN
     ↓
LER ARQUIVO PRINCIPAL
     ↓
VERIFICAR DEPENDÊNCIAS RELACIONADAS
     ↓
ALTERAR
```

Se durante a análise aparecer outra responsabilidade necessária:

**EXPANDIR A LEITURA.**

---

> ░░░░░░░ Commits ░░░░░░░

O histórico de commits pode ser utilizado para compreender mudanças recentes
quando isso trouxer benefício real.

Exemplo:

```text
PROJETO FUNCIONAVA
       ↓
ALTERAÇÃO
       ↓
NOVO COMMIT
       ↓
PROBLEMA APARECEU
```

O histórico pode ajudar a descobrir:

* o que mudou;
* quando mudou;
* quais arquivos foram alterados;
* qual alteração pode estar relacionada ao problema.

Não é necessário analisar commits em toda tarefa.

---

> ░░░░░░░ Histórico Não Substitui Código Atual ░░░░░░░

O histórico ajuda a entender como o projeto chegou ao estado atual.

Mas a prioridade continua sendo:

**CÓDIGO ATUAL DA BRANCH DE REFERÊNCIA.**

A sequência é:

```text
CÓDIGO ATUAL
     ↓
EXISTE DÚVIDA?
     ↓
HISTÓRICO
```

Não o contrário.

---

> ░░░░░░░ Responsabilidade do Desenvolvedor ░░░░░░░

O desenvolvedor continua responsável por operações como:

```text
commit

push

pull

branch

merge
```

O Junglapp não exige que a IA execute essas operações.

Para o fluxo com IA, o importante é:

```text
DESENVOLVEDOR ALTERA
        ↓
TESTA
        ↓
FAZ PUSH
        ↓
GITHUB ATUALIZA
        ↓
IA CONSEGUE LER
```

---

> ░░░░░░░ Antes de uma Alteração ░░░░░░░

Antes de modificar código existente:

```text
LER
 ↓
ENTENDER
 ↓
IDENTIFICAR RESPONSABILIDADE
 ↓
VERIFICAR PADRÕES JUNGLAPP
 ↓
ALTERAR
 ↓
TESTAR
```

Não reconstruir uma funcionalidade simplesmente porque sua implementação atual
ainda não é conhecida.

Primeiro:

**CONSULTAR O PROJETO.**

---

> ░░░░░░░ Git Não Substitui Testes ░░░░░░░

O Git registra:

**O CÓDIGO ENVIADO.**

Ele não garante:

**QUE O CÓDIGO FUNCIONA.**

Um `push` significa apenas que aquele estado foi compartilhado.

A validação continua pertencendo ao:

**Padrão de Testes e Qualidade.**

Fluxo:

```text
ALTERAR
   ↓
TESTAR
   ↓
COMMIT
   ↓
PUSH
```

---

> ░░░░░░░ Git Não Substitui os Outros Padrões ░░░░░░░

O Git responde:

**O QUE EXISTE AGORA?**

Os outros padrões determinam:

**COMO TRABALHAR SOBRE O QUE EXISTE.**

Exemplo:

```text
GIT
 ↓
ESTADO ATUAL
 ↓
ORDER OF LION
 ↓
SNAKE
 ↓
SUFFOX
 ↓
BEAVAR
 ↓
FROGDLERS
 ↓
OUTROS PADRÕES
```

---

> ░░░░░░░ Relação com o Order of Lion ░░░░░░░

O **Git** responde:

**ONDE O PROJETO ESTÁ AGORA?**

O **Order of Lion** responde:

**O QUE DEVEMOS FAZER A SEGUIR?**

Se o projeto ainda não existe:

```text
ORDER OF LION
      ↓
COMEÇAR
```

Se o projeto já existe:

```text
GIT
 ↓
ESTADO ATUAL
 ↓
ORDER OF LION
 ↓
CONTINUAR
```

---

> ░░░░░░░ Relação com Testes e Qualidade ░░░░░░░

O Git permite recuperar:

**A VERSÃO COMPARTILHADA DO CÓDIGO.**

O padrão de **Testes e Qualidade** determina:

**SE ESSA VERSÃO POSSUI CONFIANÇA SUFICIENTE PARA CONTINUAR.**

Portanto:

```text
GIT
 ↓
CÓDIGO ATUAL
 ↓
TESTES
 ↓
COMPORTAMENTO VALIDADO
```

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao trabalhar em um projeto Junglapp já existente, uma IA deve:

1. localizar a URL declarada no início deste arquivo;
2. identificar a branch de referência;
3. verificar o estado atual do projeto;
4. analisar primeiro a estrutura necessária;
5. ler os arquivos relevantes;
6. não assumir que a última conversa representa o código atual;
7. não assumir que `main` é a branch correta;
8. não reconstruir funcionalidades sem verificar o existente;
9. considerar que alterações locais sem push não estão visíveis;
10. utilizar commits quando ajudarem a entender mudanças;
11. respeitar os padrões Junglapp presentes no projeto;
12. continuar a partir do código que realmente existe.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

O projeto já existe?

→ **VERIFICAR GIT**

Existe URL neste arquivo?

→ **USAR ESSA URL**

Existe branch de referência?

→ **USAR ESSA BRANCH**

O usuário quer continuar trabalho antigo?

→ **LER ESTADO ATUAL**

Vai alterar um arquivo existente?

→ **LER ANTES**

Não sabe onde está uma funcionalidade?

→ **ANALISAR ESTRUTURA**

Algo parece ter quebrado recentemente?

→ considerar **HISTÓRICO DE COMMITS**

A alteração está apenas no computador do desenvolvedor?

→ **NÃO ESTÁ VISÍVEL PARA A IA**

O código está no GitHub?

→ **NÃO SIGNIFICA QUE FOI VALIDADO**

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de trabalhar sobre um projeto existente, identificar:

**QUAL É O REPOSITÓRIO?**

**QUAL É A BRANCH DE REFERÊNCIA?**

**QUAL É O ESTADO ATUAL DO CÓDIGO?**

**O QUE JÁ EXISTE?**

**O QUE REALMENTE PRECISA SER ALTERADO?**

A filosofia do Git no Junglapp é:

**PUSH PARA COMPARTILHAR.**

**LER ANTES DE ALTERAR.**

**USAR O CÓDIGO ATUAL COMO REFERÊNCIA.**

**NÃO ADIVINHAR O ESTADO DO PROJETO.**

**CONTINUAR A PARTIR DO QUE REALMENTE EXISTE.**

# ███████ FIM — GIT ███████