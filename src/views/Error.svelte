<div class="text-center p-10" in:fade>
  <i class="color-red w-25 h-25">
    <svg class="w-25 h-25" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 12 12"><g fill="none"><path d="M5.25 8.25a.75.75 0 1 1 1.5 0a.75.75 0 0 1-1.5 0zm.258-4.84a.5.5 0 0 1 .984 0l.008.09V6l-.008.09a.5.5 0 0 1-.984 0L5.5 6V3.5l.008-.09zM11 6A5 5 0 1 1 1 6a5 5 0 0 1 10 0zm-1 0a4 4 0 1 0-8 0a4 4 0 0 0 8 0z" fill="currentColor" style="--darkreader-inline-fill: currentColor;" data-darkreader-inline-fill=""></path></g></svg>
  </i>
  <p class="color-white font-mono text-6 font-500">An error occurred</p>
  <p class="color-white op-70 font-sans max-w-70 ma">This error is our problem and usually a retry will fix it.</p>
  <br>
  <Button on:click={() => location.hash="/"}>Back</Button>
</div>

<script>
import {fade} from 'svelte/transition'
import Button from '../components/Button.svelte'
</script>