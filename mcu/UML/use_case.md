# **Documentação dos Casos de Uso**

## **Atores**

1. **Técnico da Streamphy**:
   - Responsável pela configuração inicial dos dispositivos (**Hermes** e **Iris**) utilizando o arquivo `config.ini`.
   - Atua antes do dispositivo ser entregue ao usuário final.

2. **Usuário**:
   - Responsável por configurar a rede Wi-Fi no dispositivo **Iris** (caso necessário) através do captive portal.
   - Atua apenas no dispositivo **Iris**.

3. **Servidor MQTT**:
   - Recebe os dados enviados pelo dispositivo **Iris** após o processamento das mensagens LoRa.

4. **Rede Wi-Fi**:
   - Representa a infraestrutura de rede à qual o dispositivo **Iris** se conecta para enviar dados ao servidor MQTT.

---

### **Casos de Uso do Hermes**

1. **UC1 - Configurar dispositivo via config.ini**:
   - **Ator**: Técnico da Streamphy.
   - **Descrição**: O técnico configura o dispositivo **Hermes** utilizando um arquivo `config.ini` que define os parâmetros de operação, como `DEVICE_ID`, `SENSOR_CONFIG`, `MESSAGE_INTERVAL`, entre outros.
   - **Fluxo principal**:
      - O técnico conecta o dispositivo Hermes ao computador via cabo USB.
      - O técnico abre o arquivo config.ini em um editor de texto.
      - O técnico insere os parâmetros necessários, como DEVICE_ID, SENSOR_CONFIG, MESSAGE_INTERVAL, etc.
      - O técnico salva o arquivo e o transfere para o dispositivo.
      - O técnico desliga o dispositivo e o reinicia para aplicar as configurações.
   - **Pré-condição**: O dispositivo deve estar desligado e acessível para configuração.
   - **Pós-condição**: O dispositivo está configurado e pronto para operação.

2. **UC2 - Coletar dados dos sensores**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo coleta dados dos sensores configurados no arquivo `config.ini` em intervalos definidos.
   - **Fluxo principal**:
     - O dispositivo inicia o processo de coleta de dados automaticamente após ser configurado e ligado.
     - O dispositivo lê os sensores configurados no arquivo config.ini.
     - Os dados coletados são armazenados na memória interna do dispositivo.
     - O processo se repete em intervalos definidos pelo parâmetro MESSAGE_INTERVAL.
   - **Pré-condição**: O dispositivo deve estar configurado e em operação.
   - **Pós-condição**: Os dados dos sensores são armazenados para transmissão.

3. **UC3 - Transmitir dados via LoRa**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo transmite os dados coletados para o gateway **Iris** utilizando o protocolo LoRa.
   - **Fluxo principal**:
      - O dispositivo verifica se há dados armazenados prontos para transmissão.
      - O dispositivo estabelece comunicação com o gateway Iris utilizando o protocolo LoRa.
      - Os dados são transmitidos ao gateway.
      - O dispositivo aguarda um ACK do gateway para confirmar o recebimento.
   - **Pré-condição**: Dados devem estar prontos para transmissão.
   - **Pós-condição**: Os dados são enviados ao gateway.

4. **UC4 - Fragmentar pacotes grandes**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: Caso o tamanho do pacote exceda 247 bytes, o dispositivo fragmenta os dados em pacotes menores antes de transmiti-los.
   - **Fluxo principal**:
      - O dispositivo verifica o tamanho do pacote de dados a ser transmitido.
      - Caso o tamanho exceda 247 bytes, o dispositivo divide os dados em pacotes menores.
      - Cada pacote fragmentado é preparado para transmissão.
      - O dispositivo transmite os pacotes fragmentados ao gateway Iris.
   - **Pré-condição**: O tamanho do pacote deve exceder o limite permitido.
   - **Pós-condição**: Os pacotes são fragmentados e prontos para transmissão.

5. **UC5 - Retransmitir pacotes em caso de falha**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo retransmite pacotes caso não receba um ACK dentro do tempo definido (`ACK_TIMEOUT`).
   - **Fluxo principal**:
      - O dispositivo transmite um pacote de dados ao gateway Iris.
      - O dispositivo aguarda um ACK dentro do tempo definido pelo parâmetro ACK_TIMEOUT.
      - Caso o ACK não seja recebido, o dispositivo retransmite o pacote.
      - O processo de retransmissão se repete até que o ACK seja recebido ou o número máximo de tentativas seja atingido.
   - **Pré-condição**: O dispositivo deve estar aguardando um ACK.
   - **Pós-condição**: O pacote é retransmitido ou o número máximo de tentativas é atingido.

6. **UC6 - Coletar dados continuamente (CONTINUOUS_COLLECT_TIME)**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo realiza coletas contínuas de dados dos sensores durante o tempo definido por `CONTINUOUS_COLLECT_TIME`, caso configurado.
   - **Fluxo principal**:
      - O dispositivo verifica se o parâmetro CONTINUOUS_COLLECT_TIME está configurado.
      - O dispositivo inicia a coleta contínua de dados dos sensores.
      - Os dados coletados são armazenados na memória interna do dispositivo.
      - O processo de coleta contínua termina quando o tempo definido por CONTINUOUS_COLLECT_TIME expira.
   - **Pré-condição**: O parâmetro `CONTINUOUS_COLLECT_TIME` deve estar configurado.
   - **Pós-condição**: Os dados coletados continuamente são armazenados para transmissão.

---

### **Casos de Uso do Iris**

1. **UC7 - Configurar dispositivo via config.ini**:
   - **Ator**: Técnico da Streamphy.
   - **Descrição**: O técnico configura o dispositivo **Iris** utilizando um arquivo `config.ini` que define os parâmetros de operação, como `DEVICE_ID`, `SSID`, `PASS`, `SERVER_URL`, entre outros.
   - **Fluxo principal**:
      - O técnico conecta o dispositivo Iris ao computador via cabo USB.
      - O técnico abre o arquivo config.ini em um editor de texto.
      - O técnico insere os parâmetros necessários, como DEVICE_ID, SSID, PASS, SERVER_URL, etc.
      - O técnico salva o arquivo e o transfere para o dispositivo.
      - O técnico desliga o dispositivo e o reinicia para aplicar as configurações.
   - **Pré-condição**: O dispositivo deve estar desligado e acessível para configuração.
   - **Pós-condição**: O dispositivo está configurado e pronto para operação.

2. **UC8 - Conectar à rede Wi-Fi**:
   - **Ator**: Usuário.
   - **Descrição**: O dispositivo tenta se conectar automaticamente à rede Wi-Fi configurada no arquivo `config.ini`.
   - **Fluxo principal**:
      - O dispositivo lê as credenciais da rede Wi-Fi configuradas no arquivo config.ini.
      - O dispositivo tenta se conectar à rede Wi-Fi utilizando as credenciais fornecidas.
      - Caso a conexão seja bem-sucedida, o dispositivo entra em operação normal.
      - Caso a conexão falhe, o dispositivo inicia o processo descrito no UC9.
   - **Pré-condição**: O arquivo `config.ini` deve conter as credenciais da rede Wi-Fi.
   - **Pós-condição**: O dispositivo está conectado à rede Wi-Fi.

3. **UC9 - Abrir AP com captive portal**:
   - **Ator**: Usuário.
   - **Descrição**: Caso a conexão Wi-Fi falhe, o dispositivo abre um Access Point (AP) com um captive portal para que o usuário configure uma nova rede.
   - **Fluxo principal**:
      - O dispositivo verifica que não conseguiu se conectar à rede Wi-Fi configurada.
      - O dispositivo abre um Access Point (AP) com um captive portal.
      - O usuário conecta ao AP e acessa o captive portal via navegador.
      - O usuário insere as credenciais da nova rede Wi-Fi no captive portal.
      - O dispositivo tenta se conectar à nova rede configurada.
   - **Pré-condição**: O dispositivo não conseguiu se conectar à rede Wi-Fi configurada.
   - **Pós-condição**: O dispositivo está pronto para tentar se conectar à nova rede configurada.

4. **UC10 - Receber pacotes LoRa**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo escuta continuamente por pacotes LoRa enviados pelo **Hermes**.
   - **Fluxo principal**:
      - O dispositivo Iris entra em modo de escuta para pacotes LoRa.
      - O dispositivo verifica continuamente se há pacotes sendo enviados pelo Hermes.
      - Quando um pacote é recebido, ele é armazenado na memória interna para processamento.
   - **Pré-condição**: O dispositivo deve estar em operação.
   - **Pós-condição**: Os pacotes LoRa são recebidos e armazenados para processamento.

5. **UC11 - Montar mensagens completas**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: Caso os pacotes LoRa recebidos estejam fragmentados, o dispositivo monta a mensagem completa antes de enviá-la ao servidor MQTT.
   - **Fluxo principal**:
      - O dispositivo verifica se os pacotes LoRa recebidos estão fragmentados.
      - Caso estejam fragmentados, o dispositivo monta a mensagem completa utilizando os pacotes recebidos.
      - A mensagem completa é armazenada na memória interna e preparada para envio ao servidor MQTT.
   - **Pré-condição**: Pacotes fragmentados devem ter sido recebidos.
   - **Pós-condição**: A mensagem completa está pronta para envio.

6. **UC12 - Enviar dados ao servidor MQTT**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo envia os dados processados ao servidor MQTT configurado no arquivo `config.ini`.
   - **Fluxo principal**:
      - O dispositivo verifica se há dados processados prontos para envio.
      - O dispositivo estabelece comunicação com o servidor MQTT configurado no arquivo config.ini.
      - Os dados são enviados ao servidor MQTT.
      - O dispositivo aguarda uma confirmação de recebimento do servidor.
   - **Pré-condição**: Os dados devem estar prontos para envio.
   - **Pós-condição**: Os dados são enviados ao servidor MQTT.

7. **UC13 - Operar continuamente (escutar e processar mensagens)**:
   - **Ator**: Nenhum (processo automático).
   - **Descrição**: O dispositivo retorna ao estado de escuta após processar cada mensagem, operando continuamente.
   - **Fluxo principal**:
      - O dispositivo entra em modo de escuta após processar cada mensagem.
      - O dispositivo verifica continuamente se há novas mensagens ou pacotes LoRa sendo recebidos.
      - Quando uma nova mensagem ou pacote é recebido, o dispositivo inicia o processo de processamento e envio.
      - O dispositivo retorna ao estado de escuta após concluir o processamento.
   - **Pré-condição**: O dispositivo deve estar em operação.
   - **Pós-condição**: O dispositivo está pronto para processar a próxima mensagem.
