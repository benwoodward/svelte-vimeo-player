<svelte:options accessors={true}/>

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
  let vimeo
  export let player;

  $: loadVideo(videoId)

  function loadVideo(id) {
    if (!player) return

    return player.loadVideo(id)
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

  let handler = {
    get: function(target, prop) {
      var value = target[prop];
      return typeof value == 'function' ? value.bind(target) : value;
    }
  }

  onMount(async () => {
    const options = {
      id: videoId,
      width: playerWidth,
      height: playerHeight,
      loop: loop,
      autoplay: autoplay
    }

    vimeo = new Player(elementId, assign(options, options))
    player = new Proxy(vimeo, handler)

    setEvents()
  });

  onDestroy(() => {
    player.unload()
  });
</script>

<div id="{elementId}">
</div>
