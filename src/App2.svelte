<script>
	let images = [
		{ id: 1, text: `kitten.png`, width: `80px`},
		{ id: 2, text: `puppy.png` },
		{ id: 3, text: `flower.png` }
	];

	let selected;

	let answer = '';

	function handleSubmit() {
		alert(`answered question ${selected.id} (${selected.text}) with "${answer}"`);
	}
</script>

<h2>Insecurity questions</h2>

<form on:submit|preventDefault={handleSubmit}>
    {#each images as image}
        <img id="cursor" src={`kitten.png`} style="width:80px; visibility: visible; position:inline">
    {/each}
	<select bind:value={selected} on:change="{() => answer = ''}">
		{#each images as image}
			<option  value={image} style="width:80px;height:64px; position: inline">
				
			</option>
		{/each}
	</select>

	<input bind:value={answer}>

	<button disabled={!answer} type=submit>
		Submit
	</button>
</form>

<p>selected question {selected ? selected.id : '[waiting...]'}</p>

<style>
	input { display: block; width: 500px; max-width: 100%; }
</style>