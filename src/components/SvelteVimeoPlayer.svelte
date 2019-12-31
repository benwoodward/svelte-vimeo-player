<script>
  import VimeoPlayer from './VimeoPlayer.svelte'
	import { onMount } from 'svelte';

  export let playerHeight = 320;
  export let playerWidth = 640;
  export let options = () => ({});
  export let videoId;
  export let loop = false;
  export let autoplay = false;

  let vimeo
  export let player

  onMount(async () => {
    player = vimeo.player
  })
</script>

<VimeoPlayer
  videoId={videoId}
  playerHeight={playerHeight}
  playerWidth={playerWidth}
  options={options}
  loop={loop}
  autoplay={autoplay}
  bind:this={vimeo}
  player={vimeo}
/>
