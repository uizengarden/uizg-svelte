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
<path d="M15 3h4a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2h-4">
</path>
<polyline points="10 17 15 12 10 7">
</polyline>
<line x1="15" y1="12" x2="3" y2="12">
</line>
</svg>
