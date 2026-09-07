# MIDI_throughput tester

 ## A simple tool to test throughput of multiple MIDI interfaces at once, under the stress of intense traffic.
While working on DURA_MIDI, I need a tool to gauge my newly created hardware performance against original - MTP_AV_USB. With lack of comparable existing tools, this one was hastily coded in VisualStudioCode with CoPilot. The result maybe not authoritative, but appeared to produce believable results. Comparing to other tools with subset of functions - it is matching pretty well.

Releasing with hope that it can be useful to others.

It sends only note ON/OFF messages, back to back, on single channel. (No chance for "Running Status" to kick in.) So the message length is fixed. Started at generous 40mSec intervals it will gradually pack them tighter, till only 1mSec apart. This is close to a physical limit of MIDI. In real life scenarios, Running State may allow to transmit more messages, but this was not intent of this tester.
It is pure HTML and it runs in browser, if WebMIDI is supported. Tested in Edge only but should work in Chrome and others.


## How to use
Run in browser. If using Edge - running local file is fine. If hosted on server - must be HTTPS, as HTTP does not allow MIDI control. Firefox does not allow local files.
First after opening it will prompt to allow MIDI. There is only one way to go forward.
You need to make selection of interfaces by selecting first and last one to test, it will test all in between. This setting will be saves and should survive page reloads.+
It expects to have each port's input looped back to the output. Will not work if all cables to be tested are not looped back.
Vertical axis is round-trip latency in mSec.

Warning: My MTP send SysEx on boot. Being looped - it gets echoed in infinite loop. I guess it is possible to set message filters with ClockWorks, but then it is too much work. I just boot it without loop-back cables plugged, and plug them in the back only after MTP is already awake. But most MIDI interfaces do not care.

Note that browser activity may affect the results. I have also noticed that initial run after opening may have a few corrupted messages at the beginning. This appeared to be the way Edge functions, just ignore those on the first run.

<img width="800" height="480" alt="Screenshot 2026-09-07 180720" src="https://github.com/user-attachments/assets/a445a977-24eb-45c0-a3ca-72cabf090274" />
<img width="800" height="480" alt="Screenshot 2026-09-07 180433" src="https://github.com/user-attachments/assets/cd629027-0bfa-43cd-89ba-70fb96181cc8" />

