<script>
	import { Client } from "boardgame.io/client";
	import { onMount } from "svelte";
	import { TicTacToe } from "./game.js";

	const client = Client({ game: TicTacToe });

	$: G = $client.G;
	$: ctx = $client.ctx;

	function clickCell(id) {
		client.moves.clickCell(id);
	}

	onMount(() => {
		client.start();

		return client.stop;
	});
</script>

<style>
	.board {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		max-width: 300px;
	}

	.cell {
		border: 0.5px solid #444;
		height: 30px;
		text-align: center;
		padding: 1em;
		cursor: pointer;
	}

	div.reset {
		margin: 1em 0;
	}
</style>

<main>
	<h1>Tic Tac Toe</h1>

	{#if ctx.gameover}
		<h2>
			{#if ctx.gameover.draw}It's a draw{:else}Winner: Player {ctx.gameover.winner}{/if}
		</h2>
		<div class="reset"><button on:click={client.reset}>Play again?</button></div>
	{/if}

	<div class="board">
		{#each G.cells as cell, i}
			<div class="cell" on:click={e => clickCell(i)}>{cell === null ? '' : cell}</div>
		{/each}
	</div>
</main>
