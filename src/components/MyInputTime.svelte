<script>
export let value = null
</script>

<div class="c-input__container">
	<label for="" class="c-input__label a-fz--s">
		<slot />
	</label>
	<input type="time" class="c-input__input" bind:value={value}>
</div>

<style lang="scss">
	.c-input__container {
		display: flex;
		flex-flow: column nowrap;
		margin-bottom: 10px;
	}

	.c-input__label {
		margin-bottom: 10px;
	}

	.c-input__input {
		padding: 5px 5px;
		outline: none;
		border: none;
		border: 2px solid $primary-color;
		border-radius: 10px;
	}
</style>
