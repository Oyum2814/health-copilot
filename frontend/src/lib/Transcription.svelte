<script lang="ts">
  import { Tile, Content } from "carbon-components-svelte";
  import SvelteMarkdown from "svelte-markdown";
  import CircleDash from "carbon-icons-svelte/lib/CircleDash.svelte";

  import { DoctorSocket, type TranscriptMessage } from "../types";
  import { onMount } from "svelte";

  let live: string;
  let loading = false;

  onMount(async () => {
    DoctorSocket.on("transcript", (x) => {
      console.log(x);
      loading = true;
      live = x.replaceAll("\n", "\n\n");
    });
  });
</script>

<div
  class="h-full border-2 border-gray-600 border-solid flex flex-col overflow-x-hidden"
>
  <Tile class="w-full flex justify-between bg-black ">
    <p class="text-lg">Transcription</p>
    <!-- <CircleDash
      class="w-6 h-6 block  {loading && 'animate-duration-[1s] animate-pulse'}"
    /> -->
  </Tile>

  <div class="overflow-y-scroll h-full bg-white p-2 text-black">
    {#if live}
      <SvelteMarkdown source={live} />
    {:else}
      <p class="text-black">Conversation Transcript</p>
    {/if}
  </div>
</div>
