<script lang="ts">
	import '@app.postcss';
	let inputFile = $state<HTMLInputElement>();
	let formModel = $state<HTMLFormElement>();
	$effect(() => {
		console.log('inputFile: ', inputFile);
	});
	function beforeSubmit(event: HTMLFormElement) {
		const formData: Record<string, any> = {};
		console.log('event: ', event);
		for (const [name, value] of new FormData(event)) {
			console.log('name, value: ', name, value);
			formData[name] = value;
		}
		console.log('formData: ', formData);
		return formData;
	}
</script>

<div class="flex h-screen w-screen items-center justify-center">
	<form class="m-auto grid w-3/5 grid-cols-12 gap-4" bind:this={formModel} on:submit|preventDefault={() => beforeSubmit(formModel!)}>
		<div class="col-span-8">
			<label for="files">Converta arquivos PDF para XLS</label>
			<input
				class="file-input file-input-bordered file-input-accent w-full"
				name="files"
				type="file"
				bind:this={inputFile}
				on:change={() => {
					console.log('change do on:change');
				}}
				onchange={() => {
					console.log('inputFile do change: ', inputFile);
				}}
				multiple
				accept=".pdf"
			/>
		</div>
		<div class="col-span-4">
			<button type="submit" class="btn btn-secondary mt-6 w-full">Download XLS</button>
		</div>
	</form>
</div>
