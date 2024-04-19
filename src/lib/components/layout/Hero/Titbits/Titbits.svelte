<script lang="ts">
	import { fly } from 'svelte/transition';

	let data = [
		{ id: 1, text: "It's your vibe; You can merge it as you want!", color: '--aquamarine' },
		{ id: 2, text: 'Enjoy the mashup of your favourite artists altogether', color: '--light-red' },
		{ id: 3, text: 'Focus on your day while we make it a blissful one', color: '--ultra-violet' },
		{ id: 4, text: 'Enjoy the mashup of your favourite artists altogether', color: '--vista-blue' }
	];

	function cycleCards() {
		data = [...data.slice(1), data[0]];
	}

	setInterval(cycleCards, 5000);
</script>

<section class="flex gap-4">
	<div class="titbit_image flex flex-col justify-between p-4">
		<span class="merged px-3 py-1 text-white rounded-full text-sm">merged</span>
		<div class="text-white">
			<h3 class="text-xl font-semibold text-[var(--aquamarine)]">
				All those jams <br /> merged on the go
			</h3>
		</div>
	</div>
	<div class="card_stacks">
		{#each data as { id, text, color } (id)}
			<div
				class="card"
				style="background-color: var({color});"
				in:fly={{ y: 20, delay: 200, duration: 300 }}
				out:fly={{ y: 10, delay: 100, duration: 1000 }}
			>
				{text}
			</div>
		{/each}
	</div>
</section>

<style>
	section {
		--first-card-translateY: 0px;
		--second-card-translateY: -20px;
		--third-card-translateY: -40px;
		--fourth-card-translateY: -60px;
		--fifth-card-translateY: -80px;
		--sixth-card-translateY: -100px;
	}

	section {
		height: 250px;
	}

	.merged {
		width: max-content;
		color: var(--aquamarine);
		border: 1px solid var(--aquamarine);
	}

	.titbit_image,
	.card_stacks,
	.card {
		border-radius: 1rem;
	}

	.titbit_image {
		height: 100%;
		width: 50%;
		background-image: url('/src/lib/assets/images/vibing-lady.jpg');
		background-size: cover;
		background-position: top center;
		background-repeat: no-repeat;
	}

	.card_stacks {
		overflow: hidden;
		height: 100%;
		width: 50%;
		position: relative;
	}
	.card {
		padding: 1rem;
		display: grid;
		place-items: center;
		background-color: var(--light-red);
		transition: transform 0.5s ease;

		position: absolute;
		bottom: 0;
		width: 100%;
		height: 85%;
		border-radius: 1rem;
	}

	.card:nth-child(1) {
		z-index: 6;
		transform: translateY(var(--first-card-translateY)) scale(1);
	}
	.card:nth-child(2) {
		z-index: 5;
		transform: translateY(var(--second-card-translateY)) scale(0.9);
	}
	.card:nth-child(3) {
		z-index: 4;
		transform: translateY(var(--third-card-translateY)) scale(0.8);
	}
	.card:nth-child(4) {
		z-index: 3;
		transform: translateY(var(--fourth-card-translateY)) scale(0.7);
	}
	.card:nth-child(5) {
		z-index: 2;
		transform: translateY(var(--fifth-card-translateY)) scale(0.6);
	}
	.card:nth-child(6) {
		z-index: 1;
		transform: translateY(var(--sixth-card-translateY)) scale(0.5);
	}

	/* hover effect??? */
</style>
