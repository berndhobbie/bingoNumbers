<script lang="ts">
	import BingoHeader from '$lib/components/BingoHeader.svelte';
	import BingoNumber from '$lib/components/BingoNumber.svelte';
	let randNumber = 0;
	let minBingoNum = 1;
	let maxBingoNum = 75;
	let drawnNumbers: number[] = [];
	let B: number[] = [];
	let I: number[] = [];
	let N: number[] = [];
	let G: number[] = [];
	let O: number[] = [];

	const categorizeNumber = (number: number) => {
		if (number >= 1 && number <= 15) {
			B.push(number);
			B = B; // This will notify Svelte about the change.
		} else if (number >= 16 && number <= 30) {
			I.push(number);
			I = I; // This will notify Svelte about the change.
		} else if (number >= 31 && number <= 45) {
			N.push(number);
			N = N; // This will notify Svelte about the change.
		} else if (number >= 46 && number <= 60) {
			G.push(number);
			G = G; // This will notify Svelte about the change.
		} else if (number >= 61 && number <= 75) {
			O.push(number);
			O = O; // This will notify Svelte about the change.
		}
	};

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
		categorizeNumber(randNumber);
		drawnNumbers = drawnNumbers; // This will notify Svelte about the change.
	};
</script>

<div class="flex justify-center items-center w-full h-full">
	<div class="grid grid-cols-2 w-full h-full">
		<div class="flex flex-col items-center self-center">
			<h1 class="text-9xl">{randNumber}</h1>
			<button
				class="bg-green-700 rounded-full p-6 shadow-md font-mono text-3xl font-semibold hover:bg-green-800"
				on:click={genNewNumber}>Neue Nummer</button
			>
		</div>
		<div class="flex flex-col items-center">
			<div class="grid grid-cols-5 w-full center justify-items-center mt-3">
				<BingoHeader>B</BingoHeader>
				<BingoHeader>I</BingoHeader>
				<BingoHeader>N</BingoHeader>
				<BingoHeader>G</BingoHeader>
				<BingoHeader>O</BingoHeader>
			</div>
			<div class="grid grid-cols-5 w-full center justify-items-center mt-3">
				<div>
					{#each B as number}
						<BingoNumber>{number}</BingoNumber>
					{/each}
				</div>
				<div>
					{#each I as number}
						<BingoNumber>{number}</BingoNumber>
					{/each}
				</div>
				<div>
					{#each N as number}
						<BingoNumber>{number}</BingoNumber>
					{/each}
				</div>
				<div>
					{#each G as number}
						<BingoNumber>{number}</BingoNumber>
					{/each}
				</div>
				<div>
					{#each O as number}
						<BingoNumber>{number}</BingoNumber>
					{/each}
				</div>
			</div>
		</div>
	</div>
</div>
