<script>
  import Icon from "$lib/icons/_IconWrapper.svelte";
</script>

<Icon {...$$props}>
  <rect x="4" y="5" width="6" height="14" rx="2" />
  <rect x="14" y="7" width="6" height="10" rx="2" />
  <path d="M17 22v-5" />
  <path d="M17 7V2" />
  <path d="M7 22v-3" />
  <path d="M7 5V2" />
</Icon>
