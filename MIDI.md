<h2>Connect the MIDI keyboard to the SW synthesizer</h1>
<ol>
<li><code>aconnect -o</code> shows the devices involved. In my case:
  $ aconnect -o
client 14: 'Midi Through' [type=kernel]
    0 'Midi Through Port-0'
client 24: 'Novation SL MkIII' [type=kernel,card=2]
    0 'Novation SL MkIII SL MkIII MIDI'
    1 'Novation SL MkIII SL MkIII InCo'
    2 'Novation SL MkIII SL MkIII To D'
    3 'Novation SL MkIII SL MkIII To D'
    4 'Novation SL MkIII SL MkIII To C'
client 128: 'FLUID Synth (609)' [type=user,pid=609]
    0 'Synth input port (609:0)'
</li>
<li>Connect the MIDI devide to Fluidsynth by running <pre>aconnect 24:0 128:0</pre></li>
</ol>
