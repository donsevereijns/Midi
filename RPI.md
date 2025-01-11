<h2>Raspberry PI microSD and OS</h2>
First I run a simple PoC to check if the latency of response to pressing keys on the midi keyboard can be managed via realtime scheduling. If this appears too slow I will need to install a linux low-latency kernel, and perform associated remediations. 
As I plan to use digital audio out, the USB interface will add latency, so this will be important.
<ul>
<li>Image de microSD card, using Raspberry PI Imager and the Raspberry PI OS Lite image, bootable and SSH enabled.</li>
<li>Add <code>rpi/wpa_supplicant.config</code> to the boot partition.</li>
<li>Boot the RPI with the new image. Use the Fink app to SSH into the RPI. Login with UID pi, pswd raspberry.</li>
<li>Update the RPI: <code>sudo apt-get update</code> and <code>sudo apt-get upgrade</code></li>
</ul>
