<script lang="ts">
	import { steps } from '$lib/data';
</script>

<section id="process" class="section process-bg" aria-labelledby="proc-heading">
	<div class="container">
		<div class="section-header reveal">
			<div class="section-tag">Cara Kerja Kami</div>
			<h2 id="proc-heading">Proses yang <span class="gradient-text">Transparan</span></h2>
			<p>4 langkah mudah dari konsultasi hingga website Anda siap online</p>
		</div>
		<div class="steps-grid">
			{#each steps as step, i}
				<div class="step-card reveal" style="transition-delay:{i * 80}ms">
					<span class="step-num" aria-label="Langkah {step.num}">{step.num}</span>
					<h3>{step.title}</h3>
					<p>{step.desc}</p>
				</div>
			{/each}
		</div>
	</div>
</section>

<style>
	.section { padding: 6rem 0; }
	.container { max-width: 1200px; margin: 0 auto; padding: 0 1.5rem; }
	.process-bg { background: #0d0b1a; }
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
	.steps-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 1.5rem; contain: layout; }
	.step-card {
		text-align: center; padding: 2rem 1.5rem;
		background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06);
		border-radius: 1.25rem; transition: border-color 0.3s, transform 0.3s; will-change: transform;
	}
	.step-card:hover { border-color: rgba(124,58,237,0.35); transform: translateY(-4px); }
	.step-num {
		font-size: 3rem; font-weight: 900; display: block; margin-bottom: 1rem;
		background: linear-gradient(135deg, #7c3aed, #38bdf8);
		-webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
	}
	.step-card h3 { font-size: 1.05rem; font-weight: 700; color: #f1f5f9; margin-bottom: 0.5rem; }
	.step-card p { color: #64748b; font-size: 0.85rem; line-height: 1.6; }
</style>
