# Iris - Casos de teste

**CT-001 - Conexão ao WiFi após o flash do software**

- **Pré-condições**:
  1. O software deve ter sido corretamente "flashado" no dispositivo.
  2. O dispositivo deve estar desconectado de qualquer rede WiFi.

- **Passos para execução**:
  1. Conecte o dispositivo à tomada.
  2. Verifique se uma rede WiFi com o nome **"Iris-wifi"** foi criada.
  3. Conecte-se à rede **"Iris-wifi"** usando um dispositivo (ex.: smartphone ou laptop).
  4. Após a conexão, aguarde o redirecionamento automático para a página de configuração (captive portal).
  5. Na página de configuração:
     a. Escolha uma rede WiFi disponível.
     b. Insira a senha da rede selecionada.
     c. Clique no botão **"Salvar"**.
  6. Aguarde o dispositivo reiniciar automaticamente.

- **Entradas**:
  - Nome da rede WiFi: (ex.: "MinhaRedeWiFi").
  - Senha da rede WiFi: (ex.: "senha123").

- **Resultado esperado**:
  1. O dispositivo reinicia automaticamente após salvar as configurações.
  2. A rede **"Iris-wifi"** não aparece mais como disponível.
  3. O dispositivo conecta-se com sucesso à rede WiFi configurada.

- **Notas adicionais**:
  - Caso a rede **"Iris-wifi"** continue aparecendo após o reinício, o processo de configuração falhou.
  - Certifique-se de que a senha da rede WiFi foi inserida corretamente.


**CT-002 - Verificação da conexão LoRa e recebimento de logs**

- **Pré-condições**:
  1. O dispositivo Iris deve estar conectado à internet.
  2. O log do dispositivo Iris deve estar ativo e configurado para exibir informações no PC.
  3. O dispositivo Hermes deve estar configurado para enviar informações via LoRa a cada 10 segundos.

- **Passos para execução**:
  1. Certifique-se de que o dispositivo Iris está conectado à internet.
  2. Ative o log do dispositivo Iris e configure-o para exibir as informações no PC.
  3. Configure o dispositivo Hermes para enviar informações via LoRa a cada 10 segundos.
  4. No PC, monitore os logs recebidos do dispositivo Iris.

- **Entradas**:
  - Informações enviadas pelo dispositivo Hermes.

- **Resultado esperado**:
  1. Os logs no PC mostram as informações enviadas pelo dispositivo Hermes a cada 10 segundos.
  2. Não há falhas ou perdas de mensagens nos logs.
  3. As mensagens recebidas tem a tag "LoRa" e o campo de "payload" é != 0.

- **Notas adicionais**:
  - Caso os logs não sejam exibidos no PC, verifique:
    a. A conexão do dispositivo Iris com a internet.
    b. A configuração do log no dispositivo Iris.
    c. A configuração do dispositivo Hermes para envio via LoRa.
  - Se houver falhas ou perdas de mensagens, pode ser necessário verificar a qualidade do sinal LoRa, possíveis interferências, conexao com
  a antena e a frequencia correta.

**CT-003 - Verificação da integração e transmissão de mensagens**

- **Pré-condições**:
  1. O dispositivo Iris deve estar corretamente configurado e conectado à internet.
  2. O dispositivo Hermes deve estar configurado para enviar mensagens a cada 10 segundos.
  3. O painel do Midfield deve estar acessível e funcional.

- **Passos para execução**:
  1. Inicie o dispositivo Iris e conecte-o à internet.
  2. Certifique-se de que o dispositivo Hermes está configurado para enviar mensagens a cada 10 segundos.
  3. No painel do Midfield, localize o dispositivo Iris pelo seu ID.
  4. Verifique se as mensagens enviadas pelo dispositivo Hermes estão sendo recebidas no painel do Midfield.
  5. Confirme se as mensagens estão sendo:
     a. Recebidas com sucesso (sem falhas ou perdas).
     b. Decodificadas corretamente (conteúdo das mensagens está legível e conforme esperado).

- **Entradas**:
  - ID do dispositivo Iris no painel do Midfield.
  - Mensagens enviadas pelo dispositivo Hermes (ex.: "Mensagem de teste").

- **Resultado esperado**:
  1. As mensagens enviadas pelo dispositivo Hermes aparecem no painel do Midfield associadas ao ID do dispositivo Iris.
  2. As mensagens são recebidas a cada 10 segundos, sem falhas ou perdas.
  3. O conteúdo das mensagens é decodificado corretamente no painel do Midfield.

- **Notas adicionais**:
  - Caso as mensagens não sejam recebidas ou apresentem erros de decodificação, verifique:
    a. A conexão do dispositivo Iris com a internet.
    b. A configuração do dispositivo Hermes.
    c. O status do painel do Midfield.
  - Se o teste falhar, pode ser necessário refazer o processo de flash do dispositivo Iris.
