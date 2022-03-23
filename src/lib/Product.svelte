<script>
	export let product, editProduct;
	let editStock = false;
	let inputStock = 0;
	let stockEditType = 'plus';

	const submitStock = () => {
		if (stockEditType === 'plus') {
			product.stock = product.stock + inputStock;
		} else {
			product.stock = product.stock - inputStock;
		}
		editStock = false;
	};

	const changeStock = () => {
		editStock = true;
	};
</script>

<div class="product">
	<div class="product-name">
		<p>{product.title}</p>
	</div>
	<div class="product-details">
		<div>
			<span>{product.stock}</span>
			{#if editStock}
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
			{:else}
				<button on:click={changeStock}>Edit</button>
			{/if}
		</div>
		<p>{product.price}</p>
	</div>
	<a href={`/products/${product.id}`}>Edit</a>
</div>
