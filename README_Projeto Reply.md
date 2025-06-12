
# Monitoramento Ambiental com ESP32 e Sensor DHT22

Este projeto simula um sistema básico de monitoramento ambiental utilizando a plataforma Wokwi. O objetivo 
é demonstrar a coleta de dados de temperatura e umidade com um microcontrolador ESP32 e o sensor digital DHT22, refletindo um cenário industrial de monitoramento climático.

## 🔧 Componentes Utilizados
- **Placa de desenvolvimento ESP32**
- **Sensor digital de temperatura e umidade DHT22**
- **Plataforma de simulação: Wokwi**

## ⚙️ Objetivo
Simular a coleta de dados ambientais (temperatura e umidade) em um ambiente industrial digitalizado, utilizando um circuito funcional com ESP32 e sensor DHT22, realizando análise inicial dos dados.

## 🔌 Ligações do Circuito
| Pino do DHT22 | Pino do ESP32 |
|---------------|----------------|
| VCC           | 3V3            |
| DATA (SDA)    | GPIO 15        |
| GND           | GND            |

## 📄 Código-fonte (Arduino)
```cpp
#include "DHT.h"

#define DHTPIN 15
#define DHTTYPE DHT22

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
  Serial.println("Iniciando leitura do DHT22...");
}

void loop() {
  delay(2000);
  float temperatura = dht.readTemperature();
  float umidade = dht.readHumidity();

  if (isnan(temperatura) || isnan(umidade)) {
    Serial.println("Falha na leitura do sensor DHT!");
    return;
  }

  Serial.print("Temperatura: ");
  Serial.print(temperatura);
  Serial.print(" °C | Umidade: ");
  Serial.print(umidade);
  Serial.println(" %");
}
```

## 📊 Dados Simulados
Foram registrados 10 valores simulando a leitura do sensor em um ambiente estável. Os dados estão salvos em `dados_simulados_dht22.csv`.

## 📈 Gráfico Gerado
O gráfico a seguir representa as variações de temperatura e umidade ao longo do tempo:

![Gráfico de Dados](grafico.png)

## 📃 Análise dos Dados
Durante o período simulado, observou-se uma variação suave e estável tanto na temperatura quanto na umidade. A temperatura permaneceu entre 24.0 °C e 24.7 °C, enquanto a umidade oscilou levemente de 40.0% para 38.5%. Esse comportamento é típico de um ambiente industrial climatizado, simulando com fidelidade um sistema real de coleta de dados ambientais.

## 📷 Imagens do Projeto
- Circuito completo com sensor DHT22 (`imagens/circuito.png`)
- Monitor Serial exibindo os dados (`imagens/monitor_serial.png`)

## 🔹 Conclusão
Este projeto demonstra de forma simples e funcional como integrar sensores a sistemas embarcados utilizando o ESP32, simulando um cenário real de monitoramento ambiental industrial.

---

Desenvolvido como parte do desafio Hermes Reply - Fase 4.
