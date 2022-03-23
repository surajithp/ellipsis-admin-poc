<script context="module">
	export const load = async ({ params, fetch }) => {
		let product = null;
		const id = params.id;
		const url = `https://fakestoreapi.com/products/${id}`;
		const response = await fetch(url);
		if (response) {
			product = await response.json();
			product.url = '';
		}

		return {
			props: {
				product
			}
		};
	};
</script>

<script>
	export let product;

	let stockEditType = 'plus';
	let inputStock = 0;

	const submitStock = () => {};
</script>

<div class="flex-container">
	<a href="/products">Back</a>
	<p>{product.title}</p>
</div>
<div>
	<label for="url">Url </label>
	<input id="url" class="width-full" type="text" bind:value={product.url} />
</div>
<div>
	<label for="category">Category </label>
	<input class="width-full" id="category" type="text" bind:value={product.category} />
</div>
<div>
	<label for="description">Description </label>
	<textarea class="width-full" id="description" type="text" bind:value={product.description} />
</div>

<div class="product-info">
	<div class="flex-space-between">
		<p>{product.category}</p>
		<label for="status"
			>Active
			<input type="checkbox" checked />
		</label>
	</div>
	<div class="flex-space-between">
		<div>
			<div>
				<h4>Price</h4>
				<div class="flex-space-between">
					<p>
						<label for="price">List Price</label>
						<input type="text" bind:value={product.price} />
					</p>
					<p>
						<label for="price">Sale Price</label>
						<input type="text" bind:value={product.price} />
					</p>
				</div>
			</div>
			<div>
				<h4>Stock</h4>
				<div class="flex-space-between">
					<div>
						<label for="sku">SKU</label>
						<input type="text" bind:value={product.id} />
					</div>
					<div>
						<div class="flex-space-between">
							<p>{product.rating.count}</p>
							<div>
								<label>
									<input type="radio" bind:group={stockEditType} name="stock" value="plus" />
									+
								</label>
								<label>
									<input type="radio" bind:group={stockEditType} name="stock" value="minus" />
									-
								</label>
								<input type="number" bind:value={inputStock} />
								<button on:click|preventDefault={submitStock}>Submit</button>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div>
			<img src={product.image} width="200" height="300" alt="" />
		</div>
	</div>
</div>

<style>
	.flex-container {
		display: flex;
		justify-content: flex-start;
	}

	.product-info {
		background-color: lightgray;
	}

	.flex-space-between {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.width-full {
		width: 50%;
	}

	div {
		margin: 10px;
	}

	p {
		text-transform: uppercase;
	}
</style>
