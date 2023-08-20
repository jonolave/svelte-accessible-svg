<script>
  import Tooltip from "$components/Tooltip.svelte";

  // Illustration size
  let width = 500;
  let height = 300;

  // Circle radius
  let radius = 40;

  let circles = [
    { id: 1, xpos: 150, ypos: 100, color: "red" },
    { id: 2, xpos: 350, ypos: 100, color: "blue" },
    { id: 3, xpos: 250, ypos: 200, color: "green" },
  ];

  let hoverData;
  let hoverX;
  let hoverY;
  $: console.log(hoverData);

  function buttonClick() {
    console.log("Button clicked!");
    // Add your custom logic here
  }
</script>

<main>
  <h1>Let's create an interactive and accessible SVG</h1>

  <button on:click={buttonClick}>Click Me</button>
  <br>

  <div
    class="chart-container"
    bind:clientWidth={width}
    on:mouseleave={() => (hoverData = null)}
  >
    <svg {width} {height}
    aria-labelledby="svg-title"
    >
    <!-- Title for screen reader to read -->
    <title id="svg-title">Illustration with three circles next to each other</title>
      {#each circles as circle}
        <!-- describedby: tell screen reader to connect the circle to the hover -->
        <circle
          aria-describedby="tooltip"
          cx={circle.xpos}
          cy={circle.ypos}
          r={hoverData == circle.id ? radius * 1.2 : radius}
          fill={hoverData == circle.id ? "yellow" : circle.color}
          aria-label="Aria label on the circle {circle.id}"
          on:mouseover={() => {
            hoverData = circle.id;
            hoverX = circle.xpos;
            hoverY = circle.ypos;
          }}
          on:focus={() => {
            hoverData = circle.id;
            hoverX = circle.xpos;
            hoverY = circle.ypos;
          }}
          on:mouseleave={() => {
            hoverData = null;
          }}
          on:blur={() => {
            hoverData = null;
          }}
          tabIndex="0"
        />
      {/each}
    </svg>
    {#if hoverData}
      <Tooltip {hoverData} {hoverX} {hoverY} />
    {/if}
  </div>
  <br>
  <button on:click={buttonClick}>Click Me</button>
</main>

<style>
  main {
    text-align: center;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: #f0f0f0;
  }

  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    font-weight: 700;
  }

  circle {
    transition: r 300ms ease, opacity 500ms ease;
    cursor: pointer;
}

  .chart-container {
    position: relative;
    background: #c9bcbc;
  }

  .tooltip {
    background: #ffffff;
  }
</style>
