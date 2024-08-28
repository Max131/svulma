<script>
	/** Icon string name or component */
	export let icon = "";

	/** Icon size */
	export let size = "";

	/** Icon props */
	export let iconProps = {};
</script>

<!--
@component

# Icon comopnent that supports iconfonts and icon components

## Props

- icon: icon string name for fonticon or a component for icon component
- iconProps: an object with properties for the icon font/component

```
// Fontawesome
<Icon icon="fas fa-user" />

// Boxicons
<Icon icon="bx bxs-bell bx-tada" />

// Lucide svelte icons
import {Skull} from "lucide-svelte"
<Icon icon={Skull} iconProps={{label: "Skull guy", color: "goldenrod", size: 36}} />


// Other icon fonts (no tested yet)
<Icon iconProps={{"data-icon": "user"}} />

```
-->

<span class="icon" class:is-size={size}>
	{#if typeof icon === "string"}
		<i class={icon} {...iconProps} role="img" />
	{/if}

	{#if typeof icon === "function"}
		<svelte:component this={icon} {...iconProps} />
	{/if}
</span>
