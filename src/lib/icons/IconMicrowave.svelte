<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <rect x="2" y="4" width="20" height="15" rx="2" />
  <rect x="6" y="8" width="8" height="7" rx="1" />
  <path d="M18 8v7" />
  <path d="M6 19v2" />
  <path d="M18 19v2" />
</Icon>
