<script lang="ts">
import Icon from '@iconify/svelte';
	import emergencyData from '$lib/data/emergency.json';
	const emergencyNational = emergencyData.emergencyNational;
	const tollNumbers = emergencyData.tollNumbers;
	const hospitals = emergencyData.hospitals;

	function callNumber(number: string) {
		window.open(`tel:${number.replace(/[^0-9+]/g, '')}`, '_self');
	}

	function navigateToHospital(coord: string) {
		window.open(`https://www.google.com/maps/dir/?api=1&destination=${coord}&travelmode=driving`, '_blank');
	}
</script>

<div class="emergency">
	<section class="em-section">
		<h2 class="section-title"><span><Icon icon="solar:sos-bold" width="20" /></span> Nomor Darurat Nasional</h2>
		<div class="em-list">
			{#each emergencyNational as item}
				<div class="em-card">
					<span class="em-icon"><Icon icon={item.icon} width="22" /></span>
					<div class="em-info">
						<span class="em-name">{item.name}</span>
						<span class="em-desc">{item.desc}</span>
					</div>
					<button class="call-btn" onclick={() => callNumber(item.number)}>
						<Icon icon="solar:phone-bold" width="16" /> {item.number}
					</button>
				</div>
			{/each}
		</div>
	</section>

	<section class="em-section">
		<h2 class="section-title"><span><Icon icon="solar:road-bold" width="20" /></span> Nomor Penting di Tol</h2>
		<div class="em-list">
			{#each tollNumbers as item}
				<div class="em-card">
					<span class="em-icon"><Icon icon={item.icon} width="22" /></span>
					<div class="em-info">
						<span class="em-name">{item.name}</span>
						<span class="em-desc">{item.desc}</span>
					</div>
					<button class="call-btn toll" onclick={() => callNumber(item.number)}>
						<Icon icon="solar:phone-bold" width="16" /> {item.number}
					</button>
				</div>
			{/each}
		</div>
	</section>

	<section class="em-section">
		<h2 class="section-title"><span><Icon icon="solar:hospital-bold" width="20" /></span> Rumah Sakit di Sepanjang Rute</h2>
		<div class="em-list">
			{#each hospitals as item}
				<div class="em-card hospital">
					<div class="hospital-top">
						<span class="em-icon"><Icon icon={item.icon} width="22" /></span>
						<div class="em-info">
							<span class="em-name">{item.name}</span>
							<span class="em-desc">{item.desc}</span>
						</div>
					</div>
					<div class="hospital-actions">
						<button class="call-btn hospital-call" onclick={() => callNumber(item.number)}>
							<Icon icon="solar:phone-bold" width="16" /> {item.number}
						</button>
						<button class="nav-btn" onclick={() => navigateToHospital(item.coord)}>
							<Icon icon="solar:map-point-bold" width="16" /> Navigasi
						</button>
					</div>
				</div>
			{/each}
		</div>
	</section>
</div>

<style>
	.emergency { display: flex; flex-direction: column; gap: 24px; }

	.em-section { display: flex; flex-direction: column; gap: 10px; }

	.section-title {
		display: flex; align-items: center; gap: 8px;
		font-size: 16px; font-weight: 700; color: var(--text-primary);
		padding-bottom: 6px;
		border-bottom: 1px solid var(--border-subtle);
	}

	.em-list { display: flex; flex-direction: column; gap: 8px; }

	.em-card {
		display: flex; align-items: center; gap: 12px;
		background: var(--bg-card); border-radius: 12px; padding: 12px;
		border: 1px solid var(--border-card);
		box-shadow: var(--shadow-sm);
	}
	.em-card.hospital {
		flex-direction: column; align-items: stretch; gap: 10px;
	}
	.hospital-top { display: flex; align-items: center; gap: 12px; }

	.em-icon { font-size: 22px; flex-shrink: 0; }
	.em-info { flex: 1; display: flex; flex-direction: column; min-width: 0; }
	.em-name { font-size: 13px; font-weight: 600; color: var(--text-primary); }
	.em-desc { font-size: 11px; color: var(--text-secondary); }

	.call-btn {
		display: flex; align-items: center; gap: 4px;
		background: var(--gradient-green);
		color: white; padding: 8px 12px; border-radius: 10px;
		font-size: 12px; font-weight: 700; white-space: nowrap;
		transition: opacity 0.2s;
	}
	.call-btn:hover { opacity: 0.85; }
	.call-btn.toll { background: var(--gradient-warm); }

	.hospital-actions { display: flex; gap: 8px; }
	.hospital-call {
		flex: 1; justify-content: center;
		background: var(--gradient-green);
	}
	.nav-btn {
		flex: 1; display: flex; align-items: center; justify-content: center; gap: 4px;
		background: linear-gradient(135deg, #7c5bf5, #f78fb3);
		color: white; padding: 8px 12px; border-radius: 10px;
		font-size: 12px; font-weight: 700;
		transition: opacity 0.2s;
	}
	.nav-btn:hover { opacity: 0.85; }
</style>
