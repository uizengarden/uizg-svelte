<script>

  export let size = null;

  export let classBase = "icon";
  export let classSize = size ? `${classBase}--${size}` : '';

  let className = "";
  export { className as class }; // Pass extra classes

</script>
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
  fill="currentColor" stroke="none"
  class="{classBase} {classSize} {className}"
>
  <circle cx="12" cy="12" r="8" />
</svg>
