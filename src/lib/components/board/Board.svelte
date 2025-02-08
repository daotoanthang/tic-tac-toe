<script lang="ts">
	import Cell from '../cell/Cell.svelte';
	import WinnerModal from '../modal/WinnerModal.svelte';
	import PlayerInfo from './PlayerInfo.svelte';

	let board: (string | null)[] = $state([null, null, null, null, null, null, null, null, null]);
	let isX = $state(true);
	let winner: null | string = $state(null);
	let score: any = $state();

	const loadScore = () => {
		if (winner === 'X' || winner === 'O') {
			score = JSON.parse(localStorage.getItem('tic_tac_toe_score') || '{"X": 0, "O": 0}');

			score[winner] = score[winner] + 1;
			localStorage.setItem('tic_tac_toe_score', JSON.stringify(score));
		}
	};

	const resetGame = () => {
		board = [null, null, null, null, null, null, null, null, null];
		isX = true;
		loadScore();
		winner = null;
		window.location.href = '/';
	};

	const resetScore = () => {
		localStorage.setItem(
			'tic_tac_toe_score',
			JSON.stringify({
				X: 0,
				O: 0
			})
		);
		window.location.href = '/';
	};

	const checkWinner = (cells: (string | null)[]) => {
		const winnerPatterns = [
			[0, 1, 2],
			[3, 4, 5],
			[6, 7, 8],
			[0, 3, 6],
			[2, 5, 8],
			[1, 4, 7],
			[0, 4, 8],
			[2, 4, 6]
		];
		for (let i = 0; i < winnerPatterns.length; i++) {
			const [a, b, c] = winnerPatterns[i];
			if (cells[a] && cells[a] === cells[b] && cells[a] === cells[c]) {
				return cells[a];
			}
		}

		if (cells.every((cell) => cell !== null)) {
			return 'Draw';
		}

		return null;
	};

	const handleClickCell = (index: number) => {
		if (winner || board[index] !== null) return;
		board[index] = isX ? 'X' : 'O';
		isX = !isX;
	};

	$effect(() => {
		winner = checkWinner(board);
	});
</script>

<div
	class="flex h-screen flex-col items-center justify-center bg-gradient-to-b from-blue-400 to-blue-600"
>
	<PlayerInfo {isX} />
	<div class="my-2 grid grid-cols-3 gap-2 rounded-2xl bg-white p-4 shadow-lg md:my-4 lg:my-0">
		{#each board, i}
			<Cell onclick={() => handleClickCell(i)} value={board[i]} />
		{/each}
	</div>
	<div class="flex items-center gap-12">
		<button
			onclick={() => resetGame()}
			class="mt-4 flex items-center gap-2 rounded-lg bg-orange-500 px-4 py-2 text-white shadow-md transition-all hover:bg-orange-600"
		>
			<span>🔄</span> Reset Game
		</button>
		<button
			onclick={() => resetScore()}
			class="mt-4 flex items-center gap-2 rounded-lg bg-green-500 px-4 py-2 text-white shadow-md transition-all hover:bg-green-600"
		>
			<span>🗑️</span> Reset Score
		</button>
	</div>

	<WinnerModal {winner} onclick={() => resetGame()} />
</div>
