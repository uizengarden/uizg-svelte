<script>
  import Highlight from "$lib/Highlight.svelte";

  import ToggleGroup from "$lib/ToggleGroup.svelte";
  import Button from "$lib/Button.svelte";
  import Checkbox from "$lib/Checkbox.svelte";
  import Collapsible from "$lib/Collapsible.svelte";


  let currentTab = 1;

</script>


<h2>ToggleGroup</h2>

<hr />

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <ToggleGroup let:current let:setCurrent>
      <p on:click={() => setCurrent(1)}>Item 1 {current == 1 ? '(selected)' : ''}</p>
      <p on:click={() => setCurrent(2)}>Item 2 {current == 2 ? '(selected)' : ''}</p>
      <p on:click={() => setCurrent(3)}>Item 3 {current == 3 ? '(selected)' : ''}</p>
    </ToggleGroup>
  </div>
</div>
<Highlight code={`
  <ToggleGroup let:current let:setCurrent>
    <p on:click={() => setCurrent(1)}>Item 1 {current == 1 ? '(selected)' : ''}</p>
    <p on:click={() => setCurrent(2)}>Item 2 {current == 2 ? '(selected)' : ''}</p>
    <p on:click={() => setCurrent(3)}>Item 3 {current == 3 ? '(selected)' : ''}</p>
  </ToggleGroup>
`} />

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <ToggleGroup current={2} let:current let:setCurrent>
      <Button value={1} selected={current == 1} on:click={setCurrent}>Tab 1</Button>
      <Button value={2} selected={current == 2} on:click={setCurrent}>Tab 2</Button>
      <Button value={3} selected={current == 3} on:click={setCurrent}>Tab 3</Button>

      <!-- Content logic here -->
      <p>Current Tab is {current}</p>
    </ToggleGroup>
  </div>
</div>
<Highlight code={`
  <ToggleGroup current={2} let:current let:setCurrent>
    <Button value={1} selected={current == 1} on:click={setCurrent}>Tab 1</Button>
    <Button value={2} selected={current == 2} on:click={setCurrent}>Tab 2</Button>
    <Button value={3} selected={current == 3} on:click={setCurrent}>Tab 3</Button>

    <!-- Content logic here -->
    <p>Current Tab is {current}</p>
  </ToggleGroup>
`} />

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <ToggleGroup bind:current={currentTab} let:current let:setCurrent>
      <Button value={1} selected={current == 1} on:click={setCurrent}>Tab 1</Button>
      <Button value={2} selected={current == 2} on:click={setCurrent}>Tab 2</Button>
      <Button value={3} selected={current == 3} on:click={setCurrent}>Tab 3</Button>
    </ToggleGroup>
    <p>Current Tab with external state is {currentTab}</p>
  </div>
</div>
<Highlight code={`
  <script>
    let currentTab = 1;
  </script>
  <ToggleGroup bind:current={currentTab} let:current let:setCurrent>
    <Button value={1} selected={current == 1} on:click={setCurrent}>Tab 1</Button>
    <Button value={2} selected={current == 2} on:click={setCurrent}>Tab 2</Button>
    <Button value={3} selected={current == 3} on:click={setCurrent}>Tab 3</Button>
  </ToggleGroup>
  <p>Current Tab is {currentTab}</p>
`} />

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <ToggleGroup current={'Item 2'} let:current let:setCurrent>
      {#each ['Item 1', 'Item 2', 'Item 3'] as option}
        <p><Checkbox type="radio" value={option} checked={current == option} on:check={setCurrent} label={option} /></p>
      {/each}
    </ToggleGroup>
  </div>
</div>
<Highlight code={`
  <ToggleGroup current={'Item 2'} let:current let:setCurrent>
    {#each ['Item 1', 'Item 2', 'Item 3'] as option}
      <p><Checkbox value={option} checked={current == option} on:check={setCurrent} label={option} /></p>
    {/each}
  </ToggleGroup>
`} />

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <ToggleGroup current={1} let:current let:setCurrent>
      <Collapsible value={1} collapsed={current != 1} on:expand={setCurrent} title="Item 1">Hello World!</Collapsible>
      <Collapsible value={2} collapsed={current != 2} on:expand={setCurrent} title="Item 2">Hello World!</Collapsible>
      <Collapsible value={3} collapsed={current != 3} on:expand={setCurrent} title="Item 3">Hello World!</Collapsible>
    </ToggleGroup>
  </div>
</div>
<Highlight code={`
  <ToggleGroup current={1} let:current let:setCurrent>
    <Collapsible value={1} collapsed={current != 1} on:expand={setCurrent} title="Item 1">...</Collapsible>
    <Collapsible value={2} collapsed={current != 2} on:expand={setCurrent} title="Item 2">...</Collapsible>
    <Collapsible value={3} collapsed={current != 3} on:expand={setCurrent} title="Item 3">...</Collapsible>
  </ToggleGroup>
`} />
