<script>
	import '../fonts/fonts.css';
</script>

<div class="mainContainer">
	<slot />
</div>

<style>
	.mainContainer {
		min-height: 100vh;
		background: linear-gradient(to right, #210024, #590161);
		color: white;
		position: relative;
		display: flex;
		flex-direction: column;
	}
</style>
