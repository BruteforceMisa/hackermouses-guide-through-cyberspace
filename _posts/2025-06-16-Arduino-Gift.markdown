---
layout: posts
title:  "Sinterklaas surprise: Arduino Memory game"
date:   2025-06-16 15:00:00 +0200
tags: hardware 
categories: Projects
---

This post is coming around half a year late, but I still want to tell you about a small Arduino project. It is a yearly tradition around Sinterklaas to buy a small gift and wrap it with what we call a "surprise" - which is basically very fancy wrapping paper. All participants put their names on a paper in a big box and draw a new paper. The person you draw (hopefully not yourself) is the person you have to get a gift and a surprise for. Usually, this surprise wrapping is tailored to this particular person.

For Sinterklaas 2024, I had to get presents for my dad. He also likes electronics very much, so I thought it would be cool to create an electronic surprise. I designed a memory game using Arduino, where you have to remember sequences.

![image]({{ site.url }}{{ site.baseurl }}/assets/images/poc.jpeg)
<i>Proof of concept of the memory game</i>

For this game, I used a blue and a white led light to indicate the sequence, followed by a red or green light to give feedback to the user if their submitted sequence is correct. The yellow light is used at the end to signal morse code. Two buttons are used to get the user input. I've drawn a simple schematic on the connections between the different components. Note that resistors are needed for the LED bulbs.

![image]({{ site.url }}{{ site.baseurl }}/assets/images/circuit.png)

The sequence is a randomly generated bitstream of x bits, and the game starts by just remembering the first bit. Once the user submitted a correct sequence, the next bit is added, and so on. When an error is made, the user has to start over again from the first bit. Once the user has correctly remembered the whole bitstream, a rainbow of ledlights is shown and afterwards the yellow light starts signaling morse code, which matches with the lock on the package. The source code used for this surprise is added here:


<details>
<summary><b>Click to show/hide code</b></summary>
{% highlight python %}

const int blue_ledpin = 7;
const int white_ledpin = 4;
const int yellow_ledpin = 9;
const int green_ledpin = 5;
const int red_ledpin = 3;

const int blue_buttonpin = 2;
const int white_buttonpin = 8;

  // random seed for sequence
const int seed = 124;
const int sequence_length = 10;
int sequence[sequence_length];

const int morse1[5] = {0,0,0,0,1};
const int morse2[5] = {1,1,0,0,0};
const int morse3[5] = {0,0,0,0,0}; 

void setup() {
  // put your setup code here, to run once:
  // Initialise leds
  Serial.begin(9600);

  pinMode(blue_ledpin,OUTPUT);
  pinMode(blue_buttonpin,INPUT_PULLUP);

  pinMode(white_ledpin,OUTPUT);
  pinMode(white_buttonpin,INPUT_PULLUP);

  pinMode(red_ledpin,OUTPUT);
  pinMode(green_ledpin,OUTPUT);
  pinMode(yellow_ledpin,OUTPUT);


  // Create sequence

  randomSeed(seed);

  for(int i = 0; i < sequence_length; i++)
  {
    int value = random(0, 2);
    sequence[i] = value;
  }


}

void play_game(){
  bool finished = false;
  int count = 1;

    
    while(count <= sequence_length)
    {

      bool seq_succesful = play_sequence(count);

      if(seq_succesful)
      {
        delay(250);
        digitalWrite(green_ledpin, HIGH);
        delay(1000);
        digitalWrite(green_ledpin, LOW);
        count++;
        delay(1000);
      }
      else
      {
        delay(250);
        digitalWrite(red_ledpin, HIGH);
        delay(1000);
        digitalWrite(red_ledpin, LOW);
        count = 1;
        delay(1000);
      }

      // Serial.print(count);
      // if(count == sequence_length+1)
      // {
      //   Serial.print("Finished");
      //   finished=true;
      // }
      
    }
    

  get_flag();
}

bool play_sequence(int length)
{
  // Shine leds
  for(int j = 0; j < length; j++)
  {
    if(sequence[j] == 0)
    {
      digitalWrite(blue_ledpin, HIGH);
      delay(500);
      digitalWrite(blue_ledpin, LOW);
      delay(500);
    }
    if(sequence[j] == 1)
    {
      digitalWrite(white_ledpin, HIGH);
      delay(500);
      digitalWrite(white_ledpin, LOW);
      delay(500);
    }
  }

  // Check userinput
  int button_presses = 0;

  int user_sequence[length];

  while(button_presses < length)
  {
    if (digitalRead(blue_buttonpin) == LOW)  
      {
        user_sequence[button_presses] = 0; 
        button_presses++;                
        delay(250);                       
      }
    if (digitalRead(white_buttonpin) == LOW)  
      {
        user_sequence[button_presses] = 1;         
        button_presses++;        
        delay(250);                       
      }
  }


  bool succesful = true;

  for(int i = 0; i < length; i++)
  {
    if(user_sequence[i] != sequence[i])
    {
        succesful = false;
    }
  }

  return succesful;
}


void get_flag()
{
  happy_leds();
  while(true)
  {
    start_sequence_flag();
    delay(3000);
    flash_led(morse1);
    delay(3000);
    flash_led(morse2);
    delay(3000);
    flash_led(morse3);
    delay(3000);
  }

}

void happy_leds()
{

  int blink_count = 10;
  for(int i = 0 ;i <blink_count; i++)
  {
    digitalWrite(green_ledpin, HIGH);
    delay(100);
    digitalWrite(green_ledpin, LOW);
    delay(100);
  }

  int wave_count = 5;
  for(int i = 0; i < wave_count; i++){
    digitalWrite(blue_ledpin, HIGH);
    delay(100);
    digitalWrite(blue_ledpin, LOW);
    delay(100);
    digitalWrite(red_ledpin, HIGH);
    delay(100);
    digitalWrite(red_ledpin, LOW);
    delay(100);
    digitalWrite(green_ledpin, HIGH);
    delay(100);
    digitalWrite(green_ledpin, LOW);
    delay(100);
    digitalWrite(white_ledpin, HIGH);
    delay(100);
    digitalWrite(white_ledpin, LOW);
    delay(100);
  }

}

void flash_led(int morse[])
{
  for(int i = 0; i < 5; i++)
  {
    if(morse[i] == 0)
    {
      digitalWrite(yellow_ledpin, HIGH);
      delay(500);
      digitalWrite(yellow_ledpin, LOW);
      delay(500);
    }
    if(morse[i] == 1)
    {
      digitalWrite(yellow_ledpin, HIGH);
      delay(2000);
      digitalWrite(yellow_ledpin, LOW);
      delay(500);
    }
  }
}

void start_sequence_flag()
{
    digitalWrite(green_ledpin, HIGH);
    delay(1000);
    digitalWrite(green_ledpin, LOW);
}

void loop() {

  if (digitalRead(blue_buttonpin) == LOW) {
    delay(1000);
    play_game();
  }
}

{% endhighlight %}
</details>

<br/>

Finally, I had to attach the Arduino to the surprise itself and hide the gifts in there. I decided to stick the Arduino to the "ceiling" of the box, to make cable management a bit easier. 

![image]({{ site.url }}{{ site.baseurl }}/assets/images/insides.jpeg)


However, if the battery was connected, then the lid of the box could not open. Sticking the battery to the top part as well would become to heavy. So I had to make a seperate connection. 

![image]({{ site.url }}{{ site.baseurl }}/assets/images/powersupply.jpeg)

And tadaa, the final result from above! Now I only have to add the morse code and the lock.

![image]({{ site.url }}{{ site.baseurl }}/assets/images/setupattached.jpeg)


Dad was very surprised and entertained by his surprise, and even the whole family helped remembering the sequence to reach the code for the lock! 

![image]({{ site.url }}{{ site.baseurl }}/assets/images/surprise.jpeg)
<i>A picture of the final suprise</i>