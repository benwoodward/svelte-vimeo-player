<script>
  import { SvelteVimeoPlayer } from './components/components.module.js';

  function logEvent(event) {
    console.log(event)
  }
</script>

<style>
</style>

<SvelteVimeoPlayer
  videoId="54348266"
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
