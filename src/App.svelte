<script>
	const API = "https://jsonplaceholder.typicode.com/users"
	let data

	async function apiCall () {
		const response = await fetch(API)
		data = await response.json()
		if(response.ok){
			return data
		} else {
			throw new Error("No ha sido posible conectar")
		}
	}
	let promise = apiCall()
</script>
<style>
	*, *:before, *:after{
		margin: 0;
		padding: 0;
	}
	h1{
		margin-bottom: 1rem;
	}
	.ContentCard{
		display: flex;
		gap: 0.5rem;
		flex-wrap: wrap;
	}
	.ContentCard--Card{
		background-color: #ccc;
		border-radius: 5px;
		padding: 1rem;
		width: 100%;
	}
</style>
<main>
	<h1>Nombres</h1>
	{#await promise}
		<h1>Cargando...</h1>
	{:then data}
	<div class="ContentCard">
		{#each data as item, i}
			<div class="ContentCard--Card">
				<h2>{item.username}</h2>
				<p>{item.name}</p>
				<p>{item.website}</p>
			</div>
		{/each}
	</div>
	{/await}
</main>