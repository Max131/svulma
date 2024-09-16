<script>
  // TODO: filter props/add rest props
  import { getContext } from "svelte";
  import Icon from "$lib/Icon";

  /**
   * Input DOM reference.
   * @type {HTMLInputElement | null}
   */
  let input = null;

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
   * The value of the input field. Used for two-way binding with the input.
   * @type {string}
   * @default ""
   */
  export let value = "";

  /**
   * The class name for the left icon of the input field.
   * Usually includes an icon style class like "fas fa-user".
   * @type {string}
   * @default ""
   */
  export let icon = "";

  /**
   * The class name for the right icon of the input field.
   * Usually includes an icon style class like "fas fa-search".
   * @type {string}
   * @default ""
   */
  export let iconRight = "";

  /**
   * Determines whether a reveal button is displayed to show or hide the password in input fields of type "password".
   * @type {boolean}
   * @default false
   */
  export let revealButton = false;

  /**
   * The aria-label for the reveal button. This is used for accessibility purposes.
   * @type {string}
   * @default "Show/Hide Password"
   */
  export let revealButtonAriaLabel = "Show/Hide Password";

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

  /**
   * Extracts the color part from the type for dynamic icon color styling.
   * The color is derived from the last part of the `type` string after a dash (`-`).
   * @type {string}
   */
  $: iconColor = type.split("-").at(-1);

  /**
   * Represents the current input type, which can be any html standar input type.
   * Changes based on the reveal button state to toggle password visibility.
   * @type {string}
   * @default "text"
   */
  export let typeInput = "text";

  /**
   * Toggles the input field between "text" and "password" types to show or hide the password.
   * This function is triggered by clicking the reveal button.
   */
  const toggleShowPassword = () => {
    typeInput = typeInput === "text" ? "password" : "text";
    input.focus();
  };

  /**
   * Action to dynamically update the type attribute of an input element.
   * This is a Svelte action that is applied to the input field.
   * @param {HTMLInputElement} node - The input element.
   * @param {string} nodeType - The type of the input element (e.g., "text", "password").
   * @returns {Object} - An object containing an update function to handle type changes.
   */
  const inputType = (node, nodeType) => {
    node.type = nodeType;

    return {
      update(newType) {
        node.type = newType;
      }
    };
  };
</script>

<div
  class="control"
  class:is-loading={isLoading}
  class:is-expanded={expanded}
  class:has-icons-left={icon}
  class:has-icons-right={iconRight || revealButton}
>
  {#if icon}
    <span class="icon is-left has-text-{iconColor}">
      <Icon {icon} />
    </span>
  {/if}
  <input
    bind:this={input}
    use:inputType={typeInput}
    class="input {type} {size} {$$props.class}"
    bind:value
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
  {#if iconRight && !revealButton}
    <span class="icon is-right has-text-{iconColor}">
      <Icon icon={iconRight} />
    </span>
  {/if}
  {#if revealButton && (typeInput === "password" || typeInput === "text")}
    <button
      class="icon is-right has-text-danger"
      aria-label={revealButtonAriaLabel}
      on:click={toggleShowPassword}
    >
      <i class={typeInput === "password" ? "bx bx-show" : "bx bx-hide"} />
    </button>
  {/if}
</div>

<style>
  .control {
    overflow: hidden;
  }

  button.icon.is-right {
    pointer-events: auto;
    cursor: pointer;
  }
</style>
