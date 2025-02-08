<script lang="ts">
	let { isX } = $props();

	let score = $state({ X: 0, O: 0 });

	const loadScore = () => {
		const storedScore = localStorage.getItem('tic_tac_toe_score');
		score = storedScore ? JSON.parse(storedScore) : { X: 0, O: 0 };
	};

	$effect(() => {
		(() => {
			loadScore();
		})();
	});
</script>

<div class="mb-4 flex w-96 items-center justify-between">
	<div class="flex flex-col items-center">
		<img
			src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTYr9eqLaWTS26L79iyKt8ajfJhn5gp84OmYFj6BzvU2gpc37e_Ceyfq-x07B6UPGnLiyY&usqp=CAU"
			alt="Player X"
			class="h-16 w-16 rounded-full border-4 border-blue-500 shadow-lg"
		/>
		<p class="mt-2 font-bold text-white">Player X</p>
		{#if score}
			<p class="text-lg font-semibold text-white">
				🏆 {score.X}
			</p>
		{/if}
		<span
			class="rounded-full bg-yellow-400 px-3 py-1 text-sm font-bold text-black shadow-lg
          transition-opacity duration-300 {isX ? 'opacity-100' : 'opacity-0'}"
		>
			Your turn
		</span>
	</div>

	<div class="flex flex-col items-center">
		<img
			src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRE6uTb77WAkKgg_5HmlVyM8_dRab-AnxdCaje2hapWcEQjv4HUV8_A8XXj4TAKx2DP2_4&usqp=CAU"
			alt="Player O"
			class="h-16 w-16 rounded-full border-4 border-orange-500 shadow-lg"
		/>
		<p class="mt-2 font-bold text-white">Player O</p>
		{#if score}
			<p class="text-lg font-semibold text-white">🏆 {score.O}</p>
		{/if}
		<span
			class="rounded-full bg-yellow-400 px-3 py-1 text-sm font-bold text-black shadow-lg
          transition-opacity duration-300 {isX ? ' opacity-0' : 'opacity-100'}"
		>
			Your turn
		</span>
	</div>
</div>
