<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <line x1="3" y1="6" x2="21" y2="6" />
  <path d="M3 12h15a3 3 0 1 1 0 6h-4" />
  <polyline points="16 16 14 18 16 20" />
  <line x1="3" y1="18" x2="10" y2="18" />
</Icon>
