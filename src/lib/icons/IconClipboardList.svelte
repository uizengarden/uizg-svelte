<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <rect x="8" y="2" width="8" height="4" rx="1" ry="1" />
  <path
    d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"
  />
  <path d="M12 11h4" />
  <path d="M12 16h4" />
  <path d="M8 11h.01" />
  <path d="M8 16h.01" />
</Icon>
