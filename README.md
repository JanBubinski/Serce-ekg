# Serce-ekg
Serce zsynchronizowane z lcd, ekg


Użyte komponenty: 

-Raspberrry Pi Pico#without wi-fi 

-Wyświetlacz LCD-02351 

-7 diod czerwonych 


Algorytm dziaania:  

Zmienne odpowiadajace ledą w ukladzie: 
   ```
   pins = [18, 17, 16, 15, 14, 13, 10]

   leds = [PWM(Pin(p)) for p in pins] 
   ```
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

```
I2C_ADDR = 0x27
I2C_NUM_ROWS = 4
I2C_NUM_COLS = 20

i2c = I2C(0, sda=Pin(0), scl=Pin(1), freq=40000)

lcd = I2cLcd(i2c, I2C_ADDR, I2C_NUM_ROWS, I2C_NUM_COLS)
frame1 = [32,219,219, 32, 32, 219, 219, 32, 32, 219, 219, 32, 32, 219, 219, 32, 32, 219,32]#32-spacja w ASCII, 219-pelne pole
frame2 = [32,219,219, 32, 32, 219, 219, 32, 32, 219, 219, 32, 32, 219, 219, 32, 32, 219,32]
timer =0.75/len(frame1)
i=0
j=0
```
Dzialanie lcd: 

  lcd.move_to(0, 0)
        
        for col in range(16):
            index = (i + col) % len(frame1)
            lcd.putchar(chr(frame1[index]))
        sleep(timer)
     
    
        lcd.move_to(0, 1)
        
        for col in range(16):
            index = (j+col) % len(frame2)
            lcd.putchar(chr(frame2[index]))
        sleep(timer)
        
        i = (i + 1) % len(frame1)
        j = (j + 1) % len(frame2)
        




