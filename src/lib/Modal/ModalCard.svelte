<script>
  /**
   * @component
   * @slot {HTMLElement} default - Main component slot
   * @slot {HTMLElement} modalfooter - Footer component slot
   */

  import { fade } from "svelte/transition";

  /**
   * Indicates whether the modal is active or not.
   * @type {boolean}
   * @default false
   */
  export let active = false;

  /**
   * ModalCard Title.
   * @type {string}
   * @default ""
   */
  export let title = "";

  /**
   * Aria label for the close button of the modal.
   * @type {string}
   * @default "Close Modal"
   */
  export let ariaLabelClose = "Close Modal";

  /**
   * Aria label for the modal.
   * @type {string}
   * @default "Modal Window"
   */
  export let ariaLabel = "Modal Window";

  /**
   * Duration of the transition in milliseconds.
   * @type {number}
   * @default 200
   */
  export let transitionDuration = 200;

  /**
   * Hides the close button if set to `true`.
   * @type {boolean}
   * @default false
   */
  export let hideCloseButton = false;

  /**
   * Disables closing the modal using the "Escape" key if set to `true`.
   * @type {boolean}
   * @default false
   */
  export let disableEscKey = false;

  /**
   * Disables closing the modal when clicking on the background if set to `true`.
   * @type {boolean}
   * @default false
   */
  export let disableBackgroundClick = false;

  /**
   * Closes the modal by setting `active` to `false`.
   * @private
   */
  const close = () => (active = false);

  /**
   * Closes the modal when the "Escape" key is pressed, unless `disableEscKey` is enabled.
   * @param {KeyboardEvent} event - The keyboard event.
   * @private
   */
  const closeKey = ({ code }) => {
    if (disableEscKey) return;

    code === "Escape" && active && close();
  };

  let noHasTitle = !title;
</script>

<svelte:document on:keyup={closeKey} />
{#if active}
  <div
    class="modal is-active"
    role="dialog"
    aria-modal="true"
    aria-label={ariaLabel}
    transition:fade={{ duration: transitionDuration }}
  >
    <!-- svelte-ignore a11y-click-events-have-key-events a11y-no-static-element-interactions -->
    <div
      class="modal-background"
      aria-label={ariaLabelClose}
      on:click={() => !disableBackgroundClick && close()}
    />
    <article class="modal-card px-4">
      <header
        class="modal-card-head"
        class:p-3={!title}
        class:is-shadowless={noHasTitle}
        class:modal-card-head-background-body={noHasTitle}
      >
        <p class="modal-card-title">{title}</p>
        {#if !hideCloseButton}
          <button class="delete" aria-label={ariaLabelClose} type="button" on:click={close} />
        {/if}
      </header>
      <section class="modal-card-body" class:modal-card-bottom-radius={!$$slots.modalfooter}>
        <slot />
      </section>
      {#if $$slots.modalfooter}
        <footer class="modal-card-foot">
          <slot name="modalfooter" />
        </footer>
      {/if}
    </article>
  </div>
{/if}

<style>
  .modal-card-bottom-radius {
    border-radius: 0 0 var(--bulma-modal-card-foot-radius) var(--bulma-modal-card-foot-radius);
  }
  .modal-card-head-background-body {
    background-color: var(--bulma-modal-card-body-background-color);
  }
</style>
