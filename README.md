# ESPECIFICAÇÃO COMPLETA - APLICAÇÃO OFFICE

## 📋 RESUMO EXECUTIVO

Esta é uma aplicação web para gerenciamento de serviços IPTV/P2P, conhecida como "Office" ou "NPanel".
É um painel administrativo completo para revendedores de serviços de streaming, com funcionalidades de gestão de clientes, testes automáticos, pagamentos e muito mais.

## ARQUITETURA DO SISTEMA

#### Tecnologias Utilizadas
- **Backend**: Tecnologia flexível (PHP, Node.js, Python, etc.)
- **Banco de Dados**: Banco relacional (MySQL, PostgreSQL, etc.)
- **Frontend**: Tecnologia moderna (React, Vue.js, Angular, etc.)
- **Cache**: Sistema de cache distribuído (Redis, Memcached, etc.)
- **Servidor Web**: Qualquer servidor web moderno
- **Frameworks/Bibliotecas**: 
  - Framework de UI moderno e responsivo
  - Sistema de tabelas interativas
  - Biblioteca de ícones
  - Sistema de notificações
  - Componentes de alerta


## 🗄️ ESTRUTURA DO BANCO DE DADOS

### Tabelas Principais

#### 1. **tenants** - Multi-Tenancy (NOVA TABELA)
- Configuração de múltiplos tenants
- Dados específicos de cada tenant
- Configurações de domínio
- Status de ativação
- Limites de recursos

#### 2. **office_properties** - Configurações do Sistema
- Armazena todas as configurações do painel
- Propriedades como: server_name, email_settings, allowed_packages, etc.
- Sistema de cache para otimização
- **Relacionamento com tenant_id**

#### 3. **user_properties** - Propriedades dos Usuários
- Configurações específicas de cada usuário
- Cache de dados do usuário
- **Relacionamento com tenant_id**

#### 4. **clients** - Clientes Locais (NOVA TABELA)
- Armazenamento local de todos os clientes
- Dados completos: username, password, email, telefone, expiração
- Histórico de renovações e modificações
- Sincronização com XUIs
- Status de sincronização
- **Relacionamento com tenant_id**

#### 5. **streaming_servers** - Servidores de Streaming (NOVA TABELA)
- Configuração de múltiplos servidores (XUI, BinStream, P2BR, XtreamUI, etc.)
- URLs, tokens de acesso, status de conexão
- Configurações específicas de cada servidor
- Prioridade de sincronização
- Tipo de servidor (XUI, BinStream, P2BR, XtreamUI, etc.)
- **Relacionamento com tenant_id**

#### 6. **sync_log** - Log de Sincronização (NOVA TABELA)
- Histórico de sincronizações com servidores de streaming
- Status de sucesso/erro
- Dados sincronizados
- Timestamp de sincronização
- Tipo de servidor sincronizado
- **Relacionamento com tenant_id**

#### 7. **chatbot** - Sistema de Chatbot
- Regras de chatbot para atendimento automático
- Respostas automáticas para clientes
- **Relacionamento com tenant_id**

#### 8. **notifications** - Sistema de Notificações
- Notificações push para usuários
- Sistema de broadcast
- **Relacionamento com tenant_id**

#### 9. **payments** - Sistema de Pagamentos
- Registro de transações
- Integração com gateways de pagamento
- **Relacionamento com tenant_id**

#### 12. **plans** - Sistema de Planos (NOVA TABELA)
- Configuração de planos por tenant
- Preços e durações
- Descontos e promoções
- **Relacionamento com tenant_id**

#### 13. **credits_transactions** - Transações de Créditos (NOVA TABELA)
- Histórico de vendas de créditos
- Transferências entre revendedores
- Comissões automáticas
- **Relacionamento com tenant_id**

#### 14. **auto_renewals** - Renovação Automática (NOVA TABELA)
- Configuração de renovação automática
- Histórico de renovações
- Status de pagamento
- **Relacionamento com tenant_id**

#### 15. **whatsapp_messages** - Mensagens WhatsApp (NOVA TABELA)
- Histórico de mensagens enviadas
- Templates de mensagens
- Status de entrega
- **Relacionamento com tenant_id**

#### 16. **domains** - Sistema de Domínios (NOVA TABELA)
- Registro de domínios vendidos
- Configuração de APIs (Namecheap, etc.)
- Histórico de vendas de domínios
- Status de pagamento e renovação
- **Relacionamento com tenant_id**

#### 17. **domain_providers** - Provedores de Domínios (NOVA TABELA)
- Configuração de APIs de provedores
- Credenciais de acesso
- Preços e comissões
- **Relacionamento com tenant_id**

#### 10. **test_historic** - Histórico de Testes
- Registro de testes gratuitos realizados
- Controle de IPs e emails
- **Relacionamento com tenant_id**

#### 11. **urls** - Encurtador de URLs
- Sistema de links curtos
- Rastreamento de cliques
- **Relacionamento com tenant_id**

## 👥 SISTEMA DE USUÁRIOS E PERMISSÕES

### Multi-Tenancy
- **Isolamento completo** entre tenants
- **Domínios personalizados** para cada tenant
- **Configurações independentes** por tenant
- **Limites de recursos** configuráveis
- **Billing e cobrança** por tenant

### Tipos de Usuários
1. **Super Admin** - Acesso total ao sistema multi-tenant
2. **Tenant Admin** - Admin de um tenant específico
3. **Partner** - Acesso limitado a funcionalidades específicas
4. **Ultra** - Revendedor com privilégios especiais
5. **Master** - Revendedor master
6. **Reseller** - Revendedor comum

### Sistema de Permissões
- Controle granular por recursos (iptv, binstream, codes, p2br)
- Hierarquia de usuários (tree structure)
- Permissões por página e funcionalidade
- **Isolamento por tenant**
- **Permissões cross-tenant** para super admins

## 🎯 FUNCIONALIDADES PRINCIPAIS

### 1. **Gestão de Clientes**
- Criação de clientes IPTV/P2P
- Edição de dados do cliente
- Renovação de assinaturas
- Bloqueio/desbloqueio de clientes
- Transferência entre revendedores
- Controle de conexões simultâneas
- Histórico de atividades
- **Armazenamento local dos clientes** (não depende apenas dos servidores)
- **Sincronização com múltiplos servidores** (XUI, BinStream, P2BR, XtreamUI, etc.)
- **Funcionamento independente** dos servidores de streaming
- **Renovação automática** com notificações
- **Histórico completo** de renovações e modificações
- **Status de pagamento** e vencimento
- **Alertas automáticos** de expiração

### 2. **Sistema de Testes**
- Testes automáticos por email
- Testes rápidos via painel
- Controle de IPs e emails
- Templates personalizáveis
- Bloqueio por horários específicos
- Histórico de testes

### 3. **Gestão de Revendedores**
- Criação de revendedores
- Sistema de créditos
- Hierarquia de revendedores
- Relatórios de vendas
- Transferência de clientes
- **Sistema de vendas de créditos** entre revendedores
- **Comissões automáticas** por vendas
- **Histórico de transações** de créditos
- **Limites de créditos** configuráveis
- **Alertas de saldo baixo**
- **Relatórios de performance** por revendedor

### 4. **Sistema de Pagamentos e Planos**
- Integração com Mercado Pago
- Integração com PagSeguro
- Histórico de transações
- Relatórios financeiros
- **Sistema de planos** configuráveis
- **Planos personalizados** por tenant
- **Preços dinâmicos** por revendedor
- **Descontos automáticos** por volume
- **Renovação automática** de planos
- **Cobrança recorrente** configurável
- **Notificações de pagamento** por WhatsApp
- **Comprovantes automáticos** por email

### 5. **Sistema de Tickets**
- Suporte técnico
- Sistema de prioridades
- Notificações de novos tickets
- Histórico de conversas

### 6. **Notificações**
- Sistema de broadcast
- Notificações push
- Templates personalizáveis
- Envio por email

### 7. **Chatbot e Integração WhatsApp**
- Respostas automáticas
- Regras personalizáveis
- **Integração com Evolution API (não oficial)**
- Histórico de conversas
- **Notificações automáticas** por WhatsApp
- **Envio de testes** via WhatsApp
- **Alertas de renovação** por WhatsApp
- **Comprovantes de pagamento** via WhatsApp
- **Suporte técnico** via WhatsApp
- **Broadcast de mensagens** para clientes
- **Templates personalizáveis** para WhatsApp
- **Venda separada** para cada revendedor
- **Configuração independente** por tenant

### 8. **Relatórios e Analytics**
- Dashboard com estatísticas
- Relatórios de vendas
- Análise de clientes ativos
- Relatórios de expiração
- Gráficos de performance

### 9. **Configurações do Sistema**
- Configurações gerais
- Configurações de email
- Templates de mensagens
- Configurações de pagamento
- Configurações de teste

### 10. **Área do Cliente**
- Dashboard do cliente
- Renovação de assinatura
- Histórico de transações
- Configurações da conta

### 11. **Sistema de Venda de Domínios**
- **Venda direta**: Pagamento vai para o dono do Office
- **Venda indireta**: Revendedor configura própria API (Namecheap, etc.)
- **Cobrança por créditos** na venda indireta
- **Integração com APIs** de provedores de domínios
- **Histórico de vendas** de domínios
- **Renovação automática** de domínios
- **Notificações de expiração** por WhatsApp
- **Comissões automáticas** por venda
- **Relatórios de vendas** de domínios
- **Configuração de preços** por tenant

## 🔧 FUNÇÕES TÉCNICAS PRINCIPAIS

### Autenticação e Segurança
- Sistema de login com username/password
- Autenticação de dois fatores (2FA)
- Proteção contra brute force
- Tokens CSRF para segurança
- Sessões seguras

### Gestão de Clientes
- Criação e edição de clientes
- Renovação de assinaturas
- Bloqueio/desbloqueio de clientes
- Transferência entre revendedores
- Controle de conexões simultâneas
- Histórico de atividades

### Sistema de Testes
- Criação de testes automáticos
- Controle de IPs e emails
- Bloqueio por horários específicos
- Histórico de testes realizados

### Gestão de Revendedores
- Criação e gestão de revendedores
- Sistema de créditos
- Hierarquia de revendedores
- Transferência de clientes

### Sistema de Pagamentos
- Integração com gateways de pagamento
- Histórico de transações
- Relatórios financeiros
- Sistema de planos

### Configurações do Sistema
- Configurações gerais do painel
- Propriedades de usuários
- Sistema de cache
- Configurações de email

### Sistema de Cache
- Cache de configurações
- Cache de consultas
- Cache de templates
- Limpeza automática de cache

## 📧 SISTEMA DE EMAIL

### Configurações
- Suporte a SMTP
- Integração com SendGrid
- Templates HTML personalizáveis
- Variáveis dinâmicas nos templates

### Templates Principais
1. **Teste Automático** - Envio de dados de teste
2. **Recuperação de Senha** - Reset de senha
3. **Expiração** - Aviso de expiração
4. **Boas-vindas** - Mensagem de boas-vindas

## 🎨 INTERFACE DO USUÁRIO

### Design System
- **Framework**: Framework de UI moderno e responsivo
- **Tema**: Dark/Light mode
- **Responsivo**: Mobile-first
- **Componentes**: 
  - Sistema de tabelas interativas
  - Sistema de alertas moderno
  - Sistema de notificações
  - Biblioteca de ícones
- **Multi-tenant**: Interface personalizada por tenant

### Páginas Principais
1. **Dashboard** - Visão geral do sistema
2. **Clientes** - Gestão de clientes
3. **Revendedores** - Gestão de revendedores
4. **Testes** - Sistema de testes
5. **Pagamentos** - Gestão financeira
6. **Tickets** - Suporte técnico
7. **Configurações** - Configurações do sistema
8. **Relatórios** - Analytics e relatórios
9. **Tenants** - Gestão de tenants (Super Admin)
10. **Billing** - Sistema de cobrança por tenant
11. **Domínios** - Sistema de venda de domínios
12. **WhatsApp** - Configuração Evolution API

## 🔌 INTEGRAÇÕES EXTERNAS

### Gateways de Pagamento
1. **Mercado Pago**
   - Checkout Pro
   - Webhooks
   - API v2

2. **PagSeguro**
   - Lightbox
   - API de pagamentos
   - Notificações

### APIs Externas
1. **Múltiplos XUI** - Painéis de controle independentes
2. **Múltiplos BinStream** - Serviços P2P independentes
3. **Múltiplos P2BR** - Serviços P2P alternativos independentes
4. **XtreamUI** - Painéis de controle alternativos
5. **Outros Sistemas** - Qualquer sistema de streaming compatível
6. **SSIPTV** - Aplicativo mobile
7. **Evolution API** - WhatsApp não oficial (vendido separadamente)
8. **Gateways de Pagamento** - Mercado Pago, PagSeguro, etc.
9. **APIs de Domínios** - Namecheap, GoDaddy, etc.

### **IMPORTANTE: Nova Arquitetura Independente e Multi-Tenant**
- **Armazenamento local**: Todos os clientes são salvos localmente no banco de dados
- **Múltiplos Servidores**: Suporte a vários servidores simultaneamente (XUI, BinStream, P2BR, XtreamUI, etc.)
- **Independência**: O sistema funciona mesmo sem conexão com servidores externos
- **Sincronização bidirecional**: Dados sincronizados entre painel local e servidores
- **Redundância**: Múltiplos servidores para alta disponibilidade
- **Multi-tenancy**: Isolamento completo entre tenants
- **Domínios personalizados**: Cada tenant pode ter seu próprio domínio
- **Configurações independentes**: Cada tenant tem suas próprias configurações
- **Billing por tenant**: Sistema de cobrança individualizado

## 📊 SISTEMA DE RELATÓRIOS

### Relatórios Disponíveis
1. **Dashboard** - Visão geral
2. **Clientes Ativos** - Estatísticas de clientes
3. **Vendas** - Relatório de vendas
4. **Expirações** - Clientes próximos de expirar
5. **Testes** - Histórico de testes
6. **Pagamentos** - Transações financeiras
7. **Logs** - Histórico de atividades

### Métricas Principais
- Total de clientes ativos
- Receita mensal/anual
- Taxa de conversão de testes
- Performance de revendedores
- Uptime do serviço

## 🔒 SEGURANÇA

### Medidas de Segurança
1. **Autenticação**
   - Login com username/password
   - 2FA (Two-Factor Authentication)
   - Proteção contra brute force
   - Sessões seguras

2. **Autorização**
   - Controle de acesso por recursos
   - Hierarquia de permissões
   - Validação de CSRF

3. **Dados**
   - Senhas criptografadas
   - Sanitização de inputs
   - Validação de dados
   - Logs de auditoria

4. **Infraestrutura**
   - HTTPS obrigatório
   - Headers de segurança
   - Rate limiting
   - Backup automático

## 📈 MONITORAMENTO

### Logs do Sistema
1. **Log de Atividades** - Todas as ações dos usuários
2. **Log de Créditos** - Movimentações de créditos
3. **Log de Pagamentos** - Transações financeiras
4. **Log de Testes** - Histórico de testes
5. **Log de Erros** - Erros do sistema

### Métricas de Performance
- Tempo de resposta das páginas
- Uso de memória
- Queries do banco de dados
- Cache hit rate
- Uptime do sistema

## 🔄 ATUALIZAÇÕES

### Sistema de Updates
- Verificação automática de atualizações
- Download e instalação automática
- Backup antes da atualização
- Rollback em caso de erro

### Versionamento
- Controle de versão com Git
- Changelog detalhado
- Releases estáveis
- Hotfixes para correções críticas

## 📱 RESPONSIVIDADE

### Dispositivos Suportados
- **Desktop**: 1920x1080 e superiores
- **Tablet**: 768px - 1024px
- **Mobile**: 320px - 767px

### Funcionalidades Mobile
- Menu responsivo
- Tabelas com scroll horizontal
- Botões touch-friendly
- Formulários otimizados

## 🎯 OTIMIZAÇÕES

### Performance
1. **Cache**
   - Cache de configurações
   - Cache de consultas
   - Cache de templates

2. **Banco de Dados**
   - Índices otimizados
   - Queries otimizadas
   - Connection pooling

3. **Frontend**
   - Minificação de CSS/JS
   - Compressão de imagens
   - CDN para recursos estáticos

## 🔧 MANUTENÇÃO

### Tarefas Automáticas
1. **Limpeza de Cache** - Diariamente
2. **Backup do Banco** - Diariamente
3. **Limpeza de Logs** - Semanalmente
4. **Verificação de Updates** - Diariamente

### Monitoramento
1. **Uptime** - Monitoramento 24/7
2. **Performance** - Métricas em tempo real
3. **Erros** - Alertas automáticos
4. **Segurança** - Logs de auditoria

## 📋 CHECKLIST DE IMPLEMENTAÇÃO

### Fase 1: Estrutura Base e Multi-Tenancy
- [ ] Configuração do ambiente de desenvolvimento
- [ ] Estrutura de diretórios
- [ ] Configuração do banco de dados
- [ ] Sistema de multi-tenancy
- [ ] Sistema de autenticação básico
- [ ] Interface de login
- [ ] Gestão de tenants

### Fase 2: Funcionalidades Core
- [ ] Gestão de usuários por tenant
- [ ] Sistema de permissões multi-tenant
- [ ] Gestão de clientes por tenant
- [ ] Sistema de testes por tenant
- [ ] Dashboard básico por tenant

### Fase 3: Funcionalidades Avançadas
- [ ] Sistema de pagamentos por tenant
- [ ] Gestão de revendedores por tenant
- [ ] Sistema de tickets por tenant
- [ ] Notificações por tenant
- [ ] Relatórios por tenant
- [ ] Sistema de planos por tenant
- [ ] Sistema de vendas de créditos
- [ ] Renovação automática
- [ ] Integração Evolution API
- [ ] Sistema de venda de domínios

### Fase 4: Integrações e Billing
- [ ] Gateways de pagamento
- [ ] APIs externas
- [ ] Sistema de email
- [ ] Chatbot
- [ ] Sistema de billing por tenant
- [ ] Domínios personalizados
- [ ] Evolution API (WhatsApp)
- [ ] Sistema de renovação automática
- [ ] Notificações por WhatsApp
- [ ] APIs de provedores de domínios
- [ ] Sistema de venda direta/indireta de domínios
- [ ] Integração com múltiplos servidores de streaming
- [ ] Sincronização com XUI, BinStream, P2BR, XtreamUI

### Fase 5: Otimizações e Escalabilidade
- [ ] Cache distribuído
- [ ] Performance multi-tenant
- [ ] Segurança por tenant
- [ ] Responsividade
- [ ] Containerização

### Fase 6: Deploy e Monitoramento
- [ ] Configuração de produção
- [ ] SSL para múltiplos domínios
- [ ] Backup multi-tenant
- [ ] Monitoramento por tenant
- [ ] Sistema de alertas

## 🎯 CONCLUSÃO

Esta aplicação é um sistema completo de gestão para revendedores de serviços IPTV/P2P, com funcionalidades avançadas de automação, pagamentos e analytics. A arquitetura é robusta e escalável, permitindo crescimento do negócio.

### **MELHORIAS CRÍTICAS NA NOVA VERSÃO:**

1. **Independência Total**: O sistema não depende mais de um único servidor, funcionando de forma autônoma
2. **Armazenamento Local**: Todos os clientes são salvos localmente, garantindo controle total dos dados
3. **Múltiplos Servidores**: Suporte a vários servidores simultaneamente (XUI, BinStream, P2BR, XtreamUI, etc.) para redundância e alta disponibilidade
4. **Sincronização Inteligente**: Sistema bidirecional de sincronização entre painel local e servidores
5. **Redundância**: Múltiplos servidores garantem continuidade do serviço mesmo com falhas
6. **Multi-Tenancy**: Isolamento completo entre diferentes clientes/empresas
7. **Domínios Personalizados**: Cada tenant pode ter seu próprio domínio
8. **Billing Individualizado**: Sistema de cobrança por tenant
9. **Tecnologia Flexível**: Não amarrado a tecnologias específicas
10. **Sistema de Planos**: Planos configuráveis por tenant
11. **Vendas de Créditos**: Sistema completo de vendas entre revendedores
12. **Renovação Automática**: Sistema inteligente de renovação
13. **Evolution API**: WhatsApp não oficial vendido separadamente
14. **Sistema de Domínios**: Venda direta/indireta com APIs

### **VANTAGENS DA NOVA ARQUITETURA:**

- **Controle Total**: Dados sempre disponíveis localmente
- **Alta Disponibilidade**: Múltiplos servidores de streaming
- **Escalabilidade**: Fácil adição de novos servidores e tenants
- **Segurança**: Backup local de todos os dados e isolamento por tenant
- **Performance**: Consultas locais mais rápidas
- **Flexibilidade**: Funciona offline quando necessário
- **Multi-tenancy**: Suporte a múltiplos clientes/empresas
- **Tecnologia Agnóstica**: Pode ser implementado com qualquer stack moderno
- **Domínios Personalizados**: Cada tenant tem sua própria identidade
- **Billing Automatizado**: Cobrança individualizada por uso
- **Sistema de Planos**: Planos flexíveis e configuráveis
- **Vendas de Créditos**: Sistema completo de transações entre revendedores
- **Renovação Automática**: Reduz perda de clientes e aumenta receita
- **Evolution API**: WhatsApp não oficial vendido separadamente
- **Sistema de Domínios**: Nova fonte de receita com APIs
- **Venda Direta/Indireta**: Flexibilidade para diferentes modelos de negócio
- **Automação Completa**: Reduz trabalho manual e aumenta eficiência

O sistema possui uma arquitetura moderna e flexível, podendo ser implementado com qualquer stack tecnológico atual, oferecendo uma experiência de usuário profissional e intuitiva.

Para refazer a aplicação do zero, recomenda-se seguir a arquitetura modular apresentada, implementando as funcionalidades em fases, começando pelo core do sistema e gradualmente adicionando as funcionalidades mais complexas, com foco especial na nova arquitetura independente, sistema de sincronização e multi-tenancy. 
