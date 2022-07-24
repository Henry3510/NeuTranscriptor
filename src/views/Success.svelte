<div in:fade class="text-center p-10">
  <i class="color-green w-25 h-25">
    <svg class="w-25 h-25" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24"><g fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="--darkreader-inline-stroke: currentColor;" data-darkreader-inline-stroke=""><path d="M14 3v4a1 1 0 0 0 1 1h4"></path><path d="M17 21H7a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h7l5 5v11a2 2 0 0 1-2 2z"></path><path d="M9 15l2 2l4-4"></path></g></svg>
  </i>
  <p class="color-white font-mono text-6 font-500">Transcription completed</p>
  <p class="color-white op-70 font-sans max-w-70 ma">Next, pick up your MIDI file:</p>
  <br>
  <Button on:click={download}>
    {#if typeof window.__TAURI__ !== 'undefined'}
      Save As
    {:else}
      Download
    {/if}
  </Button>

  <Button on:click={() => location.hash="/"}>
    Back
  </Button>
</div>

<script>
import {fade} from 'svelte/transition'
import Button from '../components/Button.svelte'

import {save} from '@tauri-apps/api/dialog'
import { downloadDir } from '@tauri-apps/api/path';
import {fetch as tauriFetch} from '@tauri-apps/api/http'
import {writeBinaryFile} from '@tauri-apps/api/fs'

async function download() {
  // TODO: download the MIDI file: Get task data from backend
  let url = "https://storage.bwrrc.org.cn/DEMO.mid"
  let fileName = "DEMO.mid"

  if (typeof window.__TAURI__ !== 'undefined') {
    let targetPath = await save({
      title: "Save MIDI file",
      filters: [
        {name: "MIDI file", extensions: ["midi"]}
      ],
      defaultPath: await downloadDir() + fileName
    })
    console.log(targetPath);
    if (targetPath) {
      let resp = await fetch(url, {
        method: "GET",
      })
      // Convert body to Uint8Array
      let body = await resp.arrayBuffer()
      writeBinaryFile(targetPath, body).catch(() => location.hash="/error")
    }
  } else {
    // Normal browser: create a link and click it
    let link = document.createElement("a")
    link.href = url
    link.download = fileName
    link.click()
  }
}
</script>