<!-- https://svelte.dev/repl/a3f724e24df54b9695402576ffd68fe3?version=3.23.2 -->
<script>
	// from https://svelte.dev/repl/82b00644720a4ca2bdb89c6a653ec987
	import TreeView from './TreeView.svelte'

	const tree = {
		label: "USA", children: [
			{label: "Florida", children: [
				{label: "Jacksonville"},
				{label: "Orlando", children: [
					{label: "Disney World"},
					{label: "Universal Studio"},
					{label: "Sea World"},
				]},
				{label: "Miami"},
			]},
			{label: "California", children: [
				{label: "San Francisco"},
				{label: "Los Angeles"},
				{label: "Sacramento"},
			]},
		],
	}
</script>

<TreeView {tree} />
