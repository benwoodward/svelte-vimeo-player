<script>
  import { SvelteVimeoPlayer } from './components/components.module.js';

  let player

  function logEvent(event) {
    console.log(event)
  }

  function mute() {
    player.mute()
    document.getElementById('mute').classList.add('hide');
    document.getElementById('unmute').classList.remove('hide');
  }

  function showMuteButton() {
    document.getElementById('unmute').classList.add('hide');
    document.getElementById('mute').classList.remove('hide');
  }

  function unmute() {
    player.unmute()
    showMuteButton()
  }

  function setVolume(percent) {
    player.setVolume(percent)
    showMuteButton()
  }
</script>

<style>
  :global(.hide) {
    display: none;
  }
</style>

<SvelteVimeoPlayer
  videoId="54348266"
  bind:this={player}
  on:ready={logEvent}
  on:error={logEvent}
  on:play={logEvent}
  on:pause={logEvent}
  on:ended={logEvent}
  on:timeupdate={logEvent}
  on:progress={logEvent}
  on:seeked={logEvent}
  on:texttrackchange={logEvent}
  on:cuechange={logEvent}
  on:cuepoint={logEvent}
  on:volumechange={logEvent}
  on:error={logEvent}
  on:loaded={logEvent}
/>
Set the volume
/* Added some invisible characters to hack the jarring motion, with this the
 buttons are nearly evenly wide */
<button id='mute' on:click={mute}>‌‌ ‌‌ mute ‌‌ ‌‌</button>
<button id='unmute' class='hide' on:click={unmute}>unmute</button>
<button on:click={() => setVolume(10)}>10%</button>
<button on:click={() => setVolume(20)}>20%</button>
<button on:click={() => setVolume(30)}>30%</button>
<button on:click={() => setVolume(40)}>40%</button>
<button on:click={() => setVolume(50)}>50%</button>
<button on:click={() => setVolume(60)}>60%</button>
<button on:click={() => setVolume(70)}>70%</button>
<button on:click={() => setVolume(80)}>80%</button>
<button on:click={() => setVolume(90)}>90%</button>
<button on:click={() => setVolume(100)}>100%</button>
