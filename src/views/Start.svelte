<div class="pa-10 flex items-center flex-col color-white select-none" on:click={() => fileInput.click()} on:dragenter={dragEnter} on:dragover={dragOver} on:drop={drop}>
  <i>
    <svg class="w-25 h-25" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24"><g fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="--darkreader-inline-stroke: currentColor;" data-darkreader-inline-stroke=""><path d="M4 17v2a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-2"></path><path d="M7 9l5-5l5 5"></path><path d="M12 4v12"></path></g></svg>
  </i>
  <br>
  <p class="font-sans op-80 text-5 max-w-80 text-center" style="line-height: 35px;">Drag and drop the file here, or click here</p>
  <p style="line-height: 35px;" class="font-mono op-0 m-t--15 color-red font-600 text-5 5 max-w-80 text-center" class:important-op-100="{errorMsg}" class:important-m-0="{errorMsg}">Error: {errorMsg}</p>
  <input type="file" class="hidden" bind:this={fileInput}>
</div>

<script>
import { fade } from 'svelte/transition'

let fileInput
let errorMsg

function dragEnter(event) {
  event.preventDefault()
  event.stopPropagation()
  // Check if the file is a valid audio file(mp3 currently)
  if (event.dataTransfer.items.length > 0 && event.dataTransfer.items[0].kind === 'file' && event.dataTransfer.items[0].type === 'audio/mpeg') {
    errorMsg = null
  } else {
    errorMsg = 'Invalid file type, only .mp3 files are supported'
  }
}

function dragOver(event) {
  event.preventDefault()
  event.stopPropagation()
}

function drop(event) {
  event.preventDefault()
  event.stopPropagation()
  if (errorMsg) return
  const file = event.dataTransfer.files[0]
  globalThis.file = file
  // Goto /#/uploading
  location.hash = '/uploading'
}
</script>