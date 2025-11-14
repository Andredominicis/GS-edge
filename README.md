🏆 SkillShift – Sistema IoT com ESP32, MQTT e Dashboard Web

Projeto desenvolvido por: André Monteiro — RM 562397
                          Arthur Pastorello RM 562345
                          Gustavo Estevam Cocchi RM 562472
                          José Henrique Escobar -RM: 564419

📌 Sobre o Projeto

Este projeto implementa um sistema IoT utilizando ESP32, MQTT e uma interface web moderna, para monitoramento do estado de um buzzer de alerta ativado de forma remota.


🎯 Objetivos do Sistema

Ler o estado do buzzer enviado pelo ESP32.

Publicar/receber mensagens via MQTT.

Registrar o estado no FIWARE Orion Context Broker (NGSI-v2).

Exibir em uma interface web o status do buzzer em tempo real.

Reproduzir um som de alerta ao detectar transição "desligado → ligado".

Ser acessível via celular com design adaptado.

🛠️ Componentes Físicos

ESP32 DevKit

Buzzer piezoelétrico

Fonte 5V

Conexão Wi-Fi

Broker MQTT (IP variável do laboratório)

🔌 Funcionamento do ESP32

O ESP32:

Conecta-se ao Wi-Fi.

Conecta ao broker MQTT.

Publica mensagens no tópico configurado (ex: /skillshift/buzzer).

Envia ao FIWARE Orion o atributo a indicando o estado:

Valor	Significado
0	Buzzer desligado
1	Buzzer ligado / Alerta

Exemplo de payload enviado ao Orion:

{
  "a": {
    "type": "Number",
    "value": 1
  }
}

🌐 Funcionamento da Dashboard Web

A página HTML:

✔ Busca a cada 5s o valor do atributo do buzzer no ORION:

GET /v2/entities/urn:ngsi-ld:device:2007/attrs/a


✔ Interpreta o valor (0 ou 1).
✔ Modifica o layout visual:

Vermelho piscando quando ativo

Azul estático quando inativo

✔ Reproduz um som caso o buzzer acabe de ser ativado.
✔ Exibe tudo com design estilizado inspirado na identidade SkillShift.

🎨 Design

O design foi totalmente remodelado baseado no estilo do aplicativo SkillShift:

Gradiente futurista

Tipografia mais moderna

Cards arredondados

Animações suaves

Foco em visual mobile

Título e identidade visual alterados para SkillShift

📁 Estrutura do Projeto
/skillshift-iot
 ├── esp32/
 │    ├── skillshift_buzzer.ino
 │    └── wifi_mqtt_config.h
 │
 ├── web/
 │    └── index.html   <- Dashboard de status do buzzer
 │
 ├── docs/
 │    └── README.md
 │
 └── media/
      └── videos reduzidos (para envio no sistema)

🧪 Testes Realizados

✔ Conexão Wi-Fi estável
✔ Publicação MQTT validada em broker externo
✔ Endpoint FIWARE respondendo corretamente
✔ Dashboard detectando transições 0 → 1
✔ Teste com áudio de alarme funcionando no celular
✔ Layout responsivo testado em:

Android

iPhone

Navegador desktop

🚀 Como Executar
1. Subir o ESP32

Configurar o Wi-Fi

Configurar IP do broker MQTT

Fazer upload do código no Arduino IDE

2. Executar o FIWARE Orion

Confirmar porta aberta: 1026

Registrar entidade do dispositivo

3. Abrir a Interface Web

Basta abrir o arquivo:

web/index.html


Não requer servidor — funciona somente com acesso direto.

📡 Comunicação MQTT

Tópico sugerido:

/skillshift/buzzer


Payload padrão:

1   → ativado
0   → desligado

🔔 Notificação Sonora

Ao detectar o estado 1, a dashboard toca automaticamente:

https://actions.google.com/sounds/v1/alarms/beep_short.ogg


O áudio só toca quando ocorre uma troca de estado, evitando repetição desnecessária.

📱 Compatibilidade Mobile

A interface foi ajustada para caber perfeitamente:

Sem rolagem

Texto centralizado

Blocos responsivos

Botões e fontes dimensionados para tela de celular

🧩 Expansões Futuras

Adicionar sistema de login

Histórico de alertas

Conexão via WebSockets ao Orion

Dashboard com gráficos de eventos

Controle manual do buzzer via web

<img width="1864" height="921" alt="image" src="https://github.com/user-attachments/assets/78ed58e3-895f-44bd-b825-b878c5fd0ba4" />


<img width="1919" height="1031" alt="image" src="https://github.com/user-attachments/assets/a4df6570-8d45-4d76-b840-4caaaeb2ed3c" />



