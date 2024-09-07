<script>
  /** Icon string name or component */
  export let icon = "";

  /** Icon size */
  export let size = "";
</script>

<!--
@component

# Icon comopnent that supports iconfonts and icon components

## Props

- icon: icon can be either a string, component function or an object
If is an object, it must be in the form: 
{
  icon: string || component function,
  //icon props
  "data-label": "Icon label"
  color: "blueviolet"
  ...
}

```
// Fontawesome
<Icon icon="fas fa-user" />

// Boxicons
<Icon icon="bx bxs-bell bx-tada" />

// Lucide svelte icons
import {Skull} from "lucide-svelte"
<Icon icon={Skull} />

// Component icon with props
<Icon icon= {{
  icon: Skull,
  color: "goldenrod",
  size: 36
}} />



```
-->

<span class="icon {size}">
  {#if typeof icon === "string"}
    <i class={icon} role="img" />
  {/if}

  {#if typeof icon === "function"}
    <svelte:component this={icon} role="img" />
  {/if}

  {#if typeof icon === "object"}
    {@const { icon, ...props } = icon}
    {#if typeof icon === "string"}
      <i class={icon} {...props} role="img" />
    {/if}

    {#if typeof icon === "function"}
      <svelte:component this={icon} {...props} role="img" />
    {/if}
  {/if}
</span>
