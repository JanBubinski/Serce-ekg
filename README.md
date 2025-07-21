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

Pętla która odpowiada za miganie ledów*(Fade in-out): 


    for led in leds:
    
    led.freq(10000)
    
     led.duty_u16(0)
