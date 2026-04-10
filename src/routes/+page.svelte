<script>
	import AddExperienceDialog from '$lib/AddExperienceDialog.svelte';

	// static prototype data – will be replaced with dynamic content later
	// six experiences using sample images from static/sample (random selection)
	const samplePhotos = ['/sample/edinburgh.jpg', '/sample/greece.jpg', '/sample/train.jpg'];
	function randomPhoto() {
		return samplePhotos[Math.floor(Math.random() * samplePhotos.length)];
	}

	let experiences = [
		{
			id: 1,
			title: 'Beach sunset',
			location: 'Scotland',
			status: 'Complete',
			photo: randomPhoto()
		},
		{
			id: 2,
			title: 'Mountain hike',
			location: 'Switzerland',
			status: 'Planned',
			photo: randomPhoto()
		},
		{ id: 3, title: 'City tour', location: 'Florence', status: 'Complete', photo: randomPhoto() },
		{ id: 4, title: 'Forest walk', location: 'Oregon', status: 'Planned', photo: randomPhoto() },
		{
			id: 5,
			title: 'Desert adventure',
			location: 'Morocco',
			status: 'Planned',
			photo: randomPhoto()
		},
		{ id: 6, title: 'Snowy peak', location: 'Alps', status: 'Complete', photo: randomPhoto() }
	];

	let showAddDialog = false;

	function openAddDialog() {
		showAddDialog = true;
	}

	function closeAddDialog() {
		showAddDialog = false;
	}

	/**
	 * @param {{ detail: { title: string; location: string } }} event
	 */
	function handleSave(event) {
		const { title, location } = event.detail;
		experiences = [
			...experiences,
			{
				id: experiences.length + 1,
				title,
				location,
				status: 'Planned',
				photo: randomPhoto()
			}
		];

		closeAddDialog();
	}
</script>

<svelte:head>
	<title>Nostos – travel experiences</title>
</svelte:head>

<main class="page">
	<header class="page-header">
		<div class="page-header-inner container">
			<div class="brand">Nostos</div>
			<button type="button" class="new-experience" on:click={openAddDialog}>Add</button>
		</div>
	</header>

	{#if showAddDialog}
		<AddExperienceDialog on:cancel={closeAddDialog} on:save={handleSave} />
	{/if}

	<div class="page-body container">
		<section class="cards">
			{#each experiences as exp (exp.id)}
				<article class="card">
					<figure>
						<div class="status-chip {exp.status.toLowerCase()}">{exp.status}</div>
						<img src={exp.photo} alt={exp.title} />
						<figcaption>
							<span class="title">{exp.title}</span>
							<span class="location">{exp.location}</span>
						</figcaption>
					</figure>
				</article>
			{/each}
		</section>
	</div>
</main>

<style>
	:global(:root) {
		--page-bg: #ece3d6;
		--surface: #fff;
		--text: #141414;
		--muted: rgba(0, 0, 0, 0.65);
		--border: rgba(0, 0, 0, 0.08);
		--border-strong: rgba(0, 0, 0, 0.12);
		--shadow: rgba(0, 0, 0, 0.12);
		--shadow-strong: rgba(0, 0, 0, 0.18);
		--radius: 1rem;
		--radius-lg: 1.25rem;
		--radius-pill: 999px;
	}

	:global(html, body) {
		min-height: 100%;
		margin: 0;
		background: var(--page-bg);
		color: var(--text);
	}

	.page {
		min-height: 100vh;
		padding: 0;
	}

	.page-body {
		padding: 2rem 0 3rem;
	}

	.page-header {
		margin-bottom: 2rem;
		background: var(--surface);
		border-bottom: 1px solid var(--border);
		box-shadow: 0 18px 40px var(--shadow-strong);
	}

	.page-header-inner {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 1rem;
		padding: 1.25rem 0;
	}

	.brand {
		font-size: 1.5rem;
		font-weight: 700;
		letter-spacing: 0.02em;
	}

	.new-experience {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		border: none;
		padding: 0.65rem 1rem;
		border-radius: 0.75rem;
		background: var(--text);
		color: var(--surface);
		font-size: 0.95rem;
		font-weight: 700;
		cursor: pointer;
		box-shadow: 0 8px 18px rgba(20, 20, 20, 0.14);
		transition:
			background 0.2s ease,
			box-shadow 0.2s ease;
	}

	.new-experience:hover {
		background: #222;
		box-shadow: 0 10px 22px rgba(20, 20, 20, 0.18);
	}

	.cards {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
		gap: 1.5rem;
	}

	.card {
		background: #fffefb;
		border: 1px solid var(--border);
		border-radius: var(--radius);
		padding: 0;
		overflow: hidden;
		box-shadow: 0 22px 55px var(--shadow);
		transition: box-shadow 0.2s ease;
	}

	.card:hover {
		box-shadow: 0 28px 72px rgba(0, 0, 0, 0.18);
	}

	.card figure {
		position: relative;
		margin: 0;
		padding: 0;
	}

	.status-chip {
		position: absolute;
		top: 0.7rem;
		right: 0.7rem;
		padding: 0.2rem 0.6rem;
		border-radius: var(--radius-pill);
		font-size: 0.75rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--surface);
		background: rgba(0, 0, 0, 0.65);
		backdrop-filter: blur(4px);
		pointer-events: none;
	}

	.status-chip.planned {
		background: rgba(46, 125, 50, 0.85);
	}

	.status-chip.complete {
		background: rgba(19, 76, 143, 0.88);
	}

	.card img {
		width: 100%;
		height: auto;
		aspect-ratio: 3 / 2;
		object-fit: cover;
		display: block;
	}

	.card figcaption {
		padding: 0.5rem 0.9rem 0.7rem;
		text-align: center;
	}

	.card figcaption .title {
		display: block;
		font-size: 1rem;
		font-weight: 700;
		line-height: 1.2;
		letter-spacing: 0.01em;
	}

	.card figcaption .location {
		display: block;
		margin-top: 0.1rem;
		font-size: 0.9rem;
		font-weight: 400;
		line-height: 1.2;
		color: var(--muted);
	}
</style>
