# ███████ 🐝 DataBeezze — Padrão Universal de Persistência de Dados ███████

Este documento define o padrão oficial de persistência e acesso a dados do
**Junglapp 2.0**.

O DataBeezze organiza a relação entre:

**APLICAÇÃO → DADOS → ARMAZENAMENTO**

Ele pode ser utilizado com:

* bancos relacionais;
* bancos NoSQL;
* armazenamento local;
* APIs;
* arquivos;
* cache;
* cloud storage;
* bancos embarcados;
* serviços externos.

O objetivo é impedir que a aplicação fique dependente diretamente de uma
tecnologia específica.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A aplicação deve depender dos **dados que precisa**.

Não do **provedor que fornece esses dados**.

A regra é:

**APLICAÇÃO → CAMADA DE DADOS → PROVEDOR**

Evitar:

```text
INTERFACE
   ↓
SUPABASE DIRETAMENTE
```

Preferir:

```text
INTERFACE
   ↓
ACESSO A DADOS
   ↓
SUPABASE
```

Assim, futuramente:

```text
INTERFACE
   ↓
ACESSO A DADOS
   ↓
POSTGRES
```

sem reconstruir a interface.

---

> ░░░░░░░ Nunca Espalhar Acesso ao Banco ░░░░░░░

Chamadas ao banco, API ou armazenamento não devem ficar espalhadas pelo
projeto.

Não:

```text
LOGIN      → banco
PROFILE    → banco
HOME       → banco
SHOP       → banco
```

Preferir:

```text
LOGIN   ───┐
PROFILE ───┤
HOME    ───┼→ CAMADA DE DADOS → PROVEDOR
SHOP    ───┘
```

A tecnologia utilizada pode mudar.

O restante da aplicação deve sofrer o mínimo possível.

---

> ░░░░░░░ Estratégia do Junglapp 2.0 ░░░░░░░

O DataBeezze respeita a estratégia:

**FAZER FUNCIONAR → COMPLETAR → REFATORAR**

Isso significa que não precisamos criar desde o início:

```text
repositories/
services/
datasources/
dtos/
mappers/
```

apenas porque uma arquitetura tradicional recomenda.

Porém, o **limite entre aplicação e provedor de dados deve existir desde o
início**.

---

> ░░░░░░░ DataBeezze Dentro do Arquivo Único ░░░░░░░

Durante a construção inicial, o acesso aos dados pode permanecer dentro do
arquivo principal da funcionalidade.

Mas deve possuir um BLOCO próprio do Snake.

Exemplo:

```dart
/* ╔══════════════════════════════════════════════════════════════════════════╗
   ║ DADOS                                                                   ║
   ║ FUTURO ARQUIVO: login_auth_rep                                          ║
   ║ RESPONSABILIDADE: comunicação com a fonte de autenticação               ║
   ╚══════════════════════════════════════════════════════════════════════════╝ */

/* ///////////////////////////////// SOBRE /////////////////////////////////////
   Contexto: concentra toda comunicação externa usada pelo login.
   Objetivo: impedir dependência direta do provedor dentro da interface.
///////////////////////////////////////////////////////////////////////////// */


/* ************************ CONFIGURAÇÕES ************************************ */


/* ************************ LEITURA ****************************************** */


/* ************************ ESCRITA ****************************************** */
```

A interface não deve possuir chamadas externas espalhadas.

Ela chama o BLOCO responsável pelos dados.

---

> ░░░░░░░ Refatoração Futura ░░░░░░░

Inicialmente:

```text
login_pag

├── BLOCO INTERFACE
├── BLOCO ESTADO
├── BLOCO VALIDAÇÃO
└── BLOCO DADOS
```

Depois:

```text
login/

├── login_pag
├── login_auth_ctl
└── login_auth_rep
```

Portanto:

**SNAKE identifica o BLOCO.**

**SUFFOX nomeia o arquivo.**

**FROGDLERS define onde ele ficará.**

**DATABEEZZE define como ele acessa dados.**

---

> ░░░░░░░ Fonte de Verdade ░░░░░░░

Para cada tipo importante de dado, o projeto deve saber qual é sua
**fonte oficial de verdade**.

Exemplos:

```text
USUÁRIO
    ↓
BANCO REMOTO

CONFIGURAÇÃO LOCAL
    ↓
ARQUIVO LOCAL

SESSÃO
    ↓
ARMAZENAMENTO SEGURO

CACHE
    ↓
BANCO LOCAL
```

Cache não deve ser confundido com fonte oficial.

A aplicação precisa saber:

**QUEM POSSUI A VERSÃO VERDADEIRA DO DADO?**

---

> ░░░░░░░ Leitura e Escrita ░░░░░░░

Toda persistência possui dois grupos fundamentais:

```text
LEITURA
    ↓
OBTER DADOS

ESCRITA
    ↓
CRIAR
ALTERAR
REMOVER
```

Essas operações devem permanecer claramente organizadas.

Exemplo conceitual:

```text
getUser()

createUser()

updateUser()

deleteUser()
```

Nomes devem seguir o **Beavar**.

Arquivos extraídos devem seguir o **Suffox**.

---

> ░░░░░░░ Modelos de Dados ░░░░░░░

Dados externos não devem obrigatoriamente determinar a estrutura interna da
aplicação.

Exemplo externo:

```json
{
  "user_id": "123",
  "display_name": "Alex"
}
```

A aplicação pode trabalhar internamente com:

```text
User

id
name
```

A tradução entre formatos deve acontecer na camada de dados quando necessário.

---

> ░░░░░░░ DTOs ░░░░░░░

DTOs podem ser utilizados quando existe uma diferença real entre:

**FORMATO EXTERNO**

e

**FORMATO INTERNO**

Exemplo:

```text
UserDto
    ↓
User
```

Mas o Junglapp não exige DTO para todo dado.

Se criar um DTO não trouxer benefício:

**NÃO CRIAR.**

---

> ░░░░░░░ Repository ░░░░░░░

Repository é uma ferramenta importante do DataBeezze.

Ele cria uma fronteira entre:

```text
APLICAÇÃO
    ↓
REPOSITORY
    ↓
FONTE DE DADOS
```

Exemplo conceitual:

```text
UserRepository

getUser()
saveUser()
deleteUser()
```

A implementação pode utilizar:

```text
Supabase

PostgreSQL

Firebase

SQLite

API REST

GraphQL

arquivo local
```

sem obrigar o restante da aplicação a conhecer os detalhes.

---

> ░░░░░░░ Repository Não é Obrigatório Sempre ░░░░░░░

Não criar Repository apenas para obedecer arquitetura.

Se existe:

```text
1 arquivo
1 operação simples
1 fonte de dados
```

um BLOCO de dados bem definido pode ser suficiente durante a construção.

Quando a responsabilidade crescer:

**EXTRAIR → REPOSITORY**

A abstração deve surgir quando resolver um problema real.

---

> ░░░░░░░ Provider ░░░░░░░

O provedor é a tecnologia responsável pelos dados.

Exemplos:

```text
Supabase
PostgreSQL
Firebase
SQLite
MongoDB
MySQL
S3
API externa
arquivo local
```

O DataBeezze não recomenda um provedor universal.

A escolha depende do projeto.

---

> ░░░░░░░ Configuração do Provider ░░░░░░░

Quando um projeto possuir mais de uma implementação possível, a escolha do
provedor deve ficar centralizada.

Exemplo conceitual:

```text
DATABASE_PROVIDER = SUPABASE
```

ou:

```text
DATABASE_PROVIDER = POSTGRES
```

Nunca espalhar condições pelo código como:

```text
if supabase...
if firebase...
if postgres...
```

em diversos componentes.

---

> ░░░░░░░ Configuração Não é Credencial ░░░░░░░

Pode existir:

```text
databaseProvider = supabase
```

dentro das configurações.

Não deve existir:

```text
databasePassword = "123456"
apiSecret = "..."
privateKey = "..."
```

diretamente no código.

Credenciais e secrets seguem o **Padrão de Segurança** do Junglapp.

---

> ░░░░░░░ Segurança dos Dados ░░░░░░░

Segurança deve existir também na fonte de dados.

Não confiar apenas em:

```text
TELA ESCONDIDA
BOTÃO ESCONDIDO
VERIFICAÇÃO DO APP
```

A fonte responsável deve validar permissões.

Quando aplicável:

```text
USUÁRIO
    ↓
REQUISIÇÃO
    ↓
AUTENTICAÇÃO
    ↓
AUTORIZAÇÃO
    ↓
DADOS
```

Segurança no frontend não substitui segurança no backend.

---

> ░░░░░░░ Row-Level Security ░░░░░░░

Quando a tecnologia oferecer mecanismos como **Row-Level Security**, políticas
por documento ou controles equivalentes, eles devem ser considerados para
limitar acesso aos dados.

Exemplo conceitual:

```text
USER A
    ↓
SOMENTE DADOS DO USER A
```

O mecanismo específico depende da tecnologia.

RLS não é uma exigência universal porque nem todo banco possui esse recurso.

A regra universal é:

**A AUTORIZAÇÃO DEVE EXISTIR NA CAMADA CONFIÁVEL.**

---

> ░░░░░░░ Queries Seguras ░░░░░░░

Entrada externa nunca deve ser concatenada diretamente em queries.

Evitar:

```text
"SELECT * FROM users WHERE id = " + userInput
```

Preferir:

```text
QUERY PARAMETRIZADA
        +
VALOR SEPARADO
```

Essa regra pertence tanto ao DataBeezze quanto ao padrão de segurança.

---

> ░░░░░░░ Validação de Dados ░░░░░░░

Dados recebidos devem ser validados quando necessário.

Verificar:

```text
TIPO

FORMATO

TAMANHO

INTERVALO

OBRIGATORIEDADE

PERMISSÃO
```

Não confiar automaticamente em dados recebidos de:

```text
usuário
API
banco externo
arquivo
cache
serviço terceiro
```

---

> ░░░░░░░ Banco Local ░░░░░░░

Persistência local pode ser utilizada para:

```text
CACHE

OFFLINE

PREFERÊNCIAS

DADOS TEMPORÁRIOS

DADOS PERMANENTES LOCAIS
```

A tecnologia depende da plataforma.

Exemplos:

```text
SQLite
IndexedDB
arquivos
Key-Value Store
bancos embarcados
```

DataBeezze não exige uma implementação específica.

---

> ░░░░░░░ Offline-First ░░░░░░░

Offline-first deve ser utilizado quando o produto realmente precisar funcionar
sem conexão.

Não é obrigatório para todo projeto.

Quando necessário:

```text
UI
 ↓
DADOS LOCAIS
 ↓
SINCRONIZAÇÃO
 ↓
SERVIDOR
```

O usuário pode continuar trabalhando localmente e os dados são sincronizados
quando possível.

---

> ░░░░░░░ Cache Não é Offline-First ░░░░░░░

Cache apenas acelera ou reduz requisições.

Offline-first permite que funcionalidades continuem operando sem conexão.

São conceitos diferentes.

Exemplo:

```text
CACHE
    ↓
última resposta armazenada
```

versus:

```text
OFFLINE-FIRST
    ↓
ler
criar
editar
remover
sincronizar depois
```

---

> ░░░░░░░ Sincronização ░░░░░░░

Projetos com dados locais e remotos devem definir uma estratégia de
sincronização.

É necessário saber:

```text
QUANDO SINCRONIZAR

O QUE SINCRONIZAR

QUEM É A FONTE DE VERDADE

O QUE ACONTECE EM CONFLITO
```

Não implementar sincronização complexa sem necessidade real.

---

> ░░░░░░░ Conflitos ░░░░░░░

Quando dois locais alterarem o mesmo dado, deve existir uma regra.

Exemplos conceituais:

```text
VERSÃO MAIS NOVA VENCE
```

ou:

```text
SERVIDOR VENCE
```

ou:

```text
USUÁRIO ESCOLHE
```

A regra depende do produto.

Ela deve ser explícita.

---

> ░░░░░░░ Storage de Arquivos ░░░░░░░

Arquivos como:

```text
imagens
vídeos
documentos
áudios
```

não precisam utilizar o mesmo sistema que os dados estruturados.

A aplicação deve acessar storage através de uma responsabilidade clara.

Exemplo:

```text
APLICAÇÃO
    ↓
FILE SERVICE
    ↓
STORAGE
```

O storage pode ser:

```text
S3

Supabase Storage

Firebase Storage

servidor próprio

filesystem
```

---

> ░░░░░░░ Não Misturar Storage com UI ░░░░░░░

Evitar:

```text
BOTÃO DE AVATAR
    ↓
SDK DO S3 DIRETAMENTE
```

Preferir:

```text
BOTÃO DE AVATAR
    ↓
UPLOAD AVATAR
    ↓
FILE SERVICE
    ↓
S3
```

Assim, o provedor pode mudar posteriormente.

---

> ░░░░░░░ Schema ░░░░░░░

Quando um banco possuir schema, sua estrutura deve ser tratada como parte
versionada do projeto.

Exemplos:

```text
users

posts

orders

payments
```

Mudanças importantes não devem depender de alterações manuais esquecidas.

---

> ░░░░░░░ Migrations ░░░░░░░

Alterações de schema devem utilizar migrations ou mecanismo equivalente quando
a tecnologia suportar.

Fluxo:

```text
SCHEMA V1
    ↓
MIGRATION
    ↓
SCHEMA V2
```

Evitar:

```text
"ALTEREI DIRETO NO BANCO E DEPOIS A GENTE VÊ"
```

O histórico do banco deve ser reproduzível.

---

> ░░░░░░░ Dados de Produção ░░░░░░░

Mudanças estruturais devem considerar dados existentes.

Nunca assumir que uma tabela está vazia.

Antes de remover ou transformar dados importantes, avaliar:

```text
MIGRAÇÃO

BACKUP

COMPATIBILIDADE

ROLLBACK
```

---

> ░░░░░░░ Backups ░░░░░░░

Quando os dados forem importantes:

**BACKUP DEVE EXISTIR.**

Mas backup não é suficiente.

A regra é:

**BACKUP → PROTEGER → TESTAR RESTAURAÇÃO**

Um backup que nunca foi restaurado não deve ser considerado garantidamente
funcional.

---

> ░░░░░░░ Ambientes ░░░░░░░

Projetos que justificarem a separação devem utilizar ambientes distintos.

Exemplo:

```text
DEVELOPMENT

TEST

PRODUCTION
```

Evitar desenvolver diretamente utilizando dados reais de produção.

Credenciais também devem ser separadas.

---

> ░░░░░░░ Dados de Teste ░░░░░░░

Dados de teste não devem depender desnecessariamente de produção.

Quando possível:

```text
TESTE
  ↓
BANCO DE TESTE
```

ou:

```text
TESTE
  ↓
MOCK / FAKE PROVIDER
```

Isso permite testar sem comprometer dados reais.

---

> ░░░░░░░ Troca de Provider ░░░░░░░

O DataBeezze deve reduzir o impacto de uma eventual troca de tecnologia.

Antes:

```text
APPLICATION
     ↓
UserRepository
     ↓
Supabase
```

Depois:

```text
APPLICATION
     ↓
UserRepository
     ↓
PostgreSQL
```

Idealmente, a maior parte da aplicação permanece igual.

---

> ░░░░░░░ Não Abstrair por Medo ░░░░░░░

Isso não significa criar interfaces para tudo apenas porque um dia o banco
**talvez** mude.

A regra do Junglapp continua:

**NÃO CONSTRUIR PARA UM PROBLEMA QUE AINDA NÃO EXISTE.**

Criar abstração quando:

```text
reduz acoplamento importante

facilita testes

existem múltiplos provedores

o provider está vazando para muitas partes

a troca futura é uma necessidade real
```

---

> ░░░░░░░ Exemplo Universal ░░░░░░░

Uma estrutura conceitual simples:

```text
UI
 ↓
CONTROLLER
 ↓
DATA
 ↓
PROVIDER
```

Quando o projeto crescer:

```text
UI
 ↓
CONTROLLER
 ↓
REPOSITORY
 ↓
DATA SOURCE
 ↓
DATABASE / API / STORAGE
```

A segunda estrutura não precisa existir antes de ser necessária.

---

> ░░░░░░░ Exemplo Durante Construção ░░░░░░░

Arquivo único:

```text
profile_pag

├── BLOCO INTERFACE
├── BLOCO ESTADO
├── BLOCO LÓGICA
└── BLOCO DADOS
```

Depois da refatoração:

```text
profile/

├── profile_pag
├── profile_ctl
├── profile_mdl
└── profile_rep
```

Se ainda crescer:

```text
profile/

├── pages/
├── controllers/
├── models/
└── repositories/
```

A estrutura acompanha a necessidade real.

---

> ░░░░░░░ Configurações Centralizadas ░░░░░░░

Configurações relacionadas aos dados devem permanecer centralizadas.

Exemplos:

```text
cacheDuration

maxRetryAttempts

syncInterval

databaseProvider
```

Secrets não entram aqui.

Exemplos que devem seguir o padrão de segurança:

```text
databasePassword

privateKey

serviceRoleKey

secretToken
```

---

> ░░░░░░░ Regra do Mínimo ░░░░░░░

Não criar automaticamente:

```text
repository
DTO
mapper
cache
offline database
sync engine
service
data source
```

para toda funcionalidade.

Criar somente quando a responsabilidade existir.

O DataBeezze é um padrão de **controle de dados**.

Não uma obrigação de criar camadas.

---

> ░░░░░░░ Regra para IA ░░░░░░░

Ao trabalhar com dados em um projeto Junglapp, uma IA deve:

1. identificar onde o dado realmente pertence;
2. identificar a fonte de verdade;
3. evitar acesso ao provider espalhado pela aplicação;
4. não colocar lógica de banco diretamente na interface;
5. proteger credenciais e dados sensíveis;
6. utilizar queries seguras;
7. centralizar configurações ajustáveis;
8. criar abstrações apenas quando houver benefício real;
9. considerar migrations antes de alterar schema;
10. não assumir que offline-first é necessário;
11. não assumir que cache é fonte de verdade;
12. preparar BLOCOs de dados para futura extração.

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

A UI está chamando banco diretamente?

→ **CRIAR FRONTEIRA DE DADOS**

O provider aparece em vários lugares?

→ considerar **REPOSITORY**

Formato externo é diferente do interno?

→ considerar **DTO / MAPPER**

O app precisa funcionar sem internet?

→ considerar **OFFLINE-FIRST**

Só precisamos acelerar leituras?

→ considerar **CACHE**

O schema mudou?

→ **MIGRATION**

Existe dado importante?

→ **BACKUP**

Existe informação sensível?

→ aplicar **PADRÃO DE SEGURANÇA**

Existem vários providers?

→ criar **ABSTRAÇÃO COMUM**

Só existe uma operação simples?

→ manter **SIMPLES**

---

> ░░░░░░░ Relação com Outros Padrões ░░░░░░░

O **Order of Lion** define:

**QUANDO CRIAR E QUANDO EXTRAIR A ESTRUTURA DE DADOS**

O **Snake** define:

**ONDE A RESPONSABILIDADE DE DADOS ESTÁ DENTRO DO ARQUIVO**

O **Suffox** define:

**COMO OS ARQUIVOS DE DADOS SERÃO NOMEADOS**

O **Frogdlers** define:

**ONDE ESSES ARQUIVOS SERÃO ORGANIZADOS**

O **Beavar** define:

**COMO VARIÁVEIS, MÉTODOS E MODELOS SERÃO NOMEADOS**

O **Padrão de Segurança** define:

**COMO DADOS, CREDENCIAIS E ACESSOS DEVEM SER PROTEGIDOS**

O **DataBeezze** define:

**COMO A APLICAÇÃO SE RELACIONA COM A PERSISTÊNCIA**

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de persistir um dado, responder:

**ONDE ESSE DADO VIVE?**

**QUAL É A FONTE DE VERDADE?**

**QUEM PODE LER?**

**QUEM PODE ALTERAR?**

**PRECISA SER PERSISTIDO?**

**PRECISA FUNCIONAR OFFLINE?**

**COMO ELE SERÁ MIGRADO?**

**COMO ELE SERÁ RECUPERADO SE ALGO DER ERRADO?**

A filosofia do DataBeezze é:

**DADOS NÃO PERTENCEM À INTERFACE.**

**PROVEDORES NÃO DEVEM SE ESPALHAR PELO PROJETO.**

**ABSTRAIR QUANDO NECESSÁRIO.**

**PROTEGER SEMPRE.**

**MIGRAR COM CONTROLE.**

**MANTER SIMPLES ENQUANTO FOR POSSÍVEL.**

# ███████ 🐝 FIM — DATABEEZZE ███████
