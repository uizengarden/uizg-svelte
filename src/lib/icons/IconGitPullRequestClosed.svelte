<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <circle cx="18" cy="18" r="3" />
  <circle cx="6" cy="6" r="3" />
  <path d="M18 11.5V15" />
  <path d="m21 3-6 6" />
  <path d="m21 9-6-6" />
  <line x1="6" y1="9" x2="6" y2="21" />
</Icon>
