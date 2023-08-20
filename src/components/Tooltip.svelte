<script>
  export let hoverData;
  export let hoverX;
  export let hoverY;

  // console.log("This circle is located at:", {hoverX, hoverY})
</script>

<div role="tooltip"
  class="tooltip"
  id="tooltip"
  style="position: absolute; top: {hoverY-50}px; left: {hoverX-30}px"
>
  <h1>Some interesting details</h1>
</div>

<style>
    .tooltip {
        position: absolute;
        background: white;
        box-shadow: rgba(0, 0, 0, 0.15) 2px 3px 8px; /* Gives a nice 3d effect */
        padding: 8px 6px; /* Adds space around content within tooltip */
        border-radius: 3px; /* Rounds corners */
        pointer-events: none; /* Prevents tooltip from blocking mouse events */
        transition: top 300ms ease, left 300ms ease;
    }
</style>
