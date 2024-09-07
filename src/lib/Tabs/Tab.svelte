<script context="module">
  /**
   * Set the tab id number
   * @type {number}
   */
  let tabID = 0;
</script>

<script>
  import { getContext } from "svelte";

  /**
   * The label displayed on the tab.
   * @type {string}
   * @default "Tab"
   */
  export let label = "Tab";

  /**
   * Whether the tab is currently active.
   * @type {boolean}
   * @default false
   */
  export let active = false;

  /**
   * The icon displayed on the tab, which can be a string (e.g., an icon name) a function that returns a Svelte component or an Object wiht an icon and props.
   * @type {string | function(): SvelteComponent | object}
   * @default ""
   */
  export let icon = "";

  const { registerTab, currentTab, setActiveTab } = getContext("manageTabs");
  const id = `tab-${tabID++}`;

  registerTab({ id, label, icon, active });

  // $: if (active) {
  // 	$currentTab.id = id;
  // 	$currentTab.label = label;
  // }

  $: active && setActiveTab({ id, label });
</script>

{#if $currentTab.id === id}
  <div class="tab-panel" role="tabpanel" aria-labelledby={id} tabindex="0">
    <slot />
  </div>
{/if}
