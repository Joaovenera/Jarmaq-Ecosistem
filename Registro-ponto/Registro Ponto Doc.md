# 📌 Sistema de Registro de Ponto - Jarmaq Ecosistem

## 📝 Visão Geral

Este documento descreve os requisitos e o plano de desenvolvimento para o Sistema de Registro de Ponto da Jarmaq Ecosistem. O objetivo é criar uma solução moderna, eficiente e segura para o controle de jornada de trabalho, garantindo total conformidade com a legislação trabalhista brasileira, em especial a **Portaria 671/2021 do MTP** (nas modalidades REP-A ou REP-P, conforme aplicável) e a **Lei Geral de Proteção de Dados (LGPD - Lei 13.709/2018)**. O sistema visa integrar-se futuramente com outros módulos do ecossistema Jarmaq, como RH e Folha de Pagamento.

---

## 📌 Funcionalidades do Sistema Completo (Visão de Longo Prazo)

### 1. Conformidade Legal e Auditoria
-   Geração automática dos **Arquivos Fiscais** exigidos: AFD (Arquivo Fonte de Dados), AEJ (Arquivo Eletrônico de Jornada) e ACJEF (Arquivo de Comprovantes de Jornada Eletrônico), conforme layout da Portaria 671 e modalidade REP implementada.
-   Emissão do **Comprovante de Registro de Ponto do Trabalhador** a cada marcação (formato eletrônico ou impresso, dependendo da configuração e modalidade REP), contendo todas as informações obrigatórias (incluindo NSR) e com assinatura eletrônica qualificada ou avançada (para REP-P).
-   Garantia de **Inalterabilidade dos Registros de Marcação Originais**. Ajustes e abonos devem ser registrados separadamente com rastreabilidade.
-   **Sincronização Contínua com a Hora Legal Brasileira** (Observatório Nacional).
-   **Trilhas de Auditoria Detalhadas** para todas as ações críticas no sistema (marcações, acessos, alterações cadastrais, aprovações, etc.).

### 2. Métodos de Registro de Ponto Flexíveis
-   Aplicativo Móvel (iOS/Android) com opções de:
    -   Geolocalização (Geofencing) para validação de localidade (com consentimento).
    -   Reconhecimento Facial (com consentimento explícito e segurança reforçada - LGPD).
-   Navegador Web (para usuários em desktop).
-   Biometria Digital (via leitores integrados ou homologados, com consentimento explícito - LGPD).
-   Equipamento Físico Homologado (REP-C, se necessário em cenários específicos).

### 3. Gestão e Administração Abrangente
-   **Cadastro Completo de Colaboradores:** Nome, CPF, **PIS (essencial)**, Matrícula, Data de Admissão, Cargo, Departamento, Centro de Custo, Tipo de Perfil de Acesso, etc.
-   **Gestão de Horários e Escalas:** Cadastro de múltiplos tipos de jornadas (fixas, flexíveis, turnos, 12x36, escalas de revezamento complexas), feriados configuráveis.
-   **Apuração Automática e Precisa:** Cálculo de horas normais, extras (com diferentes percentuais), adicionais (noturno, periculosidade, insalubridade - se integrado), DSR, banco de horas (parametrizável), faltas, atrasos.
-   **Gerenciamento de Justificativas e Abonos:** Registro de férias, licenças, atestados (com anexo), folgas, com workflow para validação.
-   **Workflow de Aprovação Configurável:** Fluxo para aprovação de ajustes de ponto, solicitações de abono (Colaborador -> Gestor -> RH).

### 4. Relatórios e Monitoramento em Tempo Real
-   **Espelho de Ponto Individual:** Claro, detalhado e em conformidade legal para conferência e assinatura (eletrônica ou física).
-   **Relatórios Legais Obrigatórios:** Geração dos arquivos AFD, AEJ, ACJEF sob demanda.
-   **Relatórios Gerenciais:** Banco de Horas (saldos individuais e consolidados), Horas Extras, Absenteísmo (índices, motivos), Inconsistências, Pontualidade.
-   **Dashboard de Gestão:** Visão em tempo real de presentes/ausentes, alertas de inconsistências, resumo de horas.

### 5. Segurança Robusta e Conformidade LGPD
-   **Criptografia de Dados:** Criptografia forte para dados sensíveis em trânsito (HTTPS) e em repouso (banco de dados).
-   **Controle de Acesso Baseado em Função (RBAC):** Perfis bem definidos (Colaborador, Gestor, Administrador/RH) com permissões granulares.
-   **Hashing Seguro de Senhas.**
-   **Política Clara de Backup e Recuperação de Desastres.**
-   **Gestão de Consentimento** (para dados sensíveis como biometria e geolocalização).

### 6. Integrações Estratégicas
-   **Folha de Pagamento:** Exportação segura e automatizada dos dados apurados (horas, adicionais, descontos) via API ou arquivo estruturado.
-   **Sistemas de RH (HRIS):** Sincronização bidirecional ou unidirecional de dados cadastrais de colaboradores.
-   **Outros Sistemas Corporativos (ERP, CRM):** Possibilidade de integrações futuras conforme necessidade.

---

## 🚀 MVP (Mínimo Produto Viável)

### 🎯 Objetivo do MVP
Lançar rapidamente a **funcionalidade central e legalmente compatível** de registro de ponto eletrônico (foco no REP-P via Programa), permitindo que os colaboradores registrem suas jornadas e que o RH tenha acesso aos registros básicos para conferência inicial e geração do espelho de ponto. Validar a arquitetura e coletar feedback para iterações futuras.

### 📌 Funcionalidades Essenciais do MVP

#### 1. Registro de Ponto (Conforme Portaria 671 - REP-P)
-   Marcação via **Navegador Web** (desktop) e/ou **Aplicativo Móvel Básico** (sem geofencing/facial no MVP).
-   Registro dos tipos: Entrada, Início Intervalo, Fim Intervalo, Saída.
-   **Geração OBRIGATÓRIA e IMEDIATA do Comprovante Eletrônico** a cada marcação, contendo:
    -   Identificação do Empregador (Nome/Razão Social, CNPJ/CPF)
    -   Local da Prestação de Serviços (Endereço)
    -   Identificação do Trabalhador (Nome, CPF, **PIS**)
    -   Data e Hora da Marcação (HH:MM:SS)
    -   **NSR (Número Sequencial de Registro)** - Gerado sequencialmente por marcação.
    -   Modelo e Fabricante do SREP (se aplicável) e Versão do Programa (REP-P).
    -   Hash (SHA-256) do registro (recomendado para integridade).
-   Entrega do Comprovante ao trabalhador (ex: exibição na tela com opção de download PDF ou envio por e-mail configurado).
-   **Garantia de Inalterabilidade Técnica** do registro original no banco de dados.
-   **Sincronização com a Hora Legal Brasileira** no momento da marcação no backend.

#### 2. Controle de Acesso e Segurança Básica
-   Autenticação de usuários via **JWT** (Login com Email/CPF/Matrícula e Senha).
-   **Perfis de Acesso (RBAC) Mínimos:** `COLABORADOR`, `ADMIN_RH`.
-   **Trilhas de Auditoria Básicas:** Registrar login, logout e tentativas de marcação de ponto.
-   **Hashing de Senhas** (ex: bcrypt).
-   Backup básico do banco de dados.

#### 3. Gestão de Cadastros Essenciais
-   Cadastro de Colaboradores: `Nome Completo`, `CPF`, `PIS` (Obrigatório!), `Matrícula` (ou ID único), `Email`, `Cargo`, `Data de Admissão`, `Senha Hash`, `ID do Perfil de Acesso`. (*Atenção à LGPD*).
-   Cadastro de Escalas Fixas Simples: Definição de horário padrão de entrada, intervalos e saída para associar aos colaboradores.

#### 4. Justificativas (Submissão)
-   Tela/Endpoint (`POST /justificativas`) para o colaborador submeter uma solicitação de ajuste ou justificar uma ausência (data, motivo). *A aprovação/tratamento virá em fases posteriores*.

#### 5. Relatórios Fundamentais
-   **Espelho de Ponto Individual:** Exibição das marcações realizadas pelo colaborador em um período, com cálculo *básico* de horas trabalhadas (sem cálculo complexo de extras/banco no MVP). Deve ser claro e permitir exportação/impressão.
-   **Relatório Simples de Marcações:** Lista de todas as marcações realizadas em um período (visível para `ADMIN_RH`).

### 💻 Tecnologia e Arquitetura Sugerida (MVP)
-   **Front-end:** React.js (Web). *React Native (Mobile) pode ser fase 2*.
-   **Back-end:** Node.js com Express.js (ou framework similar).
-   **Banco de Dados:** PostgreSQL ou MySQL (Relacional é importante aqui).
-   **Autenticação:** JWT com RBAC.
-   **Repositório:** Git (GitHub - `Joaovenera/Jarmaq-Ecosistem`).
-   **Infraestrutura:** Cloud (AWS, GCP, Azure) para deploy facilitado.
-   **CI/CD:** Pipeline básico (GitHub Actions, GitLab CI) para testes automatizados e deploy em staging/produção.

#### 🏛️ Notas Cruciais sobre a Modelagem do Banco de Dados (MVP):
-   **`users`**: Incluir `pis`, `data_admissao`, `tipo_perfil_id`.
-   **`marcacoes_ponto`**:
    -   Deve ser **append-only** (sem updates ou deletes nos registros originais). Implementar via triggers de BD ou controle rígido na aplicação.
    -   Campos Essenciais: `id` (PK), `colaborador_id` (FK users), `timestamp_marcacao` (timestampz, Hora Legal), `tipo_marcacao` (enum: ENTRADA, INI_INTERVALO, FIM_INTERVALO, SAIDA), `nsr` (bigint, unique, auto-increment ou sequence), `dados_comprovante_json` (JSONB/TEXT contendo todos os dados fixos e variáveis usados para gerar o comprovante naquele momento - Nome Empregador, CNPJ, Nome/PIS Colaborador, etc.), `hash_registro` (varchar, SHA-256 do registro), `origem_marcacao` (varchar: WEB, MOBILE, etc.), `timezone_origem` (varchar).
-   **`escalas`**: Tabela para definir os horários padrões (entrada, saida, intervalos).
-   **`justificativas`**: Tabela para armazenar as solicitações dos colaboradores (`colaborador_id`, `data_referencia`, `tipo_justificativa`, `motivo`, `status` (enum: PENDENTE), `timestamp_solicitacao`).
-   **`auditoria_logs`**: Tabela para registrar ações (`usuario_id`, `acao`, `detalhes`, `timestamp_acao`, `ip_origem`).

### 📆 Roadmap Inicial Proposto (MVP)
1.  **Semana 1-2:** **Refinamento Final da Arquitetura e Modelagem Detalhada do Banco de Dados (Incluindo Scripts de Criação)**. Configuração inicial do ambiente de dev e repositório.
2.  **Semana 3-5:** Implementação do Back-end: Autenticação/RBAC, **Endpoint Crítico de Marcação de Ponto (com geração de comprovante e NSR)**, APIs de Cadastro e Justificativa (submissão). Testes unitários.
3.  **Semana 6-7:** Desenvolvimento do Front-end (Web): Telas de Login, Dashboard do Colaborador (com botão de marcar e visualização do último comprovante), Espelho de Ponto Simples, Tela de Submissão de Justificativa. Integração com APIs.
4.  **Semana 8:** Testes de Integração, Ajustes Finais, Configuração de CI/CD básico e Deploy em Ambiente de Staging (Homologação). Preparação de documentação básica.
5.  **Semana 9:** Testes com Grupo Piloto (Colaboradores e RH). Coleta de Feedback e Ajustes Críticos. Planejamento do Deploy em Produção.

### 🔥 Pontos Críticos de Atenção (MVP)
-   **Conformidade da Marcação (Portaria 671 - REP-P):** Aderência estrita aos requisitos do comprovante, geração correta do NSR, inalterabilidade do registro e sincronia com Hora Legal. **Este é o ponto de maior risco e exige mais atenção técnica.**
-   **Segurança e LGPD:** Implementar segurança desde o início (hashing, criptografia básica, controle de acesso) e garantir que dados pessoais (CPF, PIS) sejam tratados corretamente.
-   **Precisão da Hora Legal:** Garantir que o servidor backend esteja sempre sincronizado com NTP.br.
-   **Usabilidade:** O processo de marcação deve ser intuitivo e rápido para o colaborador.

---

## 🔜 Próximos Passos (Pós-MVP)
Após a validação e estabilização do MVP, o roadmap incluirá:
-   Implementação do workflow de aprovação de justificativas.
-   Cálculo completo de horas (extras, banco de horas, adicionais).
-   Geração dos arquivos fiscais (AFD, AEJ, ACJEF).
-   Integração com Folha de Pagamento e Sistema de RH.
-   Inclusão de outros métodos de marcação (Mobile com Geo/Facial, Biometria).
-   Relatórios Gerenciais Avançados e Dashboards.
-   Melhorias contínuas com base no feedback.

---

*Este documento é um guia vivo e será atualizado conforme o progresso e as necessidades do projeto Jarmaq Ecosistem.*
*Última Atualização: 2025-04-02*