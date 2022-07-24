<div in:fade class="overflow-hidden rounded">
  <div class="flex p-3 items-center justify-between">
    <div class="flex items-center">
      <i class="color-white w-10 h-10 op-80">
        <svg class="w-10 h-10" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24"><g fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="--darkreader-inline-stroke: currentColor;" data-darkreader-inline-stroke=""><path d="M14 3v4a1 1 0 0 0 1 1h4"></path><path d="M17 21H7a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h7l5 5v11a2 2 0 0 1-2 2z"></path><circle cx="11" cy="16" r="1"></circle><path d="M12 16v-5l2 1"></path></g></svg>
      </i>
      <span class="m-l-2 color-white op-80 font-sans">{file.name}</span>
    </div>
    <i class="color-white op-70 hover:color-red hover:op-100 active:op-70 transition-all w-5 h-5" on:click={cancel}>
      <svg class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24"><path d="M12 2C6.47 2 2 6.47 2 12s4.47 10 10 10s10-4.47 10-10S17.53 2 12 2zm5 13.59L15.59 17L12 13.41L8.41 17L7 15.59L10.59 12L7 8.41L8.41 7L12 10.59L15.59 7L17 8.41L13.41 12L17 15.59z" fill="currentColor" style="--darkreader-inline-fill: currentColor;" data-darkreader-inline-fill=""></path></svg>
    </i>
  </div>
  <div class="h-3px m-t--3px bg-green" style="width: {$percentage}%;">

  </div>
</div>

<script>
import {fade} from 'svelte/transition'
import {tweened} from 'svelte/motion'
import {quadInOut} from 'svelte/easing'
import { onMount } from 'svelte';

if (!globalThis.file) {
  location.hash = '/'
}

const file = globalThis.file ?? {
  name: ''
} // Prevent "read properties of undefined" when prerendering

const percentage = tweened(0, {
  duration: 500,
  easing: quadInOut
})

function cancel() {
  location.hash = '/'
}

onMount(() => {
  const xhr = new XMLHttpRequest()
  // xhr.open('POST', '/upload') TODO: Upload API
  xhr.onload = () => {
    if (xhr.status === 200) {
      location.hash = '/'
    }
  }
  xhr.upload.onprogress = (e) => {
    if (e.lengthComputable) {
      percentage.set(e.loaded / e.total * 100)
    }
  }
  // xhr.send(file)

  // TODO: DEBUG
  setTimeout(() => {
    percentage.set(50)
    setTimeout(() => {
      percentage.set(100)
      setTimeout(() => {
        localStorage.setItem('taskId', '114514')
        location.hash = '/transcripting'
      }, 1000)
    }, 1000)
  }, 1000)

})
</script>