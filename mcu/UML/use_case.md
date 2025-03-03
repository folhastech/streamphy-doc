### **Documentação dos Casos de Uso**

#### **Atores**
1. **Técnico da Streamphy**:
   - Responsável pela configuração inicial dos dispositivos (**Hermes** e **Iris**) utilizando o arquivo `config.txt`.
   - Atua antes do dispositivo ser entregue ao usuário final.

2. **Usuário**:
   - Responsável por configurar a rede Wi-Fi no dispositivo **Iris** (caso necessário) através do captive portal.
   - Atua apenas no dispositivo **Iris**.

3. **Servidor MQTT**:
   - Recebe os dados enviados pelo dispositivo **Iris** após o processamento das mensagens LoRa.

4. **Rede Wi-Fi**:
   - Representa a infraestrutura de rede à qual o dispositivo **Iris** se conecta para enviar dados ao servidor MQTT.

---

#### **Casos de Uso do Hermes**

1. **UC1 - Configurar dispositivo via config.txt**:
   - **Ator**: Técnico da Streamphy.
   - **Descrição**: O técnico configura o dispositivo **Hermes** utilizando um arquivo `config.txt` que define os parâmetros de operação, como `DEVICE_ID`, `SENSOR_CONFIG`, `MESSAGE_INTERVAL`, entre outros.
   - **Pré-condição**: O dispositivo deve estar desligado e acessível para configuração.
   - **Pós-condição**: O dispositivo está configurado e pronto para operação.

2. **UC2 - Coletar dados dos sensores**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo coleta dados dos sensores configurados no arquivo `config.txt` em intervalos definidos.
   - **Pré-condição**: O dispositivo deve estar configurado e em operação.
   - **Pós-condição**: Os dados dos sensores são armazenados para transmissão.

3. **UC3 - Transmitir dados via LoRa**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo transmite os dados coletados para o gateway **Iris** utilizando o protocolo LoRa.
   - **Pré-condição**: Dados devem estar prontos para transmissão.
   - **Pós-condição**: Os dados são enviados ao gateway.

4. **UC4 - Fragmentar pacotes grandes**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: Caso o tamanho do pacote exceda 246 bytes, o dispositivo fragmenta os dados em pacotes menores antes de transmiti-los.
   - **Pré-condição**: O tamanho do pacote deve exceder o limite permitido.
   - **Pós-condição**: Os pacotes são fragmentados e prontos para transmissão.

5. **UC5 - Retransmitir pacotes em caso de falha**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo retransmite pacotes caso não receba um ACK dentro do tempo definido (`ACK_TIMEOUT`).
   - **Pré-condição**: O dispositivo deve estar aguardando um ACK.
   - **Pós-condição**: O pacote é retransmitido ou o número máximo de tentativas é atingido.

6. **UC6 - Coletar dados continuamente (CONTINUOUS_COLLECT_TIME)**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo realiza coletas contínuas de dados dos sensores durante o tempo definido por `CONTINUOUS_COLLECT_TIME`, caso configurado.
   - **Pré-condição**: O parâmetro `CONTINUOUS_COLLECT_TIME` deve estar configurado.
   - **Pós-condição**: Os dados coletados continuamente são armazenados para transmissão.

---

#### **Casos de Uso do Iris**

1. **UC7 - Configurar dispositivo via config.txt**:
   - **Ator**: Técnico da Streamphy.
   - **Descrição**: O técnico configura o dispositivo **Iris** utilizando um arquivo `config.txt` que define os parâmetros de operação, como `DEVICE_ID`, `SSID`, `PASS`, `SERVER_URL`, entre outros.
   - **Pré-condição**: O dispositivo deve estar desligado e acessível para configuração.
   - **Pós-condição**: O dispositivo está configurado e pronto para operação.

2. **UC8 - Conectar à rede Wi-Fi**:
   - **Ator**: Usuário.
   - **Descrição**: O dispositivo tenta se conectar automaticamente à rede Wi-Fi configurada no arquivo `config.txt`.
   - **Pré-condição**: O arquivo `config.txt` deve conter as credenciais da rede Wi-Fi.
   - **Pós-condição**: O dispositivo está conectado à rede Wi-Fi.

3. **UC9 - Abrir AP com captive portal**:
   - **Ator**: Usuário.
   - **Descrição**: Caso a conexão Wi-Fi falhe, o dispositivo abre um Access Point (AP) com um captive portal para que o usuário configure uma nova rede.
   - **Pré-condição**: O dispositivo não conseguiu se conectar à rede Wi-Fi configurada.
   - **Pós-condição**: O dispositivo está pronto para tentar se conectar à nova rede configurada.

4. **UC10 - Receber pacotes LoRa**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo escuta continuamente por pacotes LoRa enviados pelo **Hermes**.
   - **Pré-condição**: O dispositivo deve estar em operação.
   - **Pós-condição**: Os pacotes LoRa são recebidos e armazenados para processamento.

5. **UC11 - Montar mensagens completas**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: Caso os pacotes LoRa recebidos estejam fragmentados, o dispositivo monta a mensagem completa antes de enviá-la ao servidor MQTT.
   - **Pré-condição**: Pacotes fragmentados devem ter sido recebidos.
   - **Pós-condição**: A mensagem completa está pronta para envio.

6. **UC12 - Enviar dados ao servidor MQTT**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo envia os dados processados ao servidor MQTT configurado no arquivo `config.txt`.
   - **Pré-condição**: Os dados devem estar prontos para envio.
   - **Pós-condição**: Os dados são enviados ao servidor MQTT.

7. **UC13 - Operar continuamente (escutar e processar mensagens)**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo retorna ao estado de escuta após processar cada mensagem, operando continuamente.
   - **Pré-condição**: O dispositivo deve estar em operação.
   - **Pós-condição**: O dispositivo está pronto para processar a próxima mensagem.
