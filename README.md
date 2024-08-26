# devgustavopacoo

Este manual descreve o funcionamento de um sistema de monitoramento de umidade utilizando duas placas ESP32. A ESP1 monitora a temperatura e umidade de dois ambientes e controla servos com base na temperatura. Caso a umidade caia abaixo de um certo limite, ela envia um alerta via MQTT para a ESP2. A ESP2, ao receber este alerta, aciona um buzzer e um LED que pisca para alertar o usuário.

Componentes Utilizados
2x ESP32
2x Sensores de Umidade/Temperatura DHT22
2x Servos Motores
1x Buzzer
1x LED
1x Resistor de 220Ω para o LED
1x Slide Switch (Chave)
Fios Jumpers
Fonte de Alimentação para ESP32
Esquema de Conexão
ESP1:
Sensor DHT22 1:
VCC -> 3.3V
GND -> GND
DATA -> GPIO 15
Sensor DHT22 2:
VCC -> 3.3V
GND -> GND
DATA -> GPIO 2
Servo 1:
VCC -> 5V (ou 3.3V, dependendo do servo)
GND -> GND
Sinal -> GPIO 13
Servo 2:
VCC -> 5V (ou 3.3V, dependendo do servo)
GND -> GND
Sinal -> GPIO 12
Slide Switch:
Um lado -> GND
Outro lado -> GPIO 14
ESP2:
Buzzer:
VCC -> GPIO 5
GND -> GND
LED:
Ânodo -> GPIO 4 (via resistor 220Ω)
Cátodo -> GND
Descrição do Código - ESP1
O código para a ESP1 é responsável por monitorar a umidade e temperatura usando dois sensores DHT22. Ele também controla dois servos motores com base na temperatura. Um slide switch é utilizado para priorizar o controle manual, desativando o envio de mensagens MQTT para a ESP2 e retornando os servos para a posição inicial.

Principais Funcionalidades:
Monitoramento de Umidade e Temperatura: Leitura dos valores dos sensores DHT22.
Controle de Servos: Ajuste dos servos baseado na temperatura lida.
Envio de Mensagens MQTT: Envio de mensagens de alerta quando a umidade está baixa.
Controle via Slide Switch: Prioriza o controle manual, desativando os envios e retornando os servos à posição inicial.
Descrição do Código - ESP2
O código para a ESP2 é responsável por receber as mensagens via MQTT enviadas pela ESP1. Ao receber uma mensagem de alerta, a ESP2 aciona um buzzer e começa a piscar um LED, indicando uma condição de baixa umidade.

Principais Funcionalidades:
Recebimento de Mensagens MQTT: Assinatura nos tópicos para receber alertas de baixa umidade.
Alerta Sonoro e Visual: Ativação do buzzer e piscamento do LED ao receber uma mensagem de alerta.
Desativação dos Alertas: Desativa os alertas quando a umidade retorna ao normal.
Funcionamento Geral
ESP1: Monitora a umidade e temperatura. Caso a umidade caia abaixo de 20%, envia um alerta via MQTT para a ESP2, a menos que o slide switch esteja ativado.
ESP2: Recebe o alerta e aciona o buzzer e o LED. Quando a umidade retorna ao normal, a ESP1 envia uma mensagem para desativar os alertas na ESP2.
Instruções de Uso
Montagem: Monte o circuito conforme o esquema de conexão.
Programação: Carregue os códigos nas respectivas ESPs.
Operação:
A ESP1 irá monitorar os ambientes automaticamente.
Se a umidade cair abaixo de 20%, a ESP2 receberá o alerta e acionará o buzzer e o LED.
Use o slide switch na ESP1 para desativar o envio de mensagens e resetar os servos.
Considerações Finais
Este sistema é útil para monitoramento ambiental em indústrias, estufas ou qualquer ambiente sensível a mudanças de umidade. A flexibilidade do controle via slide switch permite intervenção manual para garantir segurança e eficiência no controle do ambiente
