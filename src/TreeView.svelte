
<!-- https://svelte.dev/docs#3_$_marks_a_statement_as_reactive -->
<script context="module">
	// retain module scoped expansion state for each tree node
	const _expansionState = {
		/* treeNodeId: expanded <boolean> */
	}
</script>

<script>
    import { v4 as uuid} from 'uuid';
//	import { slide } from 'svelte/transition'
	export let tree
    tree.id = tree.id || uuid();
    tree.children = tree.children || [];
	const {id, label, children} = tree

	// let expanded = _expansionState[label] || false
	let expanded = _expansionState[id] || false
	const toggleExpansion = () => {
		expanded = _expansionState[id] = !expanded
	}
    const deleteNode = (tr) => {
        console.log("delete node, tr:", tr);   
        tree = false;
    }
    const addChildNode = (tr) => {
        console.log("add child node to tr:", tr);
        let childId = uuid();
        // let childChildren = [];
        children.push({id: childId, label: ''}); // not sure not working
    }

    const addSiblingNode = (tr) => {
        console.log("add sibling node to tr:", tr);
    }
    // https://svelte.dev/docs#3_$_marks_a_statement_as_reactive
	$: arrowDown = expanded
</script>

{#if tree}
<ul><!-- transition:slide -->
	<li>
        <span class="delete" on:click={deleteNode(tree)} >(d)</span>
        <span class="addChild" on:click={addChildNode(tree)} >(c)</span> <!--add child-->
        <span class="addSibling" on:click={addSiblingNode(tree)} >(s)</span> <!--add sibling -->
		{#if children && children.length >0}
			<span on:click={toggleExpansion}>
                <!-- https://svelte.dev/tutorial/classes , https://svelte.dev/tutorial/class-shorthand-->
				<span class="arrow" class:arrowDown>&#x25b6</span>
				{label}
			</span>
			{#if expanded}
				{#each children as child}
					<svelte:self tree={child} />
				{/each}
			{/if}
		{:else}
			<span>
				<span class="no-arrow"/>
				{label}
			</span>
		{/if}
	</li>
</ul>
{/if}
<style>
	ul {
		margin: 0;
		list-style: none;
		padding-left: 1.2rem; 
		user-select: none;
        border-left: 1px dotted black;
	}
	.no-arrow { padding-left: 1.0rem; }
	.arrow {
		cursor: pointer;
		display: inline-block;
		/* transition: transform 200ms; */
	}
	.arrowDown { transform: rotate(90deg); }
</style>
