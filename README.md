# README - Monitoramento de Temperatura e Umidade com ESP32 e MQTT

Este projeto utiliza um ESP32 para monitorar a temperatura e a umidade usando um sensor DHT22 e enviar os dados para um broker MQTT, permitindo o monitoramento remoto via protocolo MQTT.

## Componentes Utilizados

- **ESP32**: Microcontrolador com suporte a Wi-Fi.
- **DHT22**: Sensor de temperatura e umidade.
- **Broker MQTT**: Servidor MQTT usado para enviar e receber mensagens (neste caso, `broker.hivemq.com`).

## Bibliotecas Utilizadas

- **WiFi.h**: Para conexão à rede Wi-Fi.
- **PubSubClient.h**: Para comunicação MQTT.
- **DHTesp.h**: Para interação com o sensor DHT22.

## Funcionalidades

1. **Conexão Wi-Fi**: O ESP32 se conecta à rede Wi-Fi especificada.
2. **Publicação MQTT**: O ESP32 publica a temperatura e a umidade coletadas pelo sensor DHT22 em tópicos MQTT a cada 2 segundos.
    - Tópico de temperatura: `iotfrontier/temperature`
    - Tópico de umidade: `iotfrontier/humidity`
3. **Recepção MQTT**: O ESP32 se inscreve no tópico `iotfrontier/mqtt` e aciona um LED conforme o payload recebido.
    - Payload `'1'`: Liga o LED.
    - Qualquer outro valor: Desliga o LED.

## Como Funciona

1. **Conexão com a rede Wi-Fi**: A função `setup_wifi()` gerencia a conexão à rede.
2. **Comunicação MQTT**: 
    - O ESP32 se conecta ao broker MQTT e publica os dados do sensor de temperatura e umidade.
    - Se a conexão for perdida, o ESP tenta reconectar automaticamente.
3. **Leitura do Sensor**: O sensor DHT22 é lido a cada 2 segundos. Os valores de temperatura e umidade são publicados nos respectivos tópicos MQTT.
4. **Callback MQTT**: Quando uma mensagem é recebida no tópico `iotfrontier/mqtt`, o LED é acionado dependendo do valor do payload.

## Configuração do Ambiente

1. Conecte o ESP32 ao sensor DHT22 no pino 9 (DHT_PIN).
2. Compile e carregue o código no ESP32 usando a IDE Arduino.
3. Configure a rede Wi-Fi alterando o SSID e a senha conforme necessário:
    ```cpp
    const char* ssid = "Wokwi-GUEST";
    const char* password = "";
    ```

## Tópicos MQTT

- `iotfrontier/temperature`: Publica a temperatura lida pelo DHT22.
- `iotfrontier/humidity`: Publica a umidade lida pelo DHT22.
- `iotfrontier/mqtt`: Tópico onde o ESP32 escuta comandos para ligar ou desligar o LED.

## Observações

- O LED está conectado ao pino 2 do ESP32 e é controlado pelo payload das mensagens MQTT.
- O broker MQTT utilizado é público (`broker.hivemq.com`), o que significa que os dados são acessíveis publicamente.

## Licença

Este projeto é de código aberto e pode ser modificado e distribuído livremente.
