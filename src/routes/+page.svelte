<script>
	import TimelineTab from "$lib/components/TimelineTab.svelte";
	import WisataTab from "$lib/components/WisataTab.svelte";
	import EmergencyTab from "$lib/components/EmergencyTab.svelte";
	import ChecklistTab from "$lib/components/ChecklistTab.svelte";
	import Icon from "@iconify/svelte";

	let activeTab = $state("timeline");

	const tabs = [
		{ id: "timeline", label: "Jadwal", icon: "solar:calendar-bold" },
		{ id: "wisata", label: "Wisata", icon: "solar:camera-bold" },
		{ id: "darurat", label: "Darurat", icon: "solar:danger-triangle-bold" },
		{ id: "checklist", label: "Checklist", icon: "solar:checklist-bold" },
	];
</script>

<div class="app-container">
	<header class="app-header">
		<div class="header-content">
			<div class="header-title">
				<span class="header-emoji">🚗</span>
				<div>
					<h1>Trip Keluarga</h1>
					<p class="header-subtitle">Bandung & Tasikmalaya</p>
				</div>
			</div>
			<div class="header-badge">
				<span class="badge-people">👨‍👩‍👧‍👦 10</span>
				<span class="badge-cars">🚘 2</span>
			</div>
		</div>
	</header>

	<main class="app-main">
		{#if activeTab === "timeline"}
			<TimelineTab />
		{:else if activeTab === "wisata"}
			<WisataTab />
		{:else if activeTab === "darurat"}
			<EmergencyTab />
		{:else if activeTab === "checklist"}
			<ChecklistTab />
		{/if}
	</main>

	<nav class="bottom-nav">
		{#each tabs as tab}
			<button
				class="nav-tab"
				class:active={activeTab === tab.id}
				onclick={() => (activeTab = tab.id)}
				id={`tab-${tab.id}`}
			>
				<span class="nav-icon">
					<Icon icon={tab.icon} width="22" />
				</span>
				<span class="nav-label">{tab.label}</span>
				{#if activeTab === tab.id}
					<div class="nav-indicator"></div>
				{/if}
			</button>
		{/each}
	</nav>
</div>

<style>
	.app-container {
		min-height: 100dvh;
		display: flex;
		flex-direction: column;
		max-width: 480px;
		margin: 0 auto;
		position: relative;
	}

	.app-header {
		position: sticky;
		top: 0;
		z-index: 100;
		background: var(--header-bg);
		border-bottom: 1px solid var(--border-subtle);
		backdrop-filter: blur(20px);
	}

	.header-content {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 14px 18px;
	}

	.header-title {
		display: flex;
		align-items: center;
		gap: 12px;
	}

	.header-emoji {
		font-size: 28px;
		filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.15));
	}

	.header-title h1 {
		font-size: 18px;
		font-weight: 700;
		color: #ffffff;
		line-height: 1.2;
	}

	.header-subtitle {
		font-size: 11px;
		color: rgba(255, 255, 255, 0.9);
		font-weight: 400;
		margin-top: 2px;
	}

	.header-badge {
		display: flex;
		gap: 8px;
		align-items: center;
	}

	.header-badge span {
		background: rgba(255, 255, 255, 0.2);
		border: 1px solid rgba(255, 255, 255, 0.3);
		padding: 4px 10px;
		border-radius: 20px;
		font-size: 12px;
		font-weight: 500;
		color: #ffffff;
	}

	.app-main {
		flex: 1;
		padding: 16px;
		padding-bottom: calc(var(--tab-height) + 20px);
		overflow-y: auto;
	}

	.bottom-nav {
		position: fixed;
		bottom: 0;
		left: 50%;
		transform: translateX(-50%);
		width: 100%;
		max-width: 480px;
		height: var(--tab-height);
		background: var(--nav-bg);
		backdrop-filter: blur(20px);
		border-top: 1px solid var(--border-subtle);
		display: flex;
		align-items: center;
		justify-content: space-around;
		padding: 0 4px;
		z-index: 200;
	}

	.nav-tab {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		gap: 3px;
		padding: 8px 4px;
		background: none;
		color: var(--text-muted);
		transition: all 0.25s ease;
		position: relative;
		flex: 1;
		min-width: 0;
	}

	.nav-tab.active {
		color: var(--accent-blue);
		background: rgba(43, 125, 233, 0.12);
		border-radius: 12px;
	}

	.nav-icon {
		font-size: 22px;
		transition: transform 0.25s ease;
	}

	.nav-tab.active .nav-icon {
		transform: scale(1.15);
	}

	.nav-label {
		font-size: 10px;
		font-weight: 600;
		letter-spacing: 0.02em;
		white-space: nowrap;
	}

	.nav-indicator {
		position: absolute;
		top: 0;
		left: 50%;
		transform: translateX(-50%);
		width: 32px;
		height: 3px;
		background: var(--gradient-primary);
		border-radius: 0 0 4px 4px;
	}

	@media (min-width: 481px) {
		.app-container {
			border-left: 1px solid var(--border-card);
			border-right: 1px solid var(--border-card);
		}
	}
</style>
