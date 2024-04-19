<script>
	import { Button } from '$lib/components/ui/button';
</script>

<nav class="flex items-center justify-between">
	<a href="/">vibemerge</a>

	<a
		href="/get-started"
		class="rounded-full w-max flex items-center text-white gap-2 p-1 pr-2"
		style="background-color: var(--light-red)"
	>
		<span class="bg-white rounded-full h-8 w-8 grid place-items-center">
			<svg
				width="20"
				height="20"
				viewBox="0 0 24 24"
				fill="none"
				stroke="black"
				stroke-width="2"
				stroke-linecap="round"
				stroke-linejoin="round"
				class="lucide lucide-arrow-right"
			>
				<path d="M5 12h14" />
				<path d="m12 5 7 7-7 7" />
			</svg>
		</span>
		<p class="mr-2">get started</p>
	</a>
</nav>
