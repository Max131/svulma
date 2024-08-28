<script>
	import { fade } from 'svelte/transition';

	/**
	 * Indicates whether the modal is active or not.
	 * @type {boolean}
	 * @default false
	 */
	export let active = false;

	/**
	 * Aria label for the close button of the modal.
	 * @type {string}
	 * @default "Close Modal"
	 */
	export let ariaLabelClose = 'Close Modal';

	/**
	 * Aria label for the modal.
	 * @type {string}
	 * @default "Modal Window"
	 */
	export let ariaLabel = 'Modal Window';

	/**
	 * An ID for the modal
	 * @type {string}
	 * @default ""
	 */
	export let modalID = '';

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

		code === 'Escape' && active && close();
	};
</script>

<svelte:document on:keyup={closeKey} />
{#if active}
	<div
		class="modal is-active"
		id={modalID}
		role="dialog"
		aria-modal="true"
		aria-label={ariaLabel}
		transition:fade={{ duration: transitionDuration }}
	>
		<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-static-element-interactions -->
		<div class="modal-background" on:click={() => !disableBackgroundClick && close()} />
		<div class="modal-content p-4">
			<slot />
		</div>
		{#if !hideCloseButton}
			<button
				class="modal-close is-large"
				aria-label={ariaLabelClose}
				type="button"
				on:click={close}
			/>
		{/if}
	</div>
{/if}
