<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	let title = '';
	let location = '';
	let titleError = '';
	let locationError = '';

	function close() {
		dispatch('cancel');
	}

	function validate() {
		titleError = title.trim() ? '' : 'A title is required.';
		locationError = location.trim() ? '' : 'A location is required.';
		return !titleError && !locationError;
	}

	function save() {
		if (!validate()) return;
		dispatch('save', {
			title: title.trim(),
			location: location.trim()
		});
	}

	/**
	 * @param {MouseEvent} event
	 */
	function onBackdropClick(event) {
		if (event.currentTarget === event.target) {
			close();
		}
	}

	/**
	 * @param {KeyboardEvent} event
	 */
	function onBackdropKeyDown(event) {
		if (event.key === 'Enter' || event.key === ' ') {
			event.preventDefault();
			close();
		}
	}
</script>

<div
	class="backdrop"
	role="button"
	tabindex="0"
	on:click={onBackdropClick}
	on:keydown={onBackdropKeyDown}
	aria-label="Close dialog"
>
	<div class="dialog" role="dialog" aria-modal="true" aria-labelledby="add-experience-title">
		<div class="dialog-header">
			<h2 id="add-experience-title">Add a new experience</h2>
			<button type="button" class="close-button" on:click={close} aria-label="Close dialog"
				>×</button
			>
		</div>

		<div class="dialog-body">
			<label>
				<span>Title</span>
				<input type="text" bind:value={title} placeholder="Experience title" />
				{#if titleError}
					<span class="error">{titleError}</span>
				{/if}
			</label>

			<label>
				<span>Location</span>
				<input type="text" bind:value={location} placeholder="Location" />
				{#if locationError}
					<span class="error">{locationError}</span>
				{/if}
			</label>
		</div>

		<div class="dialog-actions">
			<button type="button" class="secondary" on:click={close}>Cancel</button>
			<button type="button" class="primary" on:click={save}>Save</button>
		</div>
	</div>
</div>

<style>
	.backdrop {
		position: fixed;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background: rgba(20, 20, 20, 0.4);
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 1.5rem;
		z-index: 50;
	}

	.dialog {
		width: min(520px, 100%);
		background: var(--surface);
		border-radius: 1rem;
		overflow: hidden;
		box-shadow: 0 24px 60px rgba(0, 0, 0, 0.16);
	}

	.dialog-header,
	.dialog-actions {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1.25rem 1.5rem;
	}

	.dialog-header {
		border-bottom: 1px solid var(--border);
	}

	.dialog-body {
		display: grid;
		gap: 1rem;
		padding: 1.5rem;
	}

	.dialog-body label {
		display: grid;
		gap: 0.5rem;
		font-weight: 600;
	}

	.dialog-body input {
		width: 100%;
		padding: 0.85rem 1rem;
		border: 1px solid rgba(0, 0, 0, 0.14);
		border-radius: 0.85rem;
		font: inherit;
	}

	.close-button,
	.dialog-actions button {
		border: none;
		cursor: pointer;
	}

	.close-button {
		background: transparent;
		font-size: 1.4rem;
		line-height: 1;
	}

	.dialog-actions {
		border-top: 1px solid var(--border);
	}

	.secondary {
		background: #f4f4f4;
		color: var(--text);
		border-radius: 0.85rem;
		padding: 0.85rem 1.25rem;
	}

	.primary {
		background: var(--text);
		color: var(--surface);
		border-radius: 0.85rem;
		padding: 0.85rem 1.25rem;
	}

	.error {
		color: #b00020;
		font-size: 0.95rem;
	}
</style>
