<script lang="ts">
	const days = [
		{
			date: 'Jumat, 1 Mei 2026',
			label: 'Hari 1',
			color: '#4facfe',
			routes: [
				{
					id: 1, from: 'Stasiun Rangkasbitung', to: 'Stasiun Pondok Ranji',
					fromCoord: '-6.3540,106.2528', toCoord: '-6.2870,106.7320',
					mode: 'KRL Commuter Line', modeIcon: '🚆',
					departure: '12:00', arrival: '14:00 - 14:30',
					distanceKm: 65, fastest: '2 jam', slowest: '2.5 jam',
					toll: null, tollCost: null,
					notes: '8 orang dari Rangkasbitung. Beli tiket KRL di stasiun.',
					people: '👨‍👩‍👧‍👦 8 orang'
				},
				{
					id: 2, from: 'Stasiun Pondok Ranji', to: 'Kota Bandung',
					fromCoord: '-6.2870,106.7320', toCoord: '-6.9175,107.6191',
					mode: '2 Mobil (dijemput Rani & Rendra)', modeIcon: '🚗',
					departure: '~14:30', arrival: '17:30 - 19:30',
					distanceKm: 180, fastest: '3 jam', slowest: '5 jam',
					toll: 'Tol Jakarta-Cikampek-Padalarang-Pasteur', tollCost: 'Rp 110.000 - 130.000/mobil',
					notes: 'Total 10 orang, 2 mobil. Lewat Tol Cipularang.',
					people: '👨‍👩‍👧‍👦 10 orang • 🚘 2 mobil'
				},
				{
					id: 3, from: 'Jalan-jalan & Makan Malam', to: 'Sekitar Kota Bandung',
					fromCoord: '-6.9175,107.6191', toCoord: '-6.9175,107.6191',
					mode: 'Aktivitas', modeIcon: '🍽️',
					departure: '~18:00', arrival: '~20:30',
					distanceKm: null, fastest: '2-3 jam', slowest: null,
					toll: null, tollCost: null,
					notes: 'Wisata kuliner malam di Braga / Cibadak / Dago',
					people: '👨‍👩‍👧‍👦 10 orang'
				},
				{
					id: 4, from: 'Kota Bandung', to: 'Villa Samakta Guest House (Lembang)',
					fromCoord: '-6.9175,107.6191', toCoord: '-6.8131,107.6186',
					mode: '2 Mobil', modeIcon: '🚗',
					departure: '~21:00', arrival: '21:30 - 22:00',
					distanceKm: 15, fastest: '30 menit', slowest: '1 jam',
					toll: null, tollCost: null,
					notes: 'Menginap di Villa. Check-in tgl 1 & 2 Mei.',
					people: '👨‍👩‍👧‍👦 10 orang • 🚘 2 mobil'
				}
			]
		},
		{
			date: 'Sabtu, 2 Mei 2026',
			label: 'Hari 2',
			color: '#00d2a0',
			routes: [
				{
					id: 5, from: 'Villa Samakta (Lembang)', to: 'Wisata & Makan Siang',
					fromCoord: '-6.8131,107.6186', toCoord: '-6.8100,107.6100',
					mode: '2 Mobil', modeIcon: '🚗',
					departure: '09:00', arrival: '~09:30',
					distanceKm: 5, fastest: '15 menit', slowest: '30 menit',
					toll: null, tollCost: null,
					notes: 'Wisata di sekitar Lembang + makan siang. Lihat tab Wisata untuk rekomendasi.',
					people: '👨‍👩‍👧‍👦 10 orang • 🚘 2 mobil'
				},
				{
					id: 6, from: 'Area Bandung/Lembang', to: 'Rumah Saudara (Tasikmalaya)',
					fromCoord: '-6.8131,107.6186', toCoord: '-7.3177507,108.2215219',
					mode: '2 Mobil', modeIcon: '🚗',
					departure: '~13:00', arrival: '17:00 - 18:00',
					distanceKm: 130, fastest: '3 jam', slowest: '4.5 jam',
					toll: 'Tol Padalarang-Cileunyi-Tasikmalaya', tollCost: 'Rp 90.000 - 120.000/mobil',
					notes: 'Target sampai jam 5-6 sore. Menginap di rumah saudara.',
					people: '👨‍👩‍👧‍👦 10 orang • 🚘 2 mobil'
				}
			]
		},
		{
			date: 'Minggu, 3 Mei 2026',
			label: 'Hari 3',
			color: '#ff8c42',
			routes: [
				{
					id: 7, from: 'Rumah Saudara', to: 'Akad & Resepsi Pernikahan',
					fromCoord: '-7.3177507,108.2215219', toCoord: '-7.3054637,108.2489170',
					mode: '2 Mobil', modeIcon: '🚗',
					departure: '15:00', arrival: '~15:20',
					distanceKm: 4, fastest: '15 menit', slowest: '30 menit',
					toll: null, tollCost: null,
					notes: 'Acara pernikahan sampai jam 9 malam.',
					people: '👨‍👩‍👧‍👦 10 orang'
				},
				{
					id: 8, from: 'Lokasi Resepsi', to: 'Rumah (Rangkasbitung)',
					fromCoord: '-7.3054637,108.2489170', toCoord: '-6.3512907,106.2626178',
					mode: 'Mobil 1 (Keluarga)', modeIcon: '🚗',
					departure: '21:00', arrival: '02:00 - 04:00',
					distanceKm: 310, fastest: '5 jam', slowest: '7 jam',
					toll: 'Tol Tasik-Bandung-Jakarta-Serang', tollCost: 'Rp 180.000 - 220.000',
					notes: 'Perjalanan malam. Istirahat di rest area jika perlu.',
					people: '👨‍👩‍👧‍👦 8 orang • 🚘 Mobil 1'
				},
				{
					id: 9, from: 'Lokasi Resepsi', to: 'Rumah Rani & Rendra (Depok)',
					fromCoord: '-7.3054637,108.2489170', toCoord: '-6.4251692,106.7857706',
					mode: 'Mobil 2 (Rani & Rendra)', modeIcon: '🚗',
					departure: '21:00', arrival: '01:00 - 03:00',
					distanceKm: 240, fastest: '4 jam', slowest: '6 jam',
					toll: 'Tol Tasik-Bandung-Cipularang-Jakarta', tollCost: 'Rp 150.000 - 190.000',
					notes: 'Rani & Rendra pulang ke Depok. Hati-hati di jalan.',
					people: '👤 Rani & Rendra • 🚘 Mobil 2'
				}
			]
		}
	];

	function getNavUrl(fromCoord: string, toCoord: string) {
		return `https://www.google.com/maps/dir/?api=1&origin=${fromCoord}&destination=${toCoord}&travelmode=driving`;
	}
</script>

<div class="timeline">
	{#each days as day}
		<div class="day-section">
			<div class="day-header" style="--day-color: {day.color}">
				<div class="day-dot"></div>
				<div class="day-info">
					<span class="day-label">{day.label}</span>
					<span class="day-date">{day.date}</span>
				</div>
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
							<span class="route-distance">{route.distanceKm} km</span>
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
										<span class="slow">🐢 {route.slowest}</span>
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
							📍 Navigasi di Google Maps
						</a>
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
	.timeline { display: flex; flex-direction: column; gap: 24px; }

	.day-section { display: flex; flex-direction: column; gap: 12px; }

	.day-header {
		display: flex; align-items: center; gap: 12px;
		padding: 10px 16px; border-radius: 12px;
		background: var(--bg-highlight);
		border: 1px solid var(--border-subtle);
	}
	.day-dot {
		width: 14px; height: 14px; border-radius: 50%;
		background: var(--day-color); box-shadow: 0 0 12px var(--day-color);
		flex-shrink: 0;
	}
	.day-info { display: flex; flex-direction: column; }
	.day-label { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; color: var(--day-color); }
	.day-date { font-size: 15px; font-weight: 600; color: var(--text-primary); }

	.route-card {
		background: var(--bg-card); border-radius: 14px;
		padding: 16px; border: 1px solid var(--border-card);
		display: flex; flex-direction: column; gap: 12px;
		transition: border-color 0.2s;
		box-shadow: var(--shadow-sm);
	}
	.route-card:hover { border-color: var(--border-subtle); }

	.route-header {
		display: flex; align-items: center; gap: 10px;
	}
	.route-mode-icon { font-size: 24px; }
	.route-mode-info { display: flex; flex-direction: column; flex: 1; min-width: 0; }
	.route-mode { font-size: 13px; font-weight: 600; color: var(--text-primary); }
	.route-people { font-size: 11px; color: var(--text-secondary); }
	.route-distance {
		background: var(--bg-highlight-strong); color: var(--accent-blue);
		padding: 4px 10px; border-radius: 20px;
		font-size: 12px; font-weight: 600; white-space: nowrap;
	}

	.route-path {
		display: flex; flex-direction: column; gap: 0;
		padding-left: 4px;
	}
	.path-point { display: flex; align-items: flex-start; gap: 12px; }
	.dot {
		width: 12px; height: 12px; border-radius: 50%;
		margin-top: 4px; flex-shrink: 0;
		border: 2.5px solid;
	}
	.dot-start { border-color: var(--accent-blue); background: transparent; }
	.dot-end { border-color: var(--accent-red); background: var(--accent-red); }
	.path-detail { display: flex; flex-direction: column; }
	.path-time { font-size: 13px; font-weight: 700; color: var(--text-primary); }
	.path-name { font-size: 12px; color: var(--text-secondary); }

	.path-line {
		margin-left: 5px; border-left: 2px dashed var(--border-subtle);
		padding: 8px 0 8px 20px; min-height: 36px;
	}
	.duration-badge {
		display: flex; gap: 12px; flex-wrap: wrap;
	}
	.duration-badge span {
		font-size: 12px; font-weight: 600; color: var(--accent-green);
		background: rgba(0,178,134,0.08); padding: 3px 10px;
		border-radius: 12px;
	}
	.duration-badge .slow { color: var(--accent-orange); background: rgba(230,126,34,0.08); }

	.toll-info {
		display: flex; align-items: flex-start; gap: 10px;
		background: rgba(230,126,34,0.06); padding: 10px 12px;
		border-radius: 10px; border: 1px solid rgba(230,126,34,0.12);
	}
	.toll-icon { font-size: 18px; }
	.toll-detail { display: flex; flex-direction: column; }
	.toll-name { font-size: 11px; color: var(--text-secondary); }
	.toll-cost { font-size: 13px; font-weight: 700; color: var(--accent-orange); }

	.route-notes {
		font-size: 12px; color: var(--text-secondary); line-height: 1.5;
		background: rgba(108,79,216,0.06); padding: 8px 12px;
		border-radius: 8px;
	}

	.nav-button {
		display: flex; align-items: center; justify-content: center; gap: 6px;
		background: var(--gradient-primary);
		color: white; padding: 10px 16px; border-radius: 10px;
		font-size: 13px; font-weight: 600; text-decoration: none;
		transition: opacity 0.2s, transform 0.1s;
	}
	.nav-button:hover { opacity: 0.9; }
	.nav-button:active { transform: scale(0.98); }

	.total-summary {
		background: var(--bg-card); border-radius: 14px; padding: 18px;
		border: 1px solid var(--border-card);
		box-shadow: var(--shadow-sm);
	}
	.total-summary h3 {
		font-size: 15px; font-weight: 700; margin-bottom: 14px; color: var(--text-primary);
	}
	.summary-grid { display: flex; flex-direction: column; gap: 8px; }
	.summary-item {
		display: flex; justify-content: space-between; align-items: center;
		padding: 8px 0; border-bottom: 1px solid var(--border-card);
	}
	.summary-label { font-size: 12px; color: var(--text-secondary); }
	.summary-value { font-size: 13px; font-weight: 600; color: var(--accent-orange); }
	.summary-item.total {
		border-bottom: none; padding-top: 12px; margin-top: 4px;
		border-top: 1px solid var(--border-subtle);
	}
	.summary-item.total .summary-label { font-weight: 700; color: var(--text-primary); font-size: 13px; }
	.summary-item.total .summary-value { color: var(--accent-blue); font-size: 15px; }
</style>
