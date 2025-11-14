 SkillShift – Sistema IoT de Monitoramento com Buzzer (FIWARE + ESP32)

Este projeto consiste na criação de um sistema IoT capaz de monitorar eventos e acionar um buzzer por meio da plataforma FIWARE, utilizando um ESP32, além de uma interface web que exibe o status do buzzer em tempo real.

O objetivo é demonstrar um fluxo completo IoT:
Dispositivo → MQTT → FIWARE Orion → Interface Web

 Integrantes do Grupo
| Nome                         | RM     |
| ---------------------------- | ------ |
| **Arthur Pastorello**        | 562345 |
| **Gustavo Estevam Cocchi**   | 562472 |
| **André Dominicis Monteiro** | 562397 |
| **José Henrique Escobar**    | 564419 |


 Índice

 Visão Geral

 Tecnologias Utilizadas

 Arquitetura do Projeto

 Hardware Necessário

 Configuração do FIWARE

 Código do ESP32

 Interface Web

 Testando o Sistema

 Passo a Passo Completo para Replicar

 Estrutura do Projeto

 Licença

 1. Visão Geral

O sistema monitora o status de um dispositivo IoT no FIWARE e, quando recebe um comando, ativa ou desativa um buzzer físico conectado ao ESP32.
Além disso, existe uma página web que lê diretamente o status da entidade no FIWARE e exibe:

 Buzzer desligado

 Buzzer ativado (com alerta visual + som)

O ESP32 se comunica com o FIWARE utilizando MQTT.

 2. Tecnologias Utilizadas
 Backend IoT:

FIWARE Orion Context Broker

FIWARE IoT Agent MQTT

Mosquitto ou Broker MQTT da AWS

 Hardware:

ESP32 DevKit v1

Buzzer ativo (5V)

 Front-end:

HTML5, CSS3, JavaScript

Fetch API para consumir FIWARE

 3. Arquitetura do Projeto
ESP32 → MQTT → IoT Agent → Orion Context Broker → Interface Web


Cada alteração feita pelo ESP32 é registrada no FIWARE, e a interface web consulta diretamente o Context Broker.

 4. Hardware Necessário
Componente	Quantidade
ESP32 DevKit	1
Buzzer ativo	1
Jumpers	3
Protoboard	1
 Ligações do Buzzer

Buzzer + → GPIO 12

Buzzer – → GND

 5. Configuração no FIWARE

Você deve registrar o dispositivo no IoT Agent:

1️ Criar serviço:
{
  "services": [{
    "apikey": "2007",
    "cbroker": "http://orion:1026",
    "entity_type": "device",
    "resource": "/iot/json"
  }]
}

2️ Registrar dispositivo:
{
  "devices": [
    {
      "device_id": "device2007",
      "entity_name": "urn:ngsi-ld:device:2007",
      "entity_type": "device",
      "protocol": "PDI-IoTA-UltraLight",
      "transport": "MQTT",
      "attributes": [
        { "object_id": "a", "name": "Buzzer", "type": "Number" }
      ],
      "commands": [
        { "name": "on", "type": "command" },
        { "name": "off", "type": "command" }
      ]
    }
  ]
}

 6. Código do ESP32

O ESP32:

 Conecta ao Wi-Fi
 Conecta ao broker MQTT
 Lê comandos do FIWARE
 Liga/desliga o buzzer

(O código completo está incluído no zip do projeto.)

 7. Interface Web

A página web:

 Consulta o FIWARE a cada 5 segundos
 Exibe status em tempo real
 Reproduz som quando o buzzer é ligado
 Usa design estilizado baseado no visual da SkillShift

 8. Como Testar o Sistema
Teste 1 – Ativar manualmente via API:
POST /v2/entities/urn:ngsi-ld:device:2007/attrs
{
  "on": { "type": "command" }
}

Teste 2 – Ver status via navegador:

Acesse:

status.html


O painel mostrará:

 Buzzer Ativado

 Buzzer Desligado

 9. PASSO A PASSO COMPLETO PARA REPLICAR O PROJETO
 PASSO 1 – Separar os Materiais

Pegue:

ESP32

Buzzer

Jumpers

Cabo USB

 PASSO 2 – Montagem do Circuito

Conecte o buzzer na protoboard.

Ligue o + do buzzer no GPIO 12 do ESP32.

Ligue o – em GND.

Conecte o ESP32 ao PC.

 PASSO 3 – Configurar o FIWARE

Suba um ambiente FIWARE (Docker).

Inicie:

Orion Context Broker

IoT Agent MQTT

Mosquitto

Registre o serviço.

Registre o dispositivo IoT.

 PASSO 4 – Configurar o Arduino IDE

Instale suporte ao ESP32:

https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json


Instale a biblioteca:

PubSubClient

Abra o código do projeto.

Configure:

SSID e senha do Wi-Fi

IP do IoT Agent

API Key

ID do dispositivo

 PASSO 5 – Fazer Upload para o ESP32

Escolha a placa ESP32 DevKit v1.

Porta correta → COMx.

Clique Upload.

 PASSO 6 – Testar Conexão

Abra o Monitor Serial.

Você deve ver mensagens como:

Conectado ao Wi-Fi
Conectado ao Broker MQTT
Aguardando comandos...

 PASSO 7 – Subir Página Web

Salve o arquivo HTML fornecido.

Abra no navegador.

O painel mostrará o estado do buzzer em tempo real.

 PASSO 8 – Acionar o Buzzer

Você pode ativar via:

 FIWARE API
 IoT Agent
 MQTT Publish Manual

 LINKS:

 link do projeto no Wokwi: https://wokwi.com/projects/447548990685211649
 
 link do video de demonstraçao: https://youtu.be/Q4ASzFgEXnU

Se tudo estiver ok, o buzzer toca e o site exibe o status em tempo real.

<img width="1864" height="921" alt="image" src="https://github.com/user-attachments/assets/78ed58e3-895f-44bd-b825-b878c5fd0ba4" />


<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/a4df6570-8d45-4d76-b840-4caaaeb2ed3c" />



