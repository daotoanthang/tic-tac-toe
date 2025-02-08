<script lang="ts">
	interface Props {
		value: string | null;
		onclick?: (event: MouseEvent) => void;
	}
	let { value, onclick }: Props = $props();
</script>

<button
	{onclick}
	class="flex h-24 w-24 cursor-pointer items-center justify-center rounded-xl text-4xl font-bold shadow-md md:h-28 md:w-28 md:text-5xl lg:h-32
                    lg:w-32 lg:text-7xl
                    {value === 'X'
		? 'cursor-none bg-gradient-to-br from-blue-300 to-blue-500 text-blue-500'
		: ''}
                    {value === 'O'
		? 'cursor-none bg-gradient-to-br from-orange-300 to-orange-500 text-orange-500'
		: ''}"
>
	{value}
</button>
