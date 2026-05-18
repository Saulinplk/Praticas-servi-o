# Praticas-serviço

📋 Descrição
O ESP32 Explorer Robot é um sistema de monitoramento ambiental que coleta dados de múltiplos sensores, calcula a probabilidade de presença de vida no ambiente e envia alertas automáticos via WhatsApp quando o índice ultrapassa um limiar crítico.

⚙️ Funcionalidades

Leitura de temperatura e umidade (DHT22)
Detecção de luminosidade (LDR)
Detecção de presença/movimento (PIR)
Controle de direção via joystick analógico
Feedback visual por LED RGB (verde = explorando, vermelho = alerta)
Cálculo de probabilidade de vida (0–100%)
Envio de alerta via WhatsApp (CallMeBot API) — sem spam, dispara apenas uma vez por evento
Log detalhado pela porta Serial


🧰 Hardware Necessário
ComponenteQuantidadeESP32 (qualquer variante com Wi-Fi)1Sensor DHT221Sensor LDR (fotoresistor)1Sensor PIR (HC-SR501 ou similar)1LED RGB (anodo/catodo comum)1Joystick analógico (2 eixos + botão)1Resistores e cabos jumper—

🔌 Pinagem
ComponentePino ESP32
DHT22 GPIO 13
LDR GPIO 4 
PIR GPIO 5 
LED R GPIO 16 
LED G GPIO 17
LED B GPIO 18
Joystick X GPIO 6 
Joystick Y GPIO 7
Joystick Botão GPIO 8

🚀 Como Usar
1. Clone ou copie o código
bashgit clone <seu-repositorio>
2. Configure o Wi-Fi
No arquivo .ino, altere as credenciais:
cppconst char* ssid = "SEU_WIFI";
const char* password = "SUA_SENHA";
3. Configure o WhatsApp (CallMeBot)

Adicione o número +34 644 44 24 04 aos seus contatos no WhatsApp
Envie a mensagem: I allow callmebot to send me messages
Você receberá sua apiKey por WhatsApp
Preencha no código:

cppString phoneNumber = "SEU_NUMERO_COM_DDI"; // Ex: 5571999999999
String apiKey = "SUA_API_KEY";
4. Compile e grave no ESP32
Use a Arduino IDE (≥ 2.0) ou PlatformIO. Selecione a placa correta (ex: ESP32 Dev Module) e faça o upload. 

📊 Lógica de Probabilidade de Vida
O sistema pontua as condições ambientais e soma até 100%:
CondiçãoCritérioPontosTemperaturaEntre 15°C e 30°C+25UmidadeEntre 40% e 70%+25LuminosidadeLeitura LDR > 2000+20PresençaSinal PIR ativo+30
Quando a probabilidade ultrapassa 75%, o robô entra em estado de ALERTA e:

O LED RGB acende em vermelho
Um alerta é enviado via WhatsApp (apenas uma vez por evento)

Abaixo de 75%, o LED fica verde e o estado volta a "Explorando".

🕹️ Controle por Joystick
PosiçãoAçãoY > 3000FrenteY < 1000RéX > 3000DireitaX < 1000EsquerdaBotão pressionadoDesligar robô (LED vermelho)

📟 Monitor Serial
Conecte-se em 115200 baud para visualizar os dados em tempo real:
------ DADOS ------
Temp: 24.50
Umidade: 55.30
Luz: 2450
Presença: Detectada
Joystick X: 2048
Joystick Y: 3200
Direção: Frente
Estado: ALERTA
Probabilidade: 100 %
-------------------

⚠️ Observações

O sensor DHT22 pode ser lento para inicializar; aguarde alguns segundos após ligar.
Os GPIOs 6, 7 e 8 podem apresentar conflito em algumas variantes do ESP32 — ajuste conforme seu hardware.
A CallMeBot é um serviço gratuito com limite de mensagens. Use com moderação.
O sistema foi projetado e testado no simulador Wokwi.
