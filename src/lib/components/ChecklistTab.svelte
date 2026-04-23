<script lang="ts">
	const STORAGE_KEY = 'familytrip_checklist';

	import checklistData from '$lib/data/checklist.json';
	const defaultData = checklistData.categories;

	function loadChecks(): boolean[][] {
		if (typeof window === 'undefined') return defaultData.map(c => c.items.map(() => false));
		try {
			const raw = localStorage.getItem(STORAGE_KEY);
			if (raw) return JSON.parse(raw);
		} catch {}
		return defaultData.map(c => c.items.map(() => false));
	}

	let checks = $state<boolean[][]>(loadChecks());

	function toggle(ci: number, ii: number) {
		checks[ci][ii] = !checks[ci][ii];
		if (typeof window !== 'undefined') {
			localStorage.setItem(STORAGE_KEY, JSON.stringify(checks));
		}
	}

	function resetAll() {
		checks = defaultData.map(c => c.items.map(() => false));
		if (typeof window !== 'undefined') {
			localStorage.setItem(STORAGE_KEY, JSON.stringify(checks));
		}
	}

	const tips = checklistData.tips;

	let totalItems = $derived(defaultData.reduce((sum, cat) => sum + cat.items.length, 0));
	let checkedItems = $derived(checks.reduce((sum, arr) => sum + arr.filter(Boolean).length, 0));
	let progress = $derived(totalItems > 0 ? Math.round((checkedItems / totalItems) * 100) : 0);
</script>

<div class="checklist">
	<!-- Progress Bar -->
	<div class="progress-card">
		<div class="progress-header">
			<span class="progress-title">📋 Progres Persiapan</span>
			<span class="progress-count">{checkedItems}/{totalItems}</span>
		</div>
		<div class="progress-bar">
			<div class="progress-fill" style="width: {progress}%"></div>
		</div>
		<div class="progress-footer">
			<span class="progress-pct">{progress}% siap</span>
			<button class="reset-btn" onclick={resetAll}>🔄 Reset</button>
		</div>
	</div>

	<!-- Checklist Categories -->
	{#each defaultData as category, ci}
		<div class="cat-section">
			<div class="cat-header">
				<span class="cat-title">{category.category}</span>
			</div>
			<div class="cat-items">
				{#each category.items as item, ii}
					<button
						class="check-row"
						class:is-checked={checks[ci][ii]}
						onclick={() => toggle(ci, ii)}
					>
						<span class="check-box" class:checked={checks[ci][ii]}>
							{#if checks[ci][ii]}
								<svg width="14" height="14" viewBox="0 0 14 14" fill="none">
									<path d="M2.5 7L5.5 10L11.5 4" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
								</svg>
							{/if}
						</span>
						<span class="check-label" class:done={checks[ci][ii]}>{item}</span>
					</button>
				{/each}
			</div>
		</div>
	{/each}

	<!-- Tips Section -->
	<div class="tips-section">
		<h3 class="tips-title">🧳 Tips Perjalanan Jauh</h3>
		<div class="tips-list">
			{#each tips as tip}
				<div class="tip-card">
					<span class="tip-icon">{tip.icon}</span>
					<div class="tip-info">
						<span class="tip-name">{tip.title}</span>
						<span class="tip-desc">{tip.desc}</span>
					</div>
				</div>
			{/each}
		</div>
	</div>
</div>

<style>
	.checklist { display: flex; flex-direction: column; gap: 20px; }

	/* ── Progress Card ── */
	.progress-card {
		background: linear-gradient(135deg, rgba(43,125,233,0.1), rgba(108,79,216,0.1));
		border: 1px solid var(--border-subtle);
		border-radius: 14px; padding: 16px;
		display: flex; flex-direction: column; gap: 8px;
	}
	.progress-header { display: flex; justify-content: space-between; align-items: center; }
	.progress-title { font-size: 14px; font-weight: 700; color: var(--text-primary); }
	.progress-count { font-size: 13px; font-weight: 600; color: var(--accent-blue); }
	.progress-bar { height: 8px; background: var(--bg-highlight-strong); border-radius: 8px; overflow: hidden; }
	.progress-fill { height: 100%; border-radius: 8px; background: var(--gradient-green); transition: width 0.4s ease; }
	.progress-footer { display: flex; justify-content: space-between; align-items: center; }
	.progress-pct { font-size: 11px; color: var(--text-secondary); }
	.reset-btn {
		font-size: 11px; font-weight: 600; color: var(--accent-red);
		background: rgba(231,76,60,0.08); border: 1px solid rgba(231,76,60,0.2);
		padding: 4px 10px; border-radius: 8px; cursor: pointer;
		transition: background 0.15s;
	}
	.reset-btn:hover { background: rgba(231,76,60,0.15); }

	/* ── Category Section ── */
	.cat-section { display: flex; flex-direction: column; gap: 0; }
	.cat-header {
		padding: 6px 4px 10px 4px;
	}
	.cat-title {
		font-size: 12px; font-weight: 700; color: var(--text-secondary);
		text-transform: uppercase; letter-spacing: 0.08em;
	}

	.cat-items { display: flex; flex-direction: column; gap: 6px; }

	/* ── Individual Check Row ── */
	.check-row {
		display: flex; align-items: center; gap: 12px;
		background: var(--bg-card);
		border: 1px solid var(--border-card);
		border-radius: 10px; padding: 12px 14px;
		cursor: pointer; text-align: left; width: 100%;
		transition: background 0.15s, border-color 0.15s;
		box-shadow: var(--shadow-sm);
	}
	.check-row:hover { border-color: var(--border-subtle); }
	.check-row.is-checked {
		background: rgba(0,179,134,0.06);
		border-color: rgba(0,179,134,0.25);
	}

	/* ── Checkbox Box ── */
	.check-box {
		width: 22px; height: 22px; border-radius: 6px; flex-shrink: 0;
		border: 2px solid var(--border-subtle);
		display: flex; align-items: center; justify-content: center;
		background: transparent;
		transition: background 0.15s, border-color 0.15s;
	}
	.check-box.checked {
		background: var(--accent-green);
		border-color: var(--accent-green);
	}

	/* ── Label ── */
	.check-label {
		font-size: 13px; font-weight: 500; color: var(--text-primary);
		line-height: 1.4; flex: 1;
		transition: color 0.15s;
	}
	.check-label.done {
		color: var(--text-muted);
		text-decoration: line-through;
	}

	/* ── Tips Section ── */
	.tips-section {
		background: var(--bg-card); border-radius: 14px; padding: 14px;
		border: 1px solid var(--border-card); box-shadow: var(--shadow-sm);
	}
	.tips-title { font-size: 15px; font-weight: 700; color: var(--text-primary); margin-bottom: 12px; }
	.tips-list { display: flex; flex-direction: column; gap: 8px; }
	.tip-card {
		display: flex; align-items: flex-start; gap: 10px;
		padding: 10px; border-radius: 10px; background: var(--bg-highlight);
	}
	.tip-icon { font-size: 22px; flex-shrink: 0; }
	.tip-info { display: flex; flex-direction: column; }
	.tip-name { font-size: 13px; font-weight: 600; color: var(--text-primary); }
	.tip-desc { font-size: 11px; color: var(--text-secondary); line-height: 1.4; }
</style>
