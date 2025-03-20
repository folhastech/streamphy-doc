# Descrição dos Casos de Teste

---

## Testes de Processamento de Mensagens

### TC01 - Processamento com sucesso via webhook
- **Objetivo:** Verificar se o sistema processa corretamente mensagens e envia via webhook  
- **Pré-condições:** Gateway Iris, empresa e webhook configurados corretamente  
- **Passos:**
  1. Enviar mensagem válida para tópico `v1/event/{id}`
  2. Verificar processamento da mensagem
  3. Verificar envio para webhook  
- **Resultado esperado:** Mensagem processada e enviada, evento registrado no banco

### TC02 - Processamento com sucesso via MQTT
- **Objetivo:** Verificar se o sistema processa corretamente mensagens e envia via MQTT  
- **Pré-condições:** Gateway Iris, empresa e tópico MQTT configurados corretamente  
- **Passos:**
  1. Enviar mensagem válida para tópico `v1/event/{id}`
  2. Verificar processamento da mensagem
  3. Verificar publicação no tópico MQTT  
- **Resultado esperado:** Mensagem processada e publicada, evento registrado no banco

### TC03 - Gateway não encontrado
- **Objetivo:** Verificar tratamento de erro quando gateway não existe  
- **Pré-condições:** ID de gateway inexistente  
- **Passos:**
  1. Enviar mensagem para tópico com ID inexistente  
- **Resultado esperado:** Erro registrado, processamento interrompido

### TC04 - Empresa não encontrada
- **Objetivo:** Verificar tratamento de erro quando empresa não está associada ao gateway  
- **Pré-condições:** Gateway sem associação com empresa  
- **Passos:**
  1. Enviar mensagem para tópico com ID de gateway sem empresa  
- **Resultado esperado:** Erro registrado, processamento interrompido

### TC05 - Erro na conversão da mensagem
- **Objetivo:** Verificar tratamento de erro na conversão de FlatBuffer para objeto Java  
- **Pré-condições:** Gateway e empresa configurados  
- **Passos:**
  1. Enviar mensagem inválida/mal-formada  
- **Resultado esperado:** Erro de conversão registrado, processamento interrompido

---

## Testes de Gestão de Cadastros

### TC06 - Cadastro de empresa
- **Objetivo:** Verificar funcionalidade de cadastro de empresa  
- **Pré-condições:** Usuário administrador logado  
- **Passos:**
  1. Acessar página de empresas
  2. Preencher formulário de cadastro
  3. Salvar nova empresa  
- **Resultado esperado:** Empresa cadastrada com sucesso

### TC07 - Cadastro de aplicativo
- **Objetivo:** Verificar funcionalidade de cadastro de aplicativo  
- **Pré-condições:** Empresa cadastrada, usuário administrador logado  
- **Passos:**
  1. Acessar empresa
  2. Preencher formulário de cadastro de aplicativo
  3. Salvar novo aplicativo  
- **Resultado esperado:** Aplicativo cadastrado com sucesso

### TC08 - Cadastro de gateway Iris
- **Objetivo:** Verificar funcionalidade de cadastro de gateway Iris  
- **Pré-condições:** Aplicativo cadastrado, usuário administrador logado  
- **Passos:**
  1. Acessar aplicativo
  2. Preencher formulário de cadastro de gateway Iris
  3. Salvar novo gateway  
- **Resultado esperado:** Gateway Iris cadastrado com sucesso e ID gerado

### TC09 - Cadastro de gateway Hermes
- **Objetivo:** Verificar funcionalidade de cadastro de gateway Hermes  
- **Pré-condições:** Gateway Iris cadastrado, usuário administrador logado  
- **Passos:**
  1. Acessar gateway Iris
  2. Preencher formulário de cadastro de gateway Hermes
  3. Salvar novo gateway  
- **Resultado esperado:** Gateway Hermes cadastrado com sucesso

### TC10 - Cadastro de sensor
- **Objetivo:** Verificar funcionalidade de cadastro de sensor  
- **Pré-condições:** Gateway Hermes cadastrado, usuário administrador logado  
- **Passos:**
  1. Acessar gateway Hermes
  2. Preencher formulário de cadastro de sensor
  3. Salvar novo sensor  
- **Resultado esperado:** Sensor cadastrado com sucesso e ID gerado

---

## Testes de Controle de Acesso

### TC11 - Login como administrador
- **Objetivo:** Verificar acesso de administrador ao sistema  
- **Pré-condições:** Usuário administrador cadastrado  
- **Passos:**
  1. Acessar página de login
  2. Inserir credenciais de administrador
  3. Submeter formulário  
- **Resultado esperado:** Acesso autorizado, menu completo visível

### TC12 - Login como usuário
- **Objetivo:** Verificar acesso de usuário comum ao sistema  
- **Pré-condições:** Usuário comum cadastrado e associado a uma empresa  
- **Passos:**
  1. Acessar página de login
  2. Inserir credenciais de usuário
  3. Submeter formulário  
- **Resultado esperado:** Acesso autorizado, menu limitado visível

### TC13 - Tentativa de acesso não autorizado
- **Objetivo:** Verificar controle de acesso a funcionalidades restritas  
- **Pré-condições:** Usuário comum logado  
- **Passos:**
  1. Tentar acessar página de cadastro de empresas via URL direta  
- **Resultado esperado:** Acesso negado, redirecionamento para dashboard

### TC14 - Cadastro de novo usuário
- **Objetivo:** Verificar funcionalidade de cadastro de usuário  
- **Pré-condições:** Usuário administrador logado, empresa cadastrada  
- **Passos:**
  1. Acessar página de usuários
  2. Preencher formulário de cadastro
  3. Definir tipo (ADMIN ou USER)
  4. Associar a uma empresa (para USER)
  5. Salvar novo usuário  
- **Resultado esperado:** Usuário cadastrado com sucesso

---

## Testes de Interface

### TC15 - Visualização de eventos por administrador
- **Objetivo:** Verificar visualização de eventos por administrador  
- **Pré-condições:** Usuário administrador logado, eventos registrados  
- **Passos:**
  1. Acessar página de eventos  
- **Resultado esperado:** Lista com eventos de todas as empresas visível

### TC16 - Visualização de eventos por usuário
- **Objetivo:** Verificar visualização de eventos por usuário comum  
- **Pré-condições:** Usuário comum logado, eventos da empresa associada registrados  
- **Passos:**
  1. Acessar página de eventos  
- **Resultado esperado:** Lista apenas com eventos da empresa associada

### TC17 - Visualização de dashboard
- **Objetivo:** Verificar exibição de dashboard para usuário  
- **Pré-condições:** Usuário comum logado, eventos da empresa associada registrados  
- **Passos:**
  1. Acessar página de dashboard  
- **Resultado esperado:** Dashboard com gráficos e estatísticas da empresa associada
