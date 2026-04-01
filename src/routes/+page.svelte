<script>
	// static prototype data – will be replaced with dynamic content later
	// six experiences using sample images from static/sample (random selection)
	const samplePhotos = ['/sample/edinburgh.jpg', '/sample/greece.jpg', '/sample/train.jpg'];
	function randomPhoto() {
		return samplePhotos[Math.floor(Math.random() * samplePhotos.length)];
	}
	const experiences = [
		{ id: 1, title: 'Beach sunset', photo: randomPhoto() },
		{ id: 2, title: 'Mountain hike', photo: randomPhoto() },
		{ id: 3, title: 'City tour', photo: randomPhoto() },
		{ id: 4, title: 'Forest walk', photo: randomPhoto() },
		{ id: 5, title: 'Desert adventure', photo: randomPhoto() },
		{ id: 6, title: 'Snowy peak', photo: randomPhoto() }
	];
</script>

<svelte:head>
	<title>Nostos – travel experiences</title>
</svelte:head>

<main class="page container">
	<section class="cards">
		{#each experiences as exp (exp.id)}
			<article class="card">
				<figure>
					<img src={exp.photo} alt={exp.title} />
					<figcaption>{exp.title}</figcaption>
				</figure>
			</article>
		{/each}
	</section>
</main>

<style>
	:global(body) {
		background: #ece3d6;
		color: #141414;
	}

	.page {
		padding: 2rem 1.5rem 3rem;
		background: #ece3d6;
	}

	.cards {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
		gap: 1.5rem;
	}

	.card {
		background: #fffefb;
		border: 1px solid rgba(0, 0, 0, 0.08);
		border-radius: 1rem;
		padding: 0;
		overflow: hidden;
		box-shadow: 0 22px 55px rgba(0, 0, 0, 0.12);
		transition:
			transform 0.2s ease,
			box-shadow 0.2s ease;
	}

	.card:hover {
		transform: translateY(-6px);
		box-shadow: 0 28px 72px rgba(0, 0, 0, 0.18);
	}

	.card figure {
		margin: 0;
		padding: 0;
	}

	.card img {
		width: 100%;
		height: auto;
		aspect-ratio: 3 / 2;
		object-fit: cover;
		display: block;
	}

	.card figcaption {
		padding: 1rem 1.25rem 1.25rem;
		font-size: 1rem;
		font-weight: 700;
		letter-spacing: 0.01em;
		text-align: center;
	}

	.eyebrow {
		text-transform: uppercase;
		letter-spacing: 0.2em;
		font-size: 0.8rem;
		opacity: 0.8;
		margin-bottom: 0.75rem;
	}
</style>
