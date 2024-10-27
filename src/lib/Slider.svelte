<script lang="ts">
  import { onMount } from "svelte";

  $:value = 25;

  let progressBar: HTMLDivElement;
  let mouseIsDown = false;
  let mouseIsInRange = false;

  function increment() {
    if (value < 100) {
      setTimeout(() => {
        value += 1;
      }, 100);
    }
  }

  function decrement() {
    if (value > 0) {
      setTimeout(() => {
        value -= 1;
      }, 100)
    }
  }

  function handleMouseUp(event: any) {
    mouseIsDown = false;
    mouseIsInRange = false;
  }

  function handleMouseDown(event: any) {
    mouseIsDown = true;
    let x = event.clientX;
    let y = event.clientY;
    let {top, right, bottom, left} = progressBar.getBoundingClientRect();
    console.log(`X: ${x}, Y: ${y}`);
    console.log(`normalize: ${x / window.innerWidth * 100}`);
    console.log(`Top: ${top}, Right: ${right}, Bottom: ${bottom}, Left: ${left}`);
    if (x < right && x > right - 30) {
      if (y < bottom && y > top) {
        mouseIsInRange = true;
        console.log("HIT");
      }
    }
  }

  function handleMouseDrag(event: any) {
    if (mouseIsDown) {
      let { right } = progressBar.getBoundingClientRect();
      value = Math.round(event.clientX / window.innerWidth * 100);
      // value = event.clientX - progressBar.getBoundingClientRect().left;
    }
  }

  onMount(() => {
    // progressBar.setAttribute("style", "width: {value}%");
  })
</script>

<div id="myContainer">
  <button class="btn btn-primary btn-small" on:click={decrement}>-</button>
  <button class="btn btn-primary btn-small" on:click={increment}>+</button>
  <div class="progress" role="progressbar" aria-label="Example 20px high" aria-valuenow="25" aria-valuemin="0" aria-valuemax="100" style="height: 20px">
    <div
      class="progress-bar bg-success"
      style="width: {value}%"
      on:mousedown={e => handleMouseDown(e)}
      on:mouseup={e => handleMouseUp(e)}
      on:drag={e => handleMouseDrag(e)}
      bind:this={progressBar}
    >{value}%</div>
  </div>
</div>


<style>
</style>