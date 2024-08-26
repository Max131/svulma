<script>
	import { getContext } from 'svelte';

	/**
	 * The label displayed on the tab.
	 * @type {string}
	 * @default "Tab"
	 */
	export let label = 'Tab';

	/**
	 * Whether the tab is currently active.
	 * @type {boolean}
	 * @default false
	 */
	export let active = false;

	/**
	 * The icon displayed on the tab, which can be a string (e.g., an icon name) or a function that returns a Svelte component.
	 * @type {string | function(): SvelteComponent}
	 * @default ""
	 */
	export let icon = '';

	/**
	 * Properties for the icon component, if any.
	 * @type {Object}
	 * @default {}
	 */
	export let iconProps = {};

	const { registerTab, currentTab, setActiveTab } = getContext('manageTabs');
	const id = crypto.randomUUID();

	registerTab({ id, label, icon, iconProps, active });

	// $: if (active) {
	// 	$currentTab.id = id;
	// 	$currentTab.label = label;
	// }

	$: active && setActiveTab({ id, label });
</script>

<div class="tab-panel" {id} class:is-hidden={$currentTab.id !== id}>
	<slot />
</div>
