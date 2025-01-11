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
