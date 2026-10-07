# ███████ 🔐 Padrão de Segurança ███████

Este documento define as regras universais de segurança do **Junglapp 2.0**.

O objetivo é garantir que segurança seja considerada **antes, durante e depois**
da construção de qualquer projeto.

Este padrão se aplica a:

* apps;
* sites;
* APIs;
* backends;
* bancos de dados;
* desktop;
* mobile;
* serviços locais;
* serviços em nuvem.

A regra principal é simples:

**Segurança não é uma etapa final.**

**Segurança faz parte da funcionalidade.**

---

> ░░░░░░░ Princípio Central ░░░░░░░

No Junglapp normalmente seguimos:

**FAZER FUNCIONAR → COMPLETAR → REFATORAR**

Para segurança, existe uma exceção:

**PROTEÇÕES IMPORTANTES NÃO ESPERAM A REFATORAÇÃO.**

Pode esperar:

* separação de arquivos;
* arquitetura final;
* otimização;
* organização definitiva.

Não pode esperar:

* autenticação necessária;
* autorização;
* proteção de senhas;
* controle de acesso;
* proteção de secrets;
* proteção de dados;
* validações de segurança.

---

> ░░░░░░░ Segurança por Padrão ░░░░░░░

Quando houver mais de uma opção válida, utilizar a opção segura como padrão.

A filosofia é:

**FECHADO POR PADRÃO → LIBERAR SOMENTE O NECESSÁRIO**

Não:

**LIBERAR TUDO → TENTAR BLOQUEAR DEPOIS**

Exemplo:

```text id="5x4zct"
Permissão desconhecida
        ↓
      NEGAR
```

Nunca:

```text id="3u5xwu"
Permissão desconhecida
        ↓
     PERMITIR
```

---

> ░░░░░░░ Pergunta de Segurança ░░░░░░░

Antes de construir qualquer funcionalidade importante, perguntar:

> **O que acontece se alguém tentar usar isso de forma indevida?**

Também verificar:

* quem pode usar;
* quem não pode usar;
* quais dados são acessados;
* onde os dados ficam;
* para onde os dados vão;
* quem pode modificar;
* o que acontece em caso de falha.

---

> ░░░░░░░ Nunca Confiar no Cliente ░░░░░░░

Tudo que roda no dispositivo do usuário deve ser considerado modificável.

Isso inclui:

* frontend;
* navegador;
* JavaScript;
* aplicativo mobile;
* aplicativo desktop;
* parâmetros;
* IDs;
* valores locais;
* requisições;
* validações visuais.

Esconder um botão **não é autorização**.

Esconder uma tela **não é autorização**.

Usar uma URL difícil de descobrir **não é segurança**.

Operações importantes devem ser verificadas pelo lado confiável do sistema.

Normalmente:

**CLIENTE → BACKEND → VERIFICAÇÃO → AÇÃO**

---

> ░░░░░░░ Autenticação ░░░░░░░

Autenticação responde:

> **Quem é você?**

Sempre considerar:

* armazenamento seguro de senhas;
* recuperação segura de conta;
* expiração de sessões;
* revogação de sessões;
* proteção contra tentativas repetidas;
* MFA quando necessário.

Nunca:

* armazenar senha em texto puro;
* colocar senha em logs;
* enviar senha por conexão insegura;
* criar algoritmo próprio de proteção de senha.

---

> ░░░░░░░ Autorização ░░░░░░░

Autorização responde:

> **O que você pode fazer?**

Estar autenticado não significa possuir acesso a tudo.

Fluxo esperado:

```text id="4b6s3n"
USUÁRIO
   ↓
SOLICITA RECURSO
   ↓
BACKEND IDENTIFICA O USUÁRIO
   ↓
BACKEND VERIFICA A PERMISSÃO
   ↓
PERMITIR OU NEGAR
```

Cada operação sensível deve verificar autorização.

---

> ░░░░░░░ Menor Privilégio ░░░░░░░

Cada parte do sistema deve possuir apenas as permissões necessárias.

Isso vale para:

* usuários;
* administradores;
* APIs;
* serviços;
* banco de dados;
* CI/CD;
* automações;
* serviços em nuvem.

A regra é:

**Se não precisa da permissão, não conceda.**

---

> ░░░░░░░ Secrets ░░░░░░░

São exemplos de secrets:

* senhas;
* API keys;
* tokens;
* private keys;
* credenciais;
* chaves de assinatura.

Secrets nunca devem ficar diretamente no código.

Não colocar em:

* código-fonte;
* Git;
* comentários;
* logs;
* mensagens de erro;
* exemplos públicos.

Utilizar mecanismos adequados como:

* variáveis de ambiente;
* secret managers;
* armazenamento seguro da plataforma.

---

> ░░░░░░░ Configuração Não é Secret ░░░░░░░

O Junglapp utiliza **Configurações Centralizadas**.

Porém:

```dart id="9xrsuz"
/* ************************ CONFIGURAÇÕES ************************************ */

const loginTimeout = 30;
const maxLoginAttempts = 5;
```

é correto.

Mas isto não:

```dart id="pfqq5f"
/* ************************ CONFIGURAÇÕES ************************************ */

const apiKey = 'minha-chave-secreta';
const password = 'minha-senha';
```

Secrets seguem este padrão de segurança e não devem ser tratados como simples
configurações.

---

> ░░░░░░░ Dados Sensíveis ░░░░░░░

Utilizar o princípio:

**COLETAR MENOS → ARMAZENAR MENOS → EXPOR MENOS**

Antes de coletar um dado, perguntar:

> **Precisamos realmente desse dado?**

Se não precisamos:

**não coletar.**

Quando necessário, definir:

* onde fica armazenado;
* quem pode acessar;
* por quanto tempo fica armazenado;
* como será removido;
* como será protegido.

---

> ░░░░░░░ Armazenamento ░░░░░░░

Dados sensíveis devem utilizar armazenamento adequado.

Verificar também:

* cache;
* arquivos temporários;
* backups;
* clipboard;
* logs;
* armazenamento compartilhado.

Em mobile, utilizar quando apropriado:

* Keychain;
* Keystore;
* mecanismo seguro equivalente.

---

> ░░░░░░░ Criptografia ░░░░░░░

Nunca inventar criptografia própria.

Utilizar:

* algoritmos consolidados;
* bibliotecas confiáveis;
* implementações mantidas;
* configurações modernas.

Regra:

**NÃO INVENTAR CRIPTOGRAFIA.**

---

> ░░░░░░░ Comunicação ░░░░░░░

Dados transmitidos pela rede devem utilizar comunicação segura.

Utilizar:

* HTTPS;
* TLS;
* mecanismo seguro equivalente.

Informações sensíveis não devem viajar em texto puro por redes não confiáveis.

---

> ░░░░░░░ Entradas Externas ░░░░░░░

Toda entrada externa deve ser considerada **não confiável**.

Exemplos:

* formulário;
* URL;
* parâmetro;
* arquivo;
* imagem;
* API;
* webhook;
* QR code;
* resposta de serviço externo.

Quando necessário, validar:

* tipo;
* tamanho;
* formato;
* intervalo;
* conteúdo;
* origem;
* permissão.

---

> ░░░░░░░ Injection ░░░░░░░

Nunca construir comandos sensíveis concatenando diretamente entrada externa.

Isso se aplica a:

* SQL;
* NoSQL;
* shell;
* comandos do sistema;
* templates;
* interpretadores.

Evitar:

```text id="qyv49v"
COMANDO + TEXTO DO USUÁRIO
```

Preferir:

```text id="grub58"
COMANDO PARAMETRIZADO
        +
VALOR SEPARADO
```

---

> ░░░░░░░ Saída Segura ░░░░░░░

Dados recebidos também precisam ser tratados antes de serem exibidos.

Isso é especialmente importante em:

* HTML;
* JavaScript;
* URLs;
* templates;
* conteúdo dinâmico.

Utilizar escaping ou encoding adequado ao contexto.

---

> ░░░░░░░ APIs ░░░░░░░

Toda API deve considerar:

* autenticação;
* autorização;
* validação;
* limites;
* tratamento de erros;
* monitoramento;
* abuso.

Nunca retornar mais dados do que o necessário.

Receber:

```text id="zltx3b"
userId = 15
```

não significa:

```text id="l31v7v"
USUÁRIO ATUAL PODE ACESSAR O USUÁRIO 15
```

O backend deve verificar a permissão.

---

> ░░░░░░░ Rate Limiting e Abuso ░░░░░░░

Operações que podem ser abusadas devem possuir limites quando necessário.

Exemplos:

* login;
* recuperação de senha;
* códigos de verificação;
* criação de contas;
* envio de mensagens;
* uploads;
* buscas caras;
* APIs públicas.

O objetivo é reduzir:

* força bruta;
* spam;
* automação abusiva;
* enumeração;
* consumo excessivo.

---

> ░░░░░░░ Uploads ░░░░░░░

Nunca confiar somente no nome ou extensão de um arquivo.

Quando necessário, verificar:

* tipo;
* MIME;
* tamanho;
* formato;
* conteúdo;
* destino.

Arquivos enviados não devem poder executar código inesperadamente.

---

> ░░░░░░░ Erros ░░░░░░░

Mensagens mostradas ao usuário não devem revelar detalhes internos.

Não expor:

* stack trace;
* caminhos internos;
* queries;
* secrets;
* credenciais;
* configurações privadas;
* detalhes de infraestrutura.

Separar:

**MENSAGEM PARA O USUÁRIO**

de:

**INFORMAÇÃO TÉCNICA PARA DIAGNÓSTICO**

---

> ░░░░░░░ Logs ░░░░░░░

Registrar eventos importantes para diagnóstico e segurança.

Exemplos:

* falhas relevantes;
* ações administrativas;
* mudanças sensíveis;
* erros críticos;
* comportamento suspeito.

Não registrar desnecessariamente:

* senha;
* token;
* secret;
* dado pessoal sensível.

---

> ░░░░░░░ Dependências ░░░░░░░

Toda dependência aumenta a superfície do projeto.

Antes de adicionar uma biblioteca, perguntar:

* realmente precisamos?
* existe alternativa nativa?
* possui manutenção?
* possui origem confiável?
* está atualizada?
* possui vulnerabilidades conhecidas?

Regra Junglapp:

**MENOS DEPENDÊNCIAS, QUANDO POSSÍVEL.**

Não porque dependência seja ruim, mas porque toda dependência precisa ser
mantida e monitorada.

---

> ░░░░░░░ Supply Chain ░░░░░░░

A segurança inclui também:

* bibliotecas;
* plugins;
* SDKs;
* ferramentas;
* extensões;
* containers;
* pipelines;
* sistemas de build;
* serviços externos.

A origem e as versões utilizadas devem ser rastreáveis.

---

> ░░░░░░░ Git ░░░░░░░

Antes dos primeiros commits:

* configurar arquivos ignorados;
* excluir secrets;
* excluir arquivos privados;
* revisar configurações locais.

Nunca assumir que apagar um secret em um commit posterior remove esse secret
do histórico.

---

> ░░░░░░░ Ambientes ░░░░░░░

Separar quando necessário:

**DESENVOLVIMENTO → TESTE → PRODUÇÃO**

Os ambientes podem possuir:

* credenciais diferentes;
* bancos diferentes;
* configurações diferentes;
* permissões diferentes.

Produção não deve manter ferramentas inseguras somente por conveniência.

Exemplos:

* debug aberto;
* credenciais de teste;
* endpoints temporários;
* contas padrão.

---

> ░░░░░░░ Configuração Segura ░░░░░░░

Evitar:

* permissões amplas;
* serviços desnecessários;
* portas desnecessárias;
* contas padrão;
* configurações temporárias esquecidas.

A configuração padrão deve favorecer segurança.

---

> ░░░░░░░ Web ░░░░░░░

Em projetos web, avaliar conforme a arquitetura:

* HTTPS;
* cookies seguros;
* CSP;
* HSTS;
* CORS;
* CSRF;
* XSS;
* headers de segurança.

Não aplicar mecanismos aleatoriamente.

Aplicar:

**PROTEÇÃO CORRETA → RISCO CORRETO**

---

> ░░░░░░░ Mobile ░░░░░░░

Aplicações mobile devem assumir que o dispositivo pode ser inspecionado.

Considerar:

* armazenamento seguro;
* comunicação segura;
* permissões;
* deep links;
* backups;
* logs;
* componentes expostos;
* reverse engineering;
* adulteração.

Não colocar secrets permanentes dentro do aplicativo esperando que ninguém os
encontre.

---

> ░░░░░░░ Banco de Dados ░░░░░░░

O banco deve utilizar somente as permissões necessárias.

Considerar:

* queries parametrizadas;
* controle de acesso;
* proteção das credenciais;
* backups;
* isolamento de rede;
* criptografia quando necessária.

A aplicação não deve utilizar uma conta administrativa sem necessidade.

---

> ░░░░░░░ Backups ░░░░░░░

Backup deve ser:

**CRIADO → PROTEGIDO → TESTADO**

Não basta possuir um backup.

É necessário confirmar que ele pode ser restaurado.

---

> ░░░░░░░ Privacidade ░░░░░░░

Privacidade faz parte da segurança.

O projeto deve saber:

* quais dados coleta;
* por que coleta;
* onde armazena;
* quem acessa;
* por quanto tempo mantém;
* como remove.

Leis e obrigações aplicáveis também devem ser consideradas.

---

> ░░░░░░░ CI/CD e Deploy ░░░░░░░

Pipelines também fazem parte da superfície de segurança.

Proteger:

* secrets;
* permissões;
* ambientes;
* artefatos;
* deploy;
* contas de automação.

Aplicar também o menor privilégio.

---

> ░░░░░░░ Testes de Segurança ░░░░░░░

Uma funcionalidade não está correta apenas porque o caminho normal funciona.

Dependendo do projeto, testar:

* autenticação;
* autorização;
* entradas inválidas;
* permissões;
* erros;
* dependências;
* configurações;
* integrações.

Quando adequado, utilizar:

* análise estática;
* análise dinâmica;
* verificação de dependências;
* testes automatizados.

---

> ░░░░░░░ Falhar de Forma Segura ░░░░░░░

Quando o sistema não conseguir confirmar uma condição de segurança:

**PREFERIR O ESTADO SEGURO**

Exemplo:

```text id="sgv16l"
CONSEGUIMOS CONFIRMAR A PERMISSÃO?
              │
        ┌─────┴─────┐
       SIM          NÃO
        │            │
   CONTINUAR       NEGAR
```

---

> ░░░░░░░ Atualizações ░░░░░░░

O projeto deve permitir correções futuras.

Manter, conforme necessário:

* runtime;
* framework;
* dependências;
* infraestrutura;
* ferramentas.

Evitar tecnologias abandonadas quando existir alternativa adequada.

---

> ░░░░░░░ Incidentes ░░░░░░░

Quando aplicável, o sistema deve permitir:

* revogar sessões;
* revogar tokens;
* trocar secrets;
* bloquear contas;
* corrigir dependências;
* desabilitar funcionalidades;
* restaurar backups;
* investigar eventos.

---

> ░░░░░░░ Segurança e Simplicidade ░░░░░░░

Segurança não deve ser desculpa para criar arquitetura gigantesca.

A regra é:

**PROTEÇÃO NECESSÁRIA + MENOR COMPLEXIDADE POSSÍVEL**

Toda proteção deve corresponder a um risco real.

Não criar segurança teatral.

---

> ░░░░░░░ Autonomia da IA ░░░░░░░

Uma IA trabalhando com Junglapp deve aplicar automaticamente boas práticas
básicas de segurança.

Ela pode decidir sozinha:

* validar entrada;
* parametrizar query;
* não expor secret;
* reduzir permissão desnecessária;
* proteger armazenamento;
* evitar exposição de dados;
* tratar erros com segurança;
* utilizar opção segura quando duas soluções forem equivalentes.

---

> ░░░░░░░ Quando a IA Deve Parar ░░░░░░░

A IA deve alertar quando uma decisão exigir:

* remover proteção necessária;
* expor secret;
* armazenar senha sem proteção;
* desativar autenticação necessária;
* ampliar permissões sem motivo;
* expor dados privados;
* ignorar vulnerabilidade importante.

---

> ░░░░░░░ Regra de Desempate ░░░░░░░

Quando duas soluções funcionarem:

**ESCOLHER A SEGURA.**

Se as duas forem igualmente seguras:

**ESCOLHER A MAIS SIMPLES.**

---

> ░░░░░░░ Checkpoint Antes de Construir ░░░░░░░

Antes de implementar uma funcionalidade, verificar:

| Pergunta                 | Se SIM                            |
| ------------------------ | --------------------------------- |
| Possui usuário?          | Verificar identidade e permissões |
| Possui dados sensíveis?  | Proteger armazenamento e acesso   |
| Recebe entrada externa?  | Validar                           |
| Envia dados pela rede?   | Proteger comunicação              |
| Utiliza secret?          | Armazenar corretamente            |
| Acessa banco?            | Limitar acesso e parametrizar     |
| Usa dependência externa? | Verificar origem e manutenção     |
| Permite upload?          | Validar arquivo                   |
| Pode sofrer abuso?       | Avaliar limites                   |
| Precisa de log?          | Registrar sem expor dados         |

---

> ░░░░░░░ Checkpoint Antes de Produção ░░░░░░░

Antes de liberar para produção, revisar:

* autenticação;
* autorização;
* secrets;
* permissões;
* dados;
* rede;
* banco;
* dependências;
* configurações;
* logs;
* erros;
* backups;
* privacidade;
* atualizações;
* testes.

---

> ░░░░░░░ Relação com o Junglapp ░░░░░░░

O **Order of Lion** define:

**QUANDO FAZER**

O **Snake** define:

**COMO ORGANIZAR**

Este padrão define:

**COMO NÃO COMPROMETER A SEGURANÇA**

A prioridade é:

```text id="4xknv9"
SEGURANÇA OBRIGATÓRIA
        ↓
FUNCIONALIDADE
        ↓
SIMPLICIDADE
        ↓
ORGANIZAÇÃO
        ↓
REFATORAÇÃO
```

---

> ░░░░░░░ Regra Final ░░░░░░░

Antes de considerar uma funcionalidade pronta, perguntar:

**Quem pode usar?**

**Quem não pode usar?**

**Quais dados ela acessa?**

**Em quem ela confia?**

**O que acontece com uma entrada maliciosa?**

**O que acontece quando algo falha?**

**Estamos expondo algo que não precisamos?**

A filosofia final é:

**NÃO CONFIE POR PADRÃO.**

**NÃO EXPONHA POR PADRÃO.**

**NÃO CONCEDA POR PADRÃO.**

**VALIDE.**

**RESTRINJA.**

**PROTEJA.**

**TESTE.**

**ATUALIZE.**

# ███████ 🔐 FIM — PADRÃO DE SEGURANÇA ███████
