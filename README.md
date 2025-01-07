# Midi
I store my configurations during a journey to explore Midi in this repository.

<h1>Piano synthesizer for midi keyboard</h1>
<h2>Raspberry PI microSD and OS</h2>
First I run a simple PoC to check the latency of response to pressing keys on the midi keyboard. If this is too slow I will need to install a linux low-latency kernel, and associated remediations. But since I plan to use digital audio out, I am hopeful that a user-level install will be sufficient.
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
Prioritize audio
<ul>
<li><code>sudo user mod -a -G audio pi</code> </li>
<li>Check that there are 2 lines in <code>/etc/security/limits.d/audio.conf</code>:
<pre>
@audio - rtprio 80
@audio - memlock unlimited
</pre>  
</li>
</ul>

<h2>References</h2>
<ul>
  <li>Raspberry instructions for configuring: https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md  </li>
</ul>

