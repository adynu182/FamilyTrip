<script lang="ts">
	import days from "$lib/data/timeline.json";

	function getNavUrl(fromCoord: string, toCoord: string) {
		return `https://www.google.com/maps/dir/?api=1&origin=${fromCoord}&destination=${toCoord}&travelmode=driving`;
	}

	function getLevelColor(level: string) {
		if (level === "lancar") return "var(--accent-green)";
		if (level === "sedang") return "#f59e0b";
		return "var(--accent-red)";
	}
	function getLevelLabel(level: string) {
		if (level === "lancar") return "🟢 Lancar";
		if (level === "sedang") return "🟡 Sedang";
		return "🔴 Padat";
	}
</script>

<div class="timeline">
	{#each days as day}
		<div class="day-section">
			<div class="day-header" style="--day-color: {day.color}">
				<div class="day-header-left">
					<div class="day-dot"></div>
					<span class="day-date">{day.date}</span>
				</div>
				<span class="day-label-badge">{day.label}</span>
			</div>

			{#each day.routes as route}
				<div class="route-card">
					<div class="route-header">
						<span class="route-mode-icon">{route.modeIcon}</span>
						<div class="route-mode-info">
							<span class="route-mode">{route.mode}</span>
							<span class="route-people">{route.people}</span>
						</div>
						{#if route.distanceKm}
							<span class="route-distance"
								>{route.distanceKm} km</span
							>
						{/if}
					</div>

					<div class="route-path">
						<div class="path-point">
							<div class="dot dot-start"></div>
							<div class="path-detail">
								<span class="path-time">{route.departure}</span>
								<span class="path-name">{route.from}</span>
							</div>
						</div>
						<div class="path-line">
							{#if route.fastest}
								<div class="duration-badge">
									<span>⚡ {route.fastest}</span>
									{#if route.slowest}
										<span class="slow"
											>🐢 {route.slowest}</span
										>
									{/if}
								</div>
							{/if}
						</div>
						<div class="path-point">
							<div class="dot dot-end"></div>
							<div class="path-detail">
								<span class="path-time">{route.arrival}</span>
								<span class="path-name">{route.to}</span>
							</div>
						</div>
					</div>

					{#if route.tollCost}
						<div class="toll-info">
							<span class="toll-icon">🛣️</span>
							<div class="toll-detail">
								<span class="toll-name">{route.toll}</span>
								<span class="toll-cost">{route.tollCost}</span>
							</div>
						</div>
					{/if}

					{#if route.notes}
						<p class="route-notes">💡 {route.notes}</p>
					{/if}

					{#if route.distanceKm && route.fromCoord !== route.toCoord}
						<a
							href={getNavUrl(route.fromCoord, route.toCoord)}
							target="_blank"
							rel="noopener noreferrer"
							class="nav-button"
						>
							📍 Lihat Rute di Google Maps
						</a>
					{/if}

					{#if route.traffic && route.traffic.length > 0}
						<details class="traffic-section">
							<summary class="traffic-section-title">
								<span>🚦 Prediksi Lalu Lintas</span>
								<span class="collapse-icon">▼</span>
							</summary>
							<div class="traffic-content">
								{#each route.traffic as seg}
									<div class="traffic-seg">
										<div class="traffic-seg-header">
											<span class="traffic-seg-route"
												>{seg.route}</span
											>
											<span
												class="traffic-seg-level"
												style="color: {getLevelColor(
													seg.level,
												)}">{getLevelLabel(seg.level)}</span
											>
										</div>
										<div class="traffic-bar">
											<div
												class="traffic-bar-fill"
												style="width:{seg.level === 'lancar'
													? '30'
													: seg.level === 'sedang'
														? '60'
														: '90'}%;background:{getLevelColor(
													seg.level,
												)}"
											></div>
										</div>
										<p class="traffic-pred">{seg.prediction}</p>
										<p class="traffic-tip">💡 {seg.tips}</p>
									</div>
								{/each}
							</div>
						</details>
					{/if}
				</div>
			{/each}
		</div>
	{/each}

	<div class="total-summary">
		<h3>📊 Ringkasan Estimasi Biaya Tol</h3>
		<div class="summary-grid">
			<div class="summary-item">
				<span class="summary-label">Pondok Ranji → Bandung</span>
				<span class="summary-value">Rp 220.000 - 260.000</span>
			</div>
			<div class="summary-item">
				<span class="summary-label">Bandung → Tasikmalaya</span>
				<span class="summary-value">Rp 180.000 - 240.000</span>
			</div>
			<div class="summary-item">
				<span class="summary-label">Tasik → Rangkasbitung</span>
				<span class="summary-value">Rp 180.000 - 220.000</span>
			</div>
			<div class="summary-item">
				<span class="summary-label">Tasik → Depok</span>
				<span class="summary-value">Rp 150.000 - 190.000</span>
			</div>
			<div class="summary-item total">
				<span class="summary-label">Total Estimasi (2 mobil)</span>
				<span class="summary-value">Rp 730.000 - 910.000</span>
			</div>
		</div>
	</div>
</div>

<style>
	.timeline {
		display: flex;
		flex-direction: column;
		gap: 24px;
	}

	.day-section {
		display: flex;
		flex-direction: column;
		gap: 12px;
	}

	.day-header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 10px 16px;
		border-radius: 12px;
		background: var(--bg-highlight);
		border: 1px solid var(--border-subtle);
	}
	.day-header-left {
		display: flex;
		align-items: center;
		gap: 12px;
	}
	.day-dot {
		width: 14px;
		height: 14px;
		border-radius: 50%;
		background: var(--day-color);
		box-shadow: 0 0 12px var(--day-color);
		flex-shrink: 0;
	}
	.day-label-badge {
		font-size: 15px;
		font-weight: 800;
		text-transform: uppercase;
		letter-spacing: 0.05em;
		color: #ffffff;
		background: var(--day-color);
		padding: 6px 14px;
		border-radius: 20px;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
	}
	.day-date {
		font-size: 15px;
		font-weight: 700;
		color: var(--text-primary);
	}

	.route-card {
		background: var(--bg-card);
		border-radius: 14px;
		padding: 16px;
		border: 1px solid var(--border-card);
		display: flex;
		flex-direction: column;
		gap: 12px;
		transition: border-color 0.2s;
		box-shadow: var(--shadow-sm);
	}
	.route-card:hover {
		border-color: var(--border-subtle);
	}

	.route-header {
		display: flex;
		align-items: center;
		gap: 10px;
	}
	.route-mode-icon {
		font-size: 22px;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 44px;
		height: 44px;
		background: rgba(59, 130, 246, 0.12);
		border-radius: 20%;
		flex-shrink: 0;
	}
	.route-mode-info {
		display: flex;
		flex-direction: column;
		flex: 1;
		min-width: 0;
	}
	.route-mode {
		font-size: 13px;
		font-weight: 600;
		color: var(--text-primary);
	}
	.route-people {
		font-size: 11px;
		color: var(--text-secondary);
	}
	.route-distance {
		background: var(--bg-highlight-strong);
		color: var(--accent-blue);
		padding: 4px 10px;
		border-radius: 20px;
		font-size: 12px;
		font-weight: 600;
		white-space: nowrap;
	}

	.route-path {
		display: flex;
		flex-direction: column;
		gap: 0;
		padding-left: 4px;
	}
	.path-point {
		display: flex;
		align-items: flex-start;
		gap: 12px;
	}
	.dot {
		width: 12px;
		height: 12px;
		border-radius: 50%;
		margin-top: 4px;
		flex-shrink: 0;
		border: 2.5px solid;
	}
	.dot-start {
		border-color: var(--accent-blue);
		background: transparent;
	}
	.dot-end {
		border-color: var(--accent-red);
		background: var(--accent-red);
	}
	.path-detail {
		display: flex;
		flex-direction: column;
	}
	.path-time {
		font-size: 13px;
		font-weight: 700;
		color: var(--text-primary);
	}
	.path-name {
		font-size: 12px;
		color: var(--text-secondary);
	}

	.path-line {
		margin-left: 5px;
		border-left: 2px dashed var(--border-subtle);
		padding: 8px 0 8px 20px;
		min-height: 36px;
	}
	.duration-badge {
		display: flex;
		gap: 12px;
		flex-wrap: wrap;
	}
	.duration-badge span {
		font-size: 12px;
		font-weight: 600;
		color: var(--accent-green);
		background: rgba(0, 178, 134, 0.08);
		padding: 3px 10px;
		border-radius: 12px;
	}
	.duration-badge .slow {
		color: var(--accent-orange);
		background: rgba(230, 126, 34, 0.08);
	}

	.toll-info {
		display: flex;
		align-items: flex-start;
		gap: 10px;
		background: rgba(230, 126, 34, 0.06);
		padding: 10px 12px;
		border-radius: 10px;
		border: 1px solid rgba(230, 126, 34, 0.12);
	}
	.toll-icon {
		font-size: 18px;
	}
	.toll-detail {
		display: flex;
		flex-direction: column;
	}
	.toll-name {
		font-size: 11px;
		color: var(--text-secondary);
	}
	.toll-cost {
		font-size: 13px;
		font-weight: 700;
		color: var(--accent-orange);
	}

	.route-notes {
		font-size: 12px;
		color: var(--text-secondary);
		line-height: 1.5;
		background: rgba(108, 79, 216, 0.06);
		padding: 8px 12px;
		border-radius: 8px;
	}

	.nav-button {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 6px;
		background: var(--gradient-primary);
		color: white;
		padding: 10px 16px;
		border-radius: 10px;
		font-size: 13px;
		font-weight: 600;
		text-decoration: none;
		transition:
			opacity 0.2s,
			transform 0.1s;
	}
	.nav-button:hover {
		opacity: 0.9;
	}
	.nav-button:active {
		transform: scale(0.98);
	}

	.total-summary {
		background: var(--bg-card);
		border-radius: 14px;
		padding: 18px;
		border: 1px solid var(--border-card);
		box-shadow: var(--shadow-sm);
	}
	.total-summary h3 {
		font-size: 15px;
		font-weight: 700;
		margin-bottom: 14px;
		color: var(--text-primary);
	}
	.summary-grid {
		display: flex;
		flex-direction: column;
		gap: 8px;
	}
	.summary-item {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 8px 0;
		border-bottom: 1px solid var(--border-card);
	}
	.summary-label {
		font-size: 12px;
		color: var(--text-secondary);
	}
	.summary-value {
		font-size: 13px;
		font-weight: 600;
		color: var(--accent-orange);
	}
	.summary-item.total {
		border-bottom: none;
		padding-top: 12px;
		margin-top: 4px;
		border-top: 1px solid var(--border-subtle);
	}
	.summary-item.total .summary-label {
		font-weight: 700;
		color: var(--text-primary);
		font-size: 13px;
	}
	.summary-item.total .summary-value {
		color: var(--accent-blue);
		font-size: 15px;
	}

	.traffic-section {
		border-top: 1px solid var(--border-subtle);
		padding-top: 12px;
	}
	.traffic-section-title {
		font-size: 12px;
		font-weight: 700;
		color: var(--text-secondary);
		text-transform: uppercase;
		letter-spacing: 0.05em;
		margin-bottom: 2px;
		cursor: pointer;
		display: flex;
		justify-content: space-between;
		align-items: center;
		list-style: none;
		user-select: none;
	}
	.traffic-section-title::-webkit-details-marker {
		display: none;
	}
	.collapse-icon {
		font-size: 10px;
		transition: transform 0.3s ease;
	}
	details[open] .collapse-icon {
		transform: rotate(180deg);
	}
	.traffic-content {
		display: flex;
		flex-direction: column;
		gap: 10px;
		margin-top: 10px;
	}
	.traffic-seg {
		display: flex;
		flex-direction: column;
		gap: 4px;
		padding: 10px 12px;
		background: var(--bg-highlight);
		border-radius: 10px;
	}
	.traffic-seg-header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 8px;
	}
	.traffic-seg-route {
		font-size: 12px;
		font-weight: 600;
		color: var(--text-primary);
	}
	.traffic-seg-level {
		font-size: 11px;
		font-weight: 700;
		white-space: nowrap;
	}
	.traffic-bar {
		height: 5px;
		background: var(--border-subtle);
		border-radius: 4px;
		overflow: hidden;
		margin: 2px 0;
	}
	.traffic-bar-fill {
		height: 100%;
		border-radius: 4px;
		transition: width 0.4s;
	}
	.traffic-pred {
		font-size: 11px;
		color: var(--text-secondary);
		line-height: 1.4;
	}
	.traffic-tip {
		font-size: 11px;
		color: var(--text-secondary);
		background: rgba(108, 79, 216, 0.06);
		padding: 6px 8px;
		border-radius: 6px;
		line-height: 1.4;
	}
</style>
