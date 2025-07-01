  # Wrist Rehab Monitor
Wrist Rehab Monitor because my wrist got injured from badminton.
You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Nathan S | Gunn High | Unknown | Incoming Sophomore

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](Adobe Express - file.jpg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/UryxP8tovaY?si=vhKdE8WHcJufKPs5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My first milestone was to connect the flex sensor to the esp32 (main controlling unit), and also add threshold values so when bending the flex sensor, the LED and piezo buzzer that I connected would beep and turn on. The flex sensor is a big resistor, and bending it to a certain degree changes the resistance values. Conductive ink sits on the top of the flex sensor, and when it is bent, the ink outside of the bend is stretched, leading to increased resistance. This is what changed the actual number values that were output by the sensor. I printed these flex sensor values to find my threshold for the LED and buzzer. When the flex sensor is straight, it outputs a value of 1800, and when bending to a degree the number increases or decreases. Since I planned to use the flex sensor for detecting bend in only one direction, I only need one threshold. I set my LED and buzzer threshold at 2400. 

![image](https://github.com/user-attachments/assets/8f77114c-049b-442f-a3d8-8aeb1de83724)

Some challenges that I faced were connecting things to the esp32 and the breadboard. The breadboard layout was confusing at first, as I didn't really understand how the electricity path flowed throughout the board. Another challenge was connecting the flex sensor. The flex sensor works off a voltage divider, which is a small circuit that that reduces voltage to a lower level, dividing input voltage into smaller outputs. I had to search some online schematics that showed me how to connect the flex sensor to the esp32. I also tried connecting the LSM6DS3+LIS3MDL (accel,gyro and magnometer), but I realized that I would also have to connect the codes and find more thresholds, so I saved that for the next milestone. 

My next plan is to connect the accelerometer to my esp32, and also get the threshold values for that sensor. As of now, I downloaded a code from the library that lets my LSM6DS3+LIS3MDL sensor give me acceleration and angular velocity data for the x,y and z axis. I plan on using some of the these values as threshold for the next step. The flex sensor will sit on the top of my wrist, regulating the up and down motions, while the LSM6DS3+LIS3MDL will regulate side to side motions on my wrist.
# Schematics 
![image](https://github.com/user-attachments/assets/50e9d166-e03b-494d-adb5-1d321a094b3b)

# Code

```c++
#include <MadgwickAHRS.h>

const int flexPin = A6; 
const int ledPin = 23; 
const int buzzer = 19;

void setup() { 
  Serial.begin(115200);
  pinMode(ledPin,OUTPUT);
  pinMode(buzzer,OUTPUT);
} 

void loop(){ 
  int flexValue;
  flexValue = analogRead(flexPin);
  Serial.print("sensor: ");
  Serial.println(flexValue);
 
  if(flexValue>2400) {
     digitalWrite(ledPin,HIGH);
     digitalWrite(buzzer,HIGH);
  }
  else {
    digitalWrite(ledPin,LOW);
    digitalWrite(buzzer,LOW);
  }
  delay(20);
  
} 
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

# Starter Project - Retro Arcade Console

<iframe width="560" height="315" src="https://www.youtube.com/embed/lbEyTJAkzWc?si=9pJWD1YZEUp0lTTe" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Description 
  My starter project was the Retro Arcade Console, and I chose it because there were only two options and the console seemed somewhat more fun. It was my first time soldering, and the project really helped as there were many joints to solder. I learned many soldering skills such as a through hole joint, soldeirng wires, stripping wires, and de-soldering. The console has a couple games such as tetris and a bad version of galaga. The 4 buttons consisting of up, down, left, and right on the left are the actual controls, while the up and down button are used for things such as selecting or firing. The two big LED matrices act as the screens, and there is also an LED scoreboard at the top. The console is also powered by usb or three AA batteries.

# Challenges 
  One challenge was that when I tried to power my console with batteries, It wouldn't turn on at all. I checked my wires and I realized that during my soldering process, I had accidentally burned a part of the ground wire, which wouldn't allow it to turn on. So I had to cut the wire to take out the burnt part, and then strip the wire. After soldering the wire back together and using a heat shrink, the console worked perfectly fine through battery power. 
  
# Next Steps
  I will use the skills that I learnt from my starter project and apply it to my intensive project, the Wrist Rehab Device. Since I dont know how to use an Arduino or how to code, I'm going to start on learning the basics first. Then I will start to work on my intensive project.  

