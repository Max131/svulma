<script>
  /**
   * Sets the size of the buttons.
   * Must be either "are-small", "are-medium", or "are-large".
   * @type {"are-small" | "are-medium" | "are-large"}
   * @default ""
   */
  export let size = "are-medium";
</script>

<div class="buttons {size}">
  <slot />
</div>
