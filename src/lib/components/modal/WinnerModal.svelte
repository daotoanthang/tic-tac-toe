<script lang="ts">
	interface Props {
		winner: string | null;
		onclick: any;
	}
	let { winner, onclick }: Props = $props();
</script>

{#if winner}
	<div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
		<div class="rounded-lg bg-white p-6 text-center shadow-lg">
			{#if winner === 'Draw'}
				<h2 class="mb-4 text-2xl font-bold text-gray-700">😐 It's a tie 😐</h2>
			{:else}
				<h2 class="mb-4 text-2xl font-bold text-blue-600">🎉 Winner: Player {winner} 🎉</h2>
			{/if}
			<button
				{onclick}
				class="mt-2 rounded-lg bg-red-500 px-4 py-2 text-white shadow-md hover:bg-red-600"
			>
				Close
			</button>
		</div>
	</div>
{/if}
