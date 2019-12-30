# SvelteVimeoPlayer
Just a thin svelte-wrapper around [Vimeo's player.js](https://github.com/vimeo/player.js/)

## Usage

```
<script>
  import { SvelteVimeoPlayer } from 'svelte-vimeo-player';

  let player

  function logEvent(event) {
    console.log(event)
  }
</script>

<SvelteVimeoPlayer videoId="54348266" bind:this={player} on:play={logEvent} />
```
