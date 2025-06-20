<script>
  import Canvas from "./Canvas.svelte";

  let padding = $state(3);
  let sizeFocused = $state(10);
  let sizeOther = $state(2);
</script>

<main>
  <div class="canvas">
    <Canvas
      padding={padding}
      sizeFocused={sizeFocused}
      sizeOther={sizeOther}
    />
  </div>

  <div class="controls">
    <label>
      <span class="label">Padding: {padding}</span>
      <input
        type="range"
        bind:value={padding}
        min="0"
        max="100"
      />
    </label>

    <label>
      <span class="label">Size A: {sizeFocused}</span>
      <input
        type="range"
        bind:value={sizeFocused}
        min="1"
        max="20"
      />
    </label>

    <label>
      <span class="label">Size B: {sizeOther}</span>
      <input
        type="range"
        bind:value={sizeOther}
        min="1"
        max="20"
      />
    </label>
  </div>
</main>

<style>
  .controls {
    margin-top: 20px;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .label {
    display: inline-block;
    width: 100px;
    text-align: left;
  }
</style>
