# Junglapp Secure Auth Standard — v1.0

**Status:** padrão de referência aprovado; implementação e auditoria pendentes.  
**Escopo:** autenticação Google e Apple com Supabase Auth; proteção de sessões, dados pessoais e integrações opcionais de pagamento.  
**Princípios:** secure by default, privacy by design, least privilege, defense in depth, fail secure, simplicidade verificável.

## Classificação
- **CORE:** exigido em todas as implementações aplicáveis.
- **CONDITIONAL:** exigido quando a plataforma, funcionalidade ou legislação se aplicar.
- **ADVANCED:** adotado conforme análise de risco.

## Checklist verificável

| ID | Nível | Controle | Critério de aceitação |
|---|---|---|---|
| AUTH-01 | CORE | Google/Apple via Supabase Auth | Login e cancelamento testados em cada provedor habilitado. |
| AUTH-02 | CORE | OAuth 2.0 / OIDC | Fluxo suportado pelos SDKs oficiais, com validação do provedor. |
| AUTH-03 | CORE | PKCE, state, nonce | Aplicados conforme o fluxo; redirecionamentos e tokens inválidos rejeitados. |
| AUTH-04 | CORE | Redirect URI allowlist | Somente URIs autorizadas funcionam. |
| AUTH-05 | CORE | Identidade estável | Usuário interno vinculado ao identificador do provedor; não confiar apenas no e-mail. |
| AUTH-06 | CONDITIONAL | Vinculação de contas | Exige prova de controle de ambas as identidades. |
| SESS-01 | CORE | Armazenamento seguro | Tokens protegidos segundo plataforma; nenhum token em logs. |
| SESS-02 | CORE | Renovação/expiração | Token expirado é renovado legitimamente ou exige novo login. |
| SESS-03 | CORE | Logout e revogação | Logout limpa credenciais locais; revogação remota testada conforme suporte. |
| SESS-04 | CONDITIONAL | Reautenticação | Exigida antes de operações sensíveis. |
| DB-01 | CORE | RLS | RLS ativa em todas as tabelas expostas; políticas testadas. |
| DB-02 | CORE | Autorização por registro | Usuário A não lê/altera dados de B sem permissão. |
| DB-03 | CORE | Políticas de escrita | INSERT/UPDATE/DELETE impedem apropriação e elevação de privilégios. |
| DB-04 | CORE | Chaves | Somente publishable key no cliente; secret/service_role exclusivamente em ambiente confiável. |
| DB-05 | CORE | Claims confiáveis | Não usar user_metadata editável para autorizar ações. |
| DB-06 | CONDITIONAL | Funções/views/storage | Permissões e comportamento de RLS revisados e testados. |
| API-01 | CORE | Validação no servidor | Nenhuma permissão depende exclusivamente da interface. |
| API-02 | CORE | Proteção contra abuso | Rate limits e tratamento de erros configurados conforme endpoints. |
| APP-01 | CORE | TLS | HTTPS e validação de certificados ativos. |
| APP-02 | CORE | Rotas protegidas | Sem sessão válida, não há acesso a conteúdo privado. |
| APP-03 | CORE | Segredos e dependências | Scan de segredos, dependências auditadas, versões controladas. |
| DATA-01 | CORE | Minimização | Coletar apenas scopes e dados necessários. |
| DATA-02 | CORE | Perfil resiliente | Nome, foto e e-mail podem estar ausentes; aplicativo trata ausência. |
| DATA-03 | CONDITIONAL | Privacidade e exclusão | Avisos, retenção, exportação e exclusão conforme legislação e loja. |
| PAY-01 | CONDITIONAL | Provedor de pagamento | Cartões tratados por PSP/SDK apropriado; não armazenar PAN/CVV no Supabase. |
| PAY-02 | CONDITIONAL | Confirmação de pagamentos | Webhooks assinados e verificados no servidor; idempotência. |
| PAY-03 | CONDITIONAL | PCI DSS / SCA / 3DS | Obrigações avaliadas conforme mercado e arquitetura. |
| OPS-01 | CORE | Auditoria de segurança | Supabase Security Advisor e testes de autorização sem achados críticos pendentes. |
| OPS-02 | CORE | Logs seguros | Eventos úteis registrados sem tokens, dados financeiros ou segredos. |
| OPS-03 | CORE | Testes de regressão | Login, expiração, logout, falha de provedor e acesso cruzado testados. |
| OPS-04 | CONDITIONAL | Incidentes e recuperação | Plano, backup e recuperação adequados à criticidade. |
| RISK-01 | ADVANCED | Threat modeling e pentest | Executados conforme superfície de ataque e exposição. |
| RISK-02 | ADVANCED | Integridade de dispositivo | Aplicada se houver justificativa de risco. |

## Regras arquiteturais
1. Separar logicamente interface, integração de provedores, Supabase Auth, ciclo de sessão e autorização. Não impor pastas extras sem necessidade.
2. O frontend exibe estados; o backend e RLS autorizam acesso.
3. Nunca confiar em nomes, fotos, e-mails ou dados do cliente como prova de autorização.
4. Google/Apple Sign-In **não fornecem automaticamente dados de cartão**. Apple Pay/Google Pay e PSP são integrações separadas.
5. Controles gerenciados pelos provedores não precisam ser reimplementados; sua configuração e comportamento devem ser testados.
6. Nenhum checklist garante segurança absoluta: a aprovação exige evidência de testes.

## Critério de aprovação (Definition of Done)
- [ ] Controles CORE aplicáveis implementados e comprovados.
- [ ] Controles CONDITIONAL pertinentes identificados e atendidos.
- [ ] Fluxos Google e Apple testados nos ambientes-alvo.
- [ ] RLS validada com usuários diferentes e chamadas diretas à API.
- [ ] Nenhuma chave privilegiada ou token exposto.
- [ ] Auditorias de dependências e Supabase revisadas.
- [ ] Decisões, exceções e riscos residuais documentados.

## Referências normativas
- OWASP MASVS: https://mas.owasp.org/MASVS/
- OWASP ASVS: https://owasp.org/www-project-application-security-verification-standard/
- OWASP API Security Top 10: https://owasp.org/API-Security/
- NIST SP 800-63: https://pages.nist.gov/800-63-4/
- Supabase Auth: https://supabase.com/docs/guides/auth
- Supabase RLS: https://supabase.com/docs/guides/database/postgres/row-level-security

**Nota de manutenção:** verificar documentação e versões atuais dos SDKs e do Supabase antes de cada implementação. Este documento é uma referência técnica, não certificação.
