<script>
	import { candidates } from '@sudoku/stores/candidates';
	import { userGrid } from '@sudoku/stores/grid';
	import { cursor } from '@sudoku/stores/cursor';
	import { hints } from '@sudoku/stores/hints';
	import { notes } from '@sudoku/stores/notes';
	import { settings } from '@sudoku/stores/settings';
	import { keyboardDisabled } from '@sudoku/stores/keyboard';
	import { gamePaused } from '@sudoku/stores/game';
	import { canUndo, canRedo, canRecall , recall_times } from '@sudoku/stores/history';

	$: hintsAvailable = true;   // 提示应始终可用

	function handleHint() {
		if (hintsAvailable) {
			userGrid.applyHint();
		}
	}

	function handleUndo() {
		if (!$gamePaused && $canUndo) {
			userGrid.undo();
		}
	}

	function handleRedo() {
		if (!$gamePaused && $canRedo) {
			userGrid.redo();
		}
	}

	function handleRecall() {
		if (!$gamePaused && $canRecall) {
			userGrid.recall();
			userGrid.check_can_recall();
		}
	}

	// function handleSolveStrategy() {
    //     if (!$gamePaused) {
    //         userGrid.applyStrategy();
    //         // 假设 applyStrategy 方法会更新 strategyValue
    //         strategyValue = userGrid.getStrategy();
    //         // 更新显示的内容
    //         updateStrategyDisplay(strategyValue);
    //     }
    // }

    // function updateStrategyDisplay(value) {
    //     const displayElement = document.getElementById('strategy-display');
    //     if (displayElement) {
    //         displayElement.textContent = `当前使用的策略：${value}`;
    //     }
    // }


</script>

<div class="action-buttons space-x-3">



		<!--<button class="btn btn-round" on:click={handleReCallGame} disabled={!$gameRecall} title="Recall"> TODO：回溯-->
			<button class="btn btn-round" disabled={$gamePaused || !$canRecall} on:click={handleRecall} title="Recall">
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a10 10 0 1 1 -2 4 m2 -4 l6 2m-6-2l2 -6" />
		</svg>
	</button>

	<button class="btn btn-round" disabled={$gamePaused || !$canUndo} on:click={handleUndo} title="Undo">
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h10a8 8 0 018 8v2M3 10l6 6m-6-6l6-6" />
		</svg>
	</button>

	<button class="btn btn-round" disabled={$gamePaused || !$canRedo} on:click={handleRedo} title="Redo">
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 10h-10a8 8 90 00-8 8v2M21 10l-6 6m6-6l-6-6" />
		</svg>
	</button>

    <button class="btn btn-round btn-badge" disabled={!hintsAvailable} on:click={handleHint} title="Hints ({$hints})">		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" />
		</svg>
		{#if $hints > 0}
		<span class="badge" class:badge-primary={hintsAvailable}>{$hints}</span>
	{/if}
</button>

	<!-- <button class="btn btn-round" disabled={$gamePaused} on:click={handleSolveStrategy} title="Solve Strategy">
			<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 2L2 7l10 5 10-5-10-5z" />
			</svg>
	</button> -->


    <!-- 这里不需要note功能 -->
	<!-- <button class="btn btn-round btn-badge" on:click={notes.toggle} title="Notes ({$notes ? 'ON' : 'OFF'})">
		<svg class="icon-outline" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
			<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z" />
		</svg>

		<span class="badge tracking-tighter" class:badge-primary={$notes}>{$notes ? 'ON' : 'OFF'}</span>
	</button> -->

</div>
<!-- <div id="strategy-display"></div> -->

<style>
	.action-buttons {
		@apply flex flex-wrap justify-evenly self-end;
	}

	.btn-badge {
		@apply relative;
	}

	.badge {
		min-height: 20px;
		min-width:  20px;
		@apply p-1 rounded-full leading-none text-center text-xs text-white bg-gray-600 inline-block absolute top-0 left-0;
	}

	.badge-primary {
		@apply bg-primary;
	}
</style>