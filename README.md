# MQTT Button and LED Control with ESP32

## Equipe
- **Leonardo Victor**
- **Rafael Felix**
- **Victor Machado**

## Descrição do Projeto
Este projeto implementa uma aplicação para ESP32 que utiliza o protocolo MQTT para comunicação com um broker MQTT. O objetivo é controlar um LED remotamente e monitorar o estado de um botão físico.

### Funcionalidades
1. **Publicação do Estado do Botão**:
   - O ESP32 monitora o estado de um botão conectado ao GPIO 14 e publica seu estado ("ON" ou "OFF") no tópico `/esp32/led`.

2. **Controle do LED via MQTT**:
   - O ESP32 se inscreve no tópico `/esp32/led` e controla o LED conectado ao GPIO 27 com base nas mensagens recebidas ("ON" para ligar e "OFF" para desligar).

3. **Eventos MQTT**:
   - Gerencia eventos como conexão, desconexão, publicação, assinatura e recebimento de mensagens.

### Configuração do Broker MQTT
- **Broker**: HiveMQ
- **Tópico para Publicação**: `/esp32/led`
- **Tópico para Assinatura**: `/esp32/led`
- **Usuário**: `ESP32`
- **Senha**: `Senha1234`
- **Protocolo**: MQTT 3.1.1

### Configuração do Hardware
- **Botão**: Conectado ao GPIO 14.
- **LED**: Conectado ao GPIO 27.

### Como Executar
1. Configure o broker MQTT no HiveMQ.
2. Compile e carregue o código no ESP32.
3. Certifique-se de que o ESP32 está conectado à rede Wi-Fi configurada.
4. Use um cliente MQTT para enviar mensagens ao tópico `/esp32/led` e controlar o LED.
5. Monitore o estado do botão no mesmo tópico.

### Melhorias no Arquivo `app_main.c`

1. **Adição de Controle de Hardware**:
   - Foram adicionadas funções para configurar o LED (GPIO 27) e o botão (GPIO 14), permitindo o controle físico do LED e a leitura do estado do botão.

2. **Publicação do Estado do Botão**:
   - Foi implementada uma tarefa (`button_task`) que monitora continuamente o estado do botão e publica seu estado ("ON" ou "OFF") no tópico `/esp32/led` do broker MQTT.

3. **Controle do LED via Mensagens MQTT**:
   - O código foi ajustado para interpretar mensagens recebidas no tópico `/esp32/led`. Com isso, o LED pode ser ligado ou desligado remotamente ao receber as mensagens "ON" ou "OFF".

4. **Configuração do Broker MQTT**:
   - Adicionada autenticação no broker MQTT com usuário (`ESP32`) e senha (`Senha1234`), além de utilizar o protocolo MQTT 3.1.1 para maior compatibilidade.

5. **Uso de Variável Global para o Cliente MQTT**:
   - Foi introduzida uma variável global (`global_mqtt_client`) para facilitar o acesso ao cliente MQTT em diferentes partes do código, como na tarefa do botão e no manipulador de eventos.

6. **Estrutura do Loop Principal**:
   - O loop principal foi alterado para manter a execução contínua, garantindo que as tarefas e eventos sejam processados indefinidamente.

Essas melhorias tornam o código mais adequado para o objetivo do projeto, permitindo o controle remoto do LED e a publicação do estado do botão de forma eficiente e integrada com o broker MQTT.
