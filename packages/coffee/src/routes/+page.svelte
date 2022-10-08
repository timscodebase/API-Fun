<script>
	import { onMount } from 'svelte';
	import Header from '@api-fun/styles/Layouts/Header.svelte';
	import Grid from '@api-fun/styles/Layouts/Grid.svelte';
	import Button from '@api-fun/styles/Elements/Button.svelte';
	import Card from '@api-fun/styles/Elements/Card.svelte';
	import Global from '@api-fun/styles/Global.svelte';

	import { icedCoffees, hotCoffees } from './store';
	const icedImage = './images/iced.png';
	const hotImage = './images/hot.png';
	const icedAPI = 'https://api.sampleapis.com/coffee/iced';
	const hotAPI = 'https://api.sampleapis.com/coffee/hot';

	let isIced = false;

	onMount(async () => {
		const icedRes = await fetch(icedAPI);
		icedCoffees.set(await icedRes.json());
		const hotRes = await fetch(hotAPI);
		hotCoffees.set(await hotRes.json());
	});

	$: coffees = isIced ? $icedCoffees : $hotCoffees;
</script>

<Global backgroundColor="#281d0b">
	<Header img={isIced ? icedImage : hotImage} headerText={isIced ? 'Iced Coffee' : 'Hot Coffee'} />

	<main>
		<nav>
			<div class="buttonGroup">
				<Button callback={() => (isIced = !isIced)} active={!isIced}>Hot</Button>
				<Button callback={() => (isIced = !isIced)} active={isIced}>Iced</Button>
			</div>
		</nav>

		<Grid>
			{#each coffees as coffee}
				<Card>
					<img src={coffee.image} alt={coffee.title} />
					<div class="content">
						<h2 class="name">{coffee.title}</h2>
						<p>{coffee.description}</p>
						<p>Ingredience</p>
						<ul>
							{#each coffee.ingredients as ingredient}
								<li>{ingredient}</li>
							{/each}
						</ul>
					</div>
				</Card>
			{/each}
		</Grid>
	</main>
</Global>
