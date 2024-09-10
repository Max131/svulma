<script>
  import { getContext } from "svelte";

  /**
   * Textarea DOM reference.
   * @type {HTMLInputElement | null}
   */
  let textarea = null;

  /**
   * Determines if the input should be expanded to fill its container.
   * When true, the input will have a `is-expanded` class.
   * @type {boolean}
   * @default false
   */
  export let expanded = false;

  /**
   * The type of input field, which affects its styling and behavior.
   * This is used to dynamically apply Bulma CSS classes like "is-primary" or "is-danger".
   * @type {string}
   * @default ""
   */
  export let type = "";

  /**
   * The size of the input field. Possible values include "is-small", "is-medium", "is-large".
   * This is used to dynamically apply Bulma CSS classes.
   * @type {string}
   * @default ""
   */
  export let size = "";

  /**
   * Add a loader icon wihtin the input control
   * @type {boolean}
   * @default false
   */
  export let isLoading = false;

  /**
   * The size of the input field. Possible values include "is-small", "is-medium", "is-large".
   * This is used to dynamically apply Bulma CSS classes.
   * @type {string}
   * @default ""
   */
  export let spinerSize = "";

  /**
   * The value of the input field. Used for two-way binding with the input.
   * @type {string}
   * @default ""
   */
  export let value = "";

  /**
   * Set fixed textearea to no resize it.
   * @type {boolean}
   * @default false
   */
  export let isFixedSize = false;

  /**
   * A reactive variable that gets context variables related to help messages from a parent component.
   * If the context is not provided, helpType and helpID will default to `null`.
   * @type {Object}
   * @property {string|null} helpType - The type of help message.
   * @property {string|null} helpID - The ID associated with the help message.
   */
  const { helpType = null, helpID = null } = getContext("help") ?? {};

  /**
   * Reactive statement to synchronize the input type with the helpType from context.
   * If helpType is available, it assigns the type to `$helpType`.
   * @type {string}
   */
  $: if (helpType) {
    $helpType = type;
  }
</script>

<div class="control {spinerSize}" class:is-expanded={expanded} class:is-loading={isLoading}>
  <textarea
    class="textarea {type} {size} {$$props.class}"
    class:has-fixed-size={isFixedSize}
    bind:value
    bind:this={textarea}
    aria-describedby={helpID}
    {...$$restProps}
    on:input
    on:change
    on:click
    on:focus
    on:blur
    on:keypress
    on:keydown
    on:keyup
  />
</div>

<style>
  .control {
    overflow: hidden;
  }
</style>
