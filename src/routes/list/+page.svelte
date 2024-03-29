<script>
  import Highlight from "$lib/Highlight.svelte";

  import List from "$lib/List.svelte";
  import ListItem from "$lib/ListItem.svelte";

  import Label from "$lib/Label.svelte";
  import Avatar from "$lib/Avatar.svelte";
  import Button from "$lib/Button.svelte";
  import Dropdown from "$lib/Dropdown.svelte";
  import ToggleGroup from "$lib/ToggleGroup.svelte";
  import ScrollArea from "$lib/ScrollArea.svelte";
  import Input from "$lib/Input.svelte";

  import IconChevronRight from "$lib/icons/IconChevronRight.svelte";
  import IconBold from "$lib/icons/IconBold.svelte";
  import IconItalic from "$lib/icons/IconItalic.svelte";
  import IconAlignLeft from "$lib/icons/IconAlignLeft.svelte";
  import IconAlignCenter from "$lib/icons/IconAlignCenter.svelte";
  import IconAlignRight from "$lib/icons/IconAlignRight.svelte";
  import IconCheck from "$lib/icons/IconCheck.svelte";
  import IconEmpty from "$lib/icons/IconEmpty.svelte";
  import IconSettings from "$lib/icons/IconSettings.svelte";
  import IconLogOut from "$lib/icons/IconLogOut.svelte";
  import IconExternalLink from "$lib/icons/IconExternalLink.svelte";
  import IconSmile from "$lib/icons/IconSmile.svelte";
  import IconPaperclip from "$lib/icons/IconPaperclip.svelte";
  import IconSend from "$lib/icons/IconSend.svelte";
  import IconSearch from "$lib/icons/IconSearch.svelte";
  import IconFilePlus from "$lib/icons/IconFilePlus.svelte";

</script>

<h2>List</h2>

<hr />

<!-- ------------------------------ -->
<!-- LIST -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Button>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST INSET -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List inset>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Dropdown direction="right">
        <Button slot="trigger" iconRight={IconChevronRight}>More</Button>
        <List>
          <Button>List item A</Button>
          <Button>List item B</Button>
        </List>
      </Dropdown>
    </List>
  </div>
</div>
<Highlight code={`
  <List inset>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST DIVIDERS -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List dividers>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Button>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List dividers>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- PROGRAMATIC  -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List options={[
      { heading: "Links" },
      { text: "Link 1", href: "#1", iconRight: IconExternalLink },
      { text: "Link 2", href: "#2", iconRight: IconExternalLink },
      { divider: true },
      { text: "Button", action: () => alert('clicked button'), class: "btn btn--primary-translucent" },
    ]} />
  </div>
</div>
<Highlight code={`
  <List options={[
    { heading: "Links" },
    { text: "Link 1", href: "#1", iconRight: IconChevronRight },
    { text: "Link 2", href: "#2", iconRight: IconChevronRight },
    { divider: true },
    { text: "Button", action: handleClick, class: "btn btn--primary-translucent" },
  ]} />
`} />

<!-- ------------------------------ -->
<!-- LIST ITEMS -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List style="width: 320px;">
      <ListItem href="#profile">
        <Avatar slot="icon" initials="UN" />
        <p>User Name</p>
        <small>@username</small>
      </ListItem>
      <ListItem divider />
      <ListItem icon={IconSettings} href="#settings">Settings</ListItem>
      <ListItem icon={IconLogOut} action={() => alert('log out')}>Log out</ListItem>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <ListItem href="#profile">
      <Avatar slot="icon" initials="UN" />
      <p>User Name</p>
      <small>@username</small>
    </ListItem>
    <ListItem divider />
    <ListItem icon={IconSettings} href="#settings">Settings</ListItem>
    <ListItem icon={IconLogOut} action={() => alert('log out')}>Log out</ListItem>
  </List>
`} />


<!-- ------------------------------ -->
<!-- LIST ROW -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List row>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Button>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List row>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST ROW DIVIDER -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List row dividers>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Button>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List row dividers>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />


<!-- ------------------------------ -->
<!-- LIST ROW ADVANCED -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List row inset>
      <Button toggle classToggled="btn--secondary" icon={IconBold} size="sm" />
      <Button toggle classToggled="btn--secondary" icon={IconItalic} size="sm" />
      <ListItem divider heading="Align" />
      <ToggleGroup current="Left" let:current let:setCurrent>
        <List row type="secondary">
          <Button size="sm" on:click={setCurrent} value="Left" icon={IconAlignLeft} type={current == "Left" ? 'secondary' : 'transparent'} />
          <Button size="sm" on:click={setCurrent} value="Center" icon={IconAlignCenter} type={current == "Center" ? 'secondary' : 'transparent'} />
          <Button size="sm" on:click={setCurrent} value="Right" icon={IconAlignRight} type={current == "Right" ? 'secondary' : 'transparent'} />
        </List>
      </ToggleGroup>
    </List>
  </div>
</div>
<Highlight code={`
  <List row inset>
    <Button toggle classToggled="btn--secondary" icon={IconBold} size="sm" />
    <Button toggle classToggled="btn--secondary" icon={IconItalic} size="sm" />
    <ListItem divider heading="Align" />
    <ToggleGroup current="Left" let:current let:setCurrent>
      <List row type="secondary">
        <Button size="sm" on:click={setCurrent} value="Left" icon={IconAlignLeft} type={current == "Left" ? 'secondary' : 'transparent'} />
        <Button size="sm" on:click={setCurrent} value="Center" icon={IconAlignCenter} type={current == "Center" ? 'secondary' : 'transparent'} />
        <Button size="sm" on:click={setCurrent} value="Right" icon={IconAlignRight} type={current == "Right" ? 'secondary' : 'transparent'} />
      </List>
    </ToggleGroup>
  </List>
`} />


<!-- ------------------------------ -->
<!-- LIST FOCUSED ITEM -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List>
      <Button>List item 1</Button>
      <Button iconRight={IconCheck} focused>List item 2</Button>
      <Button>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <Button>List item 1</Button>
    <Button iconRight={IconCheck} focused>List item 2</Button>
    <Button>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST SELECTED ITEM -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List>
      <Button icon={IconEmpty}>List item 1</Button>
      <Button icon={IconCheck} selected>List item 2</Button>
      <Button icon={IconEmpty}>List item 3</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <Button icon={IconEmpty}>List item 1</Button>
    <Button icon={IconCheck} selected>List item 2</Button>
    <Button icon={IconEmpty}>List item 3</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST ITEM DIVIDER AND HEADING -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List>
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <ListItem divider heading="format" />
      <Button icon={IconBold}>List item 3</Button>
      <Button icon={IconItalic}>List item 4</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <ListItem divider heading="format" />
    <Button icon={IconBold}>List item 3</Button>
    <Button icon={IconItalic}>List item 4</Button>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST SUBMENU -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List heading="with dropdown">
      <Button>List item 1</Button>
      <Button>List item 2</Button>
      <Dropdown direction="right">
        <Button slot="trigger" iconRight={IconChevronRight}>More</Button>
        <List>
          <Button>List item A</Button>
          <Button>List item B</Button>
        </List>
      </Dropdown>
    </List>
  </div>
</div>
<Highlight code={`
  <List heading="with dropdown">
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <Dropdown direction="right">
      <Button slot="trigger" iconRight={IconChevronRight}>More</Button>
      <List>
        <Button>List item A</Button>
        <Button>List item B</Button>
      </List>
    </Dropdown>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST SUBMENU -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List dividers>
      <List row>
        <ListItem flex text="Files" />
        <Button icon={IconFilePlus} type="primary-transparent" />
      </List>
      <Input placeholder="Search" icon={IconSearch} />
      <Button>List item 1</Button>
      <Button>List item 2</Button>
    </List>
  </div>
</div>
<Highlight code={`
  <List heading="with input" dividers>
    <Input placeholder="Search" icon={IconSearch} />
    <Button>List item 1</Button>
    <Button>List item 2</Button>
    <List inset row>
      <Button size="sm" type="primary-translucent">New file</Button>
      <Button size="sm" type="transparent">Cancel</Button>
    </List>
  </List>
`} />


<!-- ------------------------------ -->
<!-- LIST ITEM DIVIDERS -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List dividers>
      <ListItem>
        <p><strong>Title</strong></p>
        <p>Paragraph</p>
      </ListItem>
      <ListItem>
        <p><strong>Title</strong></p>
        <p>Paragraph</p>
      </ListItem>
      <ListItem>
        <p><strong>Title</strong></p>
        <p>Paragraph</p>
      </ListItem>
    </List>
  </div>
</div>
<Highlight code={`
  <List dividers>
    <ListItem>
      <p><strong>Title</strong></p>
      <p>Paragraph</p>
    </ListItem>
    <ListItem>
      <p><strong>Title</strong></p>
      <p>Paragraph</p>
    </ListItem>
    <ListItem>
      <p><strong>Title</strong></p>
      <p>Paragraph</p>
    </ListItem>
  </List>
`} />

<!-- ------------------------------ -->
<!-- LIST ITEM DIVIDERS -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List dividers>
      <ListItem>
        <Avatar slot="icon" />
        <p><strong>Title</strong></p>
        <p>Paragraph</p>
      </ListItem>
      <ListItem text="Name" subtext="@username">
        <Avatar slot="icon" />
      </ListItem>
    </List>
  </div>
</div>
<Highlight code={`
  <List dividers>
    <ListItem>
      <Avatar slot="icon" />
      <p><strong>Title</strong></p>
      <p>Paragraph</p>
    </ListItem>
    <ListItem text="Name" subtext="@username">
      <Avatar slot="icon" />
    </ListItem>
  </List>
`} />

<!-- ------------------------------ -->
<!-- SCROLLING LIST -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List dividers>
      <ScrollArea style="height: 180px;">
        {#each Array(10) as _, i}
          <ListItem>List item {i+1}</ListItem>
        {/each}
      </ScrollArea>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <ScrollArea overlap style="height: 200px;">
      {#each Array(10) as _, i}
        <ListItem>List item {i+1}</ListItem>
      {/each}
    </ScrollArea>
  </List>
`} />

<!-- ------------------------------ -->
<!-- SCROLLING LIST WITH BUTTONS -->
<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List>
      <ScrollArea style="height: 200px;">
        <List dividers>
          {#each Array(10) as _, i}
            <Button>List item {i+1}</Button>
          {/each}
        </List>
      </ScrollArea>
    </List>
  </div>
</div>
<Highlight code={`
  <List>
    <ScrollArea overlap style="height: 200px;">
      <List dividers>
        {#each Array(10) as _, i}
          <Button>List item {i+1}</Button>
        {/each}
      </List>
    </ScrollArea>
  </List>
`} />


<!-- ------------------------------ -->
<!-- Sample -->

<div class="uizg-preview">
  <div class="uizg-preview__element">
    <List row inset>
      <Avatar image="https://pbs.twimg.com/profile_images/1547348110216658950/I_8fmKjU_400x400.jpg" />
      <Input placeholder="Say something nice…" />
      <Button type="transparent" icon={IconSmile} />
      <Button type="transparent" icon={IconPaperclip} />
      <Button type="primary-transparent" icon={IconSend} />
    </List>
  </div>
</div>
<Highlight code={`
  <List row inset>
    <Avatar image="https://pbs.twimg.com/profile_images/1547348110216658950/I_8fmKjU_400x400.jpg" />
    <Input placeholder="Say something nice…" />
    <Button type="transparent" icon={IconSmile} />
    <Button type="transparent" icon={IconPaperclip} />
    <Button type="primary-transparent" icon={IconSend} />
  </List>
`} />
