<script>
  import { createEventDispatcher } from "svelte";
  import { fly } from "svelte/transition";
  import { teleport } from "$lib/helpers/teleport";

  const dispatch = createEventDispatcher();

  // Open state
  export let open = false;

  // Reference
  export let menu = undefined;

  // Size
  // Make dropdown's min-width equal to trigger's width
  export let matchWidth = false;

  // Position
  export let direction = 'down'; // up, down, left, right
  export let align = ['up', 'down'].includes(direction) ? 'left' : 'top'; // center, left, right, top, bottom

  // Classes
  export let baseClass = "dropdown";
  export let classTrigger   = `${baseClass}__trigger`;
  export let classMenu      = `${baseClass}__menu`;
  export let classDirection = `${baseClass}--${direction}-${align}`;

  let className = "";
  export { className as class }; // extra classes

  // Modifiers
  export let over = false; // Display menu over trigger
  export let distance = 4; // in px
  export let duration = 150; // Transition duration in ms

  // Open on hover
  export let hover = false;
  export let hoverDelay = 100;
  let hoverTimer;

  let style = ""; // Calculated menu style

  let triggerContainer; // Reference for trigger element
  let scrollableParent; // Close when parent scrolls

  let transitionOptions = {}; // Changing transition direction


  // ========================================================
  // Functions

  export function toggleDropdown() {
    open ? closeDropdown() : openDropdown()
  }

  export function openDropdown() {
    calculatePosition();
    open = true;
    updateScrollableParent(triggerContainer);
    dispatch('open');
    // TODO: Set and trap focus
  }

  export function closeDropdown() {
    if (!open) return;
    open = false; // Close menu
    updateScrollableParent(triggerContainer); // Reset scrollableParent
    dispatch('close');
  }

  function handleBodyClick(e) {
    if (!open) return; // Already closed
    if (!triggerContainer.contains(e.srcElement)) {
      closeDropdown();
    }
  }

  function calculatePosition() {
    const container = triggerContainer.getBoundingClientRect();
    let position = { top: 0, right: 0, bottom: 0, left: 0 };
    let transform = "";

    if (direction == 'up') {
      position.bottom = window.innerHeight - container.top + distance; // Align above with distance
      if (over) position.bottom = window.innerHeight - container.bottom; // Align with bottom edge
    }

    if (direction == 'down') {
      position.top = container.bottom + distance; // Align below with distance
      if (over) position.top = container.top; // Align with top edge
    }

    if (direction == 'right') {
      position.left = container.right + distance; // Align to the right with distance
      if (over) position.left = container.left; // Align with left edge
    }

    if (direction == 'left') {
      position.right = document.body.clientWidth - container.left + distance; // Align to the left with distance
      if (over) position.right = document.body.clientWidth - container.right; // Align with right edge
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

    // Make dropdown's min-width equal to trigger's width
    if (matchWidth) style += `min-width: ${container.width}px;`;

    // Animate from the correct direction
    if (direction == 'up')    transitionOptions = { duration: duration, y: distance };
    if (direction == 'right') transitionOptions = { duration: duration, x: distance > 0 ? distance * -1 : distance * 2 };
    if (direction == 'down')  transitionOptions = { duration: duration, y: distance > 0 ? distance * -1 : distance * 2 };
    if (direction == 'left')  transitionOptions = { duration: duration, x: distance };
  }

  function updateScrollableParent(node) {
    if (open) {
      if (!node) return;

      // Node scrolls
      if (node.scrollHeight > node.clientHeight) {
        node.addEventListener('scroll', closeDropdown);
        scrollableParent = node; // Set scrollable parent

      // Try again with node's parent
      } else {
        return updateScrollableParent(node.parentNode);
      }

    } else {
      if (scrollableParent) {
        scrollableParent.removeEventListener('scroll', closeDropdown);
        scrollableParent = null;
      }
    }
  }

  function handleKeyUp(e) {
    if (e.key == 'Escape') closeDropdown();
  }

  function handleHover(e) {
    if (!hover) return;
    if (hoverTimer) window.clearTimeout(hoverTimer); // Reset timer
    if (e.type == 'mouseenter') {
      hoverTimer = window.setTimeout(() => {
        openDropdown();
      }, hoverDelay);
    }
    if (e.type == 'mouseleave') {
      hoverTimer = window.setTimeout(() => {
        closeDropdown();
      }, 100);
    }
  }

</script>

<svelte:window on:scroll={closeDropdown} on:resize={closeDropdown} on:click={handleBodyClick} />
<svelte:body on:keyup={handleKeyUp} />


<!-- Trigger -->
<div
  bind:this={triggerContainer}
  on:click={toggleDropdown}
  class={classTrigger}
  on:mouseenter={handleHover}
  on:mouseleave={handleHover}
>
  <slot name="trigger" {open} {openDropdown} {closeDropdown} />
</div>

<!-- Menu -->
{#if open}
  <div
    bind:this={menu}
    use:teleport
    on:click|stopPropagation
    on:mouseenter={handleHover}
    on:mouseleave={handleHover}
    transition:fly={transitionOptions}
    class="{classMenu} {classDirection} {className}"
    {style}
  >
    <slot />
  </div>
{/if}
