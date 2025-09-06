# Smart Lamp - ESP32 + FIWARE

A **Smart Lamp** é um projeto desenvolvido com o microcontrolador **ESP32 DEVKIT V1**, que integra recursos de IoT com a plataforma **FIWARE**. Essa solução permite controlar uma lâmpada inteligente de forma remota, utilizando APIs REST e protocolo MQTT, além de armazenar e analisar dados contextuais com os principais **Generic Enablers (GEs)** da FIWARE Foundation.

O projeto foi pensado como uma **Prova de Conceito (PoC)** para demonstrar como dispositivos físicos podem ser conectados, monitorados e controlados através de padrões abertos, promovendo interoperabilidade e escalabilidade.

---

##  Objetivo

O objetivo do projeto é criar uma solução prática de IoT que demonstre:

- Controle remoto de uma lâmpada inteligente (ligar/desligar e checar a luminosidade do ambiente).
- Monitoramento do estado atual da lâmpada.
- Integração com o **Orion Context Broker** para gerenciamento de dados contextuais.
- Registro de dados históricos no **STH‑Comet**.
- Comunicação via **IoT Agent MQTT**.

Essa arquitetura simples pode ser expandida para aplicações em **casas inteligentes, cidades inteligentes** ou **indústrias conectadas**.

---

##  Requisitos

### Hardware

- ESP32 DevKit V1  
- Sensor LDR
- Resistores e jumpers  
- Protoboard  

### Software

- [Arduino IDE](https://www.arduino.cc/en/software) ou [PlatformIO](https://platformio.org/)  
- [Docker](https://docs.docker.com/get-docker/) e **Docker Compose**  
- [Postman](https://www.postman.com/downloads/)  
- FIWARE Descomplicado (Orion Context Broker, IoT Agent, STH‑Comet, MongoDB, Mosquitto)  

### Instalação do FIWARE Descomplicado

```bash
git clone https://github.com/fabiocabrini/fiware
cd fiware
sudo docker-compose up -d
```

Para encerrar:

```bash
sudo docker-compose down
```

---

##  Arquitetura

A arquitetura é composta por três camadas principais:

1. **IoT (ESP32)** → Publica e recebe comandos via MQTT.  
2. **Back‑end (FIWARE)** → Gerencia entidades (Orion), dados históricos (STH‑Comet), IoT Agent, e armazenamento (MongoDB).  
3. **Aplicação** → Interface para interação com o usuário, incluindo dashboards e collections no Postman.

<p align="center">
<img width="992" height="961" src="https://github.com/user-attachments/assets/dd7edb84-b625-4a26-83c2-146d94c5629f" alt="Arquitetura FIWARE Descomplicado"/ >
</p>

---

##  Como usar as collections do Postman

As **collections do Postman** facilitam a interação com a Smart Lamp e os componentes FIWARE.

### 1. Importando a coleção
1. Abra o Postman.  
2. Clique em **Import**.  
3. Faça o upload do arquivo `arquivo postman.json`.  
4. A coleção será carregada.

### 2. Configurando o ambiente
Crie um **Environment** no Postman com:

```
base_url = http://<ip-da-VM>
```

E adicione os endpoints do Orion e do IoT Agent.

### 3. Executando requisições
Na coleção você encontrará:

- **Ligar lâmpada** → Metodo 'switching on the smart lamp' 
- **Desligar lâmpada** → Trocar Metodo 'switching on the smart lamp' para off   
- **Consultar estado** → Metodos 7 e 8

---

##  PoC – Smart Lamp

A entidade "Smart Lamp" no **Orion Context Broker** é representada como:

```json
{
  "id": "SmartLamp1",
  "type": "Lamp",
  "state": { "value": "off", "type": "Text" },
}
```

A entidade pode ser manipulada via API ou pelo Postman.

- **Atributos de Estado** → Ligar/desligar.   
- **Sensoriamento Opcional** → Monitorar luminosidade ou consumo.

Links úteis:

- [Vamos criar juntos nossa Smart Lamp?](mqtt_esp32.md)  
- [Datasheet do ESP32](https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf)  
- [Simulação no Wokwi](https://wokwi.com/projects/381403531345819649)  
- [Vídeo Tutorial no YouTube](https://www.youtube.com/watch?v=8oHkAlXdWo8)  

---

##  Observações de Segurança

Este projeto é uma **versão de pesquisa/PoC**, sem segurança inclusa. Para produção, recomenda-se adicionar:

- Keyrock (Identity Manager)  
- Wilma PEP Proxy  
- AuthZForce PDP/PAP  
- Protocolos seguros: **HTTPS / MQTTS**  

---

##  Conclusão

A **Smart Lamp** demonstra como integrar um dispositivo real com o **FIWARE**, unindo hardware, APIs abertas e interoperabilidade. Uma base sólida para expandir soluções em **IoT**, **smart cities** ou **indústria conectada**.

---

##  Referências

- [FIWARE Foundation](https://www.fiware.org/)  
- [Orion Context Broker](https://fiware-orion.readthedocs.io/en/3.10.1/index.html)  
- [IoT Agent MQTT](https://github.com/FIWARE/tutorials.IoT-Agent)  
- [STH‑Comet](https://fiware-sth-comet.readthedocs.io/en/latest/)  
- [MongoDB](https://www.mongodb.com/pt-br/products/compass)  
- [Eclipse Mosquitto](https://mosquitto.org/)

---

#### © 2025 CPS – 2º Semestre, todos os direitos reservados.


# Equipe 
- Lucas de Almeida Sales da Silva
- André Ricardo Spinola Castor
- João Pedro Palmera
- Eduardo Delarissia
- Gabriel Viana
