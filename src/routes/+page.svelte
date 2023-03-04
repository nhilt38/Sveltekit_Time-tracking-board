<script>
	import '../app.css'
	import times from './times.js'
	import avatar from '$lib/images/image-jeremy.png'
	import ellipsis from '$lib/images/icon-ellipsis.svg'
    import { dirty_components } from 'svelte/internal';
	let select = 'Daily'
</script>

<svelte:head>
	<title>Time tracking board</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<main class="flex justify-center md:grid md:grid-cols-1">	
	<div class="relative w-64 rounded-lg bg-indigo-900 mr-6 md:w-full md:mb-6">
		<div class="h-2/3 bg-indigo-500 p-8 rounded-lg md:flex md:p-4">
			<img class="w-16 md:object-contain" src="{ avatar }" alt="">
			<div class="pl-4">
			<div class="text-sm text-white/50 pt-14 md:pt-6">Report for</div>
			<h1 class="text-5xl pt-4 md:text-3xl md:pt-2">Jeremy Robson</h1>
			</div>
		</div>		
		<div class="h-1/3 p-8 md:flex md:justify-between">
			<button class:active="{select === 'Daily'}"
			on:click="{() => select = 'Daily'}"
			class="block py-1 hover:text-white/50 font-semibold">Daily</button>
			<button class:active="{select === 'Weekly'}"
			on:click="{() => select = 'Weekly'}" 
			class="block py-1 hover:text-white/50 font-semibold">Weekly</button>
			<button class:active="{select === 'Monthly'}"
			on:click="{() => select = 'Monthly'}"
			class="block py-1 hover:text-white/50 font-semibold">Monthly</button>			
		</div>		
	</div>

	<div class="grid grid-rows-2 grid-cols-3 gap-6 md:w-full md:grid-rows-1 md:grid-cols-none">	
		{#each times as time}			
		<div class="relative w-64 rounded-lg mobile:width md:w-full md:h-48" style="background: {time.color}">
			<div class="h-1/5 truncate">
				<img class="float-right pr-4" src="src/lib/images/icon-{time.title}.svg" alt="">
			</div>		
			<div class="h-4/5 bg-indigo-900 rounded-lg p-6">
				<div class="flex justify-between">
					<span class="font-semibold md:text-xl">{time.title}</span>
					<img class="object-contain" src="{ellipsis}" alt="">
				</div>
				{#if select === 'Daily'}
				<div class="md:flex md:justify-between md:items-center">
					<h1 class="text-6xl pt-5 pb-3 md:text-5xl md:pt-2"> {time.timeframes.daily.current }hrs </h1>
					<span class="text-white/50">Last Week - {time.timeframes.daily.previous }hrs</span>
				</div>
				{/if}
				{#if select === 'Weekly'}
				<div>
					<h1 class="text-6xl pt-5 pb-3 md:text-5xl md:pt-2"> {time.timeframes.weekly.current }hrs </h1>
					<span class="text-white/50">Last Week - {time.timeframes.weekly.previous }hrs</span>
				</div>
				{/if}
				{#if select === 'Monthly'}
				<div>
					<h1 class="text-6xl pt-5 pb-3 md:text-5xl md:pt-2"> {time.timeframes.monthly.current }hrs </h1>
					<span class="text-white/50">Last Week - {time.timeframes.monthly.previous }hrs</span>
				</div>
				{/if}
			</div>		
		</div>		
		{/each}
    </div>
	
</main>

