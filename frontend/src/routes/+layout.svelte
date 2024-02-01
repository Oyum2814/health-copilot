<script lang="ts">
  import "carbon-components-svelte/css/g80.css";
  import "virtual:uno.css";
  import Nav from "$lib/Nav.svelte";
  export const ssr = false;

</script>

<Nav />
<div class="h-[90vh] w-screen flex justify-center items-center">
  <slot />
</div>

