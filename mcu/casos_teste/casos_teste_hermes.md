# Hermes - Casos de teste

**CT-001 - Verificação da coleta de dados de sensores digitais**

- **Pré-condições**:
  1. O dispositivo Hermes deve estar corretamente configurado e com o firmware (flash) contendo a especificação de sensor digital para as portas 01, 02 e 03.
  2. Um switch deve estar disponível para simular os sinais digitais.
  3. O log do dispositivo Hermes deve estar ativo e acessível no PC.

- **Passos para execução**:
  1. Conecte o switch à porta 01 de sensores do dispositivo Hermes.
  2. Ligue o dispositivo Hermes.
  3. Certifique-se, nos logs, de que o dispositivo reconheceu a especificação de sensor digital na porta 01.
  4. Acione o switch (ligar/desligar) 5 vezes.
  5. Verifique nos logs se o contador de mensagens do sensor 01 aumentou em 5 unidades.
  6. Repita o processo para as portas 02 e 03:
     a. Conecte o switch à porta correspondente.
     b. Acione o switch 5 vezes.
     c. Verifique nos logs se o contador de mensagens da porta correspondente aumentou em 5 unidades.

- **Entradas**:
  - Sinal digital gerado pelo switch (ligar/desligar).

- **Resultado esperado**:
  1. Para cada porta (01, 02 e 03), o contador de mensagens no log aumenta em 5 unidades após 5 acionamentos do switch.
  2. O dispositivo reconhece corretamente os sinais digitais enviados pelo switch.

- **Notas adicionais**:
  - Caso o contador de mensagens não aumente ou aumente de forma incorreta, verifique:
    a. A especificação do firmware (flash) para as portas de sensores.
    b. A conexão do switch às portas do dispositivo Hermes.
    c. A funcionalidade do switch utilizado no teste.
  - Se o problema persistir, pode ser necessário refazer o processo de flash do dispositivo.


**CT-002 - Verificação da coleta de dados de sensores analógicos**

- **Pré-condições**:
  1. O dispositivo Hermes deve estar corretamente configurado e com o firmware (flash) contendo a especificação de sensor analógico para as portas 01, 02 e 03.
  2. Um sensor analógico ou simulador de sinal analógico deve estar disponível para o teste.
  3. O log do dispositivo Hermes deve estar ativo e acessível no PC.

- **Passos para execução**:
  1. Conecte o sensor analógico (ou simulador) à porta 01 de sensores do dispositivo Hermes.
  2. Ligue o dispositivo Hermes.
  3. Certifique-se, nos logs, de que o dispositivo reconheceu a especificação de sensor analógico na porta 01.
  4. Gere diferentes valores de entrada analógica no sensor (ex.: 1V, 2V, 3V, etc.).
  5. Verifique nos logs se os valores lidos pelo dispositivo correspondem aos valores gerados pelo sensor.
  6. Repita o processo para as portas 02 e 03:
     a. Conecte o sensor analógico à porta correspondente.
     b. Gere diferentes valores de entrada analógica.
     c. Verifique nos logs se os valores lidos pelo dispositivo correspondem aos valores gerados pelo sensor.

- **Entradas**:
  - Sinais analógicos gerados pelo sensor (ex.: 0000, 0798, 1298, 4096).

- **Resultado esperado**:
  1. Para cada porta (01, 02 e 03), os valores lidos pelo dispositivo nos logs correspondem aos valores gerados pelo sensor analógico.
  2. O dispositivo reconhece corretamente os sinais analógicos enviados pelo sensor.

- **Notas adicionais**:
  - Caso os valores lidos pelo dispositivo não correspondam aos valores gerados pelo sensor, verifique:
    a. A especificação do firmware (flash) para as portas de sensores.
    b. A conexão do sensor analógico às portas do dispositivo Hermes.
    c. A funcionalidade do sensor analógico ou simulador utilizado no teste.
  - Se o problema persistir, pode ser necessário refazer o processo de flash do dispositivo ou recalibrar o sensor.


**CT-003 - Verificação da conexão entre Hermes e Iris**

- **Pré-condições**:
  1. O dispositivo Hermes deve estar configurado para enviar mensagens a cada 10 segundos.
  2. O ID do dispositivo Iris de teste deve estar configurado no Hermes antes do flash.
  3. O firmware (flash) do Hermes deve estar atualizado e corretamente configurado.
  4. O dispositivo Iris deve estar ligado e funcional.
  5. O log do dispositivo Hermes deve estar ativo e acessível no PC.

- **Passos para execução**:
  1. Certifique-se de que o dispositivo Hermes está configurado para enviar mensagens a cada 10 segundos.
  2. Configure o ID do dispositivo Iris de teste no Hermes.
  3. Realize o flash do dispositivo Hermes com as configurações acima.
  4. Ligue o dispositivo Hermes.
  5. Certifique-se de que o dispositivo Iris está ligado e funcional.
  6. Monitore os logs do dispositivo Hermes e verifique o seguinte:
     a. A cada 10 segundos, deve haver um log indicando o envio de uma mensagem para o Iris.
     b. Após cada envio, deve haver um log de "ACK" (confirmação de recebimento) do Iris.
  7. Observe o comportamento em caso de falhas:
     a. Se o "ACK" falhar até 3 vezes consecutivas, considere normal devido a possíveis interferências.
     b. Se o "ACK" não for recebido após 3 tentativas, verifique as configurações do Hermes e do Iris.

- **Entradas**:
  - ID do dispositivo Iris configurado no Hermes.
  - Mensagens enviadas pelo Hermes a cada 10 segundos.

- **Resultado esperado**:
  1. A cada 10 segundos, o Hermes envia uma mensagem para o Iris, e o log registra o envio.
  2. Após cada envio, o log registra um "ACK" recebido do Iris.
  3. No caso de falhas de "ACK", até 3 tentativas consecutivas são consideradas normais devido a interferências.
  4. Se o "ACK" não for recebido após 3 tentativas, o problema deve ser investigado.

- **Notas adicionais**:
  - Caso o "ACK" não seja recebido consistentemente, verifique:
    a. As configurações do Hermes (ID do Iris, frequência, potência de transmissão).
    b. As configurações do Iris (frequência, antena, ID configurado).
    c. A integridade das antenas e a qualidade do sinal.
  - Certifique-se de que ambos os dispositivos estão operando na mesma frequência e com as antenas corretamente conectadas.
