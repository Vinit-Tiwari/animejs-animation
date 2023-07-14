<script>
	import anime from 'animejs';
	import { onMount } from 'svelte';
	let boxSize = 20;
	let timeline;
	onMount(() => {
		anime({
			targets: '.sample',
			scale: [
				{ value: 0.1, easing: 'easeOutSine', duration: 500 },
				{ value: 1, easing: 'easeInOutQuad', duration: 1200 }
			],
			translateX: anime.stagger(5, { grid: [20, 5], from: 'center', axis: 'x' }),
			translateY: anime.stagger(5, { grid: [20, 5], from: 'center', axis: 'y' }),
			rotateZ: anime.stagger([0, 90], {
				grid: [20, 5],
				from: 'center',
				axis: 'x'
			}),
			delay: anime.stagger(200, { grid: [20, 5], from: 'center' }),
			easing: 'easeInOutQuad',
			loop: true,
			direction: 'alternate'
		});
	});
</script>

<span class="box">
	{#each { length: 100 } as _, i}
		<div class="sample box-{i}" />
	{/each}
</span>

<style>
	.box {
		display: grid;
		grid-template-rows: repeat(5, 1fr);
		grid-template-columns: repeat(20, 1fr);
		color: aliceblue;
		overflow: hidden;
	}
	.sample {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 3rem;
		border-radius: 50%;
		height: 3rem;
		background-color: brown;
	}
</style>
