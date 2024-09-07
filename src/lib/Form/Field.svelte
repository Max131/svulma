<script context="module">
  /**
   * A unique identifier for help elements in the component.
   * This is incremented each time a new help message is rendered.
   * @type {number}
   */
  let helpID = 0;
</script>

<script>
  import { writable } from "svelte/store";
  import { setContext } from "svelte";

  /**
   * The label text for the field.
   * This text is displayed as a label for the field.
   * @type {string}
   */
  export let label = "";

  /**
   * The 'for' attribute value for the label element, linking it to an input.
   * Specifies the id of the input element the label is associated with.
   * @type {string}
   */
  export let labelFor = "";

  /**
   * Determines if the field should have addons.
   * If true, the field will have additional elements or buttons aligned next to it.
   * @type {boolean}
   */
  export let hasAddons = false;

  /**
   * Aligns the addons to the center.
   * If true, the addons will be centered horizontally.
   * @type {boolean}
   */
  export let hasAddonsCenter = false;

  /**
   * Aligns the addons to the right.
   * If true, the addons will be aligned to the right.
   * @type {boolean}
   */
  export let hasAddonsRight = false;

  /**
   * Determines if the field should be grouped.
   * If true, the field will be grouped with other fields.
   * @type {boolean}
   */
  export let isGrouped = false;

  /**
   * Aligns the grouped field to the center.
   * If true, the grouped field will be centered horizontally.
   * @type {boolean}
   */
  export let isGroupedCenter = false;

  /**
   * Aligns the grouped field to the right.
   * If true, the grouped field will be aligned to the right.
   * @type {boolean}
   */
  export let isGroupedRight = false;

  /**
   * Allows the field to have multiple lines when grouped.
   * If true, grouped fields will be displayed in multiple lines.
   * @type {boolean}
   */
  export let isGroupedMultiline = false;

  /**
   * The help message text displayed below the field.
   * This message provides additional information or context for the field.
   * @type {string}
   */
  export let message = "";

  /**
   * Reference to the field element.
   * Used for binding the element to the component.
   * @type {HTMLElement | null}
   */
  let fieldRef = null;

  /**
   * Writable store that defines the type of help message.
   * This store is used to manage the class or type of the help message (e.g., success, error).
   * @type {import("svelte/store").Writable<string>}
   */
  const helpType = writable("");

  /**
   * Sets the context for the help type and unique ID, to be used by children components.
   * Provides the help type, unique ID, and addon state to the child components.
   */
  setContext("help", { helpType, helpID, inAddonField: hasAddons });

  /**
   * Checks for buttons inside the field and wraps them in a 'control' element if needed.
   * This function ensures that buttons are properly wrapped for styling purposes.
   * @param {HTMLElement} node - The DOM element to check for buttons.
   */
  const checkButtons = (node) => {
    const buttons = node.querySelectorAll(".button");

    buttons.forEach((button) => {
      if (!button.closest(".control")) {
        const control = document.createElement("DIV");
        control.classList.add("control");

        button.insertAdjacentElement("beforebegin", control);
        control.appendChild(button);
      }
    });
  };
</script>

<div
  class="field"
  use:checkButtons
  bind:this={fieldRef}
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
