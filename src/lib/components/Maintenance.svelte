<script lang="ts">
	import { SITE } from '$lib/config';
</script>

<svelte:head>
	<title>Maintenance | {SITE.name}</title>
	<meta name="robots" content="noindex, nofollow" />
</svelte:head>

<div class="maintenance">
	<div class="canvas-dots" aria-hidden="true">
		{#each Array(20) as _, i}
			<div class="dot" style="
				left:{Math.random()*100}%;
				top:{Math.random()*100}%;
				animation-delay:{(i * 0.3).toFixed(1)}s;
				width:{Math.random()*6+3}px;
				height:{Math.random()*6+3}px;
			"></div>
		{/each}
	</div>

	<div class="card">
		<div class="icon" aria-hidden="true">🔧</div>
		<h1>Sedang Perbaikan</h1>
		<p>Website sedang dalam pemeliharaan untuk memberikan pengalaman yang lebih baik.</p>
		<p class="eta">Kami akan kembali sebentar lagi. Terima kasih atas kesabaran Anda! 🙏</p>
		<a
			href="https://wa.me/{SITE.whatsapp}"
			target="_blank" rel="noopener noreferrer"
			class="btn-wa"
		>💬 Hubungi via WhatsApp</a>
	</div>
</div>

<style>
	.maintenance {
		min-height: 100vh; display: flex; align-items: center; justify-content: center;
		background: #06060f; position: relative; overflow: hidden; padding: 2rem;
	}
	.canvas-dots { position: absolute; inset: 0; pointer-events: none; }
	.dot {
		position: absolute; border-radius: 50%;
		background: rgba(167,139,250,0.25);
		animation: pulse 4s ease-in-out infinite;
	}
	@keyframes pulse {
		0%, 100% { opacity: 0.2; transform: scale(1); }
		50% { opacity: 0.6; transform: scale(1.4); }
	}
	.card {
		position: relative; z-index: 2; text-align: center; max-width: 480px;
		background: rgba(255,255,255,0.03); border: 1px solid rgba(124,58,237,0.2);
		border-radius: 1.75rem; padding: 3rem 2.5rem;
		box-shadow: 0 24px 80px rgba(124,58,237,0.15);
	}
	.icon { font-size: 4rem; margin-bottom: 1.25rem; display: block; animation: spin 4s linear infinite; }
	@keyframes spin {
		0%, 90% { transform: rotate(0deg); }
		100% { transform: rotate(360deg); }
	}
	h1 { font-size: 2rem; font-weight: 800; color: #f1f5f9; margin-bottom: 1rem; }
	p { color: #64748b; font-size: 0.95rem; line-height: 1.65; margin-bottom: 0.5rem; }
	.eta { color: #94a3b8; margin-bottom: 2rem; }
	.btn-wa {
		display: inline-block; background: #25d366; color: #fff;
		padding: 0.875rem 2rem; border-radius: 9999px; font-weight: 700;
		font-size: 1rem; text-decoration: none;
		box-shadow: 0 8px 24px rgba(37,211,102,0.3);
		transition: transform 0.2s, box-shadow 0.2s;
	}
	.btn-wa:hover { transform: translateY(-2px); box-shadow: 0 12px 32px rgba(37,211,102,0.45); }
</style>
