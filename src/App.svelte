<div>
	絞り込み:
	<button on:click={() => { condition = null }}>すべて</button>
	<button on:click={() => { condition = false }}>未完了</button>
	<button on:click={() => { condition = true }}>完了</button>
</div>
<div>
	<input type="text" bind:value={title}>
	<button on:click={() => add()}>タスク追加</button>
</div>
<div>
	<ul>
		{#each filterdTodoList(todoList, condition) as todo (todo.id)}
			<li>
				<input type="checkbox" bind:checked={todo.done}> {todo.title}
			</li>
		{/each}
	</ul>
</div>

<script>
	let todoList = [
		{ id: 0, done: false, title: 'レストランを予約する' },
		{ id: 1, done: false, title: 'サプライズ用の指輪を買う' },
		{ id: 2, done: false, title: 'フラッシュモブダンスを練習する' },
	]

	let title = ''
	function add() {
		todoList = [...todoList,
			{
				id: todoList.length,
				done: false,
				title: title
			}]
	}

	let condition = null

	$: filterdTodoList = (todoList, condition) => {
		return condition === null ? todoList : todoList.filter(t => t.done === condition)
	}
</script>

<style>

</style>
