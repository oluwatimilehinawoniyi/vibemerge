<script lang="ts">
	import { onMount } from 'svelte';

	import video1 from '$lib/assets/videos/video1.mp4';
	import video2 from '$lib/assets/videos/video2.mp4';
	import video3 from '$lib/assets/videos/video3.mp4';

	// --ultra-violet: #5e548eff;
	// --vista-blue: #9face6ff;
	// --aquamarine: #29ffa6ff;
	// --light-red: #ff6b6bff;

	const data = [
		{ id: 1, text: "It's your vibe; You can merge it as you want!", color: '--aquamarine' },
		{ id: 2, text: 'Enjoy the mashup of your favourite artists altogether', color: '--light-red' },
		{ id: 3, text: 'Focus on your day while we make it a blissful one', color: '--light-red' }
	];

	const videos = [video1, video2, video3];
	let currentIndex = 0;
	let progress = [0, 0, 0];
	let currentVideoSrc = videos[0];

	let videoElement: HTMLVideoElement;

	function preloadNextVideo() {
		const nextVideoIndex = (currentIndex + 1) % videos.length;
		const nextVideoSrc = videos[nextVideoIndex];
		fetch(nextVideoSrc)
			.then((res) => res.blob())
			.then((blob) => {
				const nextVideoUrl = URL.createObjectURL(blob);
			});
	}

	function handleVideoEnd() {
		if (currentIndex === videos.length - 1) {
			progress = progress.map(() => 0);
		}
		currentIndex = (currentIndex + 1) % videos.length;
		currentVideoSrc = videos[currentIndex];
		videoElement.load();
		videoElement.play();
		preloadNextVideo();
	}

	function updateProgress() {
		const interval = setInterval(() => {
			if (videoElement.duration) {
				const currentProgress = (videoElement.currentTime / videoElement.duration) * 100;
				progress[currentIndex] = currentProgress;
				if (currentProgress >= 100) {
					clearInterval(interval);
				}
			}
		}, 100);
	}

	onMount(() => {
		videoElement.addEventListener('ended', handleVideoEnd);
		videoElement.addEventListener('timeupdate', updateProgress);
		return () => {
			videoElement.removeEventListener('ended', handleVideoEnd);
			videoElement.removeEventListener('timeupdate', updateProgress);
		};
	});
</script>

<div class="media w-full h-full">
	<div class="progress_stack flex gap-4">
		{#each progress as p, index (index)}
			<div class="progress-bar h-2 rounded-full">
				<div
					style="height: 100%; background-color: var({data[currentIndex]
						.color}); width: {p}%; transition: width 0.5s ease;"
				></div>
			</div>
		{/each}
	</div>
	<video
		bind:this={videoElement}
		src={currentVideoSrc}
		class="w-full h-full"
		autoplay
		muted
		loop={false}
		preload="auto"
	>
		<source type="video/mp4" />
	</video>

	<div class="video_info backdrop-blur-sm">
		<h1 class="text-3xl text-center font-semibold" style="color: var({data[currentIndex].color})">
			{data[currentIndex].text}
		</h1>
	</div>
</div>

<style>
	video {
		object-fit: cover;
		object-position: top center;
	}

	.media {
		border-radius: 1rem;
		overflow: hidden;
		position: relative;
	}

	.video_info {
		position: absolute;
		height: max-content;
		bottom: 2rem;
		padding: 1rem;
		background-color: hsla(0, 0%, 100%, 0.5);
		margin: auto;
		right: 2rem;
		left: 2rem;
		border-radius: 1rem;
	}

	.progress_stack {
		position: absolute;
		z-index: 1;
		top: 1.5rem;
		left: 1.5rem;
		right: 1.5rem;
		height: 4px;
	}

	.progress-bar {
		flex: 1;
		transition: width 0.5s ease;
		width: 100%;
		position: relative;
		transition: width 0.5s ease;
		overflow: hidden;
		background-color: var(--vista-blue);
	}

	.progress-bar::after {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 0%;
		background-color: var(--light-red);
		height: 100%;
	}
</style>
