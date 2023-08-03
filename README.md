# ChunUp!

y'know, like the phrase 'tune up'

look

i thought it was a cute name alright

## What is ChunUp?

ChunUp is a variation of [48productions's Perpetual Free Credits PCB](https://github.com/48productions/Perpetual-Free-Credits-PCB). Like PFC, it keeps compatible games fully credited up at all times. Unlike PFC, ChunUp acts to be compatible with one, and only one game:

- Chunithm
- that's it, just Chunithm

ChunUp acts as a replacement to the coin mechanism in the Chunithm cab, allowing for nondestructive modification. The PCB is designed to be mounted onto a YL-6P connector by crimping the connector's pins to pin headers, then soldering the board onto those headers. Installation then becomes a trivial matter:

- Unplug the 6-pin plug for the coin mechanism
- Plug in ChunUp

To allow for this, ChunUp leverages smaller forms of the parts used in PFC. This allows the PCB to be very, _very_ small, allowing it to be tucked away.

## How does this work?

This board leverages power from the coin blocker relay on the Chunithm cab. When the game is in a state to accept coins, power is normally supplied to a mechanism that allows the cabinet to accept coins. Once the maximum credit limit in Chunithm is reached (24, because puyo), power disengages, which causes the mechanism to reject future credits.

ChunUp uses that power to drive a 555 timer, configured to supply coin pulses that repeatedly trigger the game's coin switch. This is done with an optoisolator in order to keep the coin switch line separated from the rest of the power supply. When the optoisolator is "activated", it connects the coin switch line to ground, similar to how the microswitch on a coin mechanism functions.

Once the game is at the maximum credit limit, power is cut from the 555 and the optoisolator is left in a state that stops affecting the coin switch line. 

## Credits/Disclaimers

As stated, this wasn't my original idea! Go check out the original project using the link above. As mentioned in the original project:

> This project came about because of a few relevant conversations in the awesome western arcade rhythm game community, and the general concept/design was discussed by several community members.
> You are installing this board at your own risk, and I cannot be held liable for damages, destruction, magic smoke escaping, or otherwise.
> For arcade games on an official online network, your network may not allow the use of this board or similar mods. As such, usage of this board in these circumstances isn't recommended.
> *Any games mentioned are properties of their respective owners. This design was produced independently of them, and is in no way endorsed or officially supported.*
