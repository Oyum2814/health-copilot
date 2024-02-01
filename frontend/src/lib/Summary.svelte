<script lang="ts">
  import { Tile, TextArea, Button, ButtonSet } from "carbon-components-svelte";
  import ArrowRight from "carbon-icons-svelte/lib/ArrowRight.svelte";
  import DiagramReference from "carbon-icons-svelte/lib/DiagramReference.svelte";
  import { onMount } from "svelte";
  import { DoctorSocket } from "../types";

  let value = ``;

  onMount(() => {

    DoctorSocket.on("generate_notes", (x) => {
      console.log(x);
      value = x
    });
  });

  const generate = () => {
    DoctorSocket.emit("generate_notes", value);
  };

  const setSummary = () => {
    DoctorSocket.emit("set_summary", value)
  };

</script>

<div class="w-full h-full flex  flex-col justify-start bg-white ">
  <Tile class="block rounded-t-[9px] overflow-hidden bg-black">
    <p class="text-lg">Doctors consultation notes</p>
  </Tile>
  <TextArea
    hideLabel
    placeholder={`Record any notes not captured in the transcript here. You can then use "Generate" to autogenerate a full consultation summary.`}
    class="block bg-white border-2 border-black text-black"
    bind:value
    on:change={setSummary}
    rows={20}
  />
  <ButtonSet class="flex w-full justify-evenly mb-20">
    <!-- <Button
      on:click={() => {
        location.reload();
      }}
      kind="danger-ghost">Reset</Button
    > -->
    <Button icon={DiagramReference} class="block bg-blue-600 hover:bg-blue-800 font-bold" kind="secondary" on:click={generate}
      >Generate</Button
    >
    <Button on:click={setSummary} class="block font-bold" icon={ArrowRight}>Save</Button>
  </ButtonSet>

  <div />
</div>
