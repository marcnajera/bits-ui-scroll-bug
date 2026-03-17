<script lang="ts">
	import { page } from '$app/state'
	import { Label, RadioGroup, useId } from 'bits-ui'

	const options = [
		{ value: 'one', label: 'Option one' },
		{ value: 'two', label: 'Option two' },
		{ value: 'three', label: 'Option three' }
	]

	const preFiller = Array.from({ length: 22 }, (_, i) => i + 1)
	const postFiller = Array.from({ length: 28 }, (_, i) => i + 1)

	let value = $state('one')
	const usePreFiller = $derived(page.url.searchParams.get('pre') !== '0')
	const usePostFiller = true
	const useFormSplit = true
	const useRadioName = $derived(page.url.searchParams.get('named') !== '0')
	const useRootRelativeWrapper = $derived(page.url.searchParams.get('relative') === '1')
</script>

<div class="mx-auto max-w-4xl space-y-4">
	<div class="rounded-lg border border-amber-300 bg-amber-50 p-4">
		<h2 class="text-lg font-semibold text-amber-900">Bits RadioGroup (bug reproduction)</h2>
		<p class="mt-1 text-sm text-amber-800">
			This page intentionally mimics the original failing context: large content before the group +
			nested overflow.
		</p>
		<p class="mt-2 text-sm text-amber-800">
			Expected failing combo: <code>pre filler = ON</code>, <code>pass name = ON</code>,
			<code>relative wrapper = OFF</code>.
		</p>
	</div>

	{#if usePreFiller}
		<div class="rounded-lg border border-slate-300 bg-white p-4">
			<p class="mb-3 text-sm font-medium text-slate-700">Filler before form section</p>
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
		<p class="mb-3 text-sm font-medium text-slate-700">Bits RadioGroup</p>
		<div class={useRootRelativeWrapper ? 'relative' : ''}>
			<RadioGroup.Root
				name={useRadioName ? 'radio' : undefined}
				id="bits-repro-radio"
				orientation="horizontal"
				bind:value
				class="flex gap-6"
			>
				{#each options as option}
					{@const itemId = useId()}
					<div class="flex items-center gap-2">
						<RadioGroup.Item
							id={itemId}
							value={option.value}
							class="grid h-4 w-4 place-items-center rounded-full border border-slate-400 bg-white"
						>
							{#snippet children({ checked })}
								{#if checked}
									<div class="h-2 w-2 rounded-full bg-black"></div>
								{/if}
							{/snippet}
						</RadioGroup.Item>
						<Label.Root for={itemId} class="text-sm text-slate-800">{option.label}</Label.Root>
					</div>
				{/each}
			</RadioGroup.Root>
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
