# MIDI
I keep track of my MIDI explorations in this repository.

<h1>RPI as sound module</h1>
First I want to add (hopefully) a Raspberry PI as synthesizer between my midi keyboard and usb speakers, to make it sound like a piano, without extra digital step such as a DAW or analog step such as a soundcard or audio interface in between.

<h2>Step 1: Fluidsynth PoC</h1>
To check the latency of response to pressing keys on the midi keyboard, without optimization. 
<ol>
<li>Set up a Raspberry PI OS on microSD (see RPI.md)</li>
<li>(Optional) Changing Raspbian audio defaults to use USB-speakers instead of a headset (see Audio.md)</li>
<li>Run a Fluidsynth service (see Fluidsynth.md)</li>
<li>Configure the MIDI device (see MIDI.md)</li>
</ol>
<br>This results with a RPI 3 B+ and Lite OS in a subsecond latency (I estimate it around 0.4 s), which makes it a useless configuration.

<h2>Step 2: Latency remediations</h1>
I need to define a practical auditive latency target. The sound speed in air gives a 3 ms delay for a meter distance (which would be what feels natural if you play a piano or electric guitar). Furthermore a brain decides a 20 to 30 ms delay as separate. Let's then make a 10 ms delay the target.

The following wiki suggests < 10 ms is achievable on Raspbian: https://wiki.linuxaudio.org/wiki/raspberrypi, so I maintain the RPI choice.

<!--
<li>Create fluidsynth.sh as included in [this repository](https://github.com/GeordieTomo/Fluidsynth/blob/master/fluidsynth.sh), and run <code>sudo chmod +x fluidsynth.sh</code> to make it executable</li>
<li>Create a <code>keyboard</code> file in the <code>inst/</code> directory holding the soundfonts of my liking.</li>
<li>Run <code>./fluidsynth.sh</code> to test that midi keyboard presses result in events shown in the cli and heared on the usb speakers.</li>
</ul>
<h2>Autorun</h2>
<ul>
<li>Update <code>~/.bashrc</code>, scroll to the bottom and add<pre>
./setup.sh wurli
</pre>Make that file executable as well, and reboot</li>
</ul>
<h2>Autologin</h2>
<ul>
<li>Run <code>sudo raspi-config</code> and select the "Console Autologin" boot option, under "Desktop/CLI".</li>
<li>Reboot. The RPI should run headless now, without the need to SSH into it again.</li>
</ul>
<h2>References</h2>
<ul>
<li>Raspberry instructions for configuring: https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md  </li>
<li>Well explained https://jereme.me/post/raspberry-pi-midi-sound-module/</li>
</ul>
-->
