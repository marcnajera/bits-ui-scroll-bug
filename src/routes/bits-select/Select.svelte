<script lang="ts">
	import { Select } from 'bits-ui';

	let { name, options }: { name?: string; options: { value: string; label: string }[] } = $props();

	let value = $state<string>('');
	const selectedLabel = $derived(
		value ? options.find((option) => option.value === value)?.label : 'Select an option'
	);
</script>

<Select.Root
	type="single"
	onValueChange={(v) => (value = v)}
	items={options}
	allowDeselect={true}
	{name}
>
	<Select.Trigger
		class="h-input border-border-input inline-flex w-[296px] touch-none items-center rounded-full border bg-white px-[11px] text-sm transition-colors select-none data-placeholder:text-black/50"
		aria-label="Select a theme"
	>
		{selectedLabel}
	</Select.Trigger>
	<Select.Portal>
		<Select.Content
			class="focus-override shadow-popover data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 max-h-[var(--bits-select-content-available-height)] w-[var(--bits-select-anchor-width)] min-w-[var(--bits-select-anchor-width)] rounded-xl border border-black/10 bg-white px-1 py-3 outline-hidden select-none data-[side=bottom]:translate-y-1 data-[side=left]:-translate-x-1 data-[side=right]:translate-x-1 data-[side=top]:-translate-y-1"
			sideOffset={10}
		>
			<Select.Viewport class="p-1">
				{#each options as option, i (i + option.value)}
					<Select.Item
						class="rounded-button flex h-10 w-full items-center py-3 pr-1.5 pl-5 text-sm capitalize outline-hidden select-none data-disabled:opacity-50 data-highlighted:bg-black/10"
						value={option.value}
						label={option.label}
					>
						{#snippet children({ selected })}
							{option.label}
							{#if selected}
								<div class="ml-auto">✅</div>
							{/if}
						{/snippet}
					</Select.Item>
				{/each}
			</Select.Viewport>
		</Select.Content>
	</Select.Portal>
</Select.Root>
