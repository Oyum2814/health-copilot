<script lang="ts">
  import { Tile, Content } from "carbon-components-svelte";
  import { onMount } from "svelte";
  import { DoctorSocket } from "../types";
  import SvelteMarkdown from "svelte-markdown";

  let ddx = "";
  let qa = "";

  onMount(async () => {


    // cds_ddx
    DoctorSocket.on("cds_ddx", (x) => {
      console.log(x);
      ddx = x.replaceAll("\n", "\n\n");
    });

    // cds_qa
    DoctorSocket.on("cds_qa", (x) => {
      console.log(x);
      qa = x.replaceAll("\n", "\n\n");
    });
  });
</script>

<div class="flex gap-2 h-full">
  <div class="w-1/2 border-gray-600 border-[1px] border-solid h-full rounded-md overflow-hidden">
    <Tile class="bg-black">
      <p>Diagnosis Report (Potential)</p>
    </Tile>
    <div class="h-full m-2 overflow-y-scroll">
      <Content class="text-base prose text-lg text-black" >
        <SvelteMarkdown source={ddx} />
      </Content>
    </div>
  </div>
  <div class="w-1/2 border-gray-600 border-[1px] border-solid rounded-md overflow-hidden h-full">
    <Tile class="bg-black">
      <p> Questions to be asked</p>
    </Tile>
    <div class="h-full m-2 overflow-y-scroll">
      <Content class="text-base prose text-lg text-black">
        <SvelteMarkdown source={qa} />
      </Content>
    </div>
  </div>
</div>
