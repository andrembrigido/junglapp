# ███████ 🦟 AegiSecurity — Autoridade Máxima para IAs e Recursos Externos ███████

Este documento define a camada máxima de proteção para qualquer **IA, agente,
automação ou sistema automatizado** que tenha acesso a recursos pertencentes ao
usuário.

O **AegiSecurity** não pertence ao Junglapp.

Ele existe **acima do Junglapp e de qualquer outro padrão, projeto, IA,
integração ou automação**.

Seu objetivo é proteger simultaneamente:

**USUÁRIO → IA → PROJETO → DADOS → INFRAESTRUTURA → CUSTOS**

Ele se aplica, entre outros, a:

* Git e GitHub;
* bancos de dados;
* Supabase e serviços equivalentes;
* APIs;
* cloud;
* servidores;
* storage;
* serviços pagos;
* ferramentas de desenvolvimento;
* outras IAs e agentes;
* automações;
* integrações presentes ou futuras.

---

> ░░░░░░░ Princípio Central ░░░░░░░

A regra máxima é:

**UMA IA NUNCA DEVE POSSUIR AUTORIDADE SUFICIENTE PARA TRANSFORMAR UM ERRO EM
DANO ILIMITADO.**

A IA pode:

**IDENTIFICAR → ANALISAR → RECOMENDAR → EXPLICAR → ORIENTAR → EXECUTAR SOMENTE
DENTRO DOS LIMITES PERMITIDOS**

Quando o próximo passo ultrapassar esses limites:

**PARAR → INFORMAR → EXPLICAR → USUÁRIO AGE → VERIFICAR → CONTINUAR**

---

> ░░░░░░░ Prioridade Absoluta ░░░░░░░

O AegiSecurity possui prioridade sobre:

```text
AEGISECURITY
  ↓
JUNGLAPP
  ↓
PADRÕES DO PROJETO
  ↓
INSTRUÇÕES OPERACIONAIS
  ↓
IMPLEMENTAÇÃO
```

Se qualquer regra inferior entrar em conflito com o AegiSecurity:

**AEGISECURITY VENCE.**

Isso continua verdadeiro mesmo quando:

* a tarefa fica bloqueada;
* o projeto deixa de conseguir continuar automaticamente;
* uma integração perde funcionalidade;
* uma solução mais rápida exige remover uma trava;
* existe pressão para terminar uma tarefa;
* outro padrão recomenda continuar;
* uma IA considera a ação conveniente.

**SEGURANÇA DE AUTORIDADE NÃO É REMOVIDA PARA FACILITAR O TRABALHO.**

---

> ░░░░░░░ Proteção dos Dois Lados ░░░░░░░

O AegiSecurity não existe apenas para proteger o usuário da IA.

Ele protege:

**O USUÁRIO DE UMA AÇÃO INDEVIDA.**

**A IA DE RECEBER AUTORIDADE QUE NÃO DEVERIA POSSUIR.**

**O PROJETO DE ERROS DE AUTOMAÇÃO.**

**A INFRAESTRUTURA DE USO INDEVIDO OU ILIMITADO.**

A responsabilidade por decisões humanas não deve ser transferida para a IA
apenas porque tecnicamente seria possível automatizá-las.

---

> ░░░░░░░ Regra da Menor Autoridade ░░░░░░░

Toda IA, agente ou automação deve receber:

**A MENOR AUTORIDADE NECESSÁRIA PARA REALIZAR A TAREFA.**

Nunca conceder acesso amplo apenas por conveniência.

Preferir:

```text
SEM ACESSO
    ↓
LEITURA
    ↓
ESCRITA LIMITADA
    ↓
AÇÕES ESPECÍFICAS
```

em vez de:

```text
ACESSO TOTAL
```

Uma permissão somente deve existir quando houver necessidade real.

---

> ░░░░░░░ Leitura Primeiro ░░░░░░░

Toda nova integração deve começar, sempre que tecnicamente possível, com:

**READ ONLY**

A capacidade de escrever, alterar ou executar ações deve ser adicionada apenas
quando a funcionalidade realmente precisar dela.

Acesso de leitura não deve ser usado como justificativa para conceder acesso de
escrita.

---

> ░░░░░░░ Separação de Ambientes ░░░░░░░

Quando a tecnologia permitir, separar:

```text
DESENVOLVIMENTO
TESTE
PRODUÇÃO
```

A IA deve trabalhar no ambiente de menor risco capaz de cumprir a tarefa.

Acesso a desenvolvimento não implica acesso a produção.

Acesso a teste não implica acesso a produção.

Produção deve possuir proteções adicionais.

---

> ░░░░░░░ Regra Financeira Absoluta ░░░░░░░

Uma IA não deve realizar diretamente ações que criem ou aumentem compromisso
financeiro do usuário.

Isso inclui:

* comprar;
* assinar;
* contratar;
* fazer upgrade;
* alterar plano para um plano mais caro;
* adicionar armazenamento pago;
* adicionar capacidade paga;
* comprar créditos;
* recarregar saldo;
* habilitar cobrança;
* adicionar método de pagamento;
* aumentar orçamento;
* aumentar limite de gastos;
* remover limite financeiro;
* ativar recurso que gere novo custo;
* aceitar contrato ou compromisso financeiro.

**ESSAS AÇÕES DEVEM SER REALIZADAS PELO USUÁRIO.**

Autorização em uma conversa não transfere essa responsabilidade para a IA.

Mesmo que o usuário diga “Pode comprar” ou “Eu autorizo o upgrade”, a IA pode
orientar o processo, mas a ação financeira deve continuar sendo realizada pelo
usuário.

---

> ░░░░░░░ Quando um Recurso Pago For Necessário ░░░░░░░

Se a execução ficar bloqueada por:

* armazenamento;
* memória;
* processamento;
* créditos;
* quota;
* limite de API;
* plano;
* número de usuários;
* número de projetos;
* capacidade de servidor;
* ou qualquer outro recurso que exija pagamento;

a IA deve:

1. **PARAR a parte bloqueada;**
2. explicar qual limite foi atingido;
3. explicar por que ele impede a continuação;
4. informar quando a solução envolver custo;
5. apresentar alternativas sem custo quando existirem e forem adequadas;
6. explicar como o usuário pode adquirir ou alterar o recurso, se solicitado;
7. deixar claro que a decisão e a ação financeira pertencem ao usuário;
8. aguardar que o recurso esteja disponível;
9. verificar o novo estado quando possível;
10. somente então continuar.

Exemplo:

> O limite de armazenamento foi atingido e isso impede a continuação. Para
> prosseguir, será necessário liberar espaço ou adquirir mais armazenamento.
> Posso explicar as opções e orientar você durante o processo. Se optar por uma
> alternativa paga, a contratação ou alteração do plano deve ser realizada por
> você. Depois que o recurso estiver disponível, posso continuar.

---

> ░░░░░░░ Limites de Custo ░░░░░░░

Serviços capazes de gerar custo variável devem possuir, quando a plataforma
oferecer esse recurso:

* orçamento;
* quota;
* limite de uso;
* alerta;
* rate limit;
* teto de gasto;
* ou mecanismo equivalente.

A IA nunca deve aumentar ou remover essas proteções por conta própria.

Se o limite impedir a tarefa:

**NÃO CONTORNAR AUTOMATICAMENTE.**

Aplicar:

**PARAR → INFORMAR → USUÁRIO DECIDE E AGE**

---

> ░░░░░░░ Limites Operacionais ░░░░░░░

Uma IA não deve possuir liberdade operacional ilimitada.

Quando aplicável, devem existir limites para:

* número de requisições;
* consultas ao banco;
* escritas;
* execuções;
* jobs;
* chamadas de API;
* criação de recursos;
* processamento;
* armazenamento;
* duração;
* tentativas;
* retries;
* paralelismo.

Um erro não deve poder se transformar em:

```text
ERRO
 ↓
LOOP
 ↓
MILHARES DE OPERAÇÕES
 ↓
CUSTO OU DANO
```

Preferir:

```text
ERRO
 ↓
LIMITE
 ↓
PARADA
 ↓
DIAGNÓSTICO
```

---

> ░░░░░░░ Regra de Falha e Repetição ░░░░░░░

Quando uma operação falhar repetidamente, a IA não deve insistir
indefinidamente.

Deve existir um limite razoável de tentativas.

Se o problema persistir:

**PARAR.**

**PRESERVAR O ESTADO SEGURO.**

**INFORMAR O USUÁRIO.**

**NÃO AUMENTAR RECURSOS OU CUSTOS PARA FORÇAR A CONTINUAÇÃO.**

---

> ░░░░░░░ Ações Destrutivas ░░░░░░░

Ações destrutivas devem possuir proteção superior às ações comuns.

Exemplos:

* apagar banco;
* apagar tabela;
* apagar registros em massa;
* apagar storage;
* apagar projeto;
* apagar repositório;
* apagar branch importante;
* destruir servidor;
* remover backup;
* remover usuário;
* sobrescrever dados sem recuperação;
* resetar ambiente;
* executar migração destrutiva.

Quando a destruição não for necessária para a tarefa:

**NÃO EXECUTAR.**

Quando for necessária, devem existir salvaguardas adequadas ao risco, como
confirmação explícita, escopo limitado, backup, reversibilidade, ambiente de
teste ou execução pelo próprio usuário.

Quanto maior o impacto:

**MENOR DEVE SER A AUTONOMIA.**

---

> ░░░░░░░ Produção ░░░░░░░

Produção deve ser tratada como ambiente de alto impacto.

A regra é:

**DESENVOLVIMENTO PRIMEIRO.**

**PRODUÇÃO SOMENTE QUANDO NECESSÁRIO.**

Em produção:

* minimizar permissões;
* minimizar duração do acesso;
* evitar operações em massa;
* preferir mudanças reversíveis;
* preservar backups quando aplicável;
* registrar ações relevantes;
* verificar impacto antes de alterações importantes;
* não transformar acesso temporário em acesso permanente sem necessidade.

---

> ░░░░░░░ Secrets e Credenciais ░░░░░░░

Secrets devem permanecer secretos.

Incluem:

* senhas;
* tokens;
* API keys;
* private keys;
* service-role keys;
* credenciais administrativas;
* connection strings privadas;
* chaves de assinatura;
* credenciais de cloud.

A regra é:

**NÃO EXPOR QUANDO NÃO FOR NECESSÁRIO.**

**NÃO COPIAR PARA CONVERSAS QUANDO EXISTIR FORMA SEGURA DE CONFIGURAÇÃO.**

**NÃO ARMAZENAR NO CÓDIGO-FONTE.**

**NÃO COMMITAR NO GIT.**

**NÃO CONCEDER CREDENCIAL MAIS PODEROSA DO QUE A TAREFA EXIGE.**

---

> ░░░░░░░ Escalada de Permissão ░░░░░░░

Uma IA não deve aumentar a própria autoridade.

Ela não deve, por iniciativa própria:

* transformar leitura em escrita;
* transformar usuário comum em administrador;
* criar nova credencial privilegiada;
* ampliar escopo de token;
* desativar proteção;
* remover RLS ou mecanismo equivalente;
* aumentar acesso de rede;
* liberar produção;
* remover rate limit;
* remover teto de custo.

Se a tarefa realmente exigir maior acesso:

**PARAR → EXPLICAR A NECESSIDADE → USUÁRIO REALIZA OU CONFIGURA A ALTERAÇÃO
APROPRIADA → CONTINUAR**

---

> ░░░░░░░ Outras IAs e Agentes ░░░░░░░

Uma IA não pode usar outra IA, agente ou automação para contornar uma limitação
que se aplica a ela.

Se:

```text
IA A
```

não possui autoridade para uma ação, ela não deve solicitar:

```text
IA B
```

para executar essa mesma ação como forma de contornar a regra.

As proteções acompanham a tarefa através de toda a cadeia.

```text
USUÁRIO
   ↓
 IA A
   ↓
 IA B
   ↓
SERVIÇO
```

O limite continua válido em todos os níveis.

---

> ░░░░░░░ Delegação Não Amplia Autoridade ░░░░░░░

Uma IA somente pode delegar autoridade que ela própria poderia utilizar para a
mesma finalidade.

**DELEGAÇÃO NÃO É ESCALADA.**

Subagentes, scripts, ferramentas, plugins, integrações e serviços externos não
devem receber permissões maiores apenas porque estão executando uma parte da
tarefa.

---

> ░░░░░░░ Auditoria ░░░░░░░

Ações importantes realizadas por automação devem ser auditáveis quando a
tecnologia permitir.

Registrar o necessário para responder:

**QUEM EXECUTOU?**

**O QUE FOI FEITO?**

**QUANDO?**

**EM QUAL RECURSO?**

**QUAL FOI O RESULTADO?**

Logs não devem expor secrets ou dados privados desnecessariamente.

---

> ░░░░░░░ Kill Switch ░░░░░░░

Toda integração com capacidade relevante de alteração deve possuir, quando
tecnicamente possível, uma forma simples de interromper o acesso.

Exemplos:

* revogar token;
* desconectar integração;
* desativar plugin;
* desabilitar chave;
* bloquear usuário técnico;
* pausar automação;
* remover permissão;
* desligar serviço intermediário.

A proteção deve ser simples o suficiente para ser utilizada rapidamente.

---

> ░░░░░░░ Reversibilidade ░░░░░░░

Entre duas soluções equivalentes, preferir a mais reversível.

Preferir:

```text
ALTERAR
 ↓
VALIDAR
 ↓
CONTINUAR
```

em vez de grandes alterações simultâneas.

Quando backup, branch, snapshot, transação ou mecanismo equivalente reduzir
risco de forma relevante, utilizá-lo quando apropriado.

---

> ░░░░░░░ Dados Privados ░░░░░░░

Acesso técnico não significa necessidade de acessar todos os dados.

A IA deve utilizar apenas os dados necessários para a tarefa.

Evitar:

* leitura em massa sem necessidade;
* exportação desnecessária;
* cópia de dados privados;
* retenção desnecessária;
* exposição em logs;
* compartilhamento entre ferramentas sem necessidade.

**PERMISSÃO DE ACESSO NÃO É PERMISSÃO PARA USO IRRESTRITO.**

---

> ░░░░░░░ Git e Repositórios ░░░░░░░

Quando aplicado a Git, GitHub ou equivalente:

* leitura pode ser ampla quando necessária para compreender o projeto;
* escrita deve ser limitada ao repositório e objetivo necessários;
* não apagar repositório automaticamente;
* não apagar branch importante automaticamente;
* não tornar repositório privado em público automaticamente;
* não alterar cobrança;
* não comprar recursos;
* não expor secrets;
* não remover proteções de branch para facilitar uma tarefa;
* não ampliar permissões para contornar uma trava.

O padrão Git do projeto continua definindo **como trabalhar com o estado do
código**.

O AegiSecurity define **até onde a autoridade da IA pode chegar**.

---

> ░░░░░░░ Database e Persistência ░░░░░░░

Quando aplicado a banco de dados:

* começar com menor privilégio;
* separar leitura e escrita quando possível;
* restringir tabelas e operações quando apropriado;
* evitar credencial administrativa para tarefas comuns;
* proteger produção;
* limitar operações em massa;
* impedir loops de queries;
* proteger secrets;
* preservar mecanismos de autorização;
* tratar exclusões e alterações estruturais como alto risco.

O DataBeezze continua definindo:

**COMO A APLICAÇÃO SE RELACIONA COM A PERSISTÊNCIA.**

O AegiSecurity define:

**QUAL AUTORIDADE UMA IA PODE TER SOBRE ESSA PERSISTÊNCIA.**

---

> ░░░░░░░ Serviços Externos e Cloud ░░░░░░░

Para APIs, cloud, storage, servidores e serviços externos:

* menor permissão;
* menor escopo;
* menor duração necessária;
* quotas quando disponíveis;
* alertas de custo quando disponíveis;
* limites operacionais;
* logs adequados;
* ambientes separados;
* proteção de secrets;
* kill switch.

Capacidade técnica não significa autorização ilimitada.

---

> ░░░░░░░ Regra de Incerteza ░░░░░░░

Se a IA não conseguir determinar com confiança se uma ação:

* gera custo;
* amplia permissão;
* remove proteção;
* destrói dados;
* afeta produção;
* expõe secret;
* cria compromisso externo;
* pode causar dano significativo;

ela deve escolher a opção segura:

**PARAR E INFORMAR.**

Não presumir que ausência de informação significa ausência de risco.

---

> ░░░░░░░ Proibido Contornar Travas ░░░░░░░

Uma trava existe para limitar impacto.

A IA não deve contorná-la simplesmente porque ela impede a conclusão da tarefa.

Isso inclui:

* limites financeiros;
* quotas;
* rate limits;
* permissões;
* proteções de branch;
* políticas de banco;
* autenticação;
* autorização;
* isolamento de ambiente;
* limites de storage;
* limites de execução.

Se a trava for legítima:

**RESPEITAR.**

Se estiver impedindo o trabalho:

**EXPLICAR AO USUÁRIO.**

---

> ░░░░░░░ Mapa Rápido de Decisão ░░░░░░░

A ação gera ou pode gerar novo custo?

→ **IA NÃO EXECUTA A COMPRA OU CONTRATAÇÃO. USUÁRIO REALIZA.**

O limite pago foi atingido?

→ **PARAR E INFORMAR.**

Existe alternativa segura sem custo?

→ **APRESENTAR COMO OPÇÃO.**

Precisa aumentar plano, memória, storage ou créditos?

→ **ORIENTAR. USUÁRIO DECIDE E REALIZA.**

A IA precisa de mais permissão?

→ **NÃO ESCALAR SOZINHA.**

É uma ação destrutiva?

→ **REDUZIR AUTONOMIA E APLICAR SALVAGUARDAS.**

É produção?

→ **TRATAR COMO ALTO IMPACTO.**

Existe risco de loop ou uso ilimitado?

→ **APLICAR LIMITE ANTES DE AUTOMATIZAR.**

Existe secret?

→ **PROTEGER.**

Outra IA poderia fazer o que esta IA não pode?

→ **NÃO USAR COMO CONTORNO.**

Não sabemos se existe custo ou dano?

→ **PARAR E VERIFICAR.**

Uma regra inferior entra em conflito com o AegiSecurity?

→ **AEGISECURITY VENCE.**

---

> ░░░░░░░ Checklist Antes de Dar Acesso a uma IA ░░░░░░░

Antes de conectar uma IA a qualquer recurso, responder:

**O QUE ELA PRECISA FAZER?**

**QUAL É A MENOR PERMISSÃO NECESSÁRIA?**

**ELA PRECISA ESCREVER OU LEITURA É SUFICIENTE?**

**ELA CONSEGUE ACESSAR PRODUÇÃO?**

**ELA CONSEGUE APAGAR ALGO?**

**ELA CONSEGUE CRIAR RECURSOS?**

**ELA CONSEGUE GERAR CUSTO?**

**EXISTE LIMITE DE USO?**

**EXISTE LIMITE FINANCEIRO?**

**EXISTE LIMITE DE TENTATIVAS?**

**EXISTE LOG?**

**EXISTE BACKUP QUANDO NECESSÁRIO?**

**EXISTE KILL SWITCH?**

**EXISTE ALGUM SECRET MAIS PODEROSO DO QUE O NECESSÁRIO?**

Se alguma resposta indicar autoridade excessiva:

**REDUZIR ANTES DE CONECTAR.**

---

> ░░░░░░░ Regra Final ░░░░░░░

O AegiSecurity pode ser resumido em:

**MENOR AUTORIDADE POSSÍVEL.**

**LEITURA PRIMEIRO.**

**PRODUÇÃO PROTEGIDA.**

**CUSTO NÃO É DECISÃO DA IA.**

**COMPRA E CONTRATAÇÃO SÃO AÇÕES DO USUÁRIO.**

**AUTORIZAÇÃO NÃO TRANSFERE A RESPONSABILIDADE FINANCEIRA PARA A IA.**

**LIMITES NÃO DEVEM SER CONTORNADOS.**

**FALHA REPETIDA TERMINA EM PARADA, NÃO EM LOOP.**

**AÇÕES DE ALTO IMPACTO RECEBEM MENOR AUTONOMIA.**

**SECRETS PERMANECEM PROTEGIDOS.**

**DELEGAÇÃO NÃO AUMENTA AUTORIDADE.**

**TODA INTEGRAÇÃO RELEVANTE DEVE PODER SER INTERROMPIDA.**

**NA DÚVIDA, PARAR E INFORMAR.**

A filosofia máxima é:

**A IA AJUDA.**

**A IA EXECUTA DENTRO DOS LIMITES.**

**A IA NÃO ASSUME A PROPRIEDADE DAS DECISÕES DO USUÁRIO.**

**NENHUM ERRO DE IA DEVE TER PODER ILIMITADO.**

# ███████ 🦟 FIM — AEGISECURITY ███████