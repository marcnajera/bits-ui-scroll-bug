<script lang="ts">
	import { page } from '$app/state'
	import { RadioGroup } from '@ark-ui/svelte'

	const options = [
		{ value: 'one', label: 'Option one' },
		{ value: 'two', label: 'Option two' },
		{ value: 'three', label: 'Option three' }
	]

	const preFiller = Array.from({ length: 22 }, (_, i) => i + 1)
	const postFiller = Array.from({ length: 28 }, (_, i) => i + 1)

	let value = $state('one')
	const usePreFiller = $derived(page.url.searchParams.get('pre') !== '0')
	const useRadioName = $derived(page.url.searchParams.get('named') !== '0')
	const useRootRelativeWrapper = $derived(page.url.searchParams.get('relative') === '1')
</script>

<div class="mx-auto max-w-4xl space-y-4">
	<div class="rounded-lg border border-emerald-300 bg-emerald-50 p-4">
		<h2 class="text-lg font-semibold text-emerald-900">Ark RadioGroup (expected good behavior)</h2>
		<p class="mt-1 text-sm text-emerald-800">
			Only this right panel should scroll. The left sidebar should remain visible.
		</p>
	</div>

	{#if usePreFiller}
		<div class="rounded-lg border border-slate-300 bg-white p-4">
			<p class="mb-3 text-sm font-medium text-slate-700">Filler before group</p>
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
		<p class="mb-3 text-sm font-medium text-slate-700">Ark RadioGroup</p>
		<div class={useRootRelativeWrapper ? 'relative' : ''}>
			<RadioGroup.Root
				name={useRadioName ? 'ark-repro-radio' : undefined}
				id="ark-repro-radio"
				orientation="horizontal"
				bind:value
				class="flex gap-6"
			>
				{#each options as option}
					<RadioGroup.Item value={option.value} class="flex items-center gap-2">
						<RadioGroup.ItemControl
							class={[
								'h-4 w-4 rounded-full border transition-colors',
								value === option.value ? ' bg-black' : 'border-slate-400 bg-white'
							].join(' ')}
						/>
						<RadioGroup.ItemText class="text-sm text-slate-800">{option.label}</RadioGroup.ItemText>
						<RadioGroup.ItemHiddenInput />
					</RadioGroup.Item>
				{/each}
			</RadioGroup.Root>
		</div>
	</div>

	<div class="rounded-lg border border-slate-300 bg-white p-4">
		<p class="mb-3 text-sm font-medium text-slate-700">Filler content</p>
		<div class="space-y-3">
			{#each postFiller as row}
				<div class="rounded border border-slate-200 bg-slate-50 px-3 py-4 text-sm text-slate-600">
					Post filler row {row}
				</div>
			{/each}
		</div>
	</div>
</div>
