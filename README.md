# Midi
I store my configurations during a journey to explore Midi in this repository.

<h1>Piano synthesizer for midi keyboard</h1>
<h2>Raspberry PI microSD and OS</h2>
First I run a simple PoC to check if the latency of response to pressing keys on the midi keyboard can be managed via realtime scheduling. If this appears too slow I will need to install a linux low-latency kernel, and perform associated remediations. But since I plan to use digital audio out, I am hopeful that a simplified install be sufficient.
<ul>
<li>Image de microSD card, using Raspberry PI Imager and the Raspberry PI OS Lite image, bootable and SSH enabled.</li>
<li>Add <code>rpi/wpa_supplicant.config</code> to the boot partition.</li>
<li>Boot the RPI with the new image. Use the Fink app to SSH into the RPI. Login with UID pi, pswd raspberry.</li>
<li>Update the RPI
<pre>
sudo apt-get update
sudo apt-get upgrade
</pre>
</li>
</ul>
<h2>Audio</h2>
Give the audio-group the rights to set real-time priorities
<ul>
<li><code>sudo user mod -a -G audio pi</code> </li>
<li>Check that there are 2 lines in <code>/etc/security/limits.d/audio.conf</code>:
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
<li>Run <code>speaker-test -c2 -twav</code>. Use <code>ctrl-z</code> to stop.</li>
</ul>
Maybe a reboot is needed if not working immediately.
<h2>Fluidsynth</h2>
<ul>
<li>Install Fluidsynth
<pre>
sudo apt-get install fluidsynth
</pre>
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

