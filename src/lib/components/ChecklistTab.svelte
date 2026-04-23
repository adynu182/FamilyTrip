<script>
	let checklistData = $state([
		{
			category: '👜 Pakaian & Perlengkapan',
			items: [
				{ text: 'Baju ganti 3 hari (+ cadangan 1)', done: false },
				{ text: 'Jaket tebal (Lembang dingin)', done: false },
				{ text: 'Pakaian formal untuk acara pernikahan', done: false },
				{ text: 'Sandal & sepatu nyaman', done: false },
				{ text: 'Jas hujan / payung lipat', done: false },
				{ text: 'Perlengkapan mandi (sabun, shampoo, sikat gigi)', done: false },
				{ text: 'Handuk kecil', done: false }
			]
		},
		{
			category: '💊 Kesehatan & P3K',
			items: [
				{ text: 'Obat pribadi (darah tinggi, maag, dll)', done: false },
				{ text: 'Obat anti mabuk (Antimo)', done: false },
				{ text: 'Paracetamol / Ibuprofen', done: false },
				{ text: 'Minyak kayu putih / balsem', done: false },
				{ text: 'Plester & antiseptik', done: false },
				{ text: 'Obat diare (Entrostop/Norit)', done: false },
				{ text: 'Masker & hand sanitizer', done: false },
				{ text: 'Tisu basah & kering', done: false }
			]
		},
		{
			category: '📱 Elektronik',
			items: [
				{ text: 'Charger HP & kabel data', done: false },
				{ text: 'Power bank (terisi penuh)', done: false },
				{ text: 'Charger mobil', done: false },
				{ text: 'Kamera / GoPro (opsional)', done: false },
				{ text: 'Earphone / headset', done: false }
			]
		},
		{
			category: '📄 Dokumen',
			items: [
				{ text: 'KTP semua anggota', done: false },
				{ text: 'SIM pengemudi', done: false },
				{ text: 'STNK kendaraan', done: false },
				{ text: 'Kartu BPJS / asuransi kesehatan', done: false },
				{ text: 'Uang cash secukupnya', done: false },
				{ text: 'Kartu e-toll (isi saldo min Rp 500.000)', done: false },
				{ text: 'Bukti booking villa (screenshot)', done: false }
			]
		},
		{
			category: '🚗 Kendaraan',
			items: [
				{ text: 'Cek oli mesin & radiator', done: false },
				{ text: 'Cek tekanan ban & ban serep', done: false },
				{ text: 'Cek air wiper & lampu', done: false },
				{ text: 'Dongkrak & kunci roda', done: false },
				{ text: 'Isi bensin penuh', done: false },
				{ text: 'Segitiga pengaman', done: false },
				{ text: 'Pastikan AC mobil berfungsi', done: false }
			]
		},
		{
			category: '🍼 Anak-anak',
			items: [
				{ text: 'Snack & minuman perjalanan', done: false },
				{ text: 'Bantal leher / selimut kecil', done: false },
				{ text: 'Mainan / tablet untuk hiburan', done: false },
				{ text: 'Kantong plastik (jaga-jaga mual)', done: false },
				{ text: 'Susu / makanan bayi (jika ada)', done: false }
			]
		}
	]);

	const tips = [
		{ icon: '⛽', title: 'Isi Bensin Penuh', desc: 'Isi bensin di SPBU sebelum masuk tol. Harga di rest area lebih mahal.' },
		{ icon: '🛣️', title: 'Isi Saldo e-Toll', desc: 'Pastikan saldo e-toll minimal Rp 500.000 untuk pulang-pergi.' },
		{ icon: '😴', title: 'Istirahat Cukup', desc: 'Setiap 2 jam berkendara, istirahat 15-30 menit di rest area.' },
		{ icon: '🌙', title: 'Perjalanan Malam', desc: 'Untuk perjalanan malam (Tasik→Rumah), siapkan kopi & bergantian menyetir.' },
		{ icon: '📱', title: 'Share Live Location', desc: 'Aktifkan share location di WhatsApp agar keluarga tahu posisi.' },
		{ icon: '🍱', title: 'Bekal Makanan', desc: 'Bawa bekal untuk di perjalanan, terutama malam hari saat warung tutup.' },
		{ icon: '💧', title: 'Air Minum', desc: 'Bawa minimal 2 botol air besar per mobil.' },
		{ icon: '🧊', title: 'Cooler Box', desc: 'Bawa cooler box kecil untuk menyimpan minuman & makanan tetap segar.' },
		{ icon: '🗺️', title: 'Download Offline Maps', desc: 'Download peta offline Bandung & Tasikmalaya di Google Maps sebelum berangkat.' },
		{ icon: '☀️', title: 'Cuaca Lembang', desc: 'Suhu Lembang 15-22°C, bawa jaket tebal terutama malam hari.' }
	];

	let totalItems = $derived(checklistData.reduce((sum, cat) => sum + cat.items.length, 0));
	let checkedItems = $derived(checklistData.reduce((sum, cat) => sum + cat.items.filter(i => i.done).length, 0));
	let progress = $derived(totalItems > 0 ? Math.round((checkedItems / totalItems) * 100) : 0);
</script>

<div class="checklist">
	<div class="progress-card">
		<div class="progress-header">
			<span class="progress-title">📋 Progres Persiapan</span>
			<span class="progress-count">{checkedItems}/{totalItems}</span>
		</div>
		<div class="progress-bar">
			<div class="progress-fill" style="width: {progress}%"></div>
		</div>
		<span class="progress-pct">{progress}% siap</span>
	</div>

	{#each checklistData as category}
		<div class="check-section">
			<h3 class="check-cat">{category.category}</h3>
			{#each category.items as item}
				<label class="check-item" class:checked={item.done}>
					<input type="checkbox" bind:checked={item.done} />
					<span class="checkmark">{item.done ? '✅' : '⬜'}</span>
					<span class="check-text">{item.text}</span>
				</label>
			{/each}
		</div>
	{/each}

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
	.checklist { display: flex; flex-direction: column; gap: 18px; }

	.progress-card {
		background: linear-gradient(135deg, rgba(43,125,233,0.1), rgba(108,79,216,0.1));
		border: 1px solid var(--border-subtle);
		border-radius: 14px; padding: 16px;
		display: flex; flex-direction: column; gap: 8px;
	}
	.progress-header { display: flex; justify-content: space-between; align-items: center; }
	.progress-title { font-size: 14px; font-weight: 700; color: var(--text-primary); }
	.progress-count { font-size: 13px; font-weight: 600; color: var(--accent-blue); }
	.progress-bar {
		height: 8px; background: var(--bg-highlight-strong); border-radius: 8px; overflow: hidden;
	}
	.progress-fill {
		height: 100%; border-radius: 8px;
		background: var(--gradient-green);
		transition: width 0.4s ease;
	}
	.progress-pct { font-size: 11px; color: var(--text-secondary); text-align: right; }

	.check-section {
		background: var(--bg-card); border-radius: 14px; padding: 14px;
		border: 1px solid var(--border-card);
		display: flex; flex-direction: column; gap: 6px;
		box-shadow: var(--shadow-sm);
	}
	.check-cat { font-size: 14px; font-weight: 700; color: var(--text-primary); margin-bottom: 4px; }

	.check-item {
		display: flex; align-items: center; gap: 10px;
		padding: 8px 6px; border-radius: 8px; cursor: pointer;
		transition: background 0.15s;
	}
	.check-item:hover { background: var(--bg-highlight); }
	.check-item input { display: none; }
	.checkmark { font-size: 18px; flex-shrink: 0; }
	.check-text { font-size: 13px; color: var(--text-primary); }
	.check-item.checked .check-text { color: var(--text-muted); text-decoration: line-through; }

	.tips-section {
		background: var(--bg-card); border-radius: 14px; padding: 14px;
		border: 1px solid var(--border-card);
		box-shadow: var(--shadow-sm);
	}
	.tips-title { font-size: 15px; font-weight: 700; color: var(--text-primary); margin-bottom: 12px; }
	.tips-list { display: flex; flex-direction: column; gap: 8px; }

	.tip-card {
		display: flex; align-items: flex-start; gap: 10px;
		padding: 10px; border-radius: 10px;
		background: var(--bg-highlight);
	}
	.tip-icon { font-size: 22px; flex-shrink: 0; }
	.tip-info { display: flex; flex-direction: column; }
	.tip-name { font-size: 13px; font-weight: 600; color: var(--text-primary); }
	.tip-desc { font-size: 11px; color: var(--text-secondary); line-height: 1.4; }
</style>
