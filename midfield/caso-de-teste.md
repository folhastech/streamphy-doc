# Descrição dos Casos de Teste

---

## Testes de Processamento de Mensagens

### TC01 - Processamento com sucesso via webhook
- **Objetivo:** Verificar se o sistema processa corretamente mensagens e envia via webhook  
- **Pré-condições:** Gateway Iris cadastrado e ativo, empresa associada ao gateway, webhook configurado corretamente  
- **Passos:**
  1. Enviar mensagem válida para tópico `v1/event/{id}`
  2. Verificar processamento da mensagem
  3. Verificar envio para webhook  
- **Resultado esperado:** Mensagem processada e enviada, evento registrado no banco
- **Fluxos Alternativos:**
  - **FA01.1:** Webhook indisponível  
    - **Condição:** O endpoint do webhook está fora do ar  
    - **Resultado:** Mensagem não enviada, erro registrado, tentativa de reenvio ou alerta gerado
  - **FA01.2:** Mensagem duplicada  
    - **Condição:** Mensagem já foi processada anteriormente  
    - **Resultado:** Sistema ignora duplicidade, evento não é registrado novamente

---

### TC02 - Processamento com sucesso via MQTT
- **Objetivo:** Verificar se o sistema processa corretamente mensagens e envia via MQTT  
- **Pré-condições:** Gateway Iris cadastrado e ativo, empresa associada ao gateway, tópico MQTT configurado corretamente  
- **Passos:**
  1. Enviar mensagem válida para tópico `v1/event/{id}`
  2. Verificar processamento da mensagem
  3. Verificar publicação no tópico MQTT  
- **Resultado esperado:** Mensagem processada e publicada, evento registrado no banco
- **Fluxos Alternativos:**
  - **FA02.1:** Broker MQTT indisponível  
    - **Condição:** Broker MQTT está fora do ar  
    - **Resultado:** Mensagem não publicada, erro registrado, tentativa de reenvio ou alerta gerado
  - **FA02.2:** Mensagem duplicada  
    - **Condição:** Mensagem já foi processada anteriormente  
    - **Resultado:** Sistema ignora duplicidade, evento não é registrado novamente

---

### TC03 - Gateway não encontrado
- **Objetivo:** Verificar tratamento de erro quando gateway não existe  
- **Pré-condições:** Gateway Iris não cadastrado ou ID inexistente  
- **Passos:**
  1. Enviar mensagem para tópico com ID inexistente  
- **Resultado esperado:** Erro registrado, processamento interrompido
- **Fluxos Alternativos:**
  - **FA03.1:** ID de gateway mal formatado  
    - **Condição:** ID enviado não segue o padrão esperado  
    - **Resultado:** Erro de validação registrado, processamento interrompido

---

### TC04 - Empresa não encontrada
- **Objetivo:** Verificar tratamento de erro quando empresa não está associada ao gateway  
- **Pré-condições:** Gateway Iris cadastrado, mas sem empresa associada  
- **Passos:**
  1. Enviar mensagem para tópico com ID de gateway sem empresa  
- **Resultado esperado:** Erro registrado, processamento interrompido
- **Fluxos Alternativos:**
  - **FA04.1:** Empresa associada está inativa  
    - **Condição:** Empresa existe, mas está desativada  
    - **Resultado:** Erro registrado, processamento interrompido

---

### TC05 - Erro na conversão da mensagem
- **Objetivo:** Verificar tratamento de erro na conversão de FlatBuffer para objeto Java  
- **Pré-condições:** Gateway Iris e empresa cadastrados e ativos  
- **Passos:**
  1. Enviar mensagem inválida/mal-formada  
- **Resultado esperado:** Erro de conversão registrado, processamento interrompido
- **Fluxos Alternativos:**
  - **FA05.1:** Mensagem com campos obrigatórios ausentes  
    - **Condição:** Mensagem recebida sem campos essenciais  
    - **Resultado:** Erro de validação registrado, processamento interrompido

---

## Testes de Gestão de Cadastros

### TC06 - Cadastro de empresa
- **Objetivo:** Verificar funcionalidade de cadastro de empresa  
- **Pré-condições:** Usuário administrador logado e com permissão ativa  
- **Passos:**
  1. Acessar página de empresas
  2. Preencher formulário de cadastro
  3. Salvar nova empresa  
- **Resultado esperado:** Empresa cadastrada com sucesso
- **Fluxos Alternativos:**
  - **FA06.1:** Empresa já existente (mesmo CNPJ ou nome)  
    - **Condição:** Tentativa de cadastrar empresa duplicada  
    - **Resultado:** Erro exibido, cadastro não realizado

---

### TC07 - Cadastro de aplicativo
- **Objetivo:** Verificar funcionalidade de cadastro de aplicativo  
- **Pré-condições:** Empresa cadastrada e ativa, usuário administrador logado  
- **Passos:**
  1. Acessar empresa
  2. Preencher formulário de cadastro de aplicativo
  3. Salvar novo aplicativo  
- **Resultado esperado:** Aplicativo cadastrado com sucesso
- **Fluxos Alternativos:**
  - **FA07.1:** Nome de aplicativo já utilizado na empresa  
    - **Condição:** Nome duplicado para a mesma empresa  
    - **Resultado:** Erro exibido, cadastro não realizado

---

### TC08 - Cadastro de gateway Iris
- **Objetivo:** Verificar funcionalidade de cadastro de gateway Iris  
- **Pré-condições:** Aplicativo cadastrado e ativo, usuário administrador logado  
- **Passos:**
  1. Acessar aplicativo
  2. Preencher formulário de cadastro de gateway Iris
  3. Salvar novo gateway  
- **Resultado esperado:** Gateway Iris cadastrado com sucesso e ID gerado
- **Fluxos Alternativos:**
  - **FA08.1:** Limite de gateways atingido  
    - **Condição:** Empresa atingiu o limite de gateways permitidos  
    - **Resultado:** Erro exibido, cadastro não realizado

---

### TC09 - Cadastro de gateway Hermes
- **Objetivo:** Verificar funcionalidade de cadastro de gateway Hermes  
- **Pré-condições:** Gateway Iris cadastrado e ativo, usuário administrador logado  
- **Passos:**
  1. Acessar gateway Iris
  2. Preencher formulário de cadastro de gateway Hermes
  3. Salvar novo gateway  
- **Resultado esperado:** Gateway Hermes cadastrado com sucesso
- **Fluxos Alternativos:**
  - **FA09.1:** Gateway Iris inativo  
    - **Condição:** Tentativa de cadastrar Hermes em Iris inativo  
    - **Resultado:** Erro exibido, cadastro não realizado

---

### TC10 - Cadastro de sensor
- **Objetivo:** Verificar funcionalidade de cadastro de sensor  
- **Pré-condições:** Gateway Hermes cadastrado e ativo, usuário administrador logado  
- **Passos:**
  1. Acessar gateway Hermes
  2. Preencher formulário de cadastro de sensor
  3. Salvar novo sensor  
- **Resultado esperado:** Sensor cadastrado com sucesso e ID gerado
- **Fluxos Alternativos:**
  - **FA10.1:** Sensor já cadastrado (mesmo identificador)  
    - **Condição:** Tentativa de cadastrar sensor duplicado  
    - **Resultado:** Erro exibido, cadastro não realizado

---

## Testes de Controle de Acesso

### TC11 - Login como administrador
- **Objetivo:** Verificar acesso de administrador ao sistema  
- **Pré-condições:** Usuário administrador cadastrado, ativo e com permissão de acesso  
- **Passos:**
  1. Acessar página de login
  2. Inserir credenciais de administrador
  3. Submeter formulário  
- **Resultado esperado:** Acesso autorizado, menu completo visível
- **Fluxos Alternativos:**
  - **FA11.1:** Senha incorreta  
    - **Condição:** Senha digitada incorretamente  
    - **Resultado:** Acesso negado, mensagem de erro exibida
  - **FA11.2:** Usuário inativo  
    - **Condição:** Usuário está desativado  
    - **Resultado:** Acesso negado, mensagem de erro exibida

---

### TC12 - Login como usuário
- **Objetivo:** Verificar acesso de usuário comum ao sistema  
- **Pré-condições:** Usuário comum cadastrado, ativo e associado a uma empresa ativa  
- **Passos:**
  1. Acessar página de login
  2. Inserir credenciais de usuário
  3. Submeter formulário  
- **Resultado esperado:** Acesso autorizado, menu limitado visível
- **Fluxos Alternativos:**
  - **FA12.1:** Senha incorreta  
    - **Condição:** Senha digitada incorretamente  
    - **Resultado:** Acesso negado, mensagem de erro exibida
  - **FA12.2:** Usuário inativo  
    - **Condição:** Usuário está desativado  
    - **Resultado:** Acesso negado, mensagem de erro exibida
  - **FA12.3:** Empresa associada inativa  
    - **Condição:** Empresa do usuário está desativada  
    - **Resultado:** Acesso negado, mensagem de erro exibida

---

### TC13 - Tentativa de acesso não autorizado
- **Objetivo:** Verificar controle de acesso a funcionalidades restritas  
- **Pré-condições:** Usuário comum logado e ativo  
- **Passos:**
  1. Tentar acessar página de cadastro de empresas via URL direta  
- **Resultado esperado:** Acesso negado, redirecionamento para dashboard
- **Fluxos Alternativos:**
  - **FA13.1:** Usuário tenta acessar outra funcionalidade restrita  
    - **Condição:** Acesso a qualquer página restrita a administradores  
    - **Resultado:** Acesso negado, redirecionamento para dashboard

---

### TC14 - Cadastro de novo usuário
- **Objetivo:** Verificar funcionalidade de cadastro de usuário  
- **Pré-condições:** Usuário administrador logado, empresa cadastrada e ativa  
- **Passos:**
  1. Acessar página de usuários
  2. Preencher formulário de cadastro
  3. Definir tipo (ADMIN ou USER)
  4. Associar a uma empresa (para USER)
  5. Salvar novo usuário  
- **Resultado esperado:** Usuário cadastrado com sucesso
- **Fluxos Alternativos:**
  - **FA14.1:** E-mail já cadastrado  
    - **Condição:** Tentativa de cadastrar usuário com e-mail já existente  
    - **Resultado:** Erro exibido, cadastro não realizado

---

## Testes de Interface

### TC15 - Visualização de eventos por administrador
- **Objetivo:** Verificar visualização de eventos por administrador  
- **Pré-condições:** Usuário administrador logado, eventos registrados no sistema  
- **Passos:**
  1. Acessar página de eventos  
- **Resultado esperado:** Lista com eventos de todas as empresas visível
- **Fluxos Alternativos:**
  - **FA15.1:** Nenhum evento registrado  
    - **Condição:** Não há eventos no sistema  
    - **Resultado:** Mensagem de lista vazia exibida

---

### TC16 - Visualização de eventos por usuário
- **Objetivo:** Verificar visualização de eventos por usuário comum  
- **Pré-condições:** Usuário comum logado, empresa associada ativa, eventos da empresa registrados  
- **Passos:**
  1. Acessar página de eventos  
- **Resultado esperado:** Lista apenas com eventos da empresa associada
- **Fluxos Alternativos:**
  - **FA16.1:** Nenhum evento registrado para a empresa  
    - **Condição:** Não há eventos para a empresa do usuário  
    - **Resultado:** Mensagem de lista vazia exibida

---

### TC17 - Visualização de dashboard
- **Objetivo:** Verificar exibição de dashboard para usuário  
- **Pré-condições:** Usuário comum logado, empresa associada ativa, eventos da empresa registrados  
- **Passos:**
  1. Acessar página de dashboard  
- **Resultado esperado:** Dashboard com gráficos e estatísticas da empresa associada
- **Fluxos Alternativos:**
  - **FA17.1:** Nenhum dado para exibir  
    - **Condição:** Não há eventos ou dados para a empresa  
    - **Resultado:** Dashboard exibe mensagem de ausência de dados

---

Se precisar de mais fluxos alternativos ou detalhamento, é só pedir!
