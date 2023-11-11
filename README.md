
# Sensor de Movimento + Python OS

Esse é um projeto que pra mim foi muito divertido de construir, pois interliguei: C++, Python e obviamente minha "paixão recente" o Arduino (no meu caso o Uno).


## Desafios

Acredito que meus principais desafios nesse projeto foram:
- Receber dados vindos do Arduino e lê-los de forma que fosse possível usá-los no meu computador.
- Ao receber dados utiliza-los usando a lib [os](https://docs.python.org/3/library/os.html) do Python.
## Aprendizados

Por final aprendi algumas coisas interessantes como: 

(Não vou entrar em tantos detalhes pois o meu outro [projeto](https://github.com/Victor-Lis/Sensor-de-Movimento-e-Leds) em que trabalho com Arduino, Sensor PIR e Leds já tem bem explicadinho esses processos)
## Ligando Arduino ao Python
Por incrível que pareça o processo para fazer os dados que o Arduino Uno envia chegarem no Python ao invés do [Arduino IDE](https://www.arduino.cc/en/software) foi bem fácil, apenas usei a lib do Python [Serial](https://pyserial.readthedocs.io/en/latest/pyserial.html).
E com isso eu executo a COM em que o Arduino vai mandar informações no Python.

```python
import serial

arduino = serial.Serial("COM5", 9600)
```

### Lendo os dados
Primeiramente lá no C++ no Arduino IDE fiz o código escrever "Movimento" no monitor serial sempre que detectasse movimento.
```c++
void loop(){  

    permitido = (digitalRead(pinPIR)==HIGH); // Verificando se a Voltagem é == HIGH, ou seja, se detectou movimento

    if(permitido){
        Serial.println("Movimento"); // Como havia dito, printando no monitor serial "Movimento", justamente ao detectar movimento.
        digitalWrite(led1, HIGH); // Ligando as leds vermelhas, apenas para ser mais fácil de perceber essa dectecção.
        digitalWrite(led2, LOW); // Desligando as leds azuis, pelo mesmo motivo.
        delay(2000);
    }else{
        digitalWrite(led1, LOW); // Desligando as leds vermelhas, apenas para ser mais fácil de perceber essa não dectecção.
        digitalWrite(led2, HIGH); // Ligando as leds azuis, pelo mesmo motivo.
    }
    
}
```

Agora lá no Python, preciso ler basicamente toda vez que eu printar "Movimento" no meu monitor serial.

```python
import os # Lib que vou usar para abrir o chrome
import serial # Lib que vou usar para o Arduino passar dados aqui, na COM definida ao invés de lá no Arduino IDE

arduino = serial.Serial("COM5", 9600) # Definindo a porta COM que vou conectar e receber dados do meu Arduino, iniciando o monitor serial e a velocidade.

while True: # while True para ficar sempre verificando
  
  data = arduino.readline().decode ("utf-8") # Nessa linha eu leio o monitor serial, igual aquele da IDE Arduino

  if (data): # Se eu tiver recebido dados do monitor serial, ou seja, se escreveu algo, a condição é True
    print(data) # Printando só pra confirmar que eu recebi de fato a informação de maneira correta
    os.system("start chrome https://github.com/Victor-Lis/") # Iniciando o chrome no meu GitHub 
```
# Resultado

[Clique aqui para ver o resultado em um vídeo!](https://youtube.com/shorts/lvzliqZ_z28)
## Autores

- [@Victor-Lis](https://github.com/Victor-Lis)

