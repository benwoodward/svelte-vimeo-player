<div id="{elementId}">
</div>

<script>
  import Player from '@vimeo/player'
  import assign from 'object-assign'

  export let playerHeight = 320
  export let playerWidth = 640
  export let options = () => ({})
  export let videoId = true
  export let loop = false
  export let autoplay = false

  let playerId = parseInt(Math.random() * 100000).toString();
  let elementId = `vimeo-player-${divId}`;
  let player;

  $: loadVideo(videoId)

  function emitVueEvent (event) {
    this.player.on(event, (data) => {
      this.$emit(event, data, this.player)
    })
  }

  const eventsToEmit = [
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

  function loadVideo(id) {
    return this.player.loadVideo(id)
  }

  function play() {
    return this.player.play()
  }

  function pause() {
    return this.player.pause()
  }

  function mute() {
    return this.player.setVolume(0)
  }

  function unmute(volume = 0.5) {
    return this.player.setVolume(volume)
  }

  function setEvents() {
    const vm = this

    this.player.ready()
      .then(function () {
        vm.$emit('ready', vm.player)
      })
      .catch((error) => {
        vm.$emit('error', error, vm.player)
      })

    eventsToEmit.forEach(event => emitVueEvent.call(vm, event))
  }

  onMount(async () => {
    const options = {
      id: this.videoId,
      width: this.playerWidth,
      height: this.playerHeight,
      loop: this.loop,
      autoplay: this.autoplay
    }

    this.player = new Player(this.elementId, assign(options, this.options))

    this.setEvents()
  })

	onDestroy(() => {
    this.player.unload()
  }
</script>
