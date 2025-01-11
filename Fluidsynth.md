<h2>Fluidsynth</h2>
Fluidsynth is an open source synthesizer. It is designed to load a soundfont. 
A soundfont is a package of soundfiles, with for each midi key audio files belonging to the press of a key (attack and decay), 
holding a key (sustain) and releasing it (release). 
A soundfont may be associated with a certain instrument, e.g. a Steinway grand piano. The legality of soundfonts depends on how the audio samples were obtained. 
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
<li>Create a system wide configuration file to allow starting Fluidsynth without preamble messages (
<code>
sudo nano /etc/conf.d/fluidsynth
</code>) with content
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
