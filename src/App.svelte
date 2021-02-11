<script>
	import moment from "moment";
	import Card from "./components/Card.svelte";
	import MyInputTime from "./components/MyInputTime.svelte";
	import MyInputRadius from "./components/MyInputRadius.svelte";

	/** METHODS */
	/**
	 * @description Gets the final hour of exit of the journey
	 */
	let calculateExitTime = () => {
		let dinner = calculateDinner(horaComidaEnd, horaComidaStart);
		let result = calculateExitHour(horaEntrada, dinner);
		let m = result.minute();
		horaSalida = `${result.hour()}:${m < 10 ? (m = "0" + m) : (m = m)}`;
	};

	/**
	 * @description Gets the duration of a journey depending which week day user choose
	 * @param {Number} d Dinner durtation time
	 * @param {Object} s Journey start time
	 */
	let calculateExitHour = (s, d) => {
		let start = moment(s, "HH:mm"),
			exit;
		if (currentDay === "normal") {
			if (d > 0) {
				wHour = 8;
				wMinute = 45 + d;
				errMsg = "";
				exit = start.add(wHour, "hours").add(wMinute, "minutes");
			} else {
				errMsg = "Verifica que no haya ningún error!";
			}
		} else {
			wHour = 6;
			wMinute = 15;
			errMsg = "";
			exit = start.add(wHour, "hours").add(wMinute, "minutes");
		}

		return exit;
	};

	/**
	 * @description Gets the estimated time that took dinner time
	 * @param {String} e Dinner finish time
	 * @param {String} s Dinner start time
	 */
	let calculateDinner = (e, s) => {
		let end = moment(e, "HH:mm"),
			start = moment(s, "HH:mm");

		return end.diff(start, "minutes");
	};

	let currentDay = "normal",
		wHour = 8,
		wMinute = 45;

	let horaEntrada = "08:00",
		horaComidaStart = "13:30",
		horaComidaEnd = "14:30",
		horaSalida = null,
		errMsg = "";

	const radio = [
		{
			label: "Lunes - Jueves",
			value: "normal",
		},
		{
			label: "Viernes",
			value: "viernes",
		},
	];
</script>

<main>
	<Card>
		<h1 slot="title" class="a-title is-1">Lúcid Clock</h1>
		<div slot="body">
			<h3 class="a-title is-5 a-ta--center">Selecciona día de la semana:</h3>
			<div class="c-week__selector">
				{#each radio as { label, value }}
					<MyInputRadius bind:name={currentDay} {value}>
						{label}
					</MyInputRadius>
				{/each}
			</div>
			<div class="c-timers__container">
				<MyInputTime bind:value={horaEntrada}>Hora de entrada</MyInputTime>
				{#if currentDay !== "viernes"}
					<MyInputTime bind:value={horaComidaStart}>
						Hora de comer inicio
					</MyInputTime>
					<MyInputTime bind:value={horaComidaEnd}>
						Hora de comer fin
					</MyInputTime>
				{/if}
				<!--				-->
				<button class="a-btn" on:click={calculateExitTime}> Calcular </button>

				{#if errMsg.length > 0}
					<p class="a-msg--error">{errMsg}</p>
				{/if}
				<!--				-->
				<MyInputTime bind:value={horaSalida}>Hora de salida</MyInputTime>
			</div>
		</div>
	</Card>
</main>

<style lang="scss">
	@import "./assets/scss/global";

	main {
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: lighten($black_color, 10%);
	}

	.a-msg--error {
		color: #ff0000;
		font-weight: 600;
		text-align: center;
	}
</style>
