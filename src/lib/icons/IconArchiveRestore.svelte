<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <rect x="2" y="4" width="20" height="5" rx="2" />
  <path d="M12 13v7" />
  <path d="m9 16 3-3 3 3" />
  <path d="M4 9v9a2 2 0 0 0 2 2h2" />
  <path d="M20 9v9a2 2 0 0 1-2 2h-2" />
</Icon>
