<script>

  export let size = null;

  export let classBase = "icon";
  export let classSize = size ? `${classBase}--${size}` : '';

  let className = "";
  export { className as class }; // Pass extra classes

</script>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
  fill="none" stroke="currentColor"
  stroke-width="2" stroke-linecap="round"
  stroke-linejoin="round"
  class="{classBase} {classSize} {className}"
>
<rect x="3" y="4" width="18" height="18" rx="2" ry="2">
</rect>
<line x1="16" y1="2" x2="16" y2="6">
</line>
<line x1="8" y1="2" x2="8" y2="6">
</line>
<line x1="3" y1="10" x2="21" y2="10">
</line>
</svg>
