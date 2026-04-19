<script lang="ts">
	import { faqs } from '$lib/data';

	let openFaq = $state<number | null>(null);
	function toggle(i: number) { openFaq = openFaq === i ? null : i; }
</script>

<section id="faq" class="section faq-bg" aria-labelledby="faq-heading">
	<div class="container">
		<div class="section-header reveal">
			<div class="section-tag">Pertanyaan Umum</div>
			<h2 id="faq-heading">Ada yang ingin <span class="gradient-text">ditanyakan?</span></h2>
		</div>
		<div class="faq-list" itemscope itemtype="https://schema.org/FAQPage">
			{#each faqs as faq, i}
				<div
					class="faq-item reveal"
					class:open={openFaq === i}
					itemscope itemprop="mainEntity" itemtype="https://schema.org/Question"
				>
					<button
						class="faq-q"
						id="faq-btn-{i}"
						aria-expanded={openFaq === i}
						aria-controls="faq-ans-{i}"
						onclick={() => toggle(i)}
					>
						<span itemprop="name">{faq.q}</span>
						<span class="faq-icon" aria-hidden="true">{openFaq === i ? '−' : '+'}</span>
					</button>
					{#if openFaq === i}
						<div
							class="faq-a"
							id="faq-ans-{i}"
							role="region"
							aria-labelledby="faq-btn-{i}"
							itemscope itemprop="acceptedAnswer" itemtype="https://schema.org/Answer"
						>
							<p itemprop="text">{faq.a}</p>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.section { padding: 6rem 0; }
	.container { max-width: 720px; margin: 0 auto; padding: 0 1.5rem; }
	.faq-bg { background: #06060f; }
	.section-header { text-align: center; margin-bottom: 3.5rem; }
	.section-tag {
		display: inline-block; margin-bottom: 1rem;
		background: rgba(124,58,237,0.11); border: 1px solid rgba(167,139,250,0.28);
		color: #a78bfa; font-size: 0.72rem; font-weight: 700; letter-spacing: 0.09em;
		text-transform: uppercase; padding: 0.28rem 0.9rem; border-radius: 9999px;
	}
	.section-header h2 { font-size: clamp(1.75rem, 4vw, 2.6rem); font-weight: 800; color: #f1f5f9; margin-bottom: 0.75rem; }
	.gradient-text { background: linear-gradient(135deg, #a78bfa, #38bdf8, #818cf8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
	.faq-list { display: flex; flex-direction: column; gap: 0.75rem; }
	.faq-item {
		background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
		border-radius: 1rem; overflow: hidden; transition: border-color 0.2s;
	}
	.faq-item.open { border-color: rgba(124,58,237,0.38); }
	.faq-q {
		width: 100%; background: none; border: none; cursor: pointer; font-family: inherit;
		display: flex; align-items: center; justify-content: space-between;
		padding: 1.2rem 1.5rem; color: #f1f5f9; font-size: 0.925rem; font-weight: 600;
		text-align: left; gap: 1rem;
	}
	.faq-icon { color: #a78bfa; font-size: 1.25rem; font-weight: 400; flex-shrink: 0; }
	.faq-a { padding: 0 1.5rem 1.2rem; color: #64748b; font-size: 0.875rem; line-height: 1.7; }
</style>
