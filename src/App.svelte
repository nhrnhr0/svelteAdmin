
<script>
	import {catalogImageData} from './store/store';
	import { onMount } from "svelte";

	export let ENDPOINT_API = 'http://127.0.0.1:8000/';
	export let catalog_image_id = '77';
	$: {
		let url = ENDPOINT_API + 'api/CatalogImages/' + catalog_image_id + '/';
		console.log(url)
		fetch(url)
			.then(response => response.json())
			.then(result => {
				console.log(result);
				catalogImageData.set(result);
			})
			.catch(error => console.log('error', error));
	}

</script>

<main>
	<h2>catalog image id: {catalog_image_id}</h2>
	<p>{$catalogImageData.title}</p>
	<form action="POST">
		<input type="text" bind:value="{$catalogImageData.title}" name="title"/>

		<textarea type="text" bind:value="{$catalogImageData.description}" name="description"/>

		<input type="text" bind:value="{$catalogImageData.barcode}" name="barcode"/>
		<input type="checkbox" bind:value="{$catalogImageData.can_tag}" name="can_tag"/>
		<img src="{$catalogImageData.image}" alt="${catalogImageData.title}"/>
	</form>
</main>



<svelte:options tag="admin-part" />