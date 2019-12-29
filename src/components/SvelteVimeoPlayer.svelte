<div id="{elementId}">
</div>

<script>
  import { onMount, onDestroy, createEventDispatcher } from 'svelte';
  import Player from '@vimeo/player';
  import assign from 'object-assign';

  export let playerHeight = 320;
  export let playerWidth = 640;
  export let options = () => ({});
  export let videoId;
  export let loop = false;
  export let autoplay = false;

  const dispatch = createEventDispatcher();
  const eventsToDispatch = [
    'play',
    'pause',
    'ended',
    'timeupdate',
    'progress',
    'seeked',
    'texttrackchange',
    'cuechange',
    'cuepoint',
    'volumechange',
    'error',
    'loaded'
  ]
  let playerId = parseInt(Math.random() * 100000).toString();
  let elementId = `vimeo-player-${videoId}`;
  let player;
  let volumeBeforeMute = 1;

  $: loadVideo(videoId)

  function loadVideo(id) {
    if (!player) return

    return player.loadVideo(id)
  }

  export function play() {
    return player.play()
  }

  export function pause() {
    return player.pause()
  }

  export function mute() {
    player.getVolume()
      .then(volume => volumeBeforeMute = volume)
      .catch(error => volumeBeforeMute = 0.5)
    return player.setVolume(0)
  }

  export function unmute(volume = volumeBeforeMute) {
    return player.setVolume(volume)
  }

  function setEvents() {
    player.ready()
      .then(() => dispatch('ready', { player: player }))
      .catch(error => dispatch('error', { error: error, player: player }))

    eventsToDispatch.forEach(event => dispatchOnPlayerEvent(event))
  }

  function dispatchOnPlayerEvent (event) {
    player.on(event, data => dispatch(event, { data: data, player: player }))
  }

  onMount(async () => {
    const options = {
      id: videoId,
      width: playerWidth,
      height: playerHeight,
      loop: loop,
      autoplay: autoplay
    }

    player = new Player(elementId, assign(options, options))

    setEvents()
  });

	onDestroy(() => {
    player.unload()
  });
</script>
