<script>
  export let size = null;

  export let classBase = "icon";
  export let classSize = size ? `${classBase}--${size}` : "";

  let className = "";
  export { className as class }; // Pass extra classes

  export let style = "";
</script>

<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
  stroke-width="2"
  stroke-linecap="round"
  stroke-linejoin="round"
  class="{classBase} {classSize} {className}"
  {style}
>
  <slot />
</svg>
