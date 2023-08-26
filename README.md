# ESP32-NetworkMonitor-Telegram

# This ESP32-Based Wi-Fi Logger Is a Simple Network Monitoring Solution

# Element14 Presents host Mark Donners' Wi-Fi network monitor provides real-time alerts via Telegram with just an ESP32.

## Why build a network monitor?
Unlike the publicly accessible Wi-Fi network available in airports, cafes, and sporting events, your home Wi-Fi network is supposed to be safe. 
However, as element14 Presents host Mark Donners points out, providing the credentials to visitors can create a risk, 
especially if that password is further shared. In order to help himself more quickly identify unknown devices,
Donners set out to create an inexpensive network monitoring tool that could alert him whenever something connects.

## A short bill of materials
Compared to other Wi-Fi network monitors, or "pineapples" as they're called in the infosec profession, 
this DIY version would be quite barebones in both software and hardware capabilities.
In this iteration, Donners' design is comprised of a single ESP32 due to its onboard Wi-Fi chip/antenna, and a USB power supply.

## Configuring the device
Before any scanning can commence, the device first has to know where to connect, 
and that's done by initially pressing a button connected to a digital IO pin which causes the ESP32 to create an access point.
Once connected, the configuration webpage presents a form for entering the target access point's SSID, password, and timezone. 
Furthermore, the user can add their Telegram API token and chat ID to gain access to real-time alerts.

## UDP packets
The user datagram protocol, or UDP, is an extremely simple communication protocol where messages can be sent without the need for prior setup or extra error correction. 
Because of this, and in combination with IPv4, one can easily extract the sender's IP address and the ports being accessed.
But this only provides limited information and can be sent thousands of times a day from a single device, therefore,
Donners chose to only select DHCP packets since they are sent when a device joins the network or needs to renew its IP address.
They contain the client's MAC address, IP address, and optionally the hostname, amongst many other options.

## Telegram integration
With the Wi-Fi monitor now able to collect and parse DHCP packets into useful information, 
Donners wanted it to send alerts via Telegram whenever a device joins the network. This was accomplished by setting up a Telegram bot, 
getting the API token, and then setting up a client in the ESP32 firmware. Not only can the bot send information about new device through the chat, 
but users are also able to send it commands such as mute, unmute, and help to easily control it without the need for reprogramming or local network access.


### https://www.youtube.com/watch?v=CSV9qrF8wSk&t=130s&ab_channel=element14presents

