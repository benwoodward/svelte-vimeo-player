<script>
  import { SvelteVimeoPlayer } from './components/components.module.js';

  let player

  function logEvent(event) {
    console.log(event)
  }
</script>

<style>
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
<div on:mouseover={() => player.mute()} on:mouseout={() => player.unmute()} >Hover over this text to mute/unmute the video</div>
