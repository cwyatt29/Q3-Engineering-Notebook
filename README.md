# ENGINEERING Q3 NOTEBOOK

### this note book documents the work that was completed for the third quarter of the 22-23 school year. Most of the Quarter was spent doing CAD practice to prepare for the OnShape exam. The end of the quarter was spent doing code that relates to PID concepts.

## Credits
### Code help from @pweder69 on Github 


## Projects:

### OCE = OnShape Certification, Exam OCP= OnShape Certification Prep

## 1. OCP Single Part
 
 AKA "The Hanger" this was a very simple part to make. I learned how to use the hole tool to counterbore spots for screw heads. I also used three point arcs and relied on constraints instead of dimensions. This assignment was very simple for me because I had made things that were similar to it in the past.

 https://cvilleschools.onshape.com/documents/f64f0b76b9423291ca45d4cb/w/2dbffd8a7b4f164e38cb0800/e/76a551d1a5d1940cc344435c

 Weight: 7128.85g 
## 2. OCP Multipart Studio

The Multipart practice assignment was more chalenging because we had to make three different parts work together. Similar to the cylinder the Mic stand had to be built in order often using other parts to determine the dimensions of other parts. Replicated the provided design using the images provided whilst not relying on only dimensions. I heavily used tools like equal, parallel, and symmetric. I also used the section veiw tool which essentially let you see the part if it was cut in half. This is useful for making sure all of your parts are in the correct place. It is also good to occcacsionly use the check interfernce tool to make sure nothing is to big.

 https://cvilleschools.onshape.com/documents/adb0784129c89787096a3049/w/f7a2d19316d341d3f13e8f16/e/30499ddb62f3a9594a8f25ff

 Weight: 118.23g
## 3. OCP Assemblies

The Assemblies assignment was to assemble a pair of vice grips from parts that were provided. During this assignment I learned more about mates. I used parallel, fastened, revolute, and slider mates. This assignment helped me prepare of the OCE because it taught me how to mate and measure parts.

 https://cvilleschools.onshape.com/documents/f2f2574fe5888449d58a2038/w/e01e4f5f836abe87b000d476/e/601438236349e83909b01fbe

## 4. OCP THE SWING ARM
This was the same part that we made in Q1. We did this to see if our knowledge had grown after completing the practice.

Replicated the provided design using the images provided whilst not relying on only dimensions. I heavily used tools like equal, parallel, and symmetric. There is only one part in the assignment but the part is very complex and has holes, filets and, chamfers on every single plane.

 Weight: 2355.7g

 https://cvilleschools.onshape.com/documents/a5fd8d22b575fddb2bdee574/w/76f65086d2b77c85ffe6fc60/e/afefe01db5f326c914c81df6 

## Reflection

 The original image was black and white so it was hard to see what the final should look like. Also it was really easy to try to use dimensions on everything but it will save you so much time if you use constrains that change as needed but will also keep the structure of the shape better.

## 6. Temperature Sensor


Used Circuit Python and a temp sensor to detect and display the current temp on an LCD screen. I learned that your time is better spent looking for someone elses code rather than writing your own code. Ciruit Python tends to be unecessary for easier tasks that dont require multiple outputs. This assignment is much simplier to do in C++




![Temp_Sensor](https://github.com/cwyatt29/Q3-Engineering-Notebook/blob/master/IMG_0014.MOV?raw=true)
```python

import board
import analogio
import time
from lcd.lcd import LCD

from lcd.i2c_pcf8574_interface import I2CPCF8574Interface

TMP36_PIN = board.A0  # Analog input connected to TMP36 output.

i2c = board.I2C()

# some LCDs are 0x3f... some are 0x27.
lcd = LCD(I2CPCF8574Interface(i2c,0x27), num_rows=2, num_cols=16)
# Function to simplify the math of reading the temperature.
lcd.set_cursor_pos(0,0)
lcd.print("temp:")
def tmp36_temperature_C(analogin):
    millivolts = analogin.value * (analogin.reference_voltage * 1000 / 65535)
    return (millivolts - 500) / 10


tmp36 = analogio.AnalogIn(TMP36_PIN)


while True:
   
    temp_C = tmp36_temperature_C(tmp36)
   
    temp_F = (temp_C * 9/5) + 32
   
    print("Temperature: {}C {}F".format(temp_C, temp_F))
    time.sleep(1.0)
    lcd.set_cursor_pos(0, 6)
    lcd.print( "{}C " .format(temp_C)) 
    lcd.set_cursor_pos(1,0)
    lcd.print( "{}F" .format(temp_F)) 
```

## 7. Rotary Encoder

The RE is similar to a potentionmeter but it can continuously spin and has a built in button. I like the RE and I think that it could be used in projects later on. I again think that Circuit Py was Unnecessary for this but its not up to me.

![Rot_Encoder](https://github.com/cwyatt29/Q3-Engineering-Notebook/blob/master/ROTENCODER_REAL.MOV?raw=true)
```python
#CREDIT TO PAUL WEDER
import rotaryio
import time
import board
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
import digitalio
import neopixel

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.5 

i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x3f), num_rows=2, num_cols=16)


enc = rotaryio.IncrementalEncoder(board.D9, board.D8,2)
last_position = None

encBtn = digitalio.DigitalInOut(board.D7)
encbtn = digitalio.Direction.INPUT
encbtn  = digitalio.Pull.UP

global prevState

def btnControl(buttonVal ,out):
    global prevState
    if buttonVal and buttonVal != prevState:
        prevState = True
        if out == 0:
            dot.fill((255,0,0))
        elif out == 1:
                dot.fill((255,255,0))
        else:
                dot.fill((0,255,0))
    elif  not buttonVal:
        prevState = False
     
        

def retEnc(x):
    array = ["stop","caution","go"] 
    output = x%3
    btnControl(encBtn.value,output)
    return array[output]




while True:
    lcd.print(retEnc(enc.position))
    time.sleep(.05)
    lcd.clear()
    print(f"{retEnc(enc.position)} {enc.position} {encBtn.value}")
```

## 8. OnShape Certification


