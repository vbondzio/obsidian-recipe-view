<script lang="ts">
	import Fraction from "fraction.js";
	export let scaleNum: number | null = 1;
	export let scale;
	$: scale = new Fraction(scaleNum || 1);
</script>
<div>
	<label>
		Scale recipe
		<input
			type="number"
			inputmode="decimal"
			min="0.25"
			step="any"
			on:blur={() => (scaleNum = scaleNum || 1)}
			on:focus={() => (scaleNum = scaleNum == 1 ? null : scaleNum)}
			bind:value={scaleNum}
		/>
		<button on:click={() => {
			const current = scaleNum || 1;
			scaleNum = Math.max(0.25, current - 0.25);
		}}>-</button>
		<button on:click={() => {
			const current = scaleNum || 1;
			scaleNum = current + 0.25;
		}}>+</button>
	</label>
</div>
<style>
	div {
		width: 100%;
		text-align: center;
		font-size: var(--font-smaller);
		background-color: var(--background-secondary);
		padding: var(--size-4-2);
		margin-block-end: var(--size-4-4);
		border-radius: var(--radius-s);
		color: var(--text-muted);
	}
	input {
		width: var(--size-4-16);
		border: none;
		background-color: hsla(
			var(--accent-h),
			var(--accent-s),
			var(--accent-l),
			var(--selected-step-alpha)
		);
		margin-inline-start: var(--size-4-2);
		text-align: right;
		font-size: var(--font-smaller);
		height: var(--size-4-8);
	}
	label {
		margin-right: calc(-1 * var(--size-4-2));
	}
	label::after {
		content: "×";
		position: relative;
		width: var(--size-4-4);
		right: calc(var(--size-4-16) + var(--size-4-8) + var(--size-4-8));
		color: var(--text-accent);
	}
	
	button {
	background: var(--background-modifier-hover);
	border: none;
	margin: 0 var(--size-4-1);
	cursor: pointer;
	font-size: var(--font-smaller);
	padding: 0 var(--size-4-2);
	border-radius: var(--radius-s);
}
</style>
