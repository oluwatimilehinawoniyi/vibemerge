<script lang="ts">
	let username = '';
	let password = '';
</script>

<form
	class="forms w-2/3 mx-auto p-4 text-white flex items-start justify-center flex-col gap-10 h-full"
>
	<div class="relative field">
		<input type="text" class="h-6" bind:value={username} />
		<label for="username" class="absolute capitalize" class:has-value={username.trim() !== ''}
			>your spotify username</label
		>
	</div>

	<div class="relative field">
		<input type="password" class="h-6" bind:value={password} />
		<label for="password" class="absolute capitalize" class:has-value={password.trim() !== ''}
			>your spotify password</label
		>
	</div>

	<button>merge</button>
</form>

<style>
	.field {
		width: 100%;
	}

	.field label {
		bottom: 2px;
		left: 0;
		pointer-events: none;
		width: 100%;
		opacity: 0.5;
		font-size: 0.8rem;
		transition: all 0.3s linear;
	}

	input {
		font-size: .9rem;
		background-color: transparent;
		outline: none;
		border: none;
		border-bottom: 1px solid #fff;
		width: 100%;
		position: relative;
		z-index: 1;
		padding-left: 5px;
	}

	.field input:focus {
		background-color: transparent;
	}

	.field input:focus ~ label,
	.field label.has-value {
		opacity: 0.7;
		transform: translateY(-120%);
	}
</style>
