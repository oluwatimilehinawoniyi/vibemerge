<script>
	import authImg from '$lib/assets/images/auth-img.jpg';
</script>

<section class="p-4 h-screen">
	<div
		class="flex items-center p-4 h-full rounded-[1rem] gap-4 bg-no-repeat bg-cover relative justify-end"
		style="background-image: url({authImg}); background-position: top center;"
	>
		<a href="/" class="absolute top-4 left-4 text-[var(--aquamarine)]">vibemerge</a>

		<div
			class="absolute bottom-4 left-4 text-3xl font-semibold text-[var(--aquamarine)] capitalize"
		>
			<p>Merge your Vibes</p>
			<p>What's the limit anyway?</p>
			<p>None?? So, Keep Merging</p>
		</div>

		<div class="w-1/2 bg-[#ff6b6bff]/30 backdrop-blur-md h-full rounded-[1rem]">
			<slot />
		</div>
	</div>
</section>
