**Análise de Requisitos do Sistema Hermes e Iris**

---

### **Requisitos Funcionais (RF)**

**Hermes (Coletor de Dados):**

[RF001]: O sistema deve permitir a configuração inicial do dispositivo através de um arquivo `config.txt`.

[RF002]: O sistema deve realizar a coleta de dados dos sensores configurados no arquivo `config.txt`.

[RF003]: O sistema deve transmitir os dados coletados via LoRa para o gateway Iris.

[RF004]: O sistema deve suportar a transmissão de pacotes fragmentados caso o tamanho do pacote exceda 246 bytes.

[RF005]: O sistema deve implementar um mecanismo de retransmissão baseado em `ACK_TIMEOUT` e `RETRY_COUNT` definidos no arquivo de configuração.

[RF006]: O sistema deve utilizar o formato FlatBuffer para serializar os dados antes da transmissão.

[RF007]: O sistema deve permitir a coleta contínua de dados de sensores, respeitando o intervalo configurado em `CONTINUOUS_COLLECT_TIME`.

[RF008]: O sistema deve identificar cada sensor por um `ID` único e enviar os dados associados a ele.

---

**Iris (Gateway):**

[RF009]: O sistema deve permitir a configuração inicial do dispositivo através de um arquivo `config.txt`.

[RF010]: O sistema deve escutar continuamente por pacotes LoRa enviados pelo Hermes.

[RF011]: O sistema deve montar mensagens completas a partir de pacotes fragmentados recebidos.

[RF012]: O sistema deve enviar os dados recebidos para um servidor MQTT configurado no arquivo `config.txt`.

[RF013]: O sistema deve se conectar automaticamente à rede Wi-Fi configurada no arquivo `config.txt`.

[RF014]: Caso não haja configuração de Wi-Fi ou a conexão falhe, o sistema deve abrir um Access Point (AP) com um captive portal.

[RF015]: O captive portal deve listar as redes Wi-Fi disponíveis e permitir a configuração de uma nova rede.

[RF016]: O sistema deve desligar o AP automaticamente após uma conexão Wi-Fi bem-sucedida.

[RF017]: O sistema deve implementar um mecanismo de reconexão automática em caso de falha na conexão Wi-Fi.

---

### **Requisitos Não Funcionais (RNF)**

[RNF001]: O sistema Hermes deve operar com baixo consumo de energia, adequado para dispositivos IoT baseados em ESP32.

[RNF002]: O sistema Iris deve suportar conexões MQTT com baixa latência e alta confiabilidade.

[RNF003]: O formato de serialização FlatBuffer deve ser utilizado para garantir eficiência na transmissão de dados.

[RNF004]: O sistema deve ser capaz de operar em ambientes com baixa largura de banda, como redes LoRa.

[RNF005]: O sistema deve ser modular, permitindo a adição de novos tipos de sensores no Hermes sem grandes alterações no código.

[RNF006]: O sistema deve ser robusto contra falhas de comunicação, implementando mecanismos de retransmissão e validação de pacotes (CRC).

[RNF007]: O captive portal do Iris deve ser responsivo e compatível com dispositivos móveis.

[RNF008]: O sistema deve ser capaz de operar em temperaturas entre -20°C e 60°C, considerando o uso em ambientes externos.

[RNF009]: O tempo de boot do Hermes e do Iris deve ser inferior a 5 segundos.

[RNF010]: O sistema deve suportar até 10 sensores simultâneos no Hermes.

---

### **Requisitos de Domínio (RD)**

[RD001]: O sistema Hermes deve ser baseado no microcontrolador ESP32.

[RD002]: O sistema Iris deve ser compatível com o protocolo LoRa para comunicação com o Hermes.

[RD003]: O sistema Iris deve suportar o protocolo MQTT para envio de dados ao servidor.

[RD004]: O sistema deve utilizar o formato FlatBuffer para serialização de dados, conforme o esquema fornecido.

[RD005]: O sistema deve respeitar o limite de 246 bytes por pacote na transmissão LoRa.

[RD006]: O sistema deve implementar um mecanismo de validação de pacotes utilizando CRC.

[RD007]: O sistema deve ser configurável através de arquivos `config.txt` com parâmetros específicos para cada dispositivo.

[RD008]: O sistema deve operar em conformidade com as regulamentações de frequência e potência para dispositivos LoRa no país de operação.

[RD009]: O sistema deve ser capaz de identificar e gerenciar redes Wi-Fi disponíveis para configuração do Iris.

[RD010]: O sistema deve garantir a integridade dos dados transmitidos entre o Hermes e o Iris.
