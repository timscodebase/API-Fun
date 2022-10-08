<script>
	import { onMount } from 'svelte';
	import { arrangedRecipes, recipes, recipePhotos } from './store';
	import Button from '@api-fun/styles/Elements/Button.svelte';
	import Header from '@api-fun/styles/Layouts/Header.svelte';
	import Footer from '@api-fun/styles/Layouts/Footer.svelte';
	import Grid from '@api-fun/styles/Layouts/Grid.svelte';
	import Card from '@api-fun/styles/Elements/Card.svelte';
	import Global from '@api-fun/styles/Global.svelte';

	let displayedCuisine = 'Asian';

	onMount(async () => {
		const res = await fetch('https://api.sampleapis.com/recipes/recipes');
		recipes.set(await res.json());
		console.log('r', $recipes);
		$recipes.forEach((recipe) => {
			recipePhotos.set([...$recipePhotos, recipe.photoUrl]);
		});

		// sort recipes by cuisine. If no cuisine, then set to 'uncategorized'
		$recipes.forEach((recipe) => {
			if (recipe.cuisine) {
				arrangedRecipes.set({
					...$arrangedRecipes,
					[recipe.cuisine]: [...($arrangedRecipes[recipe.cuisine] || []), recipe]
				});
			} else {
				arrangedRecipes.set({
					...$arrangedRecipes,
					Uncategorized: [...($arrangedRecipes.uncategorized || []), recipe]
				});
			}
		});
		console.log('a', $arrangedRecipes);
	});

	// $: headerPhoto = $recipePhotos[Math.floor(Math.random() * $recipePhotos.length)];

	$: cuisineRecipes = $arrangedRecipes[displayedCuisine];
</script>

<Global backgroundColor="#18611f">
	<!-- <Header img={headerPhoto} headerText="Recipes" /> -->

	<main>
		<nav>
			<div class="buttonGroup">
				<Button callback={() => (displayedCuisine = 'Asian')} active={displayedCuisine === 'Asian'}
					>Asian</Button
				>
				<Button
					callback={() => (displayedCuisine = 'American')}
					active={displayedCuisine === 'American'}>American</Button
				>
				<Button
					callback={() => (displayedCuisine = 'Italian')}
					active={displayedCuisine === 'Italian'}>Italian</Button
				>
				<Button
					callback={() => (displayedCuisine = 'Mexican')}
					active={displayedCuisine === 'Mexican'}>Mexican</Button
				>
				<Button
					callback={() => (displayedCuisine = 'Uncategorized')}
					active={displayedCuisine === 'Uncategorized'}>Uncategorized</Button
				>
			</div>
		</nav>
		<Grid>
			{#each cuisineRecipes as { calories, carbohydrates, cholesterol, cookTime, cost, cuisine, description, directions, fat, fiber, id, ingredients, mainIngredient, photoUrl, prepTime, protein, publicUrl, servings, sodium, source, sugar, tags, title, totalTime }}
				<Card>
					<img src={photoUrl} alt={title} />
					<div class="content">
						<h2 class="name">{title}</h2>
						<p>{description ? description : 'No descriptipn'}</p>
					</div>
				</Card>
			{/each}
		</Grid>
	</main>
	<Footer />
</Global>

<style>
	img {
		width: 100%;
		height: 200px;
		object-fit: cover;
		border-radius: 0.5rem 0.5rem 0 0;
	}

	.content {
		padding: 1rem;
	}
</style>
