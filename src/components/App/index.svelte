<script lang="ts">
	import CopyIcon from './CopyIcon.svelte';

	const convertToProperURL = (webhookURL: string) => {
		let formattedURL = webhookURL;

		formattedURL = formattedURL.replace(
			'https://discord.com/api/webhooks/',
			''
		);
		formattedURL = formattedURL.replace('/', '--');
		formattedURL = `https://api.formsdeck.com/api/v1/forms/${formattedURL}`;

		return formattedURL;
	};

	let webhookURL = '';
	$: isWebhookURLValid = webhookURL && webhookURL.trim() !== '';
	let formattedURL = '';
	$: isLinkGenerated = formattedURL && formattedURL.trim() !== '';

	const copyText = () => {
		navigator.clipboard.writeText(formattedURL);

		alert('Copied. Now you can paste the link in the form');
	};

	function handleSubmit() {
		formattedURL = convertToProperURL(webhookURL);
	}
</script>

<section class="section-layout app-link-section">
	<section class="section-container">
		<h2 class="section-heading-small">Try it out yourself!</h2>
		<form on:submit|preventDefault={handleSubmit}>
			<input
				type="text"
				bind:value={webhookURL}
				placeholder="Discord Webhook URL"
			/>
			<input
				type="submit"
				disabled={!isWebhookURLValid}
				value="Generate link"
			/>
		</form>
		<div class="generated-link-area">
			<p class="generated-link-text">
				{formattedURL.trim().length === 0
					? 'Generated link appears here'
					: formattedURL}
			</p>
			<button class="copy-icon" on:click={copyText} disabled={!isLinkGenerated}
				><CopyIcon /></button
			>
		</div>
		<p id="docs-reference">
			First time using Forms Deck? Read our docs <a
				href="https://github.com/thesyedbasim/formsdeck/blob/main/README.md"
				target="_blank"
				rel="noreferrer noopener">here</a
			>
		</p>
	</section>
</section>

<!-- faq: why no proper response, how to add message -->

<!-- username and avatar -->
<style>
	.app-link-section {
		background-color: var(--color-container-bg);
		padding: 4.5rem 0;
	}

	#docs-reference {
		margin-top: 1rem;
		text-align: center;
	}

	form {
		display: grid;
		grid-template-columns: 3fr 1fr;
		align-items: stretch;
		column-gap: 1rem;
	}

	input {
		border: none;
		border-radius: 0.4rem;
	}

	input[type='text'] {
		padding: 1rem 0.7rem;
		background-color: var(--color-white);
		color: var(--color-black);
	}

	input[type='submit'] {
		background-color: var(--color-blue-1);
		padding: 1rem 2rem;
		transition: all 0.3s;
	}

	input[type='submit']:hover {
		background-color: var(--color-blue-1--dark);
	}

	input[type='submit']:not(:disabled) {
		cursor: pointer;
	}

	input[type='submit']:disabled {
		background-color: var(--color-grey-1);
		cursor: not-allowed;
	}

	.generated-link-area {
		display: grid;
		grid-template-columns: 1fr min-content;
		margin-top: 1.4rem;
		row-gap: 0.2rem;
		border-radius: 0.4rem;
		padding: 0.4rem 1rem;
		align-items: center;
		background-color: var(--color-grey-1);
	}

	.generated-link-text {
		overflow: hidden;
		max-width: 100%;
	}

	.copy-icon {
		width: 2rem;
		height: 2rem;
		padding: 0.3rem;
		border-radius: 1000rem;
		transition: all 0.3s;
		cursor: pointer;
		border: none;
		background-color: var(--color-grey-2);
	}
	.copy-icon:disabled {
		cursor: not-allowed;
	}
	.copy-icon:hover:not(:disabled) {
		background-color: var(--color-grey-1);
	}

	input[type='text']:disabled {
		background-color: var(--color-grey-1);
	}
</style>
