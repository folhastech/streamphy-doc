# Descrição dos Casos de Uso - Sistema Midfield

---

## Processamento de Mensagens

- **Ator:** Gateway  
- **Descrição:** Receber, processar e encaminhar mensagens enviadas pelos gateways Iris via MQTT

### Fluxo Principal:
1. Sistema recebe mensagem no tópico `v1/event/{id}`
2. Sistema extrai o ID do gateway
3. Sistema verifica existência do gateway na base de dados
4. Sistema associa a mensagem à empresa correta
5. Sistema converte a mensagem de FlatBuffer para objeto Java
6. Sistema encaminha a mensagem processada via webhook ou MQTT conforme configuração da empresa

---

## Gerenciar Empresas

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir empresas no sistema

### Fluxo Principal:
1. Administrador acessa a página de empresas
2. Administrador visualiza lista de empresas cadastradas
3. Administrador pode adicionar, editar ou remover empresas

---

## Gerenciar Aplicativos

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir aplicativos associados a uma empresa

### Fluxo Principal:
1. Administrador seleciona uma empresa
2. Administrador visualiza aplicativos da empresa
3. Administrador pode adicionar, editar ou remover aplicativos

---

## Gerenciar Webhook/MQTT

- **Ator:** Administrador  
- **Descrição:** Permite configurar endpoints de webhook ou tópicos MQTT para aplicativos

### Fluxo Principal:
1. Administrador seleciona um aplicativo
2. Administrador configura webhook ou tópico MQTT para encaminhamento de mensagens
3. Administrador salva a configuração

---

## Gerenciar Gateways Iris

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir gateways Iris associados a aplicativos

### Fluxo Principal:
1. Administrador seleciona um aplicativo
2. Administrador visualiza gateways Iris cadastrados
3. Administrador pode adicionar, editar ou remover gateways Iris

---

## Gerenciar Gateways Hermes

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir gateways Hermes associados a um Iris

### Fluxo Principal:
1. Administrador seleciona um gateway Iris
2. Administrador visualiza gateways Hermes cadastrados
3. Administrador pode adicionar, editar ou remover gateways Hermes

---

## Gerenciar Sensores

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir sensores associados a um gateway Hermes

### Fluxo Principal:
1. Administrador seleciona um gateway Hermes
2. Administrador visualiza sensores cadastrados
3. Administrador pode adicionar, editar ou remover sensores

---

## Visualizar Eventos

- **Atores:** Administrador, Usuário  
- **Descrição:** Permite visualizar eventos processados pelo sistema

### Fluxo Principal:
1. Ator acessa a página de eventos
2. Administrador visualiza eventos de todas as empresas
3. Usuário visualiza apenas eventos da empresa associada

---

## Gerenciar Usuários

- **Ator:** Administrador  
- **Descrição:** Permite criar, editar e excluir usuários no sistema

### Fluxo Principal:
1. Administrador acessa a página de usuários
2. Administrador visualiza lista de usuários cadastrados
3. Administrador pode adicionar, editar ou remover usuários
4. Administrador define o tipo (ADMIN ou USER) e a empresa associada

---

## Visualizar Dashboard

- **Ator:** Usuário  
- **Descrição:** Permite visualizar dashboard com eventos e estatísticas da empresa

### Fluxo Principal:
1. Usuário acessa o dashboard
2. Usuário visualiza gráficos e estatísticas sobre eventos da empresa associada
