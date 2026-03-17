<div class="mx-auto max-w-3xl rounded-lg border border-slate-300 bg-white p-6">
	<h2 class="text-xl font-semibold">Bits UI scroll bug reproduction</h2>
	<p class="mt-2 text-sm text-slate-700">
		Some Bits UI elements that render a hidden input cause the whole page to scroll (including the
		sidebar).
	</p>
	<p class="mt-2 text-sm text-slate-700">
		I've tested with RadioGroup and Select. I've included an Ark UI version of a RadioGroup to make
		sure it's not related to the layout/page structure. Both pages use the same layout and filler
		content.
	</p>
	<div class="mt-4 flex gap-3">
		<a
			href="/ark"
			class="rounded bg-slate-900 px-4 py-2 text-sm font-medium text-white hover:bg-slate-800"
		>
			Open Ark page
		</a>
		<a
			href="/bits"
			class="rounded bg-slate-900 px-4 py-2 text-sm font-medium text-white hover:bg-slate-800"
		>
			Open Bits page
		</a>
	</div>
</div>
