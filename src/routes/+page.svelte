<script lang="ts">
	import Authenticate from '../components/Authenticate.svelte';
	import type { PageData } from './$types';
	export let data: PageData;

	$: data;
</script>

<Authenticate />
