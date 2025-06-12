// Importa a biblioteca que permite ler o sensor DHT (temperatura e umidade)
#include "DHT.h"

// Define o pino digital do ESP32 onde o sensor está conectado (GPIO 15)
#define DHTPIN 15

// Define o tipo de sensor utilizado (DHT22 ou DHT11)
#define DHTTYPE DHT22

// Cria um objeto chamado 'dht' com as configurações acima
DHT dht(DHTPIN, DHTTYPE);

// Função executada uma vez no início do programa
void setup() {
  // Inicializa a comunicação serial com o computador (Monitor Serial)
  Serial.begin(9600);

  // Inicializa o sensor DHT
  dht.begin();

  // Mensagem inicial indicando que a leitura vai começar
  Serial.println("Iniciando leitura do DHT22...");
}

// Função que roda repetidamente (loop infinito)
void loop() {
  // Aguarda 2 segundos entre uma leitura e outra
  delay(2000);

  // Lê a temperatura em graus Celsius
  float temperatura = dht.readTemperature();

  // Lê a umidade relativa do ar em porcentagem
  float umidade = dht.readHumidity();

  // Verifica se houve falha na leitura (por exemplo, sensor desconectado)
  if (isnan(temperatura) || isnan(umidade)) {
    Serial.println("Falha na leitura do sensor DHT!");
    return; // Encerra esse ciclo do loop
  }

  // Exibe os dados lidos no Monitor Serial
  Serial.print("Temperatura: ");
  Serial.print(temperatura);
  Serial.print(" °C | Umidade: ");
  Serial.print(umidade);
  Serial.println(" %");
}