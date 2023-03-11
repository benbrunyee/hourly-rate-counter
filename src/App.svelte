<script lang="ts">
  import { onDestroy, onMount } from "svelte";

  let hourly = 40;
  let counter = 0;

  let interval: number | null = null;

  onMount(() => {
    interval = setInterval(() => {
      // Every second, add the second value to the counter
      counter += hourly / 3600;
    }, 1000);
  });

  onDestroy(() => {
    if (interval) {
      clearInterval(interval);
    }
  });
</script>

<div class="w-screen h-screen flex bg-neutral-800">
  <div class="m-auto flex flex-col gap-4 text-center text-white">
    <span class="text-9xl font-bold">£{Math.floor(counter * 100) / 100}</span>
    <div class="flex gap-2 justify-center">
      <span>£</span>
      <input
        bind:value={hourly}
        class="border px-2 w-10 text-black rounded-sm"
      />
      <span>per hour</span>
    </div>
  </div>
</div>
