<h2>Fluidsynth</h2>
<ul>
<li>Install and run Fluidsynth to see warning messages
<pre>
sudo apt-get install fluidsynth
fluidsynth -a alsa -g 5 /usr/share/sounds/sf2/FluidR3_GM.sf2
</pre>
Warnings concern latency:
<sl>
<li>warning: Requested a period size of 64, got 940 instead</li>
<li>warning: Failed to set thread to high priority</li>
</sl>
</li>
<li>Create a system wide configuration file to allow starting Fluidsynth without preamble messages (<code>sudo nano /etc/conf.d/fluidsynth</code>) with content:
<pre>
SOUND_FONT=/usr/share/soundfonts/FluidR3_GM.sf2
OTHER_OPTS='-a alsa -g 5 -m alsaseq -p FluidSynth\ GM -r 48000'
sudo nano /etc/conf.d/fluidsynth
</pre>
</li>
<li>Run Fluidsynth as a service
<pre>
sudo reboot
systemctl --user start fluidsynth
</pre>
</li>
</ul>
