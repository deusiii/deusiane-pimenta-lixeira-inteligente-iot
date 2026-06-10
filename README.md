# Lixeira Inteligente - IOT

## 📌 Descrição do Projeto

O projeto **Lixeira Inteligente IoT** tem como objetivo automatizar o monitoramento do nível de preenchimento de lixeiras, permitindo identificar quando elas estão vazias, parcialmente cheias ou totalmente cheias.
Para isso, foi utilizado um **sensor ultrassônico HC-SR04**, responsável por medir a distância entre a tampa da lixeira e o lixo acumulado. Com base nessa medição, o sistema calcula o percentual de ocupação da lixeira.
Além disso, um **LED RGB** fornece uma indicação visual imediata do estado da lixeira, eliminando a necessidade de abrir a tampa ou acessar o dashboard para verificar seu nível.
O **ESP32** é utilizado como controlador principal, realizando a leitura dos sensores, acionamento dos LEDs e envio dos dados para a plataforma ThingSpeak através da Internet.

## 🎯 Objetivos

* Monitorar automaticamente o nível de preenchimento da lixeira.
* Informar visualmente o estado da lixeira através de um LED RGB.
* Enviar os dados para um dashboard IoT na plataforma ThingSpeak.
* Facilitar o gerenciamento da coleta de resíduos.


## Componentes Utilizados

| Componente                  | Especificação                                               |
| --------------------------- | ----------------------------------------------------------- |
| ESP32                       | Microcontrolador com conectividade Wi-Fi integrada          |
| Sensor Ultrassônico HC-SR04 | Sensor de distância com alcance aproximado de 2 cm a 400 cm |
| LED RGB                     | Indicação visual do nível da lixeira                        |
| Jumpers                     | Conexões elétricas entre os componentes                     |
| Protoboard                  | Montagem do circuito sem solda                              |
| Balde (Lixeira)             | Estrutura física utilizada para armazenamento dos resíduos  |

---

## 🔌 Funcionamento do Sistema

O sensor ultrassônico mede continuamente a distância entre a tampa da lixeira e o lixo.
Com base na distância medida, o sistema calcula o percentual de ocupação da lixeira e altera a cor do LED RGB:

| Nível da Lixeira | Cor do LED                     |
| ---------------- | ------------------------------ |
| Menor que 50%    | 🟢 Verde (Vazia)               |
| Entre 50% e 80%  | 🔵 Azul (Metade da Capacidade) |
| Acima de 80%     | 🔴 Vermelho (Cheia)            |

Os dados também são enviados para a plataforma ThingSpeak para monitoramento remoto.

## Protocolo de Comunicação Utilizado

### HTTP

O protocolo de comunicação utilizado foi o **HTTP (Hypertext Transfer Protocol)**.

### Justificativa

Inicialmente foi testada a utilização do protocolo MQTT, bastante comum em aplicações IoT. Entretanto, durante o desenvolvimento foram encontrados diversos problemas de comunicação e estabilidade.
Por esse motivo, optou-se pelo uso da plataforma ThingSpeak, que utiliza requisições HTTP para o envio dos dados.
A escolha do HTTP foi motivada pelos seguintes fatores:

* Facilidade de implementação com o ESP32;
* Compatibilidade nativa com a plataforma ThingSpeak;
* Maior estabilidade durante os testes realizados;
* Facilidade de monitoramento dos dados enviados.

## ⚙️ Instruções de Instalação

### 1. Materiais Necessários

* ESP32
* Sensor HC-SR04
* LED RGB
* Jumpers
* Protoboard
* Cabo USB para programação
### 2. Conexões sensores e ESP32
| Sensor HC-SR04   | ESP32                          |
| ---------------- | ------------------------------ |
| VCC              | 5V (Vin)                       |
| GND              | GND                            |
| TRIG             | GPIO 5                         |
| ECHO             | GPIO 18                        |

| LED RGB (CÁTODO) | ESP32                          |
| ---------------- | ------------------------------ |
| R                | GPIO 25                        |
| G                | GPIO 26                        |
| B                | GPIO 27                        |
| Comum (-)        | GND                            |


### 3. Instalar Dependências

Na Arduino IDE, instalar as bibliotecas:

* WiFi.h
* ThingSpeak.h

Também é necessário configurar o suporte à placa ESP32 na Arduino IDE.

### 4. Configurar Wi-Fi

No código, alterar as seguintes variáveis:

```cpp
const char* ssid = "SEU_WIFI";
const char* password = "SUA_SENHA";
```

### 5. Configurar ThingSpeak

Substituir pelos dados do seu canal:

```cpp
unsigned long channelID = SEU_CHANNEL_ID;
const char* writeAPIKey = "SUA_API_KEY";
```

### 6. Enviar o Código

* Conectar o ESP32 ao computador.
* Selecionar a porta correta na Arduino IDE.
* Compilar e enviar o código para a placa.


## 🚀 Como Utilizar

1. Energize o ESP32.
2. Aguarde a conexão com a rede Wi-Fi.
3. O sensor começará a monitorar o nível da lixeira.
4. Observe a cor do LED RGB para identificar o estado da lixeira.
5. Acompanhe os dados remotamente através do ThingSpeak.

## Diagrama ou Foto do Circuito

O diagrama elétrico e as fotos da montagem serão adicionados em futuras atualizações do projeto.

## 👩‍💻 Autora

**Deusiane Pimenta Rocha**

Estudante do 7 período do curso de Sistemas de Informação.

Projeto desenvolvido para a disciplina de Internet das Coisas (IoT).
