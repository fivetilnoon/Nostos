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

<div class="page">
	{#each experiences as exp}
		<article class="card">
			<img src={exp.photo} alt={exp.title} />
			<h2>{exp.title}</h2>
		</article>
	{/each}
</div>

<style>
	.page {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 1rem;
		padding: 1rem;
	}

	.card {
		border: 1px solid #ccc;
		border-radius: 8px;
		overflow: hidden;
		text-align: center;
		background: #fff;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.card img {
		display: block;
		width: 100%;
		height: auto;
	}

	.card h2 {
		font-size: 1.1rem;
		margin: 0.5rem 0;
		font-family: 'Trebuchet MS', Verdana, sans-serif;
	}
</style>
