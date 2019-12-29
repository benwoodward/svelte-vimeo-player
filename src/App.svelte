<script>
  import { SvelteVimeoPlayer } from './components/components.module.js';

  let player
  let volumeBeforeMute = 1;

  function mute() {
    player.getVolume()
      .then(volume => volumeBeforeMute = volume)
      .catch(error => volumeBeforeMute = 0.5)

    hideMuteButton()

    return setVolume(0)
  }

  function unmute(volume = volumeBeforeMute) {
    showMuteButton()
    return setVolume(volume)
  }

  function setVolume(volume) {
    player.getVolume().then(function(volume) {
      console.log(volume)
    })
    showMuteButton()
    return player.setVolume(volume)
  }

  function logEvent(event) {
    console.log(event)
  }

  function hideMuteButton() {
    document.getElementById('mute').classList.add('hide');
    document.getElementById('unmute').classList.remove('hide');
  }

  function showMuteButton() {
    document.getElementById('unmute').classList.add('hide');
    document.getElementById('mute').classList.remove('hide');
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
  on:error={logEvent}
  on:play={logEvent}
  on:pause={logEvent}
/>

Set the volume
/* Added some invisible characters to hack the jarring motion, with this the
 buttons are nearly evenly wide */
<button id='mute' on:click={mute}>‌‌ ‌‌ mute ‌‌ ‌‌</button>
<button id='unmute' class='hide' on:click={unmute}>unmute</button>
<button on:click={() => setVolume(0.1)}>10%</button>
<button on:click={() => setVolume(0.2)}>20%</button>
<button on:click={() => setVolume(0.3)}>30%</button>
<button on:click={() => setVolume(0.4)}>40%</button>
<button on:click={() => setVolume(0.5)}>50%</button>
<button on:click={() => setVolume(0.6)}>60%</button>
<button on:click={() => setVolume(0.7)}>70%</button>
<button on:click={() => setVolume(0.8)}>80%</button>
<button on:click={() => setVolume(0.9)}>90%</button>
<button on:click={() => setVolume(1)}>100%</button>
