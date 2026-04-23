<script>
	let filter = $state("semua");
	let searchQuery = $state("");

	import Icon from "@iconify/svelte";

	const categories = [
		{ id: "semua", label: "Semua", icon: "solar:target-bold" },
		{ id: "wisata", label: "Wisata", icon: "solar:mountain-bold" },
		{ id: "kuliner", label: "Kuliner", icon: "solar:noodles-bold" },
		{ id: "oleh", label: "Oleh-oleh", icon: "solar:gift-bold" },
		{ id: "unik", label: "Unik", icon: "solar:sparkle-bold" },
	];

	import places from "$lib/data/wisata.json";

	let filteredPlaces = $derived(
		places.filter((p) => {
			const matchCat = filter === "semua" || p.cat === filter;
			const matchSearch =
				!searchQuery ||
				p.name.toLowerCase().includes(searchQuery.toLowerCase());
			return matchCat && matchSearch;
		}),
	);
</script>

<div class="wisata">
	<div class="search-box">
		<span class="search-icon"
			><Icon icon="solar:magnifer-bold" width="18" /></span
		>
		<input
			type="text"
			placeholder="Cari tempat..."
			bind:value={searchQuery}
		/>
	</div>

	<div class="filter-row">
		{#each categories as cat}
			<button
				class="filter-chip"
				class:active={filter === cat.id}
				onclick={() => (filter = cat.id)}
			>
				<span><Icon icon={cat.icon} width="16" /></span>
				{cat.label}
			</button>
		{/each}
	</div>

	<p class="result-count">{filteredPlaces.length} tempat ditemukan</p>

	<div class="places-list">
		{#each filteredPlaces as place, i}
			<div class="place-card">
				<div class="place-header">
					<div class="place-num">{i + 1}</div>
					<div class="place-title">
						<h3>{place.name}</h3>
						<span class="place-cat">
							<Icon
								icon={categories.find((c) => c.id === place.cat)
									?.icon ?? "solar:target-bold"}
								width="13"
							/>
							{categories.find((c) => c.id === place.cat)?.label}
						</span>
					</div>
				</div>
				<p class="place-desc">{place.desc}</p>
				<div class="place-meta">
					{#if place.tiket !== "-" && place.tiket !== "Gratis"}
						<div class="meta-item">
							<span class="meta-label">🎟️ Tiket</span>
							<span class="meta-value ticket">{place.tiket}</span>
						</div>
					{/if}
					<div class="meta-item">
						<span class="meta-label">💰 Spend Money</span>
						<span class="meta-value spend">{place.spend}</span>
					</div>
					<div class="meta-item">
						<span class="meta-label">🕐 Jam Buka</span>
						<span class="meta-value hours">{place.jam}</span>
					</div>
				</div>
				{#if place.menu}
					<div class="place-menu">
						<span>🍽️</span>
						{place.menu}
					</div>
				{/if}
				<div class="place-tips">
					<span>💡</span>
					{place.tips}
				</div>
				{#if place.ig || place.web || place.maps}
					<div class="place-links">
						{#if place.ig}
							<a
								href={place.ig}
								target="_blank"
								rel="noopener noreferrer"
								class="link-btn ig"
							>
								<Icon icon="mdi:instagram" width="14" /> Instagram
							</a>
						{/if}
						{#if place.web}
							<a
								href={place.web}
								target="_blank"
								rel="noopener noreferrer"
								class="link-btn web"
							>
								<Icon icon="mdi:web" width="14" /> Website
							</a>
						{/if}
						{#if place.maps}
							<a
								href={place.maps}
								target="_blank"
								rel="noopener noreferrer"
								class="link-btn maps"
							>
								<Icon icon="mdi:map-marker" width="14" /> Maps
							</a>
						{/if}
					</div>
				{/if}
			</div>
		{/each}
	</div>
</div>

<style>
	.wisata {
		display: flex;
		flex-direction: column;
		gap: 14px;
	}

	.search-box {
		display: flex;
		align-items: center;
		gap: 10px;
		background: var(--bg-card);
		border-radius: 12px;
		padding: 10px 14px;
		border: 1px solid var(--border-subtle);
		box-shadow: var(--shadow-sm);
	}
	.search-icon {
		font-size: 18px;
	}
	.search-box input {
		flex: 1;
		background: none;
		border: none;
		outline: none;
		color: var(--text-primary);
		font-size: 14px;
	}
	.search-box input::placeholder {
		color: var(--text-muted);
	}

	.filter-row {
		display: flex;
		gap: 6px;
		overflow-x: auto;
		padding-bottom: 4px;
		scrollbar-width: none;
	}
	.filter-row::-webkit-scrollbar {
		display: none;
	}

	.filter-chip {
		display: flex;
		align-items: center;
		gap: 4px;
		padding: 7px 12px;
		border-radius: 20px;
		white-space: nowrap;
		background: var(--bg-highlight);
		color: var(--text-secondary);
		font-size: 12px;
		font-weight: 500;
		border: 1px solid var(--border-subtle);
		transition: all 0.2s;
	}
	.filter-chip.active {
		background: var(--gradient-primary);
		color: white;
		border-color: transparent;
	}

	.result-count {
		font-size: 12px;
		color: var(--text-muted);
	}

	.places-list {
		display: flex;
		flex-direction: column;
		gap: 10px;
	}

	.place-card {
		background: var(--bg-card);
		border-radius: 14px;
		padding: 14px;
		border: 1px solid var(--border-card);
		display: flex;
		flex-direction: column;
		gap: 10px;
		box-shadow: var(--shadow-sm);
	}
	.place-header {
		display: flex;
		align-items: center;
		gap: 12px;
	}
	.place-num {
		width: 28px;
		height: 28px;
		border-radius: 8px;
		background: var(--gradient-primary);
		color: white;
		font-size: 18px;
		font-weight: 700;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-shrink: 0;
	}
	.place-title {
		flex: 1;
		min-width: 0;
	}
	.place-title h3 {
		font-size: 14px;
		font-weight: 700;
		color: var(--text-primary);
		line-height: 1.3;
	}
	.place-cat {
		font-size: 11px;
		color: var(--text-secondary);
	}

	.place-desc {
		font-size: 12px;
		color: var(--text-secondary);
		line-height: 1.5;
	}

	.place-meta {
		display: flex;
		gap: 8px;
		flex-wrap: wrap;
	}
	.meta-item {
		display: flex;
		flex-direction: column;
		gap: 2px;
		background: var(--bg-highlight);
		padding: 6px 10px;
		border-radius: 8px;
		flex: 1;
		min-width: 80px;
	}
	.meta-label {
		font-size: 10px;
		color: var(--text-muted);
	}
	.meta-value {
		font-size: 12px;
		font-weight: 700;
	}
	.meta-value.ticket {
		color: var(--accent-blue);
	}
	.meta-value.spend {
		color: var(--accent-orange);
	}
	.meta-value.hours {
		color: var(--accent-green);
	}

	.place-menu {
		font-size: 11px;
		color: var(--text-secondary);
		line-height: 1.4;
		background: rgba(43, 125, 233, 0.05);
		padding: 8px 10px;
		border-radius: 8px;
		display: flex;
		gap: 6px;
		align-items: flex-start;
	}

	.place-tips {
		font-size: 11px;
		color: var(--text-secondary);
		line-height: 1.4;
		background: rgba(108, 79, 216, 0.06);
		padding: 8px 10px;
		border-radius: 8px;
		display: flex;
		gap: 6px;
		align-items: flex-start;
	}

	.place-links {
		display: flex;
		flex-wrap: wrap;
		gap: 8px;
		margin-top: 4px;
	}

	.link-btn {
		display: inline-flex;
		align-items: center;
		gap: 4px;
		padding: 6px 10px;
		border-radius: 8px;
		font-size: 11px;
		font-weight: 600;
		text-decoration: none;
		transition:
			opacity 0.2s,
			transform 0.1s;
	}
	.link-btn:hover {
		opacity: 0.8;
	}
	.link-btn:active {
		transform: scale(0.96);
	}
	.link-btn.ig {
		background: rgba(225, 48, 108, 0.1);
		color: #e1306c;
	}
	.link-btn.web {
		background: rgba(59, 130, 246, 0.1);
		color: #3b82f6;
	}
	.link-btn.maps {
		background: rgba(34, 197, 94, 0.1);
		color: #16a34a;
	}
</style>
