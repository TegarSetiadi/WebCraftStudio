<script lang="ts">
	import { testimonials } from '$lib/data';
</script>

<section id="testimonials" class="section testi-bg" aria-labelledby="testi-heading">
	<div class="container">
		<div class="section-header reveal">
			<div class="section-tag">Kata Mereka</div>
			<h2 id="testi-heading">Klien yang <span class="gradient-text">Bahagia</span></h2>
			<p>Ribuan bisnis telah berkembang bersama kami. Ini kisah mereka.</p>
		</div>
		<div class="testi-grid">
			{#each testimonials as t, i}
				<article
					class="testi-card reveal"
					style="transition-delay:{i * 80}ms"
					itemscope itemtype="https://schema.org/Review"
				>
					<div class="stars" aria-label="Rating 5 bintang">★★★★★</div>
					<p class="testi-msg" itemprop="reviewBody">"{t.msg}"</p>
					<div class="testi-author">
						<div class="avatar" aria-hidden="true">{t.avatar}</div>
						<div>
							<div class="author-name" itemprop="author">{t.name}</div>
							<div class="author-role">{t.role}</div>
						</div>
					</div>
				</article>
			{/each}
		</div>
	</div>
</section>

<style>
	.section { padding: 6rem 0; }
	.container { max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }
	.testi-bg { background: linear-gradient(180deg, #0d0b1a 0%, #06060f 100%); }
	.section-header { text-align: center; margin-bottom: 3.5rem; }
	.section-tag {
		display: inline-block; margin-bottom: 1rem;
		background: rgba(124,58,237,0.11); border: 1px solid rgba(167,139,250,0.28);
		color: #a78bfa; font-size: 0.72rem; font-weight: 700; letter-spacing: 0.09em;
		text-transform: uppercase; padding: 0.28rem 0.9rem; border-radius: 9999px;
	}
	.section-header h2 { font-size: clamp(1.75rem, 4vw, 2.6rem); font-weight: 800; color: #f1f5f9; margin-bottom: 0.75rem; }
	.section-header p { color: #64748b; font-size: 0.95rem; max-width: 480px; margin: 0 auto; }
	.gradient-text { background: linear-gradient(135deg, #a78bfa, #38bdf8, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
	.testi-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(290px, 1fr)); gap: 1.5rem; contain: layout; }
	.testi-card {
		background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
		border-radius: 1.25rem; padding: 2rem; transition: transform 0.3s, border-color 0.3s; will-change: transform;
	}
	.testi-card:hover { transform: translateY(-4px); border-color: rgba(124,58,237,0.3); }
	.stars { color: #fbbf24; font-size: 0.95rem; margin-bottom: 1rem; letter-spacing: 0.08em; }
	.testi-msg { color: #94a3b8; font-size: 0.875rem; line-height: 1.7; margin-bottom: 1.5rem; font-style: italic; }
	.testi-author { display: flex; align-items: center; gap: 0.875rem; }
	.avatar {
		width: 42px; height: 42px; border-radius: 50%; flex-shrink: 0;
		background: linear-gradient(135deg, #7c3aed, #4f46e5);
		display: flex; align-items: center; justify-content: center;
		font-size: 0.72rem; font-weight: 700; color: #fff;
	}
	.author-name { font-weight: 700; font-size: 0.875rem; color: #f1f5f9; }
	.author-role { font-size: 0.75rem; color: #64748b; margin-top: 0.1rem; }
</style>
