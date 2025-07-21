# Wrist Rehab Monitor

This is a wrist rehab monitor that uses sensors to track my wrist position. Using these sensors, I can do exercises with certain commands on my phone.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Nathan S | Gunn High | Mechanical Engineering | Incoming Sophomore


# Modifications and Milestone 4
<iframe width="560" height="315" src="https://www.youtube.com/embed/prqU0wx1FoE?si=R8ZuYPn1hL16R7zK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description
For my modifications and final milestone, I added a vibration motor, soldered all my wires to the pcb, and attached all components to my wrist compression band using either sewing or velcro tape. The vibration motor works by rotating an unbalanced mass, which causes vibrations. Some vibration motors work differently, using internal parts that move back and forth instead of rotating to create the vibration effect. I used the vibration motor to alert my wrist of bad posture when none of the serial processes were running, essentially an “idle mode” to ensure my wrist stayed out of the incorrect range. In the code, when no other processes were active, the vibration motor would activate (see Milestone 4 Modification Code, Appendix). I set pitch thresholds for the vibration motor. Although I tried using roll and pitch values for more precise thresholds, I decided to keep it simple and used only the pitch. Since the accelerometer readings are relative to the sensor’s position, the motor would activate even when I moved my arm, not just my wrist. To avoid this, I chose to rely on only pitch data. Soldering the wires was relatively straightforward, with only minor issues. The only component I sewed directly onto the wrist compression band was the esp32. Due to the number of pins, I sewed it upside down to avoid the discomfort of pins pressing into my skin while exercising. For the flex sensor, neopixel strip, and pcb, I used velcro tape to secure them to the wristband.


<img width="1398" height="1056" alt="image" src="https://github.com/user-attachments/assets/e756b088-a63c-4ea7-9862-bd27f7247598" />

Figure 1 - Vibration motor with forward and back motion to create vibrations


# Challenges
One minor inconvenience was about the size of my original pcb. The pcb kit that I recieved contained 2 pcbs, one big and one small. The bigger pcb had a the negative and positive power rails, but the smaller one did not. So I originally planned on using my big pcb board for this project. However, after checking how many parts I had, I realized that I didn't have enough space for the big pcb board. However, the smaller pcb didn't have power rails, which was a problem. On the breadboard, my project took advantage of many holes in the power rails. But now that I was using a small pcb without any power rails, I had to make my own power rails. Since 5 of the holes on each side of the pcb were connected, I decided to use a jumper wire and connect the 5 on each side together. This made my rail for power, and on the other side, I did the same to make another rail for ground. Once I had these 2 rails, soldering everything else wasn't a challenge. 

Once I was finished soldering, I tested all my process on the BLE serial, but the buzzer wasn't buzzing like normal. I tested another buzzer on my breadboard with my flex sensor, but it was working fine. My buzzer that was soldered in was also connected properly, so I figured it was an issue with the buzzer itself, or the resistor. I de-soldered the resistor, and then the buzzer came back to life. It turns out that my resisor was actually dampening my buzzer to the point where I couldn't hear it. After taking out this resistor and soldering a wire jumper in its place, my project was finally working like it should have been.

# Next Steps
I think I am going to make some final tweaks to my vibration motor threshold, and start practicing for demo night.
  
# Milestone 3
<iframe width="560" height="315" src="https://www.youtube.com/embed/TtNWwhgmzoE?si=y4RP5K2Os8aOa1Lf" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description
For my final milestone, I decided to add bluetooth capabilites to my wrist rehab monitor. This allows me to project a serial monitor on an app on my phone via bluetooth. For bluetooth, I first had to download the BLE serial library off Arduino IDE. After including this library in my code, I just had to use BLE.print instead of Serial.print. The Serial.print command prints lines into the serial monitor on my computer, while BLE.print prints using bluetooth connection, which prints onto the serial on my phone. Once I replaced the Serial.prints to BLE.prints, the data that was originally printing on my computer was printing onto my serial app on the phone. Once I got the bluetooth working, I decided to work on some physical aspects of my project. I decided to hold off sewing and soldering everything onto my main wrist compressin band because de-soldering and undoing the sews could become complicated if I made a mistake before the modification process. However, to start preparing to put my components onto the wrist compression band, I disconnected my flex sensor from the breadboard. I soldered the flex sensors to the wires, and then plugged the wire back into the breadboard. I also sewed on the accelerometer onto my wrist compression band so testing some mechanisms would be easier.

The flex sensor functions seemed relatively empty compared to the accelerometer, so I decided to turn that into another exercise tracker. Instead of alerting for improper posture, I decided that I would turn it into a tracker for holding my wrist at a certain position. To track the time that I was holding my wrist at a position, I decided to use neopixel light strips. The idea was that after bending my wrist, the flex threshold would be exceeded, and then the neopixel lights would start to turn on one by one. I quickly soldered on the neopixel light strip to some wires and connected these wires to my breadboard. Then I downloaded the correct library for the lights and included them into the code. The main function of the lights were, when the flex threshold was exceeded, the sequence turned on. When it turned on, the first light would be set to blue, and using the same timer logic that I used for the calibration system, after 0.5 seconds the next light would also turn blue, and then the timer would reset and start back from 0. Now I had 6 lights on my light strip. After all 6 turned to blue, I changed the color so it would turn to green for 1 second. After 1 second, the lights all turn off and the sequence starts again. Another part that I added was that if the flex sensor went back under the threshold while the sequence was running, all the lights would turn off (refer to Milestone 3 Neopixel Code).

## Neopixel LED Strips
NeoPixels are  LEDs that are individually addressable, meaning each one contains a tiny circuit with red, green, and blue LEDs, along with a driver chip. This allows each LED to be controlled independently in terms of color and brightness. The neopixel LEDS use a single digital pin on the microcontroller, which is enough to control the entire strip of LEDS. The microcontroller sends a stream of 24-bit data or 3 bytes for RGB, and each LED reads it before passing the rest down the line. This data transmission relies on precise timing, where the length of electrical pulses determines whether a bit is read as a 1 or a 0. Each LED decodes its information, updates its color, and then refreshes and passes on the data to the next LED, ensuring reliable communication across the entire LED strip.

<img width="1000" height="450" alt="image" src="https://github.com/user-attachments/assets/07838909-788d-48a8-bc04-703fac3c1d3e" />
Figure 2 - Neopixel LED diagram. The middle circle is the driver chip

## Bluetooth User Interface

After this, I turned my attention back to the bluetooth serial on my phone. I wanted to make a little user interface system. Currently, the serial on my phone was printing all data values, like the flex sensor value, roll, pitch, reps, and sets. Instead of printing all of these at the same time, I wanted them to print one at a time if I entered little commands into the serial. So, using booleans and if statements, I organized my code into this format. To start, I wrote a little code block to check if there was anything available to read using the BLE.available code. Then, if anything is available, it reads the full string up to a new line using BLE.readStringUntil('\n'). Now I added my conditions for my commands using the booleans. I used the command.equals to check if the string that I input into the serial monitor was the correct command. If it was the correct command, the corresponding boolean would be set to true, and all other booleans would be set to false. I used an if statement for the first command, then a series of else if statements for the rest of the commands (refer to Milestone 3 User Interface Code). 

My first command was to display the menu when the string "menu" was typed into the phone serial. If it was typed, the BLE.print would display the menu. My menu consisted of the commands that a user could type into the serial for certain functions. The commands that I had were "calibrate", "start workout", "end workout", and "show angle". Each of the commands set a certain boolean to true, and all others to false. The calibrate command started the calibration process. I also decided to change the wait time in the range from 3 seconds to 2.5 seconds, and the inactivity time from 15 seconds to 2 minutes. After calibration, the monitor was ready to start the workouts. The "start workout" shows the rep and set counter. At this point in time, my rep and set counter was printing every delay, and was lagging my phone. After a couple challenges, I was able to change to rep and set counter so that it would only print when it was updated. The "end workout" command turns off the rep and set counter, and displays a workout summary. The workout summary consists of a total amount of reps and sets that the user did during the workout. Displaying this screen was also a bit of a challenge due to some placement errors in my code. Finally, the "show angle" command displays the pitch and flex sensor values, and I plan to change the flex sensor values into angular values later on. Now these commands are very specific to things like spaces or capital letters, so I added an or statement to each command, and made another command option. For example, "start workout" or "start workout ". This space at the end ensured that even if the user typed in a space at the end (which is common if the phone autocorrects the word), the correct displays would still pop up. 

<img width="750" height="1286" alt="image" src="https://github.com/user-attachments/assets/8b0c81da-26de-49e6-92a7-b0eb4b42a805" />

Figure 3 - Menu display with new serial monitor. Available commands are shown under

# Challenges
Some of the big challenges was creating the user interface and connecting the esp32 to the bluetooth. The concept was a little confusing at first, because of all the booleans and conditions. But after creating one condition for the calibrate function, I was able to create the rest of the conditions and start organizing my code into the specific conditions. Another obstacle I faced was how laggy my phone got when the rep and sets counter was printing. Due to how fast it was printing, it overloaded my serial monitor. So I decided to only print out the reps and sets if the rep or set count got updated. I created a new variable called prevRep. The idea was that I would set my repCount equal to the prevRep, and while this was true, my code wouldn't print out anything. But as soon as the repCount increased and was no longer equal to the prevRep value, the serial monitor would print the rep and set count once. The problem was I didn't know where to put my prevRep = repCount statement. After an hour of debugging, I finally realized that if I wanted my serial monitor to only print once, I would have to immediately set prevRep = repCount after the counts printed. So, I put the statement right after all the print functions, and the serial monitor finally printed out the counts only when they were updated. 

<img width="750" height="1277" alt="image" src="https://github.com/user-attachments/assets/2f156c25-562d-437d-ae65-75be1e4a727c" />

Figure 4 - New serial monitor with fixed counters

Another challenge I faced was that even when I typed the "end workout" command in my serial monitor, the display screen wouldn't pop up and the rep and set counts would keep going (this is before I fixed the counters to update only once). At first, I set the boolean that starts the counters to false within the loop that set my end workout boolean to true, but that didn't really do anything. And then I saw that my end workout loop was actually inside my loop that started the workout and counters. At the beginning of my void loop, the statements that turned on my boolean to true or false set one thing to true, and all others to false. Because my end workout loop was within my start workout counters loop, the end workout would always be set to false. So I moved the end workout loop outside of the start workout loop, and it was working. If I typed in "end workout" the display would stop showing the counters for the workout, and display the total number of reps and sets. 

<img width="750" height="1294" alt="image" src="https://github.com/user-attachments/assets/8808be41-a3a8-4003-afe9-5da09255032d" />

Figure 5 - New serial monitor with workout summary and fixed counters

# Next Steps
The next steps are to start putting all the components together, and solder the components onto a pcb. Also, I will start to add modifications to my wrist rehab monitor. I was thinking of adding a vibration component that vibrates if bad posture is detected. It will only vibrate if the other functions like the workout or calibration are not on.


# Schematics

<img width="867" height="563" alt="Screenshot 2025-07-15 at 9 56 20 AM" src="https://github.com/user-attachments/assets/4cfdf0cf-3267-40b4-a43c-aa6406b001ea" />

# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/zGtJvBaJgOA?si=yHCSrj1Uw0e5ISD-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description
Before working with LSM6DS3 + LIS3MD, I learned about how it worked. The LSM6DS3 + LIS3MDL is a sensor combo that includes an accelerometer, a gyroscope, and a magnetometer. The accelerometer measures movement or tilt (like if something is going up, down, or sideways). The gyroscope measures rotation and angular velocity (like turning or spinning). The magnetometer works like a digital compass, as it can sense direction based on the Earth's magnetic field. All together, these three sensors help track motion and orientation in three axes. Inside the accelerometer there’s a tiny mass called a proof mass that moves a little when the device moves. Because of inertia, this mass resists changes in motion. When the device accelerates, a force (F) acts on the mass, and according to Newton’s second law, F = ma, this force is equal to the mass times its acceleration. This force causes the proof mass to push or pull on a spring. This movement changes an electrical property in the sensor, like resistance, which the sensor turns into an electrical signal. By measuring that signal, we can tell how much the device is accelerating and in what direction.

![image](https://github.com/user-attachments/assets/acc4e815-edb2-49d7-b2e6-0d4a5cb08871)

Figure 6 - Accelerometer diagram

For the sake of not typing out "LSM6DS3+LIS3MDL" every single time, from now on I will just call it "accelerometer" or "module". For my second milestone, I first connected my accelerometer to my esp32. Then I downloaded a bunch of libraries for the module. It took a couple times because there were many codes for different versions of the accelerometer. But after finding the correct code off the library, I was able to upload the code and get my values for the accelerometer. The accelerometer had values x, y, and z, and it also had gyro data, which measured angular velocity. However, I didn't use gyro data as the movment of my wrist would be relatively slow, and velocity values wouldn't have varied enough in movement for me to use them. When I rotate the accelerometer in a certain way, the values change. When stationary, the z value always hovers at around 9.8 m/s^2 due to gravity.

![image](https://github.com/user-attachments/assets/499fa274-1a19-4c1f-aa17-6cb33e9ccb12)

Figure 7 - Accelerometer data

I originally planned on using these values to put a threshold on them and also make the LED and piezo buzzer. However, when I put the accelerometer on my wrist, I realized that the accelerometer values had minimal change when I moved my wrist side to side. Accelerometer values weren't going to work for my side to side motion on the wrist. So, I downloaded the Madgwick filter from the library, and took a code off of it. This Madgwick filter code changed my acceleration x,y and z data into roll, pitch, and yaw data. Roll, pitch, and yaw are usually used for aviation (see figure below). 

![image](https://github.com/user-attachments/assets/1c562fa3-2452-40d5-8d3b-734b37a9df4b)

Figure 8 - Roll, pitch, and yaw diagram

For my side to side motion, yaw was the perfect fit as it calculated the angles when I rotated my wrist. At the stable position with the accelerometer facing straight, the angle measured 360 degrees. I wanted my side to side movement to trigger the buzzer and LED after a certain angle that my wrist went past. So I first set two thresholds, one when my wrist went right and the other for when my wrist went left. I set my first value at 40 deg to the left, and 340 deg for the right, which is 20 deg off from center position. When my wrist angle went past these certain angles, the LED would turn on and the buzzer would beep. One thing to note was that my data values for yaw were drifting heavily; the values were constantly decreasing even without any movement on the accelerometer. Realizing that there would always be some drifting on my yaw values, completely scratched the idea of having thresholds on my yaw values. 

I repurposed my accelerometer to graph data whenever I fully rotated my wrist. I wanted my wrist rehab device to track things like how many rotations someone has done or track the range of motion from a wrist. To make the graph from my accelerometer data values, I first changed my code. I took out all the thresholds, and replaced the code to first print out only roll and pitch. Since my yaw data kept drifting, I just decided to not use it at all. I also decided to change my data outputs to CSV which is comma separated variables. These comma separated variables had no words, only numerical values separated by commas, which would be easier to be plotted by a serial plotter. Then I downloaded a separated serial monitor/plotter as the one on arduino was very laggy. When I first plotted the values, the graph was very unstable. After fixing this issue, the graph was working properly, with the roll and pitch values spiking whenever I rotated my wrist. 

After graphing the roll and pitch properly, I decided to find thresholds for only the pitch, which is the up and down motion. For one exercise such as the wrist rotation, the pitch and roll goes up and down, but for an exercise like wrist flexing, the roll doesn't change and only the pitch goes up and down. For now, I decided to only find the pitch thresholds to be simple. I set the high pitch threshold at 20 degrees, and the low pitch threshold at -38 degrees. However, a wrist rotation or a flex motion that is too slow doesn't have much affect. So, I set a millis function and variables in order to start a timer when the pitch value hit the high threshold (refer to Milestone 2 Threshold and Counter Code, Appendix). If the time that is spent getting to the lower threshold from the higher threshold is greater than 1.75 seconds, that specific rotation won't count towards a repition. 

I wanted a way to keep track of each repition that went above 20 deg and below -38 deg in the span of 1.75 seconds. So, in the code, I made a repCount variable to count how many reps of the wrist rotation or flex that I had done. The repCount starts at 0 and every rep, the count is increased by 1 until 10. Then, I also added a set count. I used a setCount variable to keep track of sets. If the repCount hit 10, the repCount would be set back to 0, and the setCount would go up by one. After 3 sets, the setCount would be set back to 0, and the exercise would be complete. 

Since measuring data or finding thresholds while the wrist was unstable or when it was moving too much is not reliable, I added a calibration system to the wrist rehab monitor. I wanted the pitch to be relatively close to 0 when starting the exercises, so I put the calibration range to -2 to 2 degrees. If the wrist was in this position for pitch, I considered it safe enough to start exercising. I also put a time requierment of 3 seconds. The pitch data had to be at -2 to 2 for at least 3 seconds before the calibration process was complete. While it wasn't calibrated, the serial monitor prints out "Calibrating...", and when after the 3 seconds of calibration, the serial monitor starts printing the repCount and setCounts. 

# Challenges
A big challenge that I faced in this milestone is that my yaw values kept on drifting, even in the stationary position. At first I thought this was because of the built in compass. The accelerometer module calculates yaw using the built in compass and magnometer. However, in a room full of magnetically conductive materials, these calculations may have been distorted. So in my code, I told arduino to not use the compass, in hopes that the yaw data would stop drifting. After doing some research, I learned that no matter what, due to certain limitations within the sensor or environment, there would always be some drift in yaw values. The only real way to fix it was to press the reboot button on my esp32 So, I repurposed my accelerometer and made it so it didn't use yaw. Also because I realized that I wouldn't really be moving my wrist from side to side. Another challenge that I faced was incorrect graph readings. When I first printed my data values for roll and pitch, I didn't use csv, and the words "roll" and "pitch" were also printed. This lead to unstable graphs, and only one line of value, instead of two for roll and pitch (see figure 9 below). So, I altered the print lines in the code to only print numerical values, seperated by commas. This time when I made the graph, it had two lines for roll and pitch, but it was very unstable. So I altered my code again. This time, I created a loop that took the average of 5 readings for roll and pitch, then gave me the value of the averages (see Milstone 2 Average code, Appendix). While this graph did look more stable, the lables on the y axis didn't make sense, as the values were too small to be averages. When I rotated my wrist, I was making big angular changes in position. Since roll and pitch measure angles, there should have been pretty big spacing on the y axis. So, I also scratched this code. I went back to my first problem, when my graph was unstable. I changed the sample frequency to 20 milliseconds, and the delay time to 50 milliseconds. The delay time (50) times the sample frequency (20) was 1000 milliseconds, which made for a more stable graph. Now the angle readings were also correct. Every time I completed a rotation, the values would spike at a consistent height. 



<p float="left">
  <img src="https://github.com/user-attachments/assets/248c6972-4578-457c-9108-50c756b31698" width="230" />

  <img src="https://github.com/user-attachments/assets/8e424ad8-e848-4ded-b81c-6fb16fa4dd61" width="230" /> 

  <img src="https://github.com/user-attachments/assets/89acac75-edd3-47c3-8ecf-11cdb2cf70c4" width="230" /> 

</p>

Figure 9 - Graphs of roll and pitch, with time on the x axis and roll and pitch angles on the y axis

Graph 1 - First unstable graph WITHOUT csv

Graph 2 - Second graph WITH csv and averaging

Graph 3 - Third graph WITH csv and NO averaging

Creating the calibration system was also a bit challenging because of the timer. I had to use the millis function and lots of variables to calculate the exact time. The inRangeStart timer starts counting as soon as the wrists position goes in the range of -2 to 2. For 3 seconds the wrist position must stay in this range. If at any point it exists the range, the inRangeStart timer will reset. This calibration system ensures that the tracking only starts when I'm at a consistent starting position.   

# Next Steps
Next, I will sew my accelerometer on my wrist compression sleeve so I don't have to keep holding on to it, and so the movement of the accelerometer is more natural. I'm also going to figure out the bluetooth on my esp32 because I want to display some certain texts on the serial monitor on my phone, and having the esp32 always connect to the computer is a bit inconvenient.

# Schematics

<img width="946" height="543" alt="Screenshot 2025-07-15 at 9 56 31 AM" src="https://github.com/user-attachments/assets/c523b0ca-2f3f-4cf4-a101-7d74ced67101" />

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/UryxP8tovaY?si=vhKdE8WHcJufKPs5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description
As a part of my first milestone and learning experience, I decided to make a mini project using the arduino to figure out some basic coding in C++. I made a little sequence of lights that acted like traffic lights, with decently accurate time delays to replicated real life traffic lights. In the code, the leds that I used work off a digital signal to turn it on (HIGH) or off (LOW). The code digitalWrite signals these on and offs (see code below, traffic light code, Appendix). I also used some 220 ohm resistors as these were the best fit from the Ohms law calculations. The arduino charged 5 volts, and the leds current value was 0.02, so the right resistor to use was near 250 ohms. The close option was 220, so that's what I decided to use. 

![Headstone Image](Adobe Express - file.jpg)

Figure 10 - Traffic light arduino project

My first milestone was to connect the flex sensor to the esp32 (main controlling unit), and also add threshold values. The code I'd have to make is that when the threshold is exceeded by bending the sensor, the LED and piezo buzzer that I connected would beep and turn on. The flex sensor is a big resistor, and bending it to a certain degree changes the resistance values. Conductive ink sits on the top of the flex sensor, and when it is bent, the ink outside of the bend is stretched, leading to increased resistance. This is what changed the actual number values that were output by the sensor (see figure below). I printed these flex sensor values to find my threshold for the LED and buzzer. When the flex sensor is straight, it outputs a value of 1800, and when bent to a certain degree, the number increases or decreases. Since I planned to use the flex sensor for detecting bend in only one direction, I only need one threshold. I set my LED and buzzer threshold at 2400. The code sets the LED and buzzer to HIGH once the flex sensor threshold is exceeded, turning them on, otherwise, they are both set to LOW. I used analog read because the flex sensor is connected to pinA6 on the esp32, which is an analog pin. When the sensor bends, the resistance changes, so voltage at the analog pin changes, and the analog read reads the data values (see code below, Milestone 1 code, Appendix). 

![image](https://github.com/user-attachments/assets/8f77114c-049b-442f-a3d8-8aeb1de83724)

Figure 11 - Flex sensor diagram

## Piezo Buzzer
The piezo buzzer has a piezoelectric ceramic disk inside of it. Piezoelectric materials, such as the disk, produce physical deformation when an alternating voltage is applied to the buzzer, the ceramic disk rapidly expands and contracts. This movement pulls on the surrounding air and generates sound waves. The pitch and frequency of the buzzer is determined by how fast this ceramic disk is vibrating. Higher rates of vibration result in higher pitch and vice versa. 

<img width="928" height="497" alt="image" src="https://github.com/user-attachments/assets/ba2b5717-38d6-4794-ab85-159a81cb174c" />

Figure 12 - Diagram of the piezoelectric buzzer

# Challenges
Some challenges that I faced were connecting things to the esp32 and the breadboard. The breadboard layout was confusing at first, as I didn't really understand how the electricity path flowed throughout the board. Another challenge was connecting the flex sensor. The flex sensor works off a voltage divider, which is a small circuit that that reduces voltage to a lower level, dividing input voltage into smaller outputs. I had to search some online schematics that showed me how to connect the flex sensor to the esp32. I also tried connecting the LSM6DS3+LIS3MDL (accel,gyro and magnometer), but I realized that I would also have to connect the codes and find more thresholds, so I saved that for the next milestone.

# Next Steps
My next plan is to connect the accelerometer to my esp32, and also get the threshold values for that sensor. As of now, I downloaded a code from the library that lets my LSM6DS3+LIS3MDL sensor give me acceleration and angular velocity data for the x, y and z axis. I plan on using some of the these values as threshold for the next step. The flex sensor will sit on the top of my wrist, regulating the up and down motions, while the LSM6DS3+LIS3MDL will regulate side to side motions on my wrist.
# Schematics 
![image](https://github.com/user-attachments/assets/50e9d166-e03b-494d-adb5-1d321a094b3b)

Figure 13 - Flex sensor connected with led and buzzer to esp32

# Bill of Materials

| **Part**               | **Note**                                   | **Price** | **Link**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|:----------------------:|:------------------------------------------|:---------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ESP32                  | Main microcontroller for project           | $5.33     | [Link](https://www.amazon.com/ESP-WROOM-32-Development-Microcontroller-Integrated-Compatible/dp/B08D5ZD528?source=ps-sl-shoppingads-lpcontext&ref_=fplfs&smid=A2Z10KY0342329&gQT=2&th=1)                                                                                                                                                                                                                                                                                                          |
| Flex Sensor 4.5"       | Measures wrist tilt                         | $17.95    | [Link](https://www.sparkfun.com/flex-sensor-4-5.html)                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Adafruit LSM6DS3+LIS3MDL | Accelerometer, Gyroscope, and Magnetometer | $19.95    | [Link](https://www.adafruit.com/product/5543?gad_source=1&gclid=Cj0KCQjw4MSzBhC8ARIsAPFOuyW3bKrwhMSo2VoSfvSt319uDnnbDld4MoYm0IzXAV2mbivYMjEGez4aApeGEALw_wcB)                                                                                                                                                                                                                                                                                                          |
| Wrist Compression Sleeve | Main baseplate for all components          | $15.97    | [Link](https://www.amazon.com/Sparthos-Wrist-Support-Sleeves-Pair/dp/B074CXL9RM/ref=sxin_16_pa_sp_search_thematic-asin_sspa?content-id=amzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04%3Aamzn1.sym.f5052e1c-21bb-4068-ada8-6befb6325d04&crid=BSDK6TEHKM0P&cv_ct_cx=wrist%2Bcompression%2Bsleeve&dib=eyJ2IjoiMSJ9.a0DsiZrtl24MGErE3gc3hs-1seJpCWa444LFuc4uL7pQ2OfUK_CsEha6Uf9uNkDHGCFhBOGcesu0YlU33vWUZg.4T09Mf5m41lcN3unhAgnkf-BS-7wLZL42PAvfgzOW1I&dib_tag=se&keywords=wrist%2Bcompression%2Bsleeve&pd_rd_i=B07G4JCSJ7&pd_rd_r=5b8b03e2-eea7-49ee-9e5f-8cbb186e681e&pd_rd_w=S03mj&pd_rd_wg=NPat3&pf_rd_p=f5052e1c-21bb-4068-ada8-6befb6325d04&pf_rd_r=0BBVYDM9P8428SY3RMC3&qid=1719355435&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=wrist%2Bcompress%2Caps%2C446&sr=1-2-baa1f287-65d3-41a3-a655-8bbba0531537-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9zZWFyY2hfdGhlbWF0aWM&th=1&psc=1) |
| Anker Power Supply      | Supplies power when not connected to computer | $45.99    | [Link](https://www.amazon.com/Anker-PowerCore-Compact-Charging-Technology/dp/B0D12T6R7M/ref=sr_1_1?crid=X0W755UZJA4U&dib=eyJ2IjoiMSJ9.8NRafpLKlAfEdfReu0S2LYFCA-GU_fEs3WW88yk-qnFHppOI0gxpZ_PhpBodwFOGt1Lmr7miX0m0OuQ_TJi1jEjkNLwvDEJ3NoCVKPCW9vcglBQLZ7JULPlQOFlmcnZZTtBkljT2WD9L01BbujwW1BYplH4Wss6RvU0QbaFrB44spbT9WsIxgn1U7lrOlDt96vqw-heVP2VKe4HInv8Pe20nvvxUQ0FJkXxEfBXth_k.u1Oh5LuoEIGvIXLSutmbjl9I5Z7iE_uYqOWohhYT264&dib_tag=se&keywords=anker%2Bpower%2Bcore%2Bslim%2B10000&qid=1752249912&sprefix=anker%2Bpower%2Bcore%2Bslim%2Caps%2C178&sr=8-1&th=1) |
| Sewing Kit             | To connect components onto the wrist compression sleeve | $5.99     | [Link](https://www.amazon.com/Coquimbo-Traveler-Beginner-Emergency-Organizer/dp/B01G3LOLD6/ref=sr_1_7?crid=27CESEBIVTX3Z&keywords=sewing%2Bkit&qid=1689572065&sprefix=sewing%2Bk%2Caps%2C192&sr=8-7&th=1)                                                                                                                                                                                                                                                                               |
| EPZLON PCB             | Plate to solder on all wires and components | $8.99     | [Link](https://www.amazon.com/EPLZON-Solder-able-Breadboard-Electronics-Compatible/dp/B09X1D1YMP/ref=sr_1_3?crid=23Z14BJ82C0RN&dib=eyJ2IjoiMSJ9.Fs9Pt-Jp_mMT29OohvW3YZHw4lUJpA-Trj1wH7yRXmoF3DU3m2_PzGaeocJeDNOfopXY5KD36-DSmggi50Lvp5oqzh3EIxq7GAh2tDgSob4hNsmQu3ovyT6VkKq_Z5golvsD9zEDuxBkT1xhH5tuZ4fgAUdpIwzqUH_QE5d9ZKR5PI1jbtJLE1zRN2XNTrqpGf9z4WzBdUAUGq6i0FpYTtV54PMXcLROUpqiT2_crPY.LmfxnsVzuu9ucKLL-83MhoWy0GCb2BVmPUYz8l_I1rc&dib_tag=se&keywords=EPLZON%2Bprotoboard&qid=1752250150&sprefix=eplzon%2Bprotoboard%2Caps%2C199&sr=8-3&th=1)  |
| Piezo Buzzer           | Buzz for improper form                      | $6.99     | [Link](https://www.amazon.com/mxuteuk-Electronic-Computers-Printers-Components/dp/B07VK1GJ9X/ref=sr_1_6?dib=eyJ2IjoiMSJ9.wAyBeRS6gVe44PjVRBtGDNKks-EH_IddvvbrS5lP7ws8lbLh8RNqBaH9kb5xhXhl7MI8WQtio_tKkeH1YD6_yiGX7h2PwsC4Xm4emaporthsw8TqLLYHf3gw3xr_dTGaPUfmfdeCkpORNEhcAxsMfZYgGrRB0yphDoV5bsa_IT1CHUCMRTKJWfTyijyewlOycoYia-zs1sdJNdwYkWur90jqeI909HZS__vONk1Wv9DgVwvs1mk42ujIPDjLdWqpExujHId0l_C_ESKqP2n46A47I6sWRHoHtI9DI8k_ecA.kZsqmeDgDZNGjmc9dBGyjua1olRzvS49-2NieqlP5hI&dib_tag=se&keywords=piezo+buzzer&qid=1719416785&sr=8-6)  |

# Starter Project - Retro Arcade Console

<iframe width="560" height="315" src="https://www.youtube.com/embed/lbEyTJAkzWc?si=9pJWD1YZEUp0lTTe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description 
  My starter project was the Retro Arcade Console, and I chose it because there were only two options and the console seemed somewhat more fun. It was my first time soldering, and the project really helped as there were many joints to solder. I learned many soldering skills such as a through hole joint, soldeirng wires, stripping wires, and de-soldering. The console has a couple games such as tetris and a bad version of galaga. The 4 buttons consisting of up, down, left, and right on the left are the actual controls, while the up and down button are used for things such as selecting or firing. The two big LED matrices act as the screens, and there is also an LED scoreboard at the top. The console is also powered by usb or three AA batteries.

# Challenges 
  One challenge was that when I tried to power my console with batteries, it wouldn't turn on at all. I checked my wires and I realized that during my soldering process, I had accidentally burned a part of the ground wire, which wouldn't allow it to turn on. So I had to cut the wire to take out the burnt part, and then strip the wire. After soldering the wire back together and using a heat shrink, the console worked perfectly fine through battery power. 
  
# Next Steps
  I will use the skills that I learnt from my starter project and apply it to my intensive project, the Wrist Rehab Device. Since I dont know how to use an Arduino or how to code, I'm going to start on learning the basics first. Then I will start to work on my intensive project.  

# Appendix
# Traffic Light code
```c++

void setup() {
  // put your setup code here, to run once:
  pinMode(12,OUTPUT);
  pinMode(11,OUTPUT);
  pinMode(10,OUTPUT);
}

  
void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(12,HIGH);
  delay(6000);
  digitalWrite(12,LOW);
  digitalWrite(10,HIGH);
  delay(2000);
  digitalWrite(10,LOW);
  digitalWrite(11,HIGH);
  delay(1000);
  digitalWrite(11,LOW);

}

```

# Milestone 1 code
```c++

const int flexPin = A6;           //Flex sensor pin to A6 (esp32)
const int ledPin = 23;            //Led pin to 23 (esp32)
const int buzzer = 19;            //buzzer pin to 19 (esp32)

void setup() { 
  Serial.begin(115200);           //baud rate to 115200
  pinMode(ledPin,OUTPUT);         //set led as an output
  pinMode(buzzer,OUTPUT);         //set buzzer pin as an output
} 

void loop(){ 
  int flexValue;                  //flex sensor numerical outputs set as integers
  flexValue = analogRead(flexPin);//read flex sensor
  Serial.print("sensor: ");
  Serial.println(flexValue);
 
  if(flexValue>2400) {            //flex value threshold
     digitalWrite(ledPin,HIGH);   //turns on led if threshold exceeds
     digitalWrite(buzzer,HIGH);   //turns on buzzer if threshold exceeds
  }
  else {
    digitalWrite(ledPin,LOW);     //nothing happens if threshold is not exceeded
    digitalWrite(buzzer,LOW);
  }
  delay(20);
  
} 
```

# Milestone 2 Average code 
```c++
#include <Wire.h>                             //inclue these from library
#include <Adafruit_LSM6DS3TRC.h>
#include <Adafruit_LIS3MDL.h>
#include <MadgwickAHRS.h>

Adafruit_LSM6DS3TRC lsm6ds3trc;
Adafruit_LIS3MDL lis3mdl = Adafruit_LIS3MDL();
Madgwick filter;

const float sampleFreq = 20.0;                // sample frequency of 20 hertz
float average;                
float averagep;
int  cnt=0;
int  cntp=0;

void setup() {
  Serial.begin(115200);
  while (!Serial) delay(10);

  if (!lsm6ds3trc.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C!");
    while (1) delay(10);
  }

  if (!lis3mdl.begin_I2C()) {
    Serial.println("Failed to find LIS3MDL!");
    while (1) delay(10);
  }

  filter.begin(sampleFreq);
}

void loop() {
  sensors_event_t accel, gyro, temp;          //create events
  sensors_event_t mag;

  lsm6ds3trc.getEvent(&accel, &gyro, &temp);  //read data from these
  lis3mdl.getEvent(&mag);                     //read data from magnometer

  float gx = gyro.gyro.x * 180.0 / PI;        //convert radians per sec to degress per sec
  float gy = gyro.gyro.y * 180.0 / PI;
  float gz = gyro.gyro.z * 180.0 / PI;

  float ax = accel.acceleration.x / 9.80665;  //convert acceleration from m/s^2 to G force
  float ay = accel.acceleration.y / 9.80665;
  float az = accel.acceleration.z / 9.80665;

  filter.update(gx, gy, gz, ax, ay, az, mag.magnetic.x, mag.magnetic.y, mag.magnetic.z);

  float roll = filter.getRoll();              //Get current roll and pitch values from sensor
  float pitch = filter.getPitch();

  
    float sumr=sumr+roll;                     //current sum = past sum + value of roll or pitch
  cnt=cnt+1;

  float sump=sump+pitch;
  cntp=cntp+1;
  

  

  // Serial Plotter format: label:value, separated by commas

  if(cnt==4){                                //Set count limit to 4, start at 0
    average=sumr/5;                          //After 5 counts, take average of sum
    Serial.print(" ");                       //print average
    Serial.println(average);
    cnt=0;                                   //set count and sum back to 0
    sumr=0;
  }
  if(cntp==4){
    averagep=sump/5;
    Serial.print(", ");
    Serial.println(averagep);
    cntp=0;
    sump=0;
  }
  
  delay(50); // ~100Hz
} 
```

# Milestone 2 Threshold and Counter Code
```c++
#include <Wire.h>
#include <Adafruit_LSM6DS3TRC.h>
#include <Adafruit_LIS3MDL.h>
#include <MadgwickAHRS.h>

Adafruit_LSM6DS3TRC lsm6ds3trc;
Adafruit_LIS3MDL lis3mdl = Adafruit_LIS3MDL();
Madgwick filter;

const float sampleFreq = 20.0;

unsigned long inRangeStart = 0;
unsigned long repStart = 0;

bool calibrated = false;
bool waitingForDip = false;

int repCount = 0;
int setCount = 0;
void setup() {
  Serial.begin(115200);
  while (!Serial) delay(10);

  if (!lsm6ds3trc.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C!");
    while (1) delay(10);
  }

  if (!lis3mdl.begin_I2C()) {
    Serial.println("Failed to find LIS3MDL!");
    while (1) delay(10);
  }

  filter.begin(sampleFreq);
}

void loop() {
  sensors_event_t accel, gyro, temp;
  sensors_event_t mag;

  lsm6ds3trc.getEvent(&accel, &gyro, &temp);
  lis3mdl.getEvent(&mag);

  float gx = gyro.gyro.x * 180.0 / PI;
  float gy = gyro.gyro.y * 180.0 / PI;
  float gz = gyro.gyro.z * 180.0 / PI;

  float ax = accel.acceleration.x / 9.80665;
  float ay = accel.acceleration.y / 9.80665;
  float az = accel.acceleration.z / 9.80665;

  filter.update(gx, gy, gz, ax, ay, az, mag.magnetic.x, mag.magnetic.y, mag.magnetic.z);

  float roll = filter.getRoll();
  float pitch = filter.getPitch();

  unsigned long currentTime = millis();

  // Calibration Logic
  if (!calibrated) {
    if (pitch >= -2 && pitch <= 2) {                                      //range of the calibration zone
      if (inRangeStart == 0) {                                            //check if timer is at 0
        inRangeStart = currentTime;                                       //
      } else if (currentTime - inRangeStart >= 3000) {                    //calibration finished after 3 seconds in range
        calibrated = true;
      }
    } else {
      inRangeStart = 0;                                                   //set timer back to 0 if exited range
    }
  }

  
  if (calibrated) {                                                       //check if its calibrated
    if (!waitingForDip && pitch >= 20) {                                  //waiting for dip is false and pitch goes above 28
      repStart = currentTime;                                             //rep time starts
      waitingForDip = true;                                               //waiting for dip turned true
    }

    if (waitingForDip) {                                                  //check waiting for dip is true
      if (pitch <= -38 && (currentTime - repStart <= 1750)) {             //if pitch goes under -38 in under 1.75 seconds
        repCount++;                                                       //increase repCount
        waitingForDip = false;                                            //set waiting for dip to false
        if(repCount == 11){
          setCount++;
          repCount = 0;
        }
      } 
  

      
      if (currentTime - repStart > 1750) {                                //if over 1.75 seconds
        waitingForDip = false;                                            //reset waiting time
      }
    }
  }


  Serial.print(roll, 2);
  Serial.print(", ");
  Serial.print(pitch, 2);
  Serial.print(", ");

  if (!calibrated) {
    Serial.println("Calibrating...");
  } else {
    Serial.print("reps: ");
    Serial.print(repCount);
    Serial.print(", ");
    Serial.print("sets: ");
    Serial.println(setCount);
      if(setCount == 3){
        Serial.println("Exercise Complete!");                             //print out when the exercise is complete
        setCount=0;
      }
       
  }
  
  delay(50);
}
```

# Milestone 3 Neopixel Code
```c++
#include <Adafruit_NeoPixel.h>

#define PIN         13                                                      //lights to  pin 13 
#define NUMPIXELS   6                                                       //number of lights
#define FLEXPIN     34                                                      //
#define FLEX_THRESHOLD 2400                                                 //flex threshold at 2400 for lights

Adafruit_NeoPixel strip(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

bool sequenceRunning = false;
unsigned long lastStepTime = 0;                     
int currentPixel = 0;

void setup() {
  Serial.begin(115200);
  strip.begin();                                                 //wake up lights and prepare 
  strip.show();                                                  //start with lights off
}

void loop() {
  int flexValue = analogRead(FLEXPIN);                           //read flex sensor
  Serial.print("Flex: ");
  Serial.println(flexValue);

  
  if (flexValue > FLEX_THRESHOLD && !sequenceRunning) {         //if the threshold is exceed and the lights are not on,
    sequenceRunning = true;                                     //sequence is turned on
    currentPixel = 0;                                           
    lastStepTime = millis();
    strip.clear();
  }

  if (sequenceRunning) {
    if (flexValue < FLEX_THRESHOLD) {
      resetStrip();                                             //reset lights if flex sensor is released 
      return;
    }

    if (millis() - lastStepTime >= 500 && currentPixel < NUMPIXELS) {     
      strip.setPixelColor(currentPixel, strip.Color(0, 0, 255));          //set light to color blue
      strip.show();                                                       //show color
      currentPixel++;                                                     //next light
      lastStepTime = millis();                                            //reset 0.5 second timer again
    }

    if (currentPixel == NUMPIXELS) {                                      //if the number of pixels reaches 6
      strip.fill(strip.Color(0, 255, 0));                                 //set ALL lights color to green
      strip.show();
      delay(2000);                                                        //hold for two seconds
      resetStrip();                                                       //reset after two seconds
    }       
  }

  delay(50);
}

void resetStrip() {
  strip.clear();
  strip.show();
  sequenceRunning = false;
  currentPixel = 0;
}
```
# Milestone 3 User Interface Code
```c++
#include <Wire.h>
#include <Adafruit_LSM6DS3TRC.h>
#include <Adafruit_LIS3MDL.h>
#include <MadgwickAHRS.h>
#include <Adafruit_NeoPixel.h>
#include <BleSerial.h>

Adafruit_LSM6DS3TRC lsm6ds3trc;
Adafruit_LIS3MDL lis3mdl = Adafruit_LIS3MDL();
Madgwick filter;
BleSerial BLE;
const float sampleFreq = 20.0;

#define PIXEL_PIN      13
#define NUMPIXELS      6
#define FLEX_THRESHOLD 2400

Adafruit_NeoPixel strip(NUMPIXELS, PIXEL_PIN, NEO_GRB + NEO_KHZ800);

const int flexPin = A6;
const int ledPin = 23;
const int buzzer = 19;

unsigned long inRangeStart = 0;
unsigned long repStart = 0;
unsigned long lastActivityTime = 0;

//booleans for user interface
bool calibrated = false;
bool waitingForDip = false;
bool counting = false;
bool sensorcount = false;
bool showCalibration = false;
bool endcount = false;


bool sequenceRunning = false;
unsigned long lastStepTime = 0;
int currentPixel = 0;

int repCount = 0;
int setCount = 0;

int prevRep;                                                                          //new variable to count only when reps or sets are updated

void setup() {
  Serial.begin(115200);
  
  pinMode(ledPin, OUTPUT);
  pinMode(buzzer, OUTPUT);
  
  BLE.begin("Nathans Servant");                                                       //my serial name

  if (!lsm6ds3trc.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C!");
    while (1) delay(10);
  }

  if (!lis3mdl.begin_I2C()) {
    Serial.println("Failed to find LIS3MDL!");
    while (1) delay(10);
  }

  filter.begin(sampleFreq);

  strip.begin();
  strip.show();

  BLE.println("Type 'menu' to see commands.");

}

void loop() {
  int flexValue = analogRead(flexPin);
  sensors_event_t accel, gyro, temp;
  sensors_event_t mag;
  lsm6ds3trc.getEvent(&accel, &gyro, &temp);
  lis3mdl.getEvent(&mag);

  float gx = gyro.gyro.x * 180.0 / PI;
  float gy = gyro.gyro.y * 180.0 / PI;
  float gz = gyro.gyro.z * 180.0 / PI;
  float ax = accel.acceleration.x / 9.80665;
  float ay = accel.acceleration.y / 9.80665;
  float az = accel.acceleration.z / 9.80665;

  filter.update(gx, gy, gz, ax, ay, az, mag.magnetic.x, mag.magnetic.y, mag.magnetic.z);

  float roll = filter.getRoll();
  float pitch = -1 * filter.getPitch();

  unsigned long currentTime = millis();

  if (BLE.available()) {                                                                                      //if there is a string available to read
    String command = BLE.readStringUntil('\n');                                                               //read until new line

    if (command.equals("menu") || command.equals("help")) {                                                   //if this is the string, set other booleans to false
      counting = false;   
      showCalibration = false;
      sensorcount = false;
      endcount = false;

      BLE.println("==== MENU ====");                                                                //menu display
      BLE.println("List of available commands:");                                                   //below is the list of available commands
      BLE.println("- calibrate       : Start calibration");                                         //print in BLE serial
      BLE.println("- start workout   : Start tracking reps & sets");
      BLE.println("- end workout     : Stop and show summary");
      BLE.println("- show angle      : Show pitch and flex sensor");
    } else if (command.equals("calibrate") || command.equals("calibrate ")) {                       //two version of string to account for space on the end
      showCalibration = true;                                                                       //sets corresponding boolean to true, and others to false
      counting = false;
      sensorcount = false;
      endcount = false;
    } else if (command.equals("start workout") || command.equals("start workout ")) {               //repeat for the following 
      counting = true;
      showCalibration = false;
      sensorcount = false;
      endcount = false;
      repCount = 0;
      setCount = 0;
      prevRep = 0;

      BLE.println("Workout Started");
      BLE.println("reps: 0, sets: 0");
    } else if (command.equals("end workout") || command.equals("end workout ")) {
      endcount = true;
      counting = false;
      showCalibration = false;
      sensorcount = false;
    } else if (command.equals("show angle") || command.equals("show angle ")) {
      sensorcount = true;
      counting = false;
      showCalibration = false;
      endcount = false;
    }
  }


 
  if (showCalibration && !calibrated) {                                             //if showCalibration boolean is set to true, do this loop
    if (pitch >= -2 && pitch <= 2) {                                                //range of the calibration zone
      if (inRangeStart == 0) {                                                      //check if timer is at 0
        inRangeStart = currentTime;                                                 //start timer
      } else if (currentTime - inRangeStart >= 2500) {                              //calibration finished after 2.5 seconds in range
        calibrated = true;
        lastActivityTime = currentTime;
        BLE.println("Calibration complete.");                                       //print this in BLE serial
      }
    } else {
      inRangeStart = 0;
    }
    BLE.print(pitch);                                                               //print pitch value and calibration...
    BLE.print(", ");
    BLE.println("Calibrating...");
  }

  if (calibrated && (currentTime - lastActivityTime > 120000)) {                   //inactivity timeout
    calibrated = false;                                                            //set bool and values back to false and 0
    repCount = 0;
    setCount = 0;
    waitingForDip = false;
    BLE.println("Inactivity timeout. Recalibrating...");
  }

  if (sensorcount) {                                                              //if sensorcount boolean is true, print these in BLE serial
    
    BLE.print("Pitch: ");
    BLE.print(pitch, 2);
    BLE.print(", Flex: ");
    BLE.println(flexValue);
    
    
    
  }

if (calibrated && counting) {                                                    //if the accelerometer is calibrated and counting bool is true, start the rep and set loops
  if (!waitingForDip && pitch <= -40) {
    repStart = currentTime;
    waitingForDip = true;
  }

  if (waitingForDip) {
    if (pitch >= 50 && (currentTime - repStart <= 1750)) {
      repCount++;
      waitingForDip = false;
      lastActivityTime = currentTime;

      if (repCount == 10) {
        repCount = 0;
        setCount++;
      }
    }

    if (currentTime - repStart > 1750) {
      waitingForDip = false;
    }
  }

  if (repCount != prevRep) {                                                     //when the repCount is not equal to previous rep, update the count, and print these in BLE serial
    BLE.print("reps: ");
    BLE.print(repCount);
    BLE.print(", sets: ");
    BLE.println(setCount);
    prevRep = repCount;
  }
}

if (endcount) {                                         //if endcount is set to true
  counting = false;                                     //counting is set to false

  BLE.println("Workout Summary:");                      //print out the workout summary in BLE serial
  BLE.print("Total reps: ");
  BLE.println(repCount + (setCount * 10));              //total reps is the current repCount + (setCount times 10)
  BLE.print("Total sets: ");
  BLE.println(setCount);

  endcount = false;                                     //set endcount to false so it only prints one time
  setCount = 0;                                         //reset counts
  repCount = 0;
}






  if (flexValue > FLEX_THRESHOLD && !sequenceRunning) {
    sequenceRunning = true;
    currentPixel = 0;
    lastStepTime = millis();
    strip.clear();
  }

  if (sequenceRunning) {
    if (flexValue < FLEX_THRESHOLD) {
      resetStrip();
    }

    if (millis() - lastStepTime >= 500 && currentPixel < NUMPIXELS) {
      strip.setPixelColor(currentPixel, strip.Color(0, 0, 255));  // Blue
      strip.show();
      currentPixel++;
      lastStepTime = millis();
    }

    if (currentPixel == NUMPIXELS) {
      strip.fill(strip.Color(0, 255, 0));  // Green
      strip.show();
      delay(1000);
      resetStrip();
    }
  }


  if (flexValue > 2550) {
    digitalWrite(ledPin, HIGH);
    digitalWrite(buzzer, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
    digitalWrite(buzzer, LOW);
  }

  delay(50);
}

void resetStrip() {
  strip.clear();
  strip.show();
  sequenceRunning = false;
  currentPixel = 0;
}
```
# Milestone 4 Modification Code
```c++
#include <Wire.h>                   //I2C library
#include <Adafruit_LSM6DS3TRC.h>    //accelerometer and gyroscope library
#include <Adafruit_LIS3MDL.h>       //magnometer library
#include <MadgwickAHRS.h>           //filter that converts accel and gyro into roll, pitch, and yaw
#include <Adafruit_NeoPixel.h>      //neopixel led strip library
#include <BleSerial.h>              //BLE serial library

//Classes and Objects
Adafruit_LSM6DS3TRC lsm6ds3trc;                           
Adafruit_LIS3MDL lis3mdl = Adafruit_LIS3MDL();
Madgwick filter;
BleSerial BLE;

//Neopixel Setup
#define PIXEL_PIN      13
#define NUMPIXELS      6
#define FLEX_THRESHOLD 2300

Adafruit_NeoPixel strip(NUMPIXELS, PIXEL_PIN, NEO_GRB + NEO_KHZ800);

//Variables
const float sampleFreq = 20.0;

//ESP32 pins
const int flexPin = A6;
const int ledPin = 23;
const int buzzer = 19;
const int vibrationMotor = 12;

//calibration variables
unsigned long inRangeStart = 0;
unsigned long repStart = 0;
unsigned long lastActivityTime = 0;

//booleans for user interface
bool calibrated = false;
bool waitingForDip = false;
bool counting = false;
bool sensorcount = false;
bool showCalibration = false;
bool endcount = false;
bool flexWork = false;

//neopixel variables
bool sequenceRunning = false;
unsigned long lastStepTime = 0;
int currentPixel = 0;

//repcount and setcount
int repCount = 0;
int setCount = 0;

int prevRep;                                        //new variable to count only when reps or sets are updated

void setup() {
  Serial.begin(115200);                             //begin serial monitor at 115200 baud rate
  delay(2000);                                      //2 second delay to ensure proper loading
  
  //These two are set as outputs
  pinMode(buzzer, OUTPUT);
  pinMode(vibrationMotor, OUTPUT);
  
  BLE.begin("Gauntlet of Wires");                                     //my serial name

  if (!lsm6ds3trc.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C!");
    while (1) delay(10);
  }

  if (!lis3mdl.begin_I2C()) {
    Serial.println("Failed to find LIS3MDL!");
    while (1) delay(10);
  }

  filter.begin(sampleFreq);

  strip.begin();
  strip.show();

  BLE.println("Type 'menu' to see commands.");

}

void loop() {
  int flexValue = analogRead(flexPin);
  sensors_event_t accel, gyro, temp;
  sensors_event_t mag;
  lsm6ds3trc.getEvent(&accel, &gyro, &temp);
  lis3mdl.getEvent(&mag);

  //conversion measures
  float gx = gyro.gyro.x * 180.0 / PI;
  float gy = gyro.gyro.y * 180.0 / PI;
  float gz = gyro.gyro.z * 180.0 / PI;
  float ax = accel.acceleration.x / 9.80665;
  float ay = accel.acceleration.y / 9.80665;
  float az = accel.acceleration.z / 9.80665;

  filter.update(gx, gy, gz, ax, ay, az, mag.magnetic.x, mag.magnetic.y, mag.magnetic.z);

  float roll = filter.getRoll();                              
  float pitch = -1 * filter.getPitch();                                //multiply by -1 to inverse the values

  unsigned long currentTime = millis();                                

  if (BLE.available()) {                                               //if there is a string available to read
    String command = BLE.readStringUntil('\n');                        //read until new line

    if (command.equals("menu") || command.equals("menu ")) {           //if this is the string, set other booleans to false
      counting = false;   
      showCalibration = false;
      sensorcount = false;
      endcount = false;

      BLE.println("==== MENU ====");                                                                //menu display
      BLE.println("List of available commands:");                                                   //below is the list of available commands
      BLE.println("- calibrate       : Start calibration");                                         //print in BLE serial
      BLE.println("- start workout   : Start tracking reps & sets");
      BLE.println("- end workout     : Stop and show summary");
      BLE.println("- show angle      : Show pitch and flex sensor");
      BLE.println("- flex workout    : Start flex holds workout");
    } else if (command.equals("calibrate") || command.equals("calibrate ")) {                       //two version of string to account for space on the end
      showCalibration = true;                                                                       //sets corresponding boolean to true, and others to false
      counting = false;
      sensorcount = false;
      endcount = false;
      flexWork = false;
    } else if (command.equals("start workout") || command.equals("start workout ")) {               //repeat for the following 
      counting = true;
      showCalibration = false;
      sensorcount = false;
      endcount = false;
      flexWork = false;
      repCount = 0;
      setCount = 0;
      prevRep = 0;

      BLE.println("Workout Started");
      BLE.println("reps: 0, sets: 0");
    } else if (command.equals("end workout") || command.equals("end workout ")) {
      endcount = true;
      counting = false;
      showCalibration = false;
      sensorcount = false;
      flexWork = false;
    } else if (command.equals("show values") || command.equals("show values ")) {
      sensorcount = true;
      counting = false;
      showCalibration = false;
      endcount = false;
      flexWork = false;
    } else if (command.equals("flex workout") || command.equals("flex workout ")) {
      flexWork = true;
      sensorcount = false;
      counting = false;
      showCalibration = false;
      endcount = false;

      BLE.println("Started Flex Workout");
      BLE.println("Bend Wrist and Hold");
    }

  }


 
  if (showCalibration && !calibrated) {                                             //if showCalibration boolean is set to true, do this loop
    if (pitch >= -2 && pitch <= 2) {                                                //range of the calibration zone
      if (inRangeStart == 0) {                                                      //check if timer is at 0
        inRangeStart = currentTime;                                                 //start timer
      } else if (currentTime - inRangeStart >= 2500) {                              //calibration finished after 2.5 seconds in range
        calibrated = true;
        lastActivityTime = currentTime;
        BLE.println("Calibration complete.");                                       //print this in BLE serial
      }
    } else {
      inRangeStart = 0;
    }
    BLE.print(pitch);                                                               //print pitch value and calibration...
    BLE.print(", ");
    BLE.println("Calibrating...");
  }

  if (calibrated && (currentTime - lastActivityTime > 60000)) {                   //inactivity timeout
    calibrated = false;                                                            //set bool and values back to false and 0
    repCount = 0;
    setCount = 0;
    waitingForDip = false;
    BLE.println("Inactivity timeout. Recalibrating...");
  }

  if (sensorcount) {                                                              //if sensorcount boolean is true, print these in BLE serial
    
    BLE.print("Pitch: ");
    BLE.print(pitch, 2);
    BLE.print(", Flex: ");
    BLE.println(flexValue);
    
    
    
  }

if (calibrated && counting) {                                                    //if the accelerometer is calibrated and counting bool is true, start the rep and set loops
  if (!waitingForDip && pitch <= -40) {
    repStart = currentTime;
    waitingForDip = true;
  }

  if (waitingForDip) {
    if (pitch >= 50 && (currentTime - repStart <= 1750)) {
      repCount++;
      waitingForDip = false;
      lastActivityTime = currentTime;

      if (repCount == 10) {
        repCount = 0;
        setCount++;
      }
    }

    if (currentTime - repStart > 1750) {
      waitingForDip = false;
    }
  }

  if (repCount != prevRep) {                           //when the repCount is not equal to previous rep, update the count, and print these in BLE serial
    BLE.print("reps: ");
    BLE.print(repCount);
    BLE.print(", sets: ");
    BLE.println(setCount);
    prevRep = repCount;
  }
}

if (endcount) {                                         //if endcount is set to true
  counting = false;                                     //counting is set to false

  BLE.println("Workout Summary:");                      //print out the workout summary in BLE serial
  BLE.print("Total reps: ");
  BLE.println(repCount + (setCount * 10));              //total reps is the current repCount + (setCount times 10)
  BLE.print("Total sets: ");
  BLE.println(setCount);

  endcount = false;                                     //set endcount to false so it only prints one time
  setCount = 0;                                         //reset counts
  repCount = 0;
}

if (flexWork) {
  if (flexValue > FLEX_THRESHOLD && !sequenceRunning) {                         //if the flex value exceeds the threshold and sequence isnt running
    sequenceRunning = true;                                                     //start the sequence
    currentPixel = 0; 
    lastStepTime = millis();                                                    //timer
    strip.clear();                                                              
  }

  if (sequenceRunning) {                                                        //if the sequence is running
    if (flexValue < FLEX_THRESHOLD) {                                           //if flex sensor value suddenly goes back down reset all lights 
      resetStrip();
    }

    if (millis() - lastStepTime >= 500 && currentPixel < NUMPIXELS) {           //if it has been 0.5 seconds since the last light 
      strip.setPixelColor(currentPixel, strip.Color(0, 0, 255));  // Blue       //set color to blue
      strip.show();
      currentPixel++;                                                           //move onto next light
      lastStepTime = millis();                                                  //reset 0.5 second timer
    } 

    if (currentPixel == NUMPIXELS) {
      strip.fill(strip.Color(0, 255, 0));  // Green                             //if all colors are filled, set all led colors to green 
      strip.show();
      BLE.println("Release");
      BLE.println("good job");
      delay(1000);                                                              //hold for 1 second before resetting
      resetStrip();
    }
  }
  if (flexValue > 2600) {                                           //if flex value exceeds threshold, turn on buzzer
    digitalWrite(buzzer, HIGH);
    BLE.println("too far! Please dont bend too far")
  } else {
    digitalWrite(buzzer, LOW);
  }
}

if (!counting && !showCalibration && !sensorcount && !endcount && !flexWork) {      //if no processes are currently running
  if (pitch <= -35 || pitch >= 48) {                                                //threshold for vibration motor
    digitalWrite(vibrationMotor, HIGH);
  } else {
    digitalWrite(vibrationMotor, LOW);
  }
} else {
  digitalWrite(vibrationMotor, LOW);  


  delay(50);
}

}


void resetStrip() {                         //created reset function
  strip.clear();                            //clear led strip
  strip.show();                             //get ready for next loop
  sequenceRunning = false;
  currentPixel = 0;
}
```
