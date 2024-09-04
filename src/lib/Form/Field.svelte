<script context="module">
  /**
   * A unique identifier for help elements in the component.
   * @type {number}
   */
  let helpID = 0;
</script>

<script>
  import { writable } from "svelte/store";
  import { setContext } from "svelte";

  /**
   * The label text for the field.
   * @type {string}
   */
  export let label = "";

  /**
   * The 'for' attribute value for the label element, linking it to an input.
   * @type {string}
   */
  export let labelFor = "";

  /**
   * Determines if the field should have addons.
   * @type {boolean}
   */
  export let hasAddons;

  /**
   * Aligns the addons to the center.
   * @type {boolean}
   */
  export let hasAddonsCenter;

  /**
   * Aligns the addons to the right.
   * @type {boolean}
   */
  export let hasAddonsRight;

  /**
   * Determines if the field should be grouped.
   * @type {boolean}
   */
  export let isGrouped;

  /**
   * Aligns the grouped field to the center.
   * @type {boolean}
   */
  export let isGroupedCenter;

  /**
   * Aligns the grouped field to the right.
   * @type {boolean}
   */
  export let isGroupedRight;

  /**
   * Allows the field to have multiple lines when grouped.
   * @type {boolean}
   */
  export let isGroupedMultiline;

  /**
   * The help message text displayed below the field.
   * @type {string}
   */
  export let message = "";

  /**
   * Writable store that defines the type of help message.
   * @type {import("svelte/store").Writable<string>}
   */
  const helpType = writable("");

  // Sets the context for the help type and unique ID, to be used by children components.
  setContext("help", { helpType, helpID });
</script>

<div
  class="field"
  class:has-addons={hasAddons}
  class:has-addons-centered={hasAddonsCenter}
  class:has-addons-right={hasAddonsRight}
  class:is-grouped={isGrouped}
  class:is-grouped-centered={isGroupedCenter}
  class:is-grouped-right={isGroupedRight}
  class:is-grouped-multiline={isGroupedMultiline}
>
  {#if label}
    <label class="label {$helpType}" for={labelFor}>{label}</label>
  {/if}
  <slot />
  {#if message}
    <p class="help {$helpType}" id={`help-${helpID++}`}>{message}</p>
  {/if}
</div>
