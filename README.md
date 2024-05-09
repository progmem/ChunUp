# ChunUp!

![assembled pcb](https://raw.githubusercontent.com/progmem/ChunUp/main/chunup.jpg)

y'know, like the phrase 'tune up'

look

i thought it was a cute name alright

## What is ChunUp?

ChunUp is a variation of [48productions's Perpetual Free Credits PCB](https://github.com/48productions/Perpetual-Free-Credits-PCB). Like PFC, it keeps compatible games fully credited up at all times. Unlike PFC, ChunUp acts to be compatible with one, and only one game:

- Chunithm
- that's it, just Chunithm

ChunUp acts as a replacement to the coin mechanism in the Chunithm cab, allowing for nondestructive, reversible modification. The PCB is designed to be mounted onto a YLP-06V connector by crimping the connector's pins to bare (plastic removed) 0.1" "Dupont" pin headers.

## Disclaimer

As mentioned in 48productions's project:

> This project came about because of a few relevant conversations in the awesome western arcade rhythm game community, and the general concept/design was discussed by several community members.
> You are installing this board at your own risk, and I cannot be held liable for damages, destruction, magic smoke escaping, or otherwise.
> For arcade games on an official online network, your network may not allow the use of this board or similar mods. As such, usage of this board in these circumstances isn't recommended.
> *Any games mentioned are properties of their respective owners. This design was produced independently of them, and is in no way endorsed or officially supported.*

This project requires you have the parts and enough comfort to solder small surface-mount components (0603). Additionally, a crimper is necessary for joining the 0.1" Dupont pin to the JST YL pins. If you do not feel comfortable with soldering small parts or do not have the equipment or drive to crimp, it's advised to use 48productions's original project instead.

## How do I assemble this?

With the four plated holes oriented "up", solder the following 0603 components to these locations:

- 1k resistor, soldered to the top-left
- 56k resistor, soldered to the top-right
- 10uF ceramic capacitor (16V or higher), soldered to the bottom-left
- 5.6k resistor, soldered to the bottom-right

Next, solder the following components to their respective pads, with the dot on each part towards the top-left:

- Texas Instruments NE555PWR (or equivalent TSSOP-8 555 timer)
- onsemi FODM217C (or equivalent SOP-4 optocoupler)

Next, obtain the following parts for the connector:

- JST YLP-06V (the connector used for the coin mech)
- SYF-01T-P0.5A or SYF-41T-P0.5A pins (the socket pins used for this connector)
- At least four 0.1" Dupont header pins
  - It's advised to get the "longer" variant of these pins, intended for use in e.g. breadboards.

Separate the 0.1" Dupont header pins from their plastic retainer using e.g. a set of pliers. Crimp each bare-metal pin to one of the the socket pins. Once you have four pins prepared, orient the large retention tab on the JST YLP-06V "up" and install the crimped pins to the top-left, top-center, top-right, and bottom-left positions respectively (positions 1-4). The header pins should be sticking out of the connector.

Once installed, fit the ChunUp PCB onto the exposed header pins with the surface-mount pins facing away from the connector body (the ChunUp PCB should physically install only one way). Clip the header pins to length before soldering.

## How do I use it?

- Unplug the coin mech's 6-pin connector
- Plug in ChunUp

## How does this work?

This board leverages power from the coin blocker relay on the Chunithm cab. When the game is in a state to accept coins, power is normally supplied to a mechanism that allows the cabinet to accept coins. Once the maximum credit limit in Chunithm is reached (24), power disengages, which causes the mechanism to reject future credits.

ChunUp uses the power normally going to the coin blocker relay to drive a 555 timer. The 555 timer is configured to supply coin pulses that repeatedly trigger the game's coin switch. This is done with an optoisolator in order to keep the coin switch line separated from the rest of the power supply. When the optoisolator is "activated", it connects the coin switch line to ground, similar to how the microswitch on a coin mechanism functions.

Once the game is at the maximum credit limit, Chunithm disengages power to the coin blocker relay (cutting power from the 555 and the optoisolator), which stops the insertion of coins. Once a coin is "spent", ChunUp will re-engage after a short delay.
