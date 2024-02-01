<script lang="ts">
  import AiNotes from "$lib/AINotes.svelte";
  import Summary from "$lib/Summary.svelte";
  import Transcription from "../../lib/Transcription.svelte";

  
</script>

<div class="w-full flex justify-around gap-x-2 h-[90vh] mx-15 ">
  <div class="w-2/3 h-full flex flex-col gap-y-3">
    <div class="h-[35%] bg-black">
      <Transcription />
    </div>
    <div class="h-[60%]">
      <AiNotes />
    </div>
    
  </div>
  <div class="w-1/3 h-[97%] overflow-hidden bg-black">
    <Summary />
  </div>
</div>
