# Tic Tac Toe

Built using [boardgame.io](https://boardgame.io/documentation/#/tutorial) and [Svelte](https://svelte.dev).

## Notes

Defining a game programmatically, as a series of functions that alter game state, is easy enough to wrap my head around.

Svelte is a good fit for this. The client works as a [Svelte store](https://svelte.dev/docs#Store_contract), which makes it easy to always keep the current game state available. I used two computed properties for added convenience.

```js
$: G = $client.G;
$: ctx = $client.ctx;
```

Building a board actually takes more thought than I expected. The tutorial uses a table. I wanted to use CSS grid, because I've been playing with that lately, and it worked fine. But it meant thinking about turning a flat array of cells into a grid. Definitely will take more planning for more complex games.
