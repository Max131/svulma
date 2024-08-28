<script>
	import { setContext, createEventDispatcher } from 'svelte';
	import { writable } from 'svelte/store';
	import Icon from '$lib/Icon';

	/**
	 * Alignment of the tabs: can be `is-left`, `is-center`, `is-right`.
	 * @type {'is-center' | 'is-left' | 'is-right'}
	 * @default "is-left"
	 */
	export let align = '';

	/**
	 * Size of the tabs: can be `is-small`, `is-medium`, or `is-large`.
	 * @type {'is-small' | 'is-medium' | 'is-large'}
	 * @default "is-medium"
	 */
	export let size = '';

	/**
	 * Style of the tabs: can be `is-boxed` or `is-toggle`.
	 * @type {'is-boxed' | 'is-toggle'}
	 * @default ""
	 */
	export let style = '';

	/**
	 * If the toggle style should be rounded.
	 * @type {boolean}
	 * @default false
	 */
	export let roundedToggle = false;

	/**
	 * If the tabs should be full width.
	 * @type {boolean}
	 * @default false
	 */
	export let fullwidth = false;

	// Event dispatcher for custom events
	const dispatch = createEventDispatcher();

	/**
	 * Store that keeps track of the currently active tab.
	 * @type {import('svelte/store').Writable<{id: string, label: string}>}
	 */
	const currentTab = writable({});

	// Array to store the registered tabs
	let tabs = [];

	/**
	 * Function to register a tab. Adds the tab to the internal list of tabs.
	 * @param {{id: string, label: string, icon?: string | function(): SvelteComponent, iconProps?: Object, active?: boolean}} tab - The tab to register.
	 */
	const registerTab = (tab) => {
		if (!$currentTab.id) {
			$currentTab = { ...tab };
		}

		tabs = [...tabs, tab];
	};

	/**
	 * Function to set the active tab.
	 * @param {{id: string, label: string}} tab - The tab to set as active.
	 */
	const setActiveTab = ({ id, label }) => {
		// Update the current tab store with the new active tab
		$currentTab = { id, label };

		// Dispatch a 'change' event with the updated active tab
		dispatch('change', {
			activeTab: $currentTab
		});
	};

	// Provide the tab management functions and state to child components
	setContext('manageTabs', { registerTab, currentTab, setActiveTab });

	// Uncomment this block if you want to set a default active tab on mount
	/* onMount(() => {
        const existActiveTab = tabs.every((tab) => {
            return tab.active;
        });
        console.log({ existActiveTab });

        if (!existActiveTab) {
            setActiveTab({ id: tabs[0].id, label: tabs[0].label });
        }
    }); */
</script>

<div
	class="tabs {style} {align} {size}"
	class:is-toggle-rounded={roundedToggle}
	class:is-fullwidth={fullwidth}
	id={crypto.randomUUID()}
>
	<ul role="tablist">
		{#each tabs as { label, icon, iconProps, id } (id)}
			<li data-tab={id} class:is-active={$currentTab.id === id}>
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<a
					on:click|preventDefault={() => setActiveTab({ id, label })}
					role="tab"
					tabindex="0"
					{id}
					aria-selected={$currentTab.id === id}
				>
					{#if icon}
						<!-- Render the Icon component if `icon` is provided -->
						<Icon {icon} {iconProps} />
					{/if}
					<span>
						{label}
					</span>
				</a>
			</li>
		{/each}
	</ul>
</div>

<div class="tabs-content">
	<slot />
</div>
