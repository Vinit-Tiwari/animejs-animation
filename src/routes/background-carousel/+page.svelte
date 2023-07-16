<script>
	import anime from 'animejs';
	import { onMount } from 'svelte';
	let column = 0;
	let row = 0;
	let colorArray = [
		'#FF6633',
		'#FFB399',
		'#FF33FF',
		'#FFFF99',
		'#00B3E6',
		'#E6B333',
		'#3366E6',
		'#999966',
		'#99FF99',
		'#B34D4D',
		'#80B300',
		'#809900',
		'#E6B3B3',
		'#6680B3',
		'#66991A',
		'#FF99E6',
		'#CCFF1A',
		'#FF1A66',
		'#E6331A',
		'#33FFCC',
		'#66994D',
		'#B366CC',
		'#4D8000',
		'#B33300',
		'#CC80CC',
		'#66664D',
		'#991AFF',
		'#E666FF',
		'#4DB3FF',
		'#1AB399',
		'#E666B3',
		'#33991A',
		'#CC9999',
		'#B3B31A',
		'#00E680',
		'#4D8066',
		'#809980',
		'#E6FF80',
		'#1AFF33',
		'#999933',
		'#FF3380',
		'#CCCC00',
		'#66E64D',
		'#4D80CC',
		'#9900B3',
		'#E64D66',
		'#4DB380',
		'#FF4D4D',
		'#99E6E6',
		'#6666FF'
	];
	onMount(() => {
		const container = document.getElementById('container');

		const createElement = (index) => {
			const tile = document.createElement('div');
			tile.classList.add('tile');
			tile.style.width = '50px';
			tile.style.height = '50px';
			tile.onclick = (e) => handleOnClick(index);
			return tile;
		};

		const createTile = (quantity) => {
			Array.from(Array(quantity)).map((tile, index) => {
				container.appendChild(createElement(index));
			});
		};

		const createGrid = () => {
			container.innerHTML = ' ';
			column = Math.floor(document.body.clientWidth / 50);
			row = Math.floor(document.body.clientHeight / 50);

			container.style.setProperty('--column', column);
			container.style.setProperty('--row', row);

			createTile(column * row);
		};
		createGrid();
		window.onresize = () => createGrid();

		const handleOnClick = (index) => {
			anime({
				targets: '.tile',
				backgroundColor: colorArray[Math.floor(Math.random() * colorArray.length)],
				opacity: [0, 1],
				delay: anime.stagger(50, { grid: [column, row], from: index })
			});
		};
	});
</script>

<span id="container" class="container" />

<style>
	.container {
		padding: 0%;
		margin: 0%;
		width: 100%;
		min-height: 100vh;
		display: grid;
		grid-template-columns: repeat(var(--column), 1fr);
		grid-template-rows: repeat(var(--row), 1fr);
	}
</style>
