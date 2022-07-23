<div class="m-b-13">
  <h1 class="color-white text-center m-b-10 m-t-0 font-sans">{title}</h1>
  <main style="height: {$outerHeight}px"
    class="overflow-hidden transition-colors border-outset border-solid border-slate-700 rounded w-full"
    class:hover:border-slate-600={$location === '/'}
    class:hover:bg-zinc-800={$location === '/'}
    class:active:border-slate-700={$location === '/'}
    class:active:bg-transparent={$location === '/'}
  >
    <div bind:this={inner}>
      <Router {routes}/>
    </div>
  </main>
  <ServerStates/>
</div>

<script>
import Router from 'svelte-spa-router'
import {location} from 'svelte-spa-router'

import Start from './views/Start.svelte'
import Uploading from './views/Uploading.svelte'
import Transcripting from './views/Transcripting.svelte'
import Success from './views/Success.svelte'
import Error from './views/Error.svelte'

import ServerStates from './components/ServerStates.svelte'

const routes = {
  '/': Start,
  '/uploading': Uploading,
  '/transcripting': Transcripting,
  '/success': Success,
  '/error': Error
}

$:title={
  '/': 'Neu Transcriptor',
  '/uploading': 'Uploading...',
  '/transcripting': 'Transcripting...',
  '/success': 'Finished!',
  '/error': 'Oops!'
}[$location]

// Animation
import { tweened } from 'svelte/motion'
import { cubicInOut } from 'svelte/easing'
import { onMount } from 'svelte';
let inner
const outerHeight = tweened(310, {
  duration: 300,
  easing: cubicInOut
})

const observer = new ResizeObserver(() => {
  outerHeight.set(inner.offsetHeight)
})

onMount(() => {
  observer.observe(inner)
})
</script>
