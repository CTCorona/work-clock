<script>
</script>

<div class="c-card__container">
	<div class="c-card__title">
		<slot name="title" />
	</div>
	<div class="c-card__body">
		<slot name="body" />
	</div>
</div>


<style lang="scss">

	.c-card__container {
		background-color: $white-color;
		min-width: 300px;
		max-width: 300px;
		padding: 20px;
		border-bottom-left-radius: 10px;
		border-top-right-radius: 10px;
		box-shadow: 0 3px 5px rgba($black-color, .1);
	}

	.c-card__title {
		text-align: center;
	}
</style>
