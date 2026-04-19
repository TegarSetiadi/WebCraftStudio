<script lang="ts">
	import { services } from '$lib/data';
</script>

<section id="services" class="section services-bg" aria-labelledby="svc-heading">
	<div class="container">
		<div class="section-header reveal">
			<div class="section-tag">Apa yang Kami Tawarkan</div>
			<h2 id="svc-heading">Layanan <span class="gradient-text">Unggulan</span> Kami</h2>
			<p>Solusi digital lengkap untuk bisnis Anda berkembang pesat di era online</p>
		</div>
		<div class="services-grid">
			{#each services as svc, i}
				<article class="service-card reveal" style="transition-delay:{i * 60}ms" aria-label={svc.title}>
					<div class="svc-icon" aria-hidden="true">{svc.icon}</div>
					<h3>{svc.title}</h3>
					<p>{svc.desc}</p>
					<div class="svc-footer">
						<span class="svc-price">{svc.price}</span>
						<a href="#contact" class="svc-btn">Pesan →</a>
					</div>
				</article>
			{/each}
		</div>
	</div>
</section>

<style>
	.section { padding: 6rem 0; }
	.container { max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }
	.services-bg { background: linear-gradient(180deg, #06060f 0%, #0d0b1a 100%); }
	.section-header { text-align: center; margin-bottom: 3.5rem; }
	.section-tag {
		display: inline-block; margin-bottom: 1rem;
		background: rgba(124,58,237,0.11); border: 1px solid rgba(167,139,250,0.28);
		color: #a78bfa; font-size: 0.72rem; font-weight: 700;
		letter-spacing: 0.09em; text-transform: uppercase;
		padding: 0.28rem 0.9rem; border-radius: 9999px;
	}
	.section-header h2 { font-size: clamp(1.75rem, 4vw, 2.6rem); font-weight: 800; color: #f1f5f9; margin-bottom: 0.75rem; }
	.section-header p { color: #64748b; font-size: 0.95rem; max-width: 480px; margin: 0 auto; }
	.gradient-text {
		background: linear-gradient(135deg, #a78bfa, #38bdf8, #818cf8);
		-webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
	}
	.services-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 1.5rem; contain: layout; }
	.service-card {
		background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
		border-radius: 1.25rem; padding: 2rem; display: flex; flex-direction: column; gap: 0.75rem;
		transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s; will-change: transform;
	}
	.service-card:hover { transform: translateY(-6px); border-color: rgba(124,58,237,0.38); box-shadow: 0 16px 44px rgba(124,58,237,0.14); }
	.svc-icon { font-size: 2.2rem; }
	.service-card h3 { font-size: 1.1rem; font-weight: 700; color: #f1f5f9; }
	.service-card p { font-size: 0.875rem; color: #64748b; line-height: 1.65; flex: 1; }
	.svc-footer { display: flex; align-items: center; justify-content: space-between; margin-top: 0.5rem; padding-top: 1rem; border-top: 1px solid rgba(255,255,255,0.07); }
	.svc-price { font-size: 0.875rem; font-weight: 700; color: #a78bfa; }
	.svc-btn { color: #818cf8; font-size: 0.85rem; font-weight: 600; text-decoration: none; transition: color 0.2s; }
	.svc-btn:hover { color: #a78bfa; }
	:global(.reveal) { opacity: 0; transform: translateY(24px); transition: opacity 0.6s ease, transform 0.6s ease; will-change: opacity, transform; }
</style>
