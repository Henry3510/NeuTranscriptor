<div class="w-full h-13 bg-zinc-800 absolute left-0 bottom-0 flex justify-center items-center" style="border-radius: 5px 5px 0 0;">
  <div class="w-5 h-5 m-r3 op-70" style="border-radius: 50%" class:bg-red="{!connected}" class:bg-green="{connected}"></div>
  <p class="color-white op-50 font-sans text-4">{connected ? "Connected!" : "Not connected"} v0.1.0</p>
</div>

<script>
let connected = false
</script>