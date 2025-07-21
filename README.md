# Serce-ekg
Serce zsynchronizowane z lcd, ekg


Użyte komponenty: 

-Raspberrry Pi Pico#without wi-fi 

-Wyświetlacz LCD-02351 

-7 diod czerwonych 


Algorytm dziaania:  

Zmienne odpowiadajace ledą w ukladzie: 

   pins = [18, 17, 16, 15, 14, 13, 10]

   leds = [PWM(Pin(p)) for p in pins] 

Pętle które odpowiadają za miganie ledów*(Fade in-out): 

     for duty in range(0, 65536, 15000):
        for led in leds:
            led.duty_u16(duty)
        sleep(0.03)
     for duty in range(65535, -1, -15000):
        for led in leds:
            led.duty_u16(duty)
        sleep(0.03)

Zmienne odpowiadajace lcd w ukladzie: 


Dzialanie lcd: 






