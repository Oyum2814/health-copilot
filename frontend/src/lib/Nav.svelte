<script lang="ts">
  import { page } from "$app/stores";
  import { Button, Header, HeaderNav, HeaderNavItem } from "carbon-components-svelte";
  import { DoctorSocket, connected } from "../types";
  let isSideNavOpen = false;

  let running = false

  const stopMic = ()=>{
    DoctorSocket.emit("stop_recording", undefined, (value: boolean)=>{
      if (value) {
        running = false
      }
    })
  }

  const startMic = ()=> {
    DoctorSocket.emit("start_recording", undefined, (value: boolean)=>{
      if (value) {
        running = true
      }
    })
  }
</script>
<div class="h-[10vh]">
  <div class=" w-full flex items-center gap-x-8 ml-3">
    <a href="/" class="text-black font-bold text-lg py-2 decoration-none cursor-pointer">
      HealthCopilot
    </a>
    {#if $connected}
      {#if running}
      <button on:click={stopMic} class="bg-red-600 text-white font-bold px-4 py-2">Stop</button>  
      {:else}
      <Button on:click={startMic} class="bg-blue-600 text-white font-bold px-4 py-2">Start</Button>  
      {/if}
    {:else}
    <button on:click={stopMic} class="bg-gray-600 text-white font-bold px-4 py-2">Not connected</button>  
    {/if}
    
    <div >
      <a href="/doctor" class="decoration-none text-black px-4">
        DoctorAI
      </a>
      <a href="/patient" class="decoration-none text-black px-4">
        PatientAI
      </a>
    </div>
    </div>
</div>

