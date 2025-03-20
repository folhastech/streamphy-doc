# Análise de Requisitos do Sistema Midfield

## Requisitos Funcionais (RF)

### Autenticação e Controle de Acesso
- **[RF001]**: O sistema deve permitir autenticação de usuários com credenciais (login/senha).
- **[RF002]**: O sistema deve suportar dois níveis de acesso: ADMIN e USER.
- **[RF003]**: O sistema deve restringir o acesso de usuários comuns (USER) apenas às informações da empresa associada.
- **[RF004]**: O sistema deve permitir que administradores (ADMIN) acessem informações de todas as empresas.

### Gestão de Empresas
- **[RF005]**: O sistema deve permitir o cadastro de novas empresas.
- **[RF006]**: O sistema deve permitir a edição de empresas existentes.
- **[RF007]**: O sistema deve permitir a exclusão de empresas.
- **[RF008]**: O sistema deve associar empresas a aplicativos, gateways e usuários.

### Gestão de Aplicativos
- **[RF009]**: O sistema deve permitir o cadastro de aplicativos associados a uma empresa.
- **[RF010]**: O sistema deve permitir a edição de aplicativos existentes.
- **[RF011]**: O sistema deve permitir a exclusão de aplicativos.
- **[RF012]**: O sistema deve permitir a configuração de webhook ou tópico MQTT para cada aplicativo.

### Gestão de Gateways
- **[RF013]**: O sistema deve permitir o cadastro de gateways Iris associados a um aplicativo.
- **[RF014]**: O sistema deve permitir a edição de gateways Iris existentes.
- **[RF015]**: O sistema deve permitir a exclusão de gateways Iris.
- **[RF016]**: O sistema deve permitir o cadastro de gateways Hermes associados a um gateway Iris.
- **[RF017]**: O sistema deve permitir a edição de gateways Hermes existentes.
- **[RF018]**: O sistema deve permitir a exclusão de gateways Hermes.
- **[RF019]**: O sistema deve gerar IDs únicos para cada Iris cadastrado.

### Gestão de Sensores
- **[RF020]**: O sistema deve permitir o cadastro de sensores associados a um gateway Hermes.
- **[RF021]**: O sistema deve permitir a edição de sensores existentes.
- **[RF022]**: O sistema deve permitir a exclusão de sensores.
- **[RF023]**: O sistema deve gerar IDs únicos para cada sensor cadastrado.

### Processamento de Mensagens
- **[RF024]**: O sistema deve receber mensagens MQTT no formato de tópico v1/event/{id}.
- **[RF025]**: O sistema deve extrair o ID do gateway Iris a partir do tópico MQTT.
- **[RF026]**: O sistema deve verificar a existência do gateway na base de dados.
- **[RF027]**: O sistema deve associar a mensagem à empresa correta.
- **[RF028]**: O sistema deve converter mensagens do formato FlatBuffer para objetos Java.
- **[RF029]**: O sistema deve encaminhar mensagens processadas via webhook HTTP conforme configuração.
- **[RF030]**: O sistema deve publicar mensagens processadas em tópicos MQTT conforme configuração.
- **[RF031]**: O sistema deve registrar todas as mensagens processadas como eventos na base de dados.
- **[RF032]**: O sistema deve registrar eventos de erro quando o processamento falhar.

### Visualização e Monitoramento
- **[RF033]**: O sistema deve exibir uma página de eventos para administradores com eventos de todas as empresas.
- **[RF034]**: O sistema deve exibir uma página de eventos para usuários apenas com eventos da empresa associada.
- **[RF035]**: O sistema deve exibir um dashboard com estatísticas e gráficos para usuários.
- **[RF036]**: O sistema deve permitir filtros na visualização de eventos.

### Gestão de Usuários
- **[RF037]**: O sistema deve permitir que administradores cadastrem novos usuários.
- **[RF038]**: O sistema deve permitir que administradores editem usuários existentes.
- **[RF039]**: O sistema deve permitir que administradores excluam usuários.
- **[RF040]**: O sistema deve permitir a definição do tipo de usuário (ADMIN ou USER).
- **[RF041]**: O sistema deve permitir a associação de usuários tipo USER a uma empresa específica.

---

## Requisitos Não Funcionais (RNF)

### Desempenho
- **[RNF001]**: O sistema deve processar mensagens recebidas em no máximo 2 segundos.
- **[RNF002]**: O sistema deve suportar o processamento de pelo menos 100 mensagens por segundo.
- **[RNF003]**: O sistema deve ter tempo de resposta para operações de interface inferior a 1 segundo.

### Segurança
- **[RNF004]**: O sistema deve criptografar todas as credenciais de usuário armazenadas.
- **[RNF005]**: O sistema deve implementar autenticação baseada em tokens JWT.
- **[RNF006]**: O sistema deve registrar todas as tentativas de acesso não autorizadas.
- **[RNF007]**: O sistema deve utilizar conexões HTTPS para todas as comunicações web.
- **[RNF008]**: O sistema deve implementar TLS para conexões MQTT.

### Usabilidade
- **[RNF009]**: A interface do sistema deve ser responsiva e adaptada para dispositivos móveis.
- **[RNF010]**: O sistema deve fornecer feedback claro sobre sucesso ou falha de operações.

### Manutenibilidade
- **[RNF011]**: O sistema deve seguir padrões de codificação como Clean Code e SOLID.
- **[RNF012]**: O sistema deve implementar logs detalhados para facilitar diagnóstico de problemas.

### Confiabilidade
- **[RNF013]**: O sistema deve implementar mecanismo de persistência de mensagens para evitar perda de dados.
- **[RNF014]**: O sistema deve validar todos os dados de entrada para evitar inconsistências.

### Interoperabilidade
- **[RNF015]**: O sistema deve ser capaz de integrar-se com APIs externas via webhooks REST.
- **[RNF016]**: O sistema deve utilizar formatos padrão (JSON) para troca de dados via API.

### Compatibilidade
- **[RNF017]**: A interface web deve ser compatível com os navegadores Chrome, Firefox, Safari e Edge.
- **[RNF018]**: O sistema deve funcionar em ambientes Linux, Windows e macOS.

## Requisitos de Domínio (RD)

- **[RD001]**: Uma Empresa pode ter múltiplos Aplicativos cadastrados.  
- **[RD002]**: Um Aplicativo deve estar obrigatoriamente associado a uma única Empresa.  
- **[RD003]**: Um Aplicativo deve ter configurado ou um webhook ou um tópico MQTT para recebimento de mensagens processadas.  
- **[RD004]**: Um Aplicativo pode ter múltiplos Gateways Iris associados.  
- **[RD005]**: Um Gateway Iris deve estar obrigatoriamente associado a um único Aplicativo.  
- **[RD006]**: Um Gateway Iris é identificado por um ID único gerado automaticamente pelo sistema.  
- **[RD007]**: Um Gateway Iris pode ter múltiplos Gateways Hermes associados.  
- **[RD008]**: Um Gateway Hermes deve estar obrigatoriamente associado a um único Gateway Iris.  
- **[RD009]**: Um Gateway Hermes pode ter múltiplos Sensores associados.  
- **[RD010]**: Um Sensor deve estar obrigatoriamente associado a um único Gateway Hermes.  
- **[RD011]**: Um Sensor é identificado por um ID único gerado automaticamente pelo sistema.  
- **[RD012]**: Um Evento deve registrar minimamente: ID do Gateway, timestamp de recebimento, dados processados e status de processamento.  
- **[RD013]**: Um Evento deve estar associado a um Gateway Iris específico.  
- **[RD014]**: Um Evento deve estar indiretamente associado a uma Empresa específica através do Gateway Iris.  
- **[RD015]**: Um Usuário do tipo USER deve estar associado a uma única Empresa.  
- **[RD016]**: Um Usuário do tipo ADMIN não precisa estar associado a uma Empresa específica.  
- **[RD017]**: Sensores devem transmitir seus dados através dos Gateways Hermes.  
- **[RD018]**: Gateways Hermes devem transmitir dados coletados através dos Gateways Iris.  
- **[RD019]**: Gateways Iris devem transmitir dados para o Midfield através de mensagens MQTT em formato FlatBuffer.  
- **[RD020]**: O tópico MQTT para envio de mensagens pelos Gateways Iris deve seguir o padrão `v1/event/{id}`.  
- **[RD021]**: Apenas usuários autenticados podem acessar o sistema.  
- **[RD022]**: Administradores têm acesso total ao sistema, incluindo todas as funcionalidades de cadastro e visualização.  
- **[RD023]**: Usuários comuns têm acesso apenas às funcionalidades de visualização de eventos e dashboard, e somente para sua empresa associada.  
- **[RD024]**: Mensagens recebidas pelo Midfield devem ser armazenadas em seu formato original e também em formato processado.  
- **[RD025]**: O processamento da mensagem deve ser abortado caso o Gateway Iris não seja identificado no sistema.  
- **[RD026]**: O processamento da mensagem deve ser abortado caso a Empresa não seja encontrada.  
- **[RD027]**: O processamento da mensagem deve ser abortado caso ocorra erro na conversão do formato FlatBuffer para objeto Java.  
- **[RD028]**: Eventos de erro no processamento devem conter informações detalhadas sobre o motivo da falha.  
- **[RD029]**: A estrutura hierárquica dos componentes deve ser: Empresa > Aplicativo > Gateway Iris > Gateway Hermes > Sensor.  
- **[RD030]**: Cada Empresa deve ter suas mensagens processadas e encaminhadas apenas para seus endpoints configurados (webhook ou MQTT).

