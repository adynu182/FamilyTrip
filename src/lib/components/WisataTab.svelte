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

	const places = [
		{
			name: "Farmhouse Susu Lembang",
			cat: "wisata",
			tiket: "Rp 35.000",
			spend: "Rp 100.000 - Rp 150.000",
			desc: "Taman hiburan keluarga bertema pedesaan Eropa dengan rumah Hobbit dan penyewaan kostum Belanda.",
			menu: "Susu murni, sosis bakar, steak, pasta.",
			jam: "09:00 - 18:00",
			tips: "Tiket masuk bisa ditukar dengan susu murni atau sosis.",
		},
		{
			name: "Floating Market Lembang",
			cat: "wisata",
			tiket: "Rp 40.000",
			spend: "Rp 150.000 - Rp 200.000",
			desc: "Pasar apung di atas danau dengan beragam kuliner tradisional, wahana perahu, dan Rainbow Garden.",
			menu: "Batagor, sate kelinci, rujak, dimsum, aneka camilan.",
			jam: "09:00 - 18:00",
			tips: "Beli koin khusus untuk transaksi makanan di area perahu.",
		},
		{
			name: "Tangkuban Perahu",
			cat: "wisata",
			tiket: "Rp 20.000 (Dom) / Rp 200.000 (Int)",
			spend: "Rp 50.000 - Rp 100.000",
			desc: "Gunung berapi aktif dengan kawah besar yang ikonik dan jalur trekking yang menantang.",
			menu: "Jagung bakar, bandrek, mie instan (di warung lokal).",
			jam: "08:00 - 17:00",
			tips: "Gunakan masker karena bau belerang cukup kuat.",
		},
		{
			name: "The Great Asia Africa",
			cat: "wisata",
			tiket: "Rp 50.000",
			spend: "Rp 150.000",
			desc: "Taman miniatur bangunan ikonik dari negara-negara Asia dan Afrika (Jepang, Korea, India, dll).",
			menu: "Kimchi, takoyaki, kuliner khas India dan Afrika.",
			jam: "09:00 - 18:00",
			tips: "Gunakan sepatu yang nyaman karena banyak berjalan mendaki/menurun.",
		},
		{
			name: "Orchid Forest Cikole",
			cat: "wisata",
			tiket: "Rp 40.000",
			spend: "Rp 100.000",
			desc: "Hutan pinus dengan koleksi anggrek langka, jembatan kayu gantung, dan Wood Bridge yang cantik di malam hari.",
			menu: "Kopi, snack, masakan Indonesia.",
			jam: "09:00 - 18:00",
			tips: "Datanglah sore hari untuk melihat lampu jembatan mulai menyala.",
		},
		{
			name: "Kampung Daun",
			cat: "kuliner",
			tiket: "Gratis",
			spend: "Rp 100.000 - Rp 250.000",
			desc: "Restoran Sunda dengan nuansa lembah, air terjun, dan lesehan kayu yang sangat asri.",
			menu: "Nasi Liwet, Ikan Bakar, Sambal Terasi, Bandrek.",
			jam: "10:00 - 22:00",
			tips: "Sangat populer saat akhir pekan, disarankan reservasi.",
		},
		{
			name: "Dusun Bambu",
			cat: "wisata",
			tiket: "Rp 25.000 - Rp 40.000",
			spend: "Rp 200.000",
			desc: "Eco-tourism dengan area danau, restoran tepi air, dan fasilitas glamping.",
			menu: "Masakan Sunda, Western, Cafe dessert.",
			jam: "10:00 - 20:00",
			tips: "Naik perahu di danau untuk pengalaman foto terbaik.",
		},
		{
			name: "Tahu Susu Lembang (Pusat)",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 20.000 - Rp 100.000",
			desc: "Pusat oleh-oleh khas Lembang yang terkenal dengan tahu susu lembut dan konsep drive-thru.",
			menu: "Tahu goreng, susu murni, aneka keripik.",
			jam: "08:00 - 19:00",
			tips: "Tahu goreng hangat lebih enak dimakan langsung di tempat.",
		},
		{
			name: "Bolu Susu Lembang",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 35.000 - Rp 70.000",
			desc: "Toko kue bolu lembut dengan bahan dasar susu sapi murni khas Lembang.",
			menu: "Bolu Susu Original, Cokelat, Talas Bogor.",
			jam: "07:00 - 21:00",
			tips: "Varian Original adalah yang paling cepat habis.",
		},
		{
			name: "Sudirman Street Night Market",
			cat: "kuliner",
			tiket: "Gratis",
			spend: "Rp 50.000 - Rp 150.000",
			desc: "Pusat kuliner malam di Bandung kota dengan berbagai pilihan makanan halal dan non-halal.",
			menu: "Babi Panggang, Sate, Martabak, Aneka Seafood.",
			jam: "18:00 - 23:00",
			tips: "Perhatikan label 'Halal' atau 'Non-Halal' di setiap stand.",
		},
		{
			name: "Lembang Park & Zoo",
			cat: "wisata",
			tiket: "Rp 50.000 - Rp 70.000",
			spend: "Rp 150.000",
			desc: "Kebun binatang modern dengan desain arsitektur yang keren dan kafe kucing di dalamnya.",
			menu: "Burger, Rice Bowl, Kopi.",
			jam: "09:00 - 17:00",
			tips: "Cocok untuk membawa anak kecil karena jalurnya landai.",
		},
		{
			name: "Jalan Braga",
			cat: "unik",
			tiket: "Gratis",
			spend: "Rp 50.000 - Rp 200.000",
			desc: "Jalan bersejarah dengan bangunan kolonial, galeri seni, dan kafe-kafe estetik.",
			menu: "Kopi legendaris (Braga Permai), pastry, steak.",
			jam: "24 Jam (Kafe berbeda-beda)",
			tips: "Paling asik dinikmati dengan berjalan kaki sore menjelang malam.",
		},
		{
			name: "The Lodge Maribaya",
			cat: "wisata",
			tiket: "Rp 50.000 - Rp 100.000",
			spend: "Rp 150.000",
			desc: "Spot foto ekstrem seperti ayunan di ketinggian dengan latar hutan pinus yang luas.",
			menu: "Nasi Liwet, Snack tradisional.",
			jam: "09:00 - 17:00",
			tips: "Siapkan biaya tambahan untuk setiap wahana foto.",
		},
		{
			name: "Cihampelas Walk (Ciwalk)",
			cat: "unik",
			tiket: "Gratis",
			spend: "Rp 100.000 - Rp 500.000",
			desc: "Mall dengan konsep terbuka (open-air) yang hijau dan menyatu dengan alam.",
			menu: "Food court lengkap, Ramen, Sushi, Kopi.",
			jam: "10:00 - 22:00",
			tips: "Area yang bagus untuk shopping santai di sore hari.",
		},
		{
			name: "Kartika Sari (Dago)",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 100.000 - Rp 300.000",
			desc: "Toko oleh-oleh paling legendaris di Bandung, terkenal dengan Pisang Molen-nya.",
			menu: "Pisang Molen, Brownies, Bagelen.",
			jam: "07:00 - 20:00",
			tips: "Antrean kasir biasanya panjang saat akhir pekan, datanglah pagi.",
		},
		{
			name: "Sari Barokah Lembang",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 50.000 - Rp 150.000",
			desc: "Pusat keripik dan jajanan kiloan khas Sunda dengan harga terjangkau.",
			menu: "Keripik tempe, Oncom, Dodol, Kerupuk kulit.",
			jam: "07:00 - 21:00",
			tips: "Bisa minta tester sebelum membeli keripik.",
		},
		{
			name: "Sarae Hills",
			cat: "wisata",
			tiket: "Rp 50.000 - Rp 95.000",
			spend: "Rp 150.000",
			desc: "World of Wonders dengan replika Santorini, Menara Eiffel, dan jembatan gantung panjang.",
			menu: "Western, Grill, Coffee.",
			jam: "09:00 - 21:00",
			tips: "Gunakan sunscreen karena area ini sangat terbuka dan panas siang hari.",
		},
		{
			name: "Warung Kopi Gunung",
			cat: "kuliner",
			tiket: "Gratis",
			spend: "Rp 50.000 - Rp 100.000",
			desc: "Kafe estetik di tengah hutan pinus Cikole dengan udara yang sangat dingin.",
			menu: "Kopi susu, Pisang goreng, Indomie, Nasi goreng.",
			jam: "10:00 - 20:00",
			tips: "Bawa jaket tebal karena suhu bisa mencapai 16 derajat.",
		},
		{
			name: "Dago Dreampark",
			cat: "wisata",
			tiket: "Rp 35.000 - Rp 45.000",
			spend: "Rp 150.000",
			desc: "Taman bermain dengan wahana foto ekstrem seperti Up House dan karpet terbang.",
			menu: "Bakso, Nasi ayam, Snack.",
			jam: "09:00 - 17:00",
			tips: "Area sangat luas, tersedia shuttle bus di dalam.",
		},
		{
			name: "Observatorium Bosscha",
			cat: "unik",
			tiket: "Rp 50.000 (Sesi kunjungan)",
			spend: "Rp 50.000",
			desc: "Teropong bintang tertua di Indonesia dengan arsitektur klasik yang megah.",
			menu: "Tidak ada (Area edukasi).",
			jam: "Sesuai reservasi (Terbatas)",
			tips: "Wajib cek website resmi untuk jadwal kunjungan publik.",
		},
		{
			name: "Gubuk Makan Mang Engking",
			cat: "kuliner",
			tiket: "Gratis",
			spend: "Rp 100.000 - Rp 200.000",
			desc: "Makan di atas saung terapung dengan pemandangan gunung dan kolam ikan.",
			menu: "Udang Bakar Madu, Gurame Terbang, Karedok.",
			jam: "10:00 - 21:00",
			tips: "Pesanan Udang Bakar Madu adalah menu wajib.",
		},
		{
			name: "Mini Mania Lembang",
			cat: "wisata",
			tiket: "Rp 25.000 - Rp 50.000",
			spend: "Rp 100.000",
			desc: "Taman miniatur dunia yang menampilkan landmark populer dari berbagai negara.",
			menu: "Gelato, Snack cepat saji.",
			jam: "09:00 - 18:00",
			tips: "Taman Sakura-nya sangat bagus untuk foto ala Jepang.",
		},
		{
			name: "Mochi Lembang",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 25.000 - Rp 50.000",
			desc: "Mochi lembut khas Lembang dengan berbagai isian buah dan kacang.",
			menu: "Mochi Susu, Mochi Kacang, Mochi Cokelat.",
			jam: "08:00 - 20:00",
			tips: "Mochi ini tahan 3-4 hari di suhu ruang.",
		},
		{
			name: "Mercusuar Cafe & Resto",
			cat: "unik",
			tiket: "Rp 20.000 (Voucher makan)",
			spend: "Rp 100.000 - Rp 200.000",
			desc: "Restoran dengan bangunan berbentuk kastil abad pertengahan yang megah di Dago.",
			menu: "Pizza, Steak, Mocktails.",
			jam: "09:00 - 21:00",
			tips: "Naik ke puncak kastil untuk melihat view kota Bandung.",
		},
		{
			name: "Prima Rasa Bakery",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 100.000 - Rp 300.000",
			desc: "Toko pastry premium yang bersaing dengan Kartika Sari, terkenal dengan Cheese Stick-nya.",
			menu: "Brownies Panggang, Cheese Stick, Lapis Legit.",
			jam: "07:00 - 20:00",
			tips: "Cheese Stick-nya sering habis sebelum jam 12 siang.",
		},
		{
			name: "Lawangwangi Creative Space",
			cat: "unik",
			tiket: "Gratis",
			spend: "Rp 75.000 - Rp 150.000",
			desc: "Galeri seni kontemporer yang digabung dengan kafe pemandangan lembah.",
			menu: "Nasi Goreng Lawangwangi, Pasta, Dessert.",
			jam: "11:00 - 21:00",
			tips: "Spot anjungan kayunya adalah tempat foto favorit.",
		},
		{
			name: "Terminal Wisata Grafika Cikole",
			cat: "wisata",
			tiket: "Rp 20.000",
			spend: "Rp 100.000",
			desc: "Wisata outdoor dengan nuansa hutan, rumah kayu ala kurcaci, dan area outbond.",
			menu: "Masakan Sunda, BBQ.",
			jam: "08:00 - 18:00",
			tips: "Bisa memberi makan rusa di area belakang.",
		},
		{
			name: "Saung Angklung Udjo",
			cat: "unik",
			tiket: "Rp 70.000 - Rp 120.000",
			spend: "Rp 150.000",
			desc: "Pusat pelestarian budaya Sunda dengan pertunjukan angklung interaktif.",
			menu: "Camilan tradisional, Teh manis.",
			jam: "08:00 - 17:00",
			tips: "Pastikan datang sesuai jadwal show (biasanya jam 15.30).",
		},
		{
			name: "Armor Kopi (Tahura)",
			cat: "kuliner",
			tiket: "Rp 15.000 (Masuk Tahura)",
			spend: "Rp 40.000 - Rp 80.000",
			desc: "Kedai kopi sederhana di dalam Taman Hutan Raya dengan suasana pohon pinus.",
			menu: "Kopi Robusta/Arabika, Pisang Keju, Cireng.",
			jam: "08:00 - 20:00",
			tips: "Gunakan anti-nyamuk karena lokasinya benar-benar di dalam hutan.",
		},
		{
			name: "Pasar Baru Trade Center",
			cat: "oleh",
			tiket: "Gratis",
			spend: "Rp 200.000 - Rp 2.000.000",
			desc: "Pusat belanja grosir pakaian, kain batik, dan oleh-oleh makanan kering terbesar.",
			menu: "Lumpia basah, aneka jajanan pasar.",
			jam: "09:00 - 17:00",
			tips: "Waspada barang bawaan dan jangan ragu untuk menawar harga.",
		},
	];

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
		font-size: 12px;
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
</style>
