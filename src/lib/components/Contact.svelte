<script lang="ts">
	import { SITE } from '$lib/config';
</script>

<section id="contact" class="section contact-bg" aria-labelledby="contact-heading">
	<div class="container">
		<div class="cta-card reveal">
			<div class="cta-glow" aria-hidden="true"></div>
			<div class="section-tag" style="margin-bottom:1rem">Hubungi Kami Sekarang</div>
			<h2 id="contact-heading">Siap Buat Website <span class="gradient-text">Impian Anda?</span></h2>
			<p>Konsultasi gratis, tanpa komitmen. Kami siap membantu 24/7 melalui WhatsApp.</p>
			<div class="contact-actions">
				<a
					id="whatsapp-btn"
					href="https://wa.me/{SITE.whatsapp}?text=Halo%2C%20saya%20ingin%20konsultasi%20pembuatan%20website"
					target="_blank" rel="noopener noreferrer"
					class="btn-wa"
					aria-label="Hubungi kami via WhatsApp"
				>💬 Chat WhatsApp</a>
				<a
					id="email-btn"
					href="mailto:{SITE.email}"
					class="btn-ghost-dark"
					aria-label="Kirim email ke {SITE.name}"
				>✉️ Kirim Email</a>
			</div>
			<p class="contact-note">🔒 Data Anda aman. Tidak ada spam.</p>
		</div>
	</div>
</section>

<style>
	.section { padding: 5rem 0; }
	.container { max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }
	.contact-bg { background: linear-gradient(180deg, #06060f 0%, #0d0b1a 100%); }
	.section-tag {
		display: inline-block;
		background: rgba(124,58,237,0.11); border: 1px solid rgba(167,139,250,0.28);
		color: #a78bfa; font-size: 0.72rem; font-weight: 700; letter-spacing: 0.09em;
		text-transform: uppercase; padding: 0.28rem 0.9rem; border-radius: 9999px;
	}
	.gradient-text { background: linear-gradient(135deg, #a78bfa, #38bdf8, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
	.cta-card {
		position: relative; overflow: hidden; text-align: center;
		background: rgba(124,58,237,0.07); border: 1px solid rgba(124,58,237,0.22);
		border-radius: 2rem; padding: 4rem 3rem;
	}
	.cta-glow {
		position: absolute; top: -60px; left: 50%; transform: translateX(-50%);
		width: 480px; height: 280px; pointer-events: none;
		background: radial-gradient(ellipse, rgba(124,58,237,0.28) 0%, transparent 70%);
	}
	.cta-card h2 { font-size: clamp(1.75rem, 4vw, 2.5rem); font-weight: 800; color: #f1f5f9; margin-bottom: 0.875rem; position: relative; }
	.cta-card p { color: #64748b; margin-bottom: 2.5rem; font-size: 1rem; position: relative; }
	.contact-actions { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; margin-bottom: 1.5rem; position: relative; }
	.btn-wa {
		background: #25d366; color: #fff; padding: 0.875rem 2rem; border-radius: 9999px;
		font-weight: 700; font-size: 1rem; text-decoration: none;
		box-shadow: 0 8px 28px rgba(37,211,102,0.32); transition: transform 0.2s, box-shadow 0.2s; will-change: transform;
	}
	.btn-wa:hover { transform: translateY(-2px); box-shadow: 0 12px 36px rgba(37,211,102,0.5); }
	.btn-ghost-dark {
		background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.12);
		color: #e2e8f0; padding: 0.875rem 2rem; border-radius: 9999px;
		font-weight: 600; font-size: 1rem; text-decoration: none; transition: background 0.2s;
	}
	.btn-ghost-dark:hover { background: rgba(255,255,255,0.09); }
	.contact-note { color: #475569; font-size: 0.78rem; position: relative; }
	@media (max-width: 640px) { .cta-card { padding: 2.5rem 1.25rem; } }
</style>
