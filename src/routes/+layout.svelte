<script lang="ts">
	import './layout.css';
	import Sidebar from './Sidebar.svelte';

	interface Props {
		children?: import('svelte').Snippet;
	}

	let { children }: Props = $props();
</script>

<div class="h-screen overflow-hidden bg-slate-100 text-slate-900">
	<div class="flex h-full">
		<Sidebar />
		<main class="min-w-0 flex-1 overflow-y-auto p-6">
			{@render children?.()}
		</main>
	</div>
</div>
