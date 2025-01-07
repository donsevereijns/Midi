# Midi
I store my configurations during a journey to explore Midi in this repository.

<h1>RPI as sound module</h1>
This first step is to add a Raspberry PI as synthesizer between my midi keyboard and usb speakers, to make it sound like a piano, without extra digital step such as a DAW or analog step such as a soundcard or audio interface in between.
<h2>Raspberry PI microSD and OS</h2>
First I run a simple PoC to check if the latency of response to pressing keys on the midi keyboard can be managed via realtime scheduling. If this appears too slow I will need to install a linux low-latency kernel, and perform associated remediations. 
As I plan to use digital audio out, the USB interface will add latency, so this will be important.
<ul>
<li>Image de microSD card, using Raspberry PI Imager and the Raspberry PI OS Lite image, bootable and SSH enabled.</li>
<li>Add <code>rpi/wpa_supplicant.config</code> to the boot partition.</li>
<li>Boot the RPI with the new image. Use the Fink app to SSH into the RPI. Login with UID pi, pswd raspberry.</li>
<li>Update the RPI: <code>sudo apt-get update</code> and <code>sudo apt-get upgrade</code></li>
</ul>
<h2>Audio</h2>
<ul>
<li>Add the pi user to a supplemental audio group: <code>sudo usermod -a -G audio pi</code> </li>
<li>Give the audio group the rights to set real-time priorities: check that there are 2 lines in <code>/etc/security/limits.d/audio.conf</code>:
<pre>
@audio - rtprio 80
@audio - memlock unlimited
</pre>So when using the <code>top</code> cmd, audio processes should show 'rt' in the PR (prio) column.
</li>
<li>Connect usb speakers to the RPI and activate them.</li>
<li>Find the card no of the usb speakers via <code>aplay -l</code>. This belongs to the physical port chosen for the usb speakers (NB!).</li>
<li>Make sure that the lines in <code>/usr/share/alsa/alsa.conf</code> refer to that card no:
<pre>
defaults.ctl.card <x>
defaults.pcm.card <y>
</pre></li>
<li>Check that the usb speakers can be volume controlled in <code>alsamixer</code>.</li>
<li>Test sound. In my case by running a predefined wav, 2 channels: <code>speaker-test -c 2 -t wav</code>. Use <code>ctrl-z</code> to stop.</li>
</ul>
Maybe a reboot is needed if not working immediately.
<h2>Fluidsynth</h2>
Fluidsynth is an open source synthesizer. It is designed to load a soundfont. A soundfont is a package of soundfiles, with for each midi key audio files belonging to the press of a key (attack and decay), holding a key (sustain) and releasing it (release). A soundfont may be associated with a certain instrument, e.g. a Steinway grand piano. The legality of soundfonts depends on how the audio samples were obtained. 
<ul>
<li>Install Fluidsynth
<pre>
sudo apt-get install fluidsynth
</pre>
</li>
<li>Now when running fluidsynth as <code>fluidsynth -a alsa -g 5 /usr/share/sounds/sf2/FluidR3_GM.sf2</code> I get several warnings, the first of which is fluidsynth: warning: Requested a period size of 64, got 940 instead</li>
</li>
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
</ul>

