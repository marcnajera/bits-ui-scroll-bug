<script lang="ts">
	import { page } from '$app/state';
	import { Label, RadioGroup, useId } from 'bits-ui';
	import Select from './Select.svelte';

	const options = [
		{ value: 'one', label: 'Option one' },
		{ value: 'two', label: 'Option two' },
		{ value: 'three', label: 'Option three' }
	];

	const preFiller = Array.from({ length: 22 }, (_, i) => i + 1);
	const postFiller = Array.from({ length: 28 }, (_, i) => i + 1);

	let value = $state('one');
	const usePreFiller = $derived(page.url.searchParams.get('pre') !== '0');
	const usePostFiller = true;
	const useName = $derived(page.url.searchParams.get('named') !== '0');
	const useRootRelativeWrapper = $derived(page.url.searchParams.get('relative') === '1');
</script>

<div class="mx-auto max-w-4xl space-y-4">
	<div class="rounded-lg border border-amber-300 bg-amber-50 p-4">
		<h2 class="text-lg font-semibold text-amber-900">Bits RadioGroup (bug reproduction)</h2>
		<p class="mt-1 text-sm text-amber-800">
			This page intentionally mimics the original failing context: large content before the group +
			nested overflow.
		</p>
		<p class="mt-2 text-sm text-amber-800">
			Expected failing combo: <code>content before = ON</code>, <code>pass name prop = ON</code>,
			<code>relative wrapper = OFF</code>.
		</p>
	</div>

	{#if usePreFiller}
		<div class="rounded-lg border border-slate-300 bg-white p-4">
			<p class="mb-3 text-sm font-medium text-slate-700">Content before radio group</p>
			<div class="space-y-3">
				{#each preFiller as row}
					<div class="rounded border border-slate-200 bg-slate-50 px-3 py-4 text-sm text-slate-600">
						Pre filler row {row}
					</div>
				{/each}
			</div>
		</div>
	{/if}

	<div class="rounded-lg border border-slate-300 bg-white p-4">
		<p class="mb-3 text-sm font-medium text-slate-700">Bits Select</p>
		<div class={useRootRelativeWrapper ? 'relative' : ''}>
			<Select name={useName ? 'bits-repro-select' : undefined} {options} />
		</div>
	</div>

	{#if usePostFiller}
		<div class="rounded-lg border border-slate-300 bg-white p-4">
			<p class="mb-3 text-sm font-medium text-slate-700">Filler after form section</p>
			<div class="space-y-3">
				{#each postFiller as row}
					<div class="rounded border border-slate-200 bg-slate-50 px-3 py-4 text-sm text-slate-600">
						Post filler row {row}
					</div>
				{/each}
			</div>
		</div>
	{/if}
</div>
