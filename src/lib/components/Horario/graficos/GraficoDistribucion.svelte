<script>
	import { createGraphRecomendado } from '$src/lib/utils/utils';
	import { storeAnalisis } from '$lib/stores/analisis.svelte';

	let dialog;
	let canvas;
	$effect(() => {
		storeAnalisis.elementos.distribucion = dialog;
	});

	$effect(() => {
		if (storeAnalisis.analized) {
			createGraphRecomendado(canvas, storeAnalisis.analized);
		}
	});

	function hide() {
		dialog.close();
	}
	export function show() {
		dialog.show();
	}
</script>

<dialog bind:this={dialog} class="p-6">
	<h5 class="text-lg font-bold w-full text-center mb-4 font-mono">
		{storeAnalisis.analized ? storeAnalisis.analized.nombre : ''}
	</h5>

	<div id="contenedor-grafico">
		<canvas bind:this={canvas}></canvas>
	</div>

	<div class="flex justify-center mt-4">
		<button onclick={hide} type="button" class="btn">
			<i class="bi bi-x"></i>
		</button>
	</div>
</dialog>

<style lang="scss">
	dialog {
		z-index: 10;
		background: rgba(238, 210, 255, 0.3);
		border-radius: 16px;
		box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
		backdrop-filter: blur(14.2px);
		-webkit-backdrop-filter: blur(14.2px);
		border: 1px solid rgba(238, 210, 255, 0.3);
		transition: all 0.2s ease;

		width: auto;
		height: auto;
		max-width: 30%;

		#contenedor-grafico {
			width: 100%;
			height: 100%;
		}

		button {
			background-color: #b26eff;
			color: white;
			font-weight: bold;
			text-align: center;

			width: 2rem;
			height: 2rem;
			border-radius: 50%;

			display: flex;
			justify-content: center;
			align-items: center;

			&:hover {
				background-color: #9345ff;
				color: white;
			}
		}
	}
</style>
