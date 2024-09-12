<script>
  /**
   * The type attribute for the button element.
   * Must be either "button" or "submit".
   * Only applicable if the `as` prop is set to "button".
   * @type {"button" | "submit"}
   * @default "button"
   */
  export let type = "button";

  /**
   * Defines the appearance of the button.
   * Must be one of the following:
   * "is-white", "is-light", "is-dark", "is-black", "is-text",
   * "is-ghost", "is-primary", "is-link", "is-info", "is-success",
   * "is-warning", "is-danger".
   * @type {"is-white" | "is-light" | "is-dark" | "is-black" | "is-text" | "is-ghost" | "is-primary" | "is-link" | "is-info" | "is-success" | "is-warning" | "is-danger"}
   * @default ""
   */
  export let appearance = "";

  /**
   * Sets the size of the button.
   * Must be either "is-small", "is-medium", or "is-large".
   * @type {"is-small" | "is-medium" | "is-large"}
   * @default ""
   */
  export let size = "";

  /**
   * Makes the button responsive.
   * @type {boolean}
   * @default false
   */
  export let isResponsive = false;

  /**
   * Sets the button to be full-width.
   * @type {boolean}
   * @default false
   */
  export let isFullwidth = false;

  /**
   * Applies an outlined style to the button.
   * @type {boolean}
   * @default false
   */
  export let isOutlined = false;

  /**
   * Applies a light style to the button.
   * @type {boolean}
   * @default false
   */
  export let isLight = false;

  /**
   * Makes the button corners rounded.
   * @type {boolean}
   * @default false
   */
  export let isRounded = false;

  /**
   * Sets the button to an active state.
   * @type {boolean}
   * @default false
   */
  export let isActive = false;

  /**
   * Shows a loading indicator on the button.
   * @type {boolean}
   * @default false
   */
  export let isLoading = false;

  /**
   * Marks the button as selected.
   * @type {boolean}
   * @default false
   */
  export let isSelected = false;

  /**
   * The HTML element type to use for the button.
   * Must be either "button" or "link".
   * @type {"button" | "link"}
   * @default "button"
   */
  export let as = "button";

  /**
   * Internal computed property to determine the type of element.
   * Only applies if `as` is set to "button".
   * @private
   * @type {string | null}
   */
  $: typeElement = as === "button" ? type : null;
</script>

<svelte:element
  this={as}
  type={typeElement}
  class="button {appearance} {size}"
  class:is-responsive={isResponsive}
  class:is-fullwidth={isFullwidth}
  class:is-outlined={isOutlined}
  class:is-light={isLight}
  class:is-rounded={isRounded}
  class:is-active={isActive}
  class:is-loading={isLoading}
  class:is-selected={isSelected}
  {...$$restProps}
  role={as === "link" ? "link" : "button"}
  on:click
  on:focus
  on:blur
  on:mousedown
  on:mouseup
>
  <slot />
</svelte:element>
