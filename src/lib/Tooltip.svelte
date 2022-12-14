<script>
  import { fade } from "svelte/transition";
  import { teleport } from "$lib/helpers/teleport";

  export let text = "";
  export let open = false;

  // Position
  export let direction = 'up'; // up, down, left, right
  export let align = 'center'; // center, left, right, top, bottom
  export let distance = 4; // in px

  // Classes
  export let classBase = "tooltip";
  export let classTrigger = `${classBase}__trigger`;
  export let classContent = `${classBase}__content`;
  export let classDirection = `${classBase}--${direction}-${align}`;

  let className = "";
  export { className as class }; // Extra classes

  // Copy text
  export let copy = null; // Option 1: Text that will be copied
  export let copyFunc = null; // Option 2: Function to fetch text to be copied
  export let copiedLabel = "Copied!"; // Text to shopw when copied
  let copyStatus = null; // Control copy status
  $: if (copyStatus) {
    setTimeout(() => { copyStatus = "" }, 2000); // Reset copy status after 2 seconds
  }

  // Delay
  export let delay = 100;
  export let duration = 100;
  let timer;

  let triggerContainer;
  let scrollableParent; // Hide when parent scrolls
  let style = "";


  // ====================================
  // Functions

  function handlecopy() {
    console.log("---- handle copy");
    if (!copy && !copyFunc) return; // Nothing to copy
    if (copyFunc) copy = copyFunc(); // Get text from function
    if (navigator?.clipboard) { // Check for support
      navigator.clipboard.writeText(copy) // Copy to clipboard
      .then(() => {
        copyStatus = copiedLabel; // Show copied status
      })
    }
  }

  function showTooltip() {
    calculatePosition();
    open = true;
    updateScrollableParent(triggerContainer);
  }

  function handleClick() {
    if (copy || copyFunc) {
      handlecopy();
    } else {
      hideTooltip();
    }
  }

  function hideTooltip() {
    if (!open) return
    open = false;
    copyStatus = "";
    updateScrollableParent(triggerContainer); // Reset scrollableParent
  }

  function updateScrollableParent(node) {
    if (open) {
      if (!node) return;

      // Node scrolls
      if (node.scrollHeight > node.clientHeight) {
        node.addEventListener('scroll', hideTooltip);
        scrollableParent = node; // Set scrollable parent

      // Try again with node's parent
      } else {
        return updateScrollableParent(node.parentNode);
      }

    } else {
      if (scrollableParent) {
        scrollableParent.removeEventListener('scroll', hideTooltip);
        scrollableParent = null;
      }
    }
  }

  function handleHover(e) {
    if (timer) window.clearTimeout(timer); // Reset timer

    if (e.type == 'mouseenter') {
      timer = window.setTimeout(() => {
        showTooltip();
      }, delay);
    }

    if (e.type == 'mouseleave') {
      timer = window.setTimeout(() => {
        hideTooltip();
      }, delay);
    }
  }

  function calculatePosition() {
    const container = triggerContainer.getBoundingClientRect();
    let position = { top: 0, right: 0, bottom: 0, left: 0 };
    let transform = "";

    if (direction == 'up') {
      position.bottom = window.innerHeight - container.top + distance; // Align above with distance
    }

    if (direction == 'down') {
      position.top = container.bottom + distance; // Align below with distance
    }

    if (direction == 'right') {
      position.left = container.right + distance; // Align right with distance
    }

    if (direction == 'left') {
      position.right = document.body.clientWidth - container.left + distance; // Align right with distance
    }

    // Vertical align
    if (['up', 'down'].includes(direction)) {
      if (align == 'center') {
        position.left = container.left + (container.width / 2);
        transform = "transform: translateX(-50%);";
      }
      if (align == 'left') {
        position.left = container.left;
      }
      if (align == 'right') {
        position.right = document.body.clientWidth - container.right;
      }
    }

    // Horizontal align
    if (['left', 'right'].includes(direction)) {
      if (align == 'center') {
        position.top = container.top + (container.height / 2);
        transform = "transform: translateY(-50%);";
      }
      if (align == 'top') {
        position.top = container.top;
      }
      if (align == 'bottom') {
        position.bottom = window.innerHeight - container.bottom;
      }
    }

    style = ""; // Reset
    style += position.top     ? `top:     ${position.top}px; `    : '';
    style += position.right   ? `right:   ${position.right}px; `  : '';
    style += position.bottom  ? `bottom:  ${position.bottom}px; ` : '';
    style += position.left    ? `left:    ${position.left}px; `   : '';
    style += transform;
  }

</script>

<svelte:window on:scroll={hideTooltip} on:resize={hideTooltip} />

<!-- Trigger -->
<span class={classTrigger} bind:this={triggerContainer} on:mouseenter={handleHover} on:mouseleave={handleHover} on:click={handleClick}>
  <slot />
</span>

<!-- Text prop / Content slot -->
{#if open && (text || $$slots.content || copyStatus)}
  <div class="{classBase} {className} {classDirection}" use:teleport transition:fade={{duration}} {style}>
    {#if copyStatus}
      <span in:fade class={classContent}>
        {copyStatus}
      </span>
    {:else}
      <slot name="content">
        <div in:fade class={classContent}>
          {text}
        </div>
      </slot>
    {/if}
  </div>
{/if}
