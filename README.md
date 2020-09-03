# Get Up and Move

## Purpose

Timer and light setup for a move reminder.
For those times when you are so in the zone that a normal reminder won't get your attention. 

## Components

* Hue Lights
* Node Red https://nodered.org/
* MQTT - I use RabbitMQ: https://www.rabbitmq.com/
* ESP8266 board - I use these: https://www.amazon.com/gp/product/B076F52NQD
* Arcade button - I use these: https://www.amazon.com/gp/product/B01IXW9S5O
* Printed enclosure

## Theory of Operation

Pressing the button sends a message to MQTT. 
A short press puts a message in a "short" queue.
A long press (>500ms) sends a message to the "long" queue.

Node Red monitors the MQTT queues in an MQTT flow.
If Node Red sees a message in the "short" queue, the flow sets the room lights to a specific Philips Hue scene (Energize in my case).
It also starts a 45 minute timer.

At the end of 45 minutes, the Hue lights are set to a different scene (Spring Blossom), and the Node Red flow will play a text to speech line.
In my case, it is "Time to take a break." 

If Node Red sees a long press, it sets the room lights to Energize.
The timer does not start.

