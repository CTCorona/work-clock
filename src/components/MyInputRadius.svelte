<script>
	export let name, value;
</script>

<div class="c-radio__container">
	<input type="radio" class="c-radio__input" id={`check-${value}`}
	       bind:group={name} value={value}
	/>
	<label for={`check-${value}`} class="c-radio__label">
		<span class="c-radio__effect">
			<span class="c-radio__effect__icon" />
		</span>
		<slot />
	</label>
</div>

<style lang="scss">
	.c-radio__container {
		display: flex;
		justify-content: flex-start;
		align-items: center;
		margin-bottom: 10px;
	}

	.c-radio__effect__icon {
		display: block;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		margin: auto;
		border-radius: 50%;
		width: 100%;
		height: 100%;
		transition: all 0.1s ease-in-out;
	}

	.c-radio__input {
		display: none;

		&:checked ~ label {
			&:hover {
				.c-radio__effect {
					border-color: $primary-color;
				}
			}

			.c-radio__effect {
				box-shadow: 0 0 4px rgba($black_color, .2);

				.c-radio__effect__icon {
					border: $primary-color solid 6px;
				}
			}
		}
	}

	.c-radio__effect {
		position: relative;
		display: block;
		border: 2px solid $primary-color;
		border-radius: 50%;
		width: 20px;
		height: 20px;
		margin-right: 10px;
		box-shadow: 0 0 2px rgba($black_color, 0);
		transition: all .2s ease-in-out;
	}

	.c-radio__label {
		display: flex;
		align-items: center;

		&:hover {
			.c-radio__effect {
				border-color: $secondary-color;
				box-shadow: 0 0 5px rgba($black_color, .2);
			}
		}
	}
</style>
