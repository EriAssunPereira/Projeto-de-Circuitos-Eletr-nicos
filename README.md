# Projeto-de-Circuitos-Eletr-nicos

Vamos criar um projeto modular de circuitos eletrônicos que simula uma estufa de hortaliças usando o simulador TinkerCad. Este projeto envolverá um sensor de temperatura, uma buzina, um LED e um motor, todos controlados por um Arduino. Aqui está um guia detalhado dividido em módulos:

### Módulo 1: Sensor de Temperatura
O sensor de temperatura será o coração da nossa estufa eletrônica. Vamos usar o **sensor DHT22**, que é capaz de medir a temperatura e a umidade do ar. O DHT22 será conectado ao Arduino, e os dados coletados serão usados para controlar as condições dentro da estufa.

```arduino
#include "DHT.h"

#define DHTPIN 2     // Pino onde está conectado o sensor
#define DHTTYPE DHT22   // DHT 22 (AM2302)

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  float temp = dht.readTemperature();
  if (isnan(temp)) {
    Serial.println("Erro na leitura do DHT22");
    return;
  }
  Serial.print("Temperatura: ");
  Serial.print(temp);
  Serial.println(" *C");
}
```

### Módulo 2: Buzina
A buzina será utilizada para alertar quando a temperatura sair dos limites pré-estabelecidos. Se a temperatura ultrapassar 30°C, por exemplo, a buzina soará.

```arduino
int buzzerPin = 3;

void setup() {
  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  float temp = dht.readTemperature();
  if (temp > 30) {
    digitalWrite(buzzerPin, HIGH);
  } else {
    digitalWrite(buzzerPin, LOW);
  }
}
```

### Módulo 3: LED
O LED indicará visualmente o estado da estufa. Se a temperatura estiver adequada, o LED ficará verde; se estiver alta, ficará vermelho.

```arduino
int ledVerde = 4;
int ledVermelho = 5;

void setup() {
  pinMode(ledVerde, OUTPUT);
  pinMode(ledVermelho, OUTPUT);
}

void loop() {
  float temp = dht.readTemperature();
  if (temp <= 30) {
    digitalWrite(ledVerde, HIGH);
    digitalWrite(ledVermelho, LOW);
  } else {
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledVermelho, HIGH);
  }
}
```

### Módulo 4: Motor
O motor pode ser usado para abrir uma janela ou ativar um sistema de irrigação. Ele será ativado se a temperatura estiver muito alta, para ajudar a resfriar a estufa.

```arduino
int motorPin = 6;

void setup() {
  pinMode(motorPin, OUTPUT);
}

void loop() {
  float temp = dht.readTemperature();
  if (temp > 30) {
    digitalWrite(motorPin, HIGH);
  } else {
    digitalWrite(motorPin, LOW);
  }
}
```

### Módulo 5: Arduino
O Arduino será o cérebro do nosso projeto, integrando todos os módulos anteriores e controlando o funcionamento da estufa.

```arduino
void setup() {
  // Inicializa todos os módulos
}

void loop() {
  // Executa as funções de cada módulo
}
```

Esses módulos formam a base do seu projeto de estufa eletrônica. Você pode expandir cada módulo com funcionalidades adicionais conforme necessário. Lembre-se de testar cada parte individualmente antes de integrar tudo no TinkerCad.
