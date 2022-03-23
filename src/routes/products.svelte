<script context="module">
	export const hydrate = 'dev';

	export async function load({ params, fetch, session, stuff }) {
		let products = [];
		const url = `https://fakestoreapi.com/products`;
		const response = await fetch(url);
		if (response) {
			products = await response.json();
			products.forEach((item) => {
				item.stock = item.rating.count;
			});
			console.log('==products', products);
		}

		return {
			status: response.status,
			props: {
				products: products
			}
		};
	}
</script>

<script>
	import { onMount } from 'svelte';
	import Product from '$lib/Product.svelte';

	export let products;

	onMount(() => {});

	const editProduct = (product) => {
		console.log('==edit product', product.title);
	};
</script>

<table>
	<tr>
		<th>Product</th>
		<th>Stock</th>
		<th>Selling Price</th>
	</tr>
	{#each products as product}
		<Product bind:product {editProduct} />
	{/each}
</table>
