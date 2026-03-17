<script lang="ts">
	import { page } from '$app/state';

	function currentRouteUrl(overrides: Record<string, boolean>) {
		const params = new URLSearchParams(page.url.searchParams);
		for (const [key, enabled] of Object.entries(overrides)) {
			params.set(key, enabled ? '1' : '0');
		}
		return `${page.url.pathname}?${params.toString()}`;
	}

	const showKeyToggles = $derived(page.url.pathname === '/bits' || page.url.pathname === '/ark');

	const isPreEnabled = $derived(page.url.searchParams.get('pre') !== '0');
	const isNamedEnabled = $derived(page.url.searchParams.get('named') !== '0');
	const isRelativeEnabled = $derived(page.url.searchParams.get('relative') === '1');
</script>

<aside class="h-full w-64 shrink-0 border-r border-slate-300 bg-white p-4">
	<h1 class="text-lg font-semibold">Bits RadioGroup bug repro</h1>
	<p class="mt-2 text-sm text-slate-600">
		The sidebar should stay fixed while only the right panel scrolls.
	</p>
	<nav class="mt-4 flex flex-col gap-2 text-sm">
		<a
			href={`/ark?${page.url.searchParams.toString()}`}
			class={[
				'rounded border px-3 py-2',
				page.url.pathname === '/ark/'
					? 'border-blue-600 bg-blue-50 text-blue-700'
					: 'border-slate-300 bg-white text-slate-700 hover:bg-slate-50'
			].join(' ')}
		>
			Ark version
		</a>
		<a
			href={`/bits?${page.url.searchParams.toString()}`}
			class={[
				'rounded border px-3 py-2',
				page.url.pathname === '/bits/'
					? 'border-blue-600 bg-blue-50 text-blue-700'
					: 'border-slate-300 bg-white text-slate-700 hover:bg-slate-50'
			].join(' ')}
		>
			Bits version
		</a>
	</nav>

	{#if showKeyToggles}
		<div class="mt-5 border-t border-slate-200 pt-4">
			<p class="mb-2 text-xs font-semibold tracking-wide text-slate-500 uppercase">Key toggles</p>
			<div class="space-y-2 text-sm">
				<div class="rounded border border-slate-200 p-2">
					<p class="mb-2 text-xs text-slate-600">pre filler</p>
					<div class="flex gap-2">
						<a
							href={currentRouteUrl({ pre: !isPreEnabled })}
							class={[
								'flex items-center gap-1 rounded border px-2 py-1 text-xs',
								isPreEnabled
									? 'border-emerald-300 bg-emerald-50 text-emerald-800'
									: 'border-slate-300 bg-white text-slate-700 hover:bg-slate-50'
							].join(' ')}
						>
							<span>{isPreEnabled ? '☑' : '☐'}</span>
							<span>{isPreEnabled ? 'ON' : 'OFF'}</span>
						</a>
					</div>
				</div>
				<div class="rounded border border-slate-200 p-2">
					<p class="mb-2 text-xs text-slate-600">pass name</p>
					<div class="flex gap-2">
						<a
							href={currentRouteUrl({ named: !isNamedEnabled })}
							class={[
								'flex items-center gap-1 rounded border px-2 py-1 text-xs',
								isNamedEnabled
									? 'border-emerald-300 bg-emerald-50 text-emerald-800'
									: 'border-slate-300 bg-white text-slate-700 hover:bg-slate-50'
							].join(' ')}
						>
							<span>{isNamedEnabled ? '☑' : '☐'}</span>
							<span>{isNamedEnabled ? 'ON' : 'OFF'}</span>
						</a>
					</div>
				</div>
				<div class="rounded border border-slate-200 p-2">
					<p class="mb-2 text-xs text-slate-600">relative wrapper</p>
					<div class="flex gap-2">
						<a
							href={currentRouteUrl({ relative: !isRelativeEnabled })}
							class={[
								'flex items-center gap-1 rounded border px-2 py-1 text-xs',
								isRelativeEnabled
									? 'border-emerald-300 bg-emerald-50 text-emerald-800'
									: 'border-slate-300 bg-white text-slate-700 hover:bg-slate-50'
							].join(' ')}
						>
							<span>{isRelativeEnabled ? '☑' : '☐'}</span>
							<span>{isRelativeEnabled ? 'ON' : 'OFF'}</span>
						</a>
					</div>
				</div>
			</div>
		</div>
	{/if}
</aside>
