<!-- see https://github.com/IBM/carbon-components-svelte/blob/master/examples/rollup-->
<script>
  import { Header, SkipToContent } from "carbon-components-svelte";
  import { getContext } from "svelte";

  const ctx = getContext("Theme");
  $: if (ctx) {
    ctx.dark.subscribe((value) => {
      console.log("dark mode?", value);
    });
    ctx.light.subscribe((value) => {
      console.log("light mode?", value);
    });
    ctx.updateVar("--cds-productive-heading-06-font-size", "4rem");
  }

  export let isSideNavOpen = false;
</script>

<Header
  company="DycodeX"
  platformName="PowtraX LoRaWAN"
  href="/"
  bind:isSideNavOpen
>
  <div slot="skip-to-content">
    <SkipToContent />
  </div>
</Header>
