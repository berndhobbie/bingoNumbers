<script lang="ts">
	import BingoNumber from '$lib/components/BingoNumber.svelte';
	let randNumber = 0;
	let minBingoNum = 1;
	let maxBingoNum = 75;
	let drawnNumbers: number[] = [];

	const genNewNumber = () => {
		if (drawnNumbers.length === maxBingoNum) {
			alert('Alle Zahlen wurden gezogen!');
			return;
		}
		randNumber = Math.floor(Math.random() * (maxBingoNum - minBingoNum + 1)) + minBingoNum;
		if (drawnNumbers.includes(randNumber)) {
			genNewNumber();
			return;
		}
		drawnNumbers.push(randNumber);
		drawnNumbers = drawnNumbers; // This will notify Svelte about the change.
	};
</script>

<div class="flex justify-center w-full h-full">
	<div class="flex flex-col items-center w-full">
		<h1 class="text-9xl">{randNumber}</h1>
		<button
			class="bg-orange-700 rounded-full p-6 shadow-md font-mono text-3xl font-semibold hover:bg-orange-800"
			on:click={genNewNumber}>Neue Zahl</button
		>
		<div class="flex flex-wrap">
			{#each drawnNumbers as number}
				<BingoNumber>{number}</BingoNumber>
			{/each}
		</div>
	</div>
</div>

<div class="fixed bottom-0 left-0 w-full bg-slate-600 p-4">
	<div class="flex justify-around">
		<label>
			Min Number:
			<input
				type="number"
				bind:value={minBingoNum}
				min="1"
				max="74"
				class="m-2 p-2 text-slate-900 text-xl text-center"
			/>
		</label>
		<label>
			Max Number:
			<input
				type="number"
				bind:value={maxBingoNum}
				min="2"
				max="75"
				class="m-2 p-2 text-slate-900 text-xl text-center"
			/>
		</label>
	</div>
</div>
