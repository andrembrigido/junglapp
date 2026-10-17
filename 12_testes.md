# ███████ 🧪 Padrão de Testes e Qualidade ███████

Este documento define o padrão oficial de testes e qualidade do
**Junglapp 2.0**.

O objetivo é garantir que uma funcionalidade não seja considerada pronta apenas
porque aparentemente funciona.

O padrão deve ajudar humanos e IAs a verificar:

* comportamento esperado;
* erros prováveis;
* limites importantes;
* integração entre componentes;
* regressões;
* segurança quando aplicável;
* qualidade antes de avançar.

O padrão é universal.

Ele não depende de:

* linguagem;
* framework;
* engine;
* plataforma;
* biblioteca de testes.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra principal é:

**CONSTRUIR → TESTAR → CORRIGIR → VALIDAR → CONTINUAR**

Não acumular várias funcionalidades não testadas.

A filosofia é:

**TESTAR O QUE IMPORTA.**

**CORRIGIR ANTES DE ACUMULAR.**

**AUTOMATIZAR QUANDO TROUXER BENEFÍCIO REAL.**

---

> ░░░░░░░ Qualidade Não é Quantidade de Testes ░░░░░░░

Ter muitos testes não significa automaticamente possuir um projeto confiável.

Exemplo:

```text
100 TESTES
    ↓
testam coisas irrelevantes
    ↓
POUCA CONFIANÇA
```

Enquanto:

```text
20 TESTES IMPORTANTES
    ↓
protegem comportamentos críticos
    ↓
MAIOR CONFIANÇA
```

O objetivo não é maximizar o número de testes.

O objetivo é:

**REDUZIR O RISCO DE COMPORTAMENTO INCORRETO.**

---

> ░░░░░░░ Cobertura Não é Objetivo Final ░░░░░░░

Cobertura de código pode ser útil como indicador.

Mas não deve ser tratada como objetivo absoluto.

Não escrever testes inúteis apenas para aumentar:

```text
70%
80%
90%
100%
```

Uma linha executada durante um teste não significa que ela foi corretamente
validada.

A prioridade é:

**COMPORTAMENTO IMPORTANTE → TESTE ÚTIL**

---

> ░░░░░░░ Estratégia do Junglapp 2.0 ░░░░░░░

O Junglapp não exige uma arquitetura completa de testes antes do projeto
começar.

Primeiro:

```text
FUNCIONALIDADE
     ↓
TESTE NECESSÁRIO
     ↓
CORREÇÃO
```

À medida que o projeto cresce:

```text
TESTES MANUAIS
      ↓
TESTES AUTOMATIZADOS
      ↓
INTEGRAÇÃO
      ↓
REGRESSÃO
```

A estrutura de testes cresce junto com a necessidade real.

---

> ░░░░░░░ Ciclo Oficial ░░░░░░░

Para cada funcionalidade:

```text
CONSTRUIR
    ↓
TESTAR CAMINHO NORMAL
    ↓
TESTAR ERROS IMPORTANTES
    ↓
TESTAR LIMITES RELEVANTES
    ↓
CORRIGIR
    ↓
RETESTAR
    ↓
VALIDAR
    ↓
CONECTAR
```

Depois de conectar:

```text
TESTAR INTEGRAÇÃO
```

Somente então avançar.

---

> ░░░░░░░ Caminho Normal ░░░░░░░

O primeiro teste deve confirmar o comportamento esperado.

Exemplo:

```text
LOGIN

e-mail válido
+
senha válida
    ↓
autenticação
    ↓
usuário entra
```

Esse é o:

**CAMINHO NORMAL**

ou:

**HAPPY PATH**

Se o caminho principal não funciona:

**A FUNCIONALIDADE NÃO ESTÁ PRONTA.**

---

> ░░░░░░░ Erros Prováveis ░░░░░░░

Depois do caminho normal, testar falhas que realmente podem acontecer.

Exemplo:

```text
LOGIN

senha incorreta

e-mail inválido

campo vazio

sem conexão

servidor indisponível
```

Não é necessário inventar centenas de cenários improváveis.

Priorizar:

**ERROS REAIS + IMPACTO REAL**

---

> ░░░░░░░ Limites ░░░░░░░

Valores com limites devem ser testados nas bordas.

Exemplo:

```text
minPasswordLength = 8
```

Testar:

```text
7 caracteres  → inválido

8 caracteres  → válido

9 caracteres  → válido
```

Outro exemplo:

```text
maxItems = 10
```

Testar:

```text
9

10

11
```

A regra é:

**SE EXISTE UM LIMITE, TESTAR A BORDA.**

---

> ░░░░░░░ Estados Importantes ░░░░░░░

Fluxos com estados devem validar suas principais transições.

Exemplo:

```text
IDLE
  ↓
LOADING
  ↓
 ┌─────────┐
 ↓         ↓
SUCCESS   ERROR
```

Verificar se:

* o estado inicial está correto;
* loading começa quando deveria;
* sucesso termina corretamente;
* erro não deixa o sistema preso;
* retry funciona quando existir.

O gerenciamento do estado segue o **Crocroller**.

---

> ░░░░░░░ Testes Locais ░░░░░░░

Testes locais verificam uma responsabilidade pequena e isolada.

Exemplos:

```text
função

validador

cálculo

conversão

controller

regra
```

Exemplo conceitual:

```text
calculateTotal(10, 2)
        ↓
       20
```

São úteis quando existe lógica que pode ser validada sem executar o sistema
inteiro.

---

> ░░░░░░░ Testes de Integração ░░░░░░░

Testes de integração verificam se partes que funcionam isoladamente também
funcionam juntas.

Exemplo:

```text
LOGIN
  ↓
CONTROLLER
  ↓
REPOSITORY
  ↓
API
```

Cada parte pode funcionar sozinha.

Ainda assim, a conexão entre elas pode falhar.

Por isso:

**FUNCIONA SOZINHO ≠ FUNCIONA INTEGRADO**

---

> ░░░░░░░ Testes de Fluxo ░░░░░░░

Fluxos importantes devem ser testados do início ao fim quando isso trouxer
benefício real.

Exemplo:

```text
ABRIR APP
    ↓
LOGIN
    ↓
HOME
    ↓
PERFIL
```

Ou:

```text
ADICIONAR PRODUTO
       ↓
CARRINHO
       ↓
PAGAMENTO
       ↓
CONFIRMAÇÃO
```

Não é necessário automatizar todos os fluxos.

Priorizar os mais importantes para o produto.

---

> ░░░░░░░ Pirâmide de Complexidade ░░░░░░░

A estratégia deve começar pelas verificações mais simples.

```text
          FLUXO COMPLETO
               ▲
             /   \
            /     \
       INTEGRAÇÃO
          ▲
        /   \
       /     \
   TESTES LOCAIS
```

Quanto maior o teste:

* mais partes envolvidas;
* maior custo de execução;
* maior chance de falhas externas;
* mais difícil localizar o problema.

Utilizar cada nível onde ele fizer sentido.

---

> ░░░░░░░ Teste Manual ░░░░░░░

Teste manual é válido.

Especialmente durante:

* construção inicial;
* interface;
* animação;
* fluxo visual;
* protótipos;
* funcionalidades ainda mudando muito.

Exemplo:

```text
CONSTRUIR
   ↓
EXECUTAR
   ↓
USAR
   ↓
VERIFICAR
```

O Junglapp não exige automação apenas para dizer que existe um teste.

---

> ░░░░░░░ Teste Automatizado ░░░░░░░

Automatizar quando o teste:

* será repetido muitas vezes;
* protege comportamento importante;
* é fácil de executar automaticamente;
* evita regressões;
* economiza trabalho manual;
* reduz risco.

Exemplo:

```text
VALIDAÇÃO DE E-MAIL
```

é um bom candidato.

Um detalhe visual subjetivo que muda constantemente pode não ser.

---

> ░░░░░░░ Quando Automatizar ░░░░░░░

Perguntar:

**VAMOS EXECUTAR ESTE TESTE VÁRIAS VEZES?**

**UMA REGRESSÃO AQUI SERIA IMPORTANTE?**

**A AUTOMAÇÃO É CONFIÁVEL?**

**O CUSTO DE MANTER O TESTE COMPENSA?**

Se sim:

**AUTOMATIZAR.**

Se não:

um teste manual pode ser suficiente.

---

> ░░░░░░░ Testes Antes ou Depois do Código ░░░░░░░

O Junglapp não obriga:

**TDD**

nem proíbe TDD.

Um teste pode ser criado:

```text
ANTES DO CÓDIGO
```

ou:

```text
DEPOIS DO CÓDIGO
```

A decisão depende da situação.

O requisito é:

**COMPORTAMENTO IMPORTANTE DEVE SER VALIDADO.**

---

> ░░░░░░░ Bugs ░░░░░░░

Quando um bug for encontrado:

```text
REPRODUZIR
    ↓
IDENTIFICAR
    ↓
CORRIGIR
    ↓
TESTAR
```

Quando o bug possuir risco real de voltar:

```text
ADICIONAR TESTE DE REGRESSÃO
```

Assim:

```text
BUG
 ↓
TESTE QUE FALHA
 ↓
CORREÇÃO
 ↓
TESTE PASSA
```

quando a automação for apropriada.

---

> ░░░░░░░ Regressão ░░░░░░░

Regressão acontece quando uma alteração quebra algo que já funcionava.

Depois de mudanças importantes:

**TESTAR A MUDANÇA**

e também:

**TESTAR O QUE A MUDANÇA PODE TER AFETADO**

Exemplo:

```text
ALTEROU LOGIN
     ↓
testar login
     ↓
testar sessão
     ↓
testar logout
```

quando esses comportamentos estiverem relacionados.

---

> ░░░░░░░ Refatoração ░░░░░░░

Refatoração deve preservar comportamento.

Fluxo:

```text
FUNCIONA
   ↓
REFATORAR
   ↓
TESTAR NOVAMENTE
   ↓
MESMO COMPORTAMENTO
```

Se o comportamento muda durante uma refatoração sem intenção:

**ALGO DEU ERRADO.**

---

> ░░░░░░░ Testar BLOCO Antes de Extrair ░░░░░░░

Antes da refatoração final:

```text
BLOCO
  ↓
FUNCIONA
```

Depois da extração:

```text
BLOCO
  ↓
NOVO ARQUIVO
  ↓
CONECTAR
  ↓
MESMO TESTE
```

O objetivo é confirmar que mover o código não alterou seu comportamento.

---

> ░░░░░░░ Segurança ░░░░░░░

Funcionalidades que envolvem segurança devem testar também comportamentos de
proteção.

Exemplos:

```text
usuário sem permissão

entrada inválida

sessão expirada

requisição não autorizada

arquivo inválido

limite excedido
```

O **Padrão de Segurança** determina quais proteções são necessárias.

Este padrão determina:

**ESSAS PROTEÇÕES TAMBÉM DEVEM SER VALIDADAS.**

---

> ░░░░░░░ Dados ░░░░░░░

Funcionalidades que utilizam persistência devem testar quando necessário:

```text
LEITURA

CRIAÇÃO

ALTERAÇÃO

REMOÇÃO

ERROS

SINCRONIZAÇÃO

CONFLITOS
```

conforme as responsabilidades existentes.

O acesso aos dados segue o **DataBeezze**.

---

> ░░░░░░░ Navegação ░░░░░░░

Rotas importantes devem verificar:

```text
DESTINO CORRETO

PARÂMETROS CORRETOS

ACESSO CORRETO

FALLBACK

REDIRECIONAMENTO
```

quando aplicável.

A organização das rotas segue o **Navgator**.

---

> ░░░░░░░ Estado ░░░░░░░

Ao testar estado, verificar:

```text
ESTADO INICIAL

AÇÃO

NOVO ESTADO
```

Exemplo:

```text
cartItems = []
      ↓
addProduct()
      ↓
cartItems = [produto]
```

Testar comportamento.

Não detalhes internos sem necessidade.

---

> ░░░░░░░ Animações ░░░░░░░

Animações não precisam ser testadas quadro por quadro.

Validar principalmente:

* início;
* término;
* estado final;
* eventos importantes;
* comportamento reduzido quando aplicável.

A aparência visual pode exigir teste manual.

As regras de animação seguem o **Animacranes**.

---

> ░░░░░░░ Interface ░░░░░░░

Quando houver interface, verificar quando aplicável:

* elemento aparece;
* ação funciona;
* erro é mostrado;
* loading é mostrado;
* elemento desabilitado realmente não executa;
* navegação acontece corretamente;
* conteúdo importante permanece compreensível.

Não testar apenas se um componente existe.

Testar:

**SE ELE CUMPRE SUA FUNÇÃO.**

---

> ░░░░░░░ Acessibilidade ░░░░░░░

Qualidade também inclui acessibilidade quando o projeto possui interface.

Verificar conforme necessário:

* texto legível;
* contraste adequado;
* navegação por teclado;
* leitores de tela;
* labels;
* foco;
* tamanho de áreas interativas;
* redução de movimento.

Não é necessário aplicar regras irrelevantes à plataforma.

---

> ░░░░░░░ Performance ░░░░░░░

Não criar testes complexos de performance sem necessidade.

Mas operações importantes devem ser observadas quando apresentarem risco.

Exemplos:

```text
lista muito grande

consulta pesada

upload grande

carregamento inicial

animação complexa

processamento intenso
```

A regra é:

**MEDIR ANTES DE OTIMIZAR.**

---

> ░░░░░░░ Testes em Diferentes Ambientes ░░░░░░░

Quando o projeto possuir:

```text
DEVELOPMENT

TEST

PRODUCTION
```

testes devem utilizar o ambiente adequado.

Evitar testes destrutivos utilizando dados reais de produção.

O DataBeezze define a separação de dados quando necessária.

---

> ░░░░░░░ Mocks, Fakes e Stubs ░░░░░░░

Substitutos podem ser utilizados para isolar dependências externas.

Exemplo:

```text
LOGIN
  ↓
FAKE AUTH PROVIDER
```

Isso pode permitir testar sem depender da internet ou do serviço real.

Porém:

**NÃO MOCKAR TUDO AUTOMATICAMENTE.**

Mocks demais podem testar uma realidade que não existe.

Utilizar quando realmente ajudam a isolar a responsabilidade testada.

---

> ░░░░░░░ Dados de Teste ░░░░░░░

Dados utilizados em testes devem ser:

* previsíveis;
* claros;
* fáceis de reconstruir;
* independentes de produção quando necessário.

Evitar testes que só passam porque existe manualmente determinado registro em
um banco externo.

---

> ░░░░░░░ Testes Determinísticos ░░░░░░░

O mesmo teste deve produzir o mesmo resultado nas mesmas condições.

Evitar dependências desnecessárias de:

```text
horário atual

ordem aleatória

internet instável

dados externos mutáveis

estado deixado por outro teste
```

Quando esses elementos fizerem parte real do comportamento, devem ser
controlados de forma apropriada.

---

> ░░░░░░░ Testes Independentes ░░░░░░░

Um teste não deve depender desnecessariamente de outro teste ter executado
antes.

Evitar:

```text
TESTE A
   ↓
cria estado necessário
   ↓
TESTE B
```

quando o Teste B puder preparar seu próprio estado.

Preferir testes que possam ser executados:

* sozinhos;
* em qualquer ordem;
* repetidamente.

---

> ░░░░░░░ Testes Instáveis ░░░░░░░

Um teste que às vezes passa e às vezes falha sem mudança real é um problema.

Não aceitar como normal:

```text
"RODA DE NOVO QUE PASSA"
```

Investigar:

* tempo;
* concorrência;
* dependência externa;
* ordem;
* estado residual;
* dados imprevisíveis.

Um teste instável reduz confiança em toda a suíte.

---

> ░░░░░░░ Código de Teste Também é Código ░░░░░░░

Testes devem continuar:

* claros;
* simples;
* legíveis;
* fáceis de manter.

Aplicar:

**Beavar**

para identificadores.

Aplicar:

**Suffox**

para arquivos.

Aplicar:

**Frogdlers**

para organização quando necessário.

Não criar uma arquitetura gigantesca apenas para os testes.

---

> ░░░░░░░ Nomeação dos Arquivos de Teste ░░░░░░░

Quando a tecnologia permitir, o arquivo de teste deve espelhar o arquivo alvo.

Exemplo:

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

Se a tecnologia possuir convenção própria obrigatória:

**UTILIZAR A CONVENÇÃO NATIVA.**

---

> ░░░░░░░ Estrutura Inicial de Testes ░░░░░░░

Não criar antecipadamente:

```text
unit/
integration/
e2e/
fixtures/
mocks/
helpers/
```

sem necessidade.

Se existe apenas um teste:

```text
tests/
└── login_ctl_test
```

pode ser suficiente.

Quando crescer:

```text
tests/

├── login/
├── profile/
└── shop/
```

E somente depois, se trouxer benefício real:

```text
tests/

├── unit/
├── integration/
└── flow/
```

O **Frogdlers** continua valendo.

---

> ░░░░░░░ Critério de Funcionalidade Pronta ░░░░░░░

Uma funcionalidade pode ser considerada funcional quando:

```text
CAMINHO NORMAL
      ✓

ERROS IMPORTANTES
      ✓

LIMITES RELEVANTES
      ✓

SEGURANÇA NECESSÁRIA
      ✓

INTEGRAÇÃO NECESSÁRIA
      ✓
```

Não significa que todos os cenários imagináveis precisam ser testados.

Significa que existe confiança suficiente para continuar.

---

> ░░░░░░░ Critério de Projeto Pronto ░░░░░░░

Antes da finalização, revisar:

* fluxos principais;
* funcionalidades críticas;
* integrações;
* erros importantes;
* segurança;
* persistência;
* navegação;
* estado;
* regressões;
* plataforma final.

Depois da refatoração:

**TESTAR NOVAMENTE.**

---

> ░░░░░░░ Regra do Mínimo ░░░░░░░

Não criar:

```text
TESTE
```

apenas porque uma regra genérica diz que tudo precisa de teste automatizado.

Também não deixar de testar:

```text
COMPORTAMENTO CRÍTICO
```

apenas porque automatizar dá trabalho.

A regra é:

**RISCO + IMPORTÂNCIA → NÍVEL DE TESTE**

Quanto maior o impacto de uma falha:

**MAIOR A NECESSIDADE DE VALIDAÇÃO.**

---

> ░░░░░░░ Prioridade de Testes ░░░░░░░

Quando não for possível testar tudo imediatamente, priorizar:

```text
1. FUNCIONALIDADE CRÍTICA

2. SEGURANÇA

3. DADOS

4. FLUXO PRINCIPAL

5. INTEGRAÇÕES

6. ERROS PROVÁVEIS

7. LIMITES

8. DETALHES MENORES
```

O contexto do projeto pode alterar essa ordem.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao construir uma funcionalidade Junglapp, uma IA deve:

1. identificar o comportamento esperado;
2. testar o caminho normal;
3. identificar erros prováveis;
4. identificar limites relevantes;
5. validar proteções de segurança quando existirem;
6. testar integrações depois de conectar componentes;
7. corrigir antes de acumular novas funcionalidades;
8. automatizar testes quando houver benefício real;
9. evitar testes artificiais apenas por cobertura;
10. adicionar regressão para bugs importantes quando apropriado;
11. manter testes simples e determinísticos;
12. retestar após refatorações importantes;
13. não criar estrutura de testes antes de existir necessidade;
14. considerar uma funcionalidade pronta apenas com confiança suficiente no
    comportamento.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

É o comportamento principal?

→ **TESTAR**

Existe um erro provável?

→ **TESTAR**

Existe limite?

→ **TESTAR A BORDA**

Existe risco de segurança?

→ **TESTAR A PROTEÇÃO**

Duas partes acabaram de ser conectadas?

→ **TESTAR INTEGRAÇÃO**

É um bug importante já corrigido?

→ considerar **TESTE DE REGRESSÃO**

O teste será repetido frequentemente?

→ considerar **AUTOMATIZAÇÃO**

É puramente visual ou subjetivo?

→ considerar **TESTE MANUAL**

O teste existe apenas para aumentar cobertura?

→ **REAVALIAR**

A refatoração terminou?

→ **TESTAR NOVAMENTE**

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO TESTAR**

O **Snake** ajuda a identificar:

**QUAL RESPONSABILIDADE ESTÁ SENDO TESTADA**

O **Suffox** define:

**COMO NOMEAR ARQUIVOS DE TESTE**

O **Frogdlers** define:

**COMO ORGANIZAR OS TESTES QUANDO CRESCEREM**

O **Beavar** define:

**COMO NOMEAR ELEMENTOS DENTRO DOS TESTES**

O **Padrão de Segurança** define:

**QUAIS PROTEÇÕES PRECISAM EXISTIR**

O **DataBeezze** define:

**COMO DADOS E PERSISTÊNCIA SÃO TRATADOS**

O **Crocroller** define:

**COMO O ESTADO DEVE SE COMPORTAR**

O **Navgator** define:

**COMO OS DESTINOS E FLUXOS DE NAVEGAÇÃO FUNCIONAM**

O **Animacranes** define:

**COMO O MOVIMENTO E AS TRANSIÇÕES SE COMPORTAM**

Este padrão define:

**COMO CONFIRMAR QUE TUDO ISSO FUNCIONA CORRETAMENTE.**

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de considerar uma funcionalidade pronta, perguntar:

**O CAMINHO NORMAL FUNCIONA?**

**OS ERROS IMPORTANTES FORAM TRATADOS?**

**OS LIMITES FORAM VERIFICADOS?**

**A SEGURANÇA NECESSÁRIA FUNCIONA?**

**A INTEGRAÇÃO FUNCIONA?**

**UMA ALTERAÇÃO FUTURA CONSEGUIRIA QUEBRAR ISSO SEM PERCEBERMOS?**

**PRECISAMOS AUTOMATIZAR ALGUM DESSES TESTES?**

A filosofia é:

**CONSTRUIR.**

**TESTAR.**

**CORRIGIR.**

**VALIDAR.**

**CONECTAR.**

**TESTAR NOVAMENTE.**

**QUALIDADE É CONFIANÇA NO COMPORTAMENTO, NÃO QUANTIDADE DE TESTES.**

# ███████ 🧪 FIM — TESTES E QUALIDADE ███████
