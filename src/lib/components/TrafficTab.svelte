<script lang="ts">
	const trafficData = [
		{
			date: 'Jumat, 1 Mei 2026',
			label: 'Hari 1',
			color: '#4facfe',
			note: '⚠️ 1 Mei = Hari Buruh Internasional (Libur Nasional). Potensi long weekend.',
			segments: [
				{
					route: 'Rangkasbitung → Pondok Ranji (KRL)',
					time: '12:00 - 14:30',
					level: 'sedang',
					prediction: 'KRL cukup padat di jam siang libur nasional. Berdiri kemungkinan besar.',
					tips: 'Naik dari stasiun awal, peluang dapat tempat duduk lebih besar.'
				},
				{
					route: 'Pondok Ranji → Tol Jakarta-Cikampek',
					time: '14:30 - 16:00',
					level: 'padat',
					prediction: 'Tol Jakarta-Cikampek sangat padat karena arus libur. Bottleneck di KM 47-57.',
					tips: 'Coba lewat Tol Desari-BORR sebagai alternatif ke Bandung via Puncak jika macet parah.'
				},
				{
					route: 'Tol Cipularang',
					time: '16:00 - 18:00',
					level: 'padat',
					prediction: 'Cipularang padat dari arah Jakarta. Tanjakan bisa memperlambat truk.',
					tips: 'Hati-hati di KM 97 (rawan kecelakaan). Nyalakan lampu, jaga jarak.'
				},
				{
					route: 'Masuk Kota Bandung',
					time: '18:00 - 19:00',
					level: 'sedang',
					prediction: 'Akses masuk kota lewat Pasteur agak macet sore hari.',
					tips: 'Keluar di Padalarang jika ingin langsung ke Lembang.'
				},
				{
					route: 'Bandung → Lembang (Villa)',
					time: '21:00 - 22:00',
					level: 'lancar',
					prediction: 'Malam hari relatif lancar menuju Lembang.',
					tips: 'Hati-hati jalanan gelap & berkabut di kawasan Lembang malam hari.'
				}
			]
		},
		{
			date: 'Sabtu, 2 Mei 2026',
			label: 'Hari 2',
			color: '#00d2a0',
			note: '📅 Weekend setelah libur nasional. Wisatawan masih ramai di Bandung.',
			segments: [
				{
					route: 'Lembang Area (Wisata)',
					time: '09:00 - 12:00',
					level: 'sedang',
					prediction: 'Jalur wisata Lembang ramai di weekend. Macet di depan Farm House & Floating Market.',
					tips: 'Datang pagi sebelum jam 10 untuk menghindari macet wisata.'
				},
				{
					route: 'Bandung → Tol Padalarang-Cileunyi',
					time: '13:00 - 14:00',
					level: 'sedang',
					prediction: 'Arus menuju timur (Cileunyi) relatif sedang di siang hari.',
					tips: 'Isi bensin dulu sebelum masuk tol. Rest area Cileunyi biasanya ramai.'
				},
				{
					route: 'Tol Cileunyi → Tasikmalaya',
					time: '14:00 - 17:00',
					level: 'lancar',
					prediction: 'Tol Cipali & Tasikmalaya relatif lancar karena arus balik belum dimulai.',
					tips: 'Istirahat di Rest Area KM 456 jika perlu. Jalanan bagus & lebar.'
				},
				{
					route: 'Exit Tol → Rumah Saudara Tasik',
					time: '17:00 - 18:00',
					level: 'sedang',
					prediction: 'Jalan dalam kota Tasik agak ramai di sore hari.',
					tips: 'Ikuti Google Maps, hindari jam pulang kerja (17:00-18:00).'
				}
			]
		},
		{
			date: 'Minggu, 3 Mei 2026',
			label: 'Hari 3',
			color: '#ff8c42',
			note: '🔴 ARUS BALIK! Minggu malam setelah long weekend = macet berat arah Jakarta.',
			segments: [
				{
					route: 'Rumah Saudara → Lokasi Acara',
					time: '15:00 - 15:30',
					level: 'lancar',
					prediction: 'Jarak dekat dalam kota, tidak ada masalah.',
					tips: 'Berangkat 30 menit sebelumnya untuk parkir & persiapan.'
				},
				{
					route: 'Tasik → Tol menuju Bandung',
					time: '21:00 - 23:00',
					level: 'sedang',
					prediction: 'Arus balik mulai mereda malam hari. Tol Tasik-Bandung cukup lancar.',
					tips: 'Waspada mengantuk. Minum kopi & bergantian menyetir.'
				},
				{
					route: 'Tol Cipularang (arah Jakarta)',
					time: '23:00 - 01:00',
					level: 'sedang',
					prediction: 'Masih ada sisa arus balik tapi sudah mulai lengang malam.',
					tips: 'SANGAT HATI-HATI di Cipularang malam hari. Banyak kecelakaan. Nyalakan lampu jauh jika perlu.'
				},
				{
					route: 'Tol Jakarta-Cikampek → Tangerang',
					time: '01:00 - 03:00',
					level: 'lancar',
					prediction: 'Dini hari sudah sangat lancar. Mobil 2 (Depok) bisa keluar di Jatibening.',
					tips: 'Jaga kecepatan stabil 80-100 km/jam. Jangan ngebut karena kantuk.'
				},
				{
					route: 'Tangerang → Rangkasbitung',
					time: '03:00 - 04:00',
					level: 'lancar',
					prediction: 'Jalur ke Rangkasbitung sangat sepi dini hari.',
					tips: 'Hati-hati truk di jalur Pandeglang. Sampai rumah, langsung istirahat!'
				}
			]
		}
	];

	function getLevelColor(level: string) {
		if (level === 'lancar') return '#00d2a0';
		if (level === 'sedang') return '#ffc107';
		return '#ff4757';
	}

	function getLevelLabel(level: string) {
		if (level === 'lancar') return '🟢 Lancar';
		if (level === 'sedang') return '🟡 Sedang';
		return '🔴 Padat';
	}
</script>

<div class="traffic">
	<div class="traffic-disclaimer">
		<span>ℹ️</span>
		<p>Prediksi ini berdasarkan pola historis lalu lintas pada long weekend & hari libur nasional. Kondisi aktual bisa berbeda.</p>
	</div>

	{#each trafficData as day}
		<div class="traffic-day">
			<div class="traffic-day-header" style="--day-color: {day.color}">
				<div class="day-dot"></div>
				<div>
					<span class="day-label">{day.label}</span>
					<span class="day-date">{day.date}</span>
				</div>
			</div>

			{#if day.note}
				<div class="traffic-note">
					<p>{day.note}</p>
				</div>
			{/if}

			{#each day.segments as seg}
				<div class="traffic-card">
					<div class="traffic-card-header">
						<div class="traffic-route">
							<span class="traffic-route-name">{seg.route}</span>
							<span class="traffic-time">🕐 {seg.time}</span>
						</div>
						<span class="traffic-level" style="color: {getLevelColor(seg.level)}">
							{getLevelLabel(seg.level)}
						</span>
					</div>
					<div class="traffic-bar">
						<div
							class="traffic-bar-fill"
							style="width: {seg.level === 'lancar' ? '30' : seg.level === 'sedang' ? '60' : '90'}%; background: {getLevelColor(seg.level)}"
						></div>
					</div>
					<p class="traffic-pred">{seg.prediction}</p>
					<p class="traffic-tip">💡 {seg.tips}</p>
				</div>
			{/each}
		</div>
	{/each}
</div>

<style>
	.traffic { display: flex; flex-direction: column; gap: 20px; }

	.traffic-disclaimer {
		display: flex; gap: 10px; align-items: flex-start;
		background: var(--bg-highlight); border: 1px solid var(--border-subtle);
		border-radius: 12px; padding: 12px; font-size: 12px; color: var(--text-secondary); line-height: 1.4;
	}

	.traffic-day { display: flex; flex-direction: column; gap: 10px; }

	.traffic-day-header {
		display: flex; align-items: center; gap: 12px;
		padding: 10px 16px; border-radius: 12px;
		background: var(--bg-highlight);
		border: 1px solid var(--border-subtle);
	}
	.day-dot {
		width: 14px; height: 14px; border-radius: 50%;
		background: var(--day-color); box-shadow: 0 0 12px var(--day-color); flex-shrink: 0;
	}
	.day-label { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; color: var(--day-color); display: block; }
	.day-date { font-size: 15px; font-weight: 600; color: var(--text-primary); }

	.traffic-note {
		background: rgba(231,76,60,0.06); border: 1px solid rgba(231,76,60,0.15);
		border-radius: 10px; padding: 10px 12px;
		font-size: 12px; color: var(--accent-orange); font-weight: 500; line-height: 1.4;
	}

	.traffic-card {
		background: var(--bg-card); border-radius: 14px; padding: 14px;
		border: 1px solid var(--border-card);
		display: flex; flex-direction: column; gap: 8px;
		box-shadow: var(--shadow-sm);
	}

	.traffic-card-header { display: flex; justify-content: space-between; align-items: flex-start; gap: 8px; }
	.traffic-route { display: flex; flex-direction: column; flex: 1; min-width: 0; }
	.traffic-route-name { font-size: 13px; font-weight: 600; color: var(--text-primary); }
	.traffic-time { font-size: 11px; color: var(--text-secondary); }
	.traffic-level { font-size: 12px; font-weight: 700; white-space: nowrap; }

	.traffic-bar {
		height: 6px; background: var(--bg-highlight-strong); border-radius: 6px; overflow: hidden;
	}
	.traffic-bar-fill { height: 100%; border-radius: 6px; transition: width 0.5s ease; }

	.traffic-pred { font-size: 12px; color: var(--text-secondary); line-height: 1.5; }
	.traffic-tip {
		font-size: 11px; color: var(--text-secondary);
		background: rgba(108,79,216,0.06); padding: 8px 10px; border-radius: 8px; line-height: 1.4;
	}
</style>
