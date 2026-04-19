<script lang="ts">
	import { onMount } from 'svelte';

	let { visible = false }: { visible: boolean } = $props();

	let canvas: HTMLCanvasElement;
	let rafId: number;

	export function initCanvas(el: HTMLCanvasElement) {
		const ctx = el.getContext('2d')!;
		let W = 0, H = 0;
		const mouse = { x: -9999, y: -9999 };
		const MOUSE_RADIUS = 160;
		const COUNT = 90;
		const CONNECT_DIST = 130;
		const SPEED = 0.45;

		interface Particle { x: number; y: number; vx: number; vy: number; r: number; }
		let particles: Particle[] = [];

		function resize() {
			W = el.offsetWidth; H = el.offsetHeight;
			el.width = W * devicePixelRatio; el.height = H * devicePixelRatio;
			ctx.scale(devicePixelRatio, devicePixelRatio);
		}
		function spawn(): Particle {
			return { x: Math.random() * W, y: Math.random() * H,
				vx: (Math.random() - 0.5) * SPEED, vy: (Math.random() - 0.5) * SPEED,
				r: Math.random() * 1.8 + 0.8 };
		}
		function init() { resize(); particles = Array.from({ length: COUNT }, spawn); }

		function tick() {
			ctx.clearRect(0, 0, W, H);
			for (let i = 0; i < particles.length; i++) {
				const p = particles[i];
				const dx = p.x - mouse.x, dy = p.y - mouse.y;
				const d2 = dx * dx + dy * dy;
				if (d2 < MOUSE_RADIUS * MOUSE_RADIUS && d2 > 0) {
					const force = (MOUSE_RADIUS - Math.sqrt(d2)) / MOUSE_RADIUS;
					const inv = 1 / Math.sqrt(d2);
					p.vx += dx * inv * force * 0.35; p.vy += dy * inv * force * 0.35;
				}
				p.vx *= 0.985; p.vy *= 0.985;
				const spd = Math.sqrt(p.vx * p.vx + p.vy * p.vy);
				if (spd > SPEED * 3) { p.vx = (p.vx / spd) * SPEED * 3; p.vy = (p.vy / spd) * SPEED * 3; }
				p.x += p.vx; p.y += p.vy;
				if (p.x < 0) p.x = W; else if (p.x > W) p.x = 0;
				if (p.y < 0) p.y = H; else if (p.y > H) p.y = 0;

				ctx.beginPath(); ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
				ctx.fillStyle = 'rgba(167,139,250,0.9)'; ctx.fill();

				for (let j = i + 1; j < particles.length; j++) {
					const q = particles[j];
					const ex = p.x - q.x, ey = p.y - q.y;
					const dist = Math.sqrt(ex * ex + ey * ey);
					if (dist < CONNECT_DIST) {
						const alpha = (1 - dist / CONNECT_DIST) * 0.45;
						ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(q.x, q.y);
						ctx.strokeStyle = `rgba(129,140,248,${alpha})`; ctx.lineWidth = 0.8; ctx.stroke();
					}
				}
				const mdist = Math.sqrt(d2);
				if (mdist < MOUSE_RADIUS) {
					const ma = (1 - mdist / MOUSE_RADIUS) * 0.7;
					ctx.beginPath(); ctx.moveTo(p.x, p.y); ctx.lineTo(mouse.x, mouse.y);
					ctx.strokeStyle = `rgba(167,139,250,${ma})`; ctx.lineWidth = 1; ctx.stroke();
				}
			}
			rafId = requestAnimationFrame(tick);
		}

		function onMove(e: MouseEvent) {
			const r = el.getBoundingClientRect();
			mouse.x = e.clientX - r.left; mouse.y = e.clientY - r.top;
		}
		function onLeave() { mouse.x = -9999; mouse.y = -9999; }
		function onTouch(e: TouchEvent) {
			const r = el.getBoundingClientRect();
			mouse.x = e.touches[0].clientX - r.left; mouse.y = e.touches[0].clientY - r.top;
		}

		const parent = el.parentElement!;
		parent.addEventListener('mousemove', onMove, { passive: true });
		parent.addEventListener('mouseleave', onLeave, { passive: true });
		parent.addEventListener('touchmove', onTouch, { passive: true });

		const ro = new ResizeObserver(() => {
			resize();
			particles.forEach(p => { p.x = Math.min(p.x, W); p.y = Math.min(p.y, H); });
		});
		ro.observe(parent);

		init(); tick();

		return () => {
			cancelAnimationFrame(rafId); ro.disconnect();
			parent.removeEventListener('mousemove', onMove);
			parent.removeEventListener('mouseleave', onLeave);
			parent.removeEventListener('touchmove', onTouch);
		};
	}

	onMount(() => {
		if (!canvas) return;
		const cleanup = initCanvas(canvas);
		return cleanup;
	});
</script>

<section id="hero" class="hero" aria-label="Hero">
	<canvas bind:this={canvas} class="canvas-web" aria-hidden="true"></canvas>
	<div class="hero-radial" aria-hidden="true"></div>

	<div class="hero-content" class:fade-in={visible}>
		<div class="badge">🚀 Terpercaya &amp; Berpengalaman</div>
		<h1>Website Impian Anda,<br /><span class="gradient-text">Kami Wujudkan</span></h1>
		<p class="hero-sub">
			Jasa pembuatan website profesional dengan desain modern, performa cepat, dan harga terjangkau.<br />
			Dari landing page hingga toko online — selesai tepat waktu, hasil memuaskan.
		</p>
		<div class="hero-cta">
			<a href="#contact" id="hero-cta-btn" class="btn-primary">Mulai Sekarang →</a>
			<a href="#services" class="btn-ghost">Lihat Layanan</a>
		</div>
		<div class="hero-stats" aria-label="Statistik layanan">
			<div class="stat"><span class="stat-num">50+</span><span class="stat-label">Proyek Selesai</span></div>
			<div class="stat-div" aria-hidden="true"></div>
			<div class="stat"><span class="stat-num">98%</span><span class="stat-label">Klien Puas</span></div>
			<div class="stat-div" aria-hidden="true"></div>
			<div class="stat"><span class="stat-num">3 Hari</span><span class="stat-label">Pengerjaan Cepat</span></div>
		</div>
	</div>
	<div class="scroll-hint" aria-hidden="true"><span>Scroll ke bawah</span><div class="scroll-arrow">↓</div></div>
</section>

<style>
	.hero {
		position: relative; min-height: 100vh;
		display: flex; flex-direction: column; align-items: center; justify-content: center;
		text-align: center; padding: 8rem 1.5rem 4rem; overflow: hidden;
	}
	.canvas-web {
		position: absolute; inset: 0; width: 100%; height: 100%; display: block;
		will-change: transform; contain: strict;
	}
	.hero-radial {
		position: absolute; inset: 0; pointer-events: none;
		background: radial-gradient(ellipse at 50% 45%, rgba(124,58,237,0.14) 0%, #06060f 68%);
	}
	.hero-content {
		position: relative; z-index: 2; max-width: 800px;
		opacity: 0; transform: translateY(28px);
		transition: opacity 0.85s ease, transform 0.85s ease;
		will-change: opacity, transform;
	}
	.hero-content.fade-in { opacity: 1; transform: translateY(0); }
	.badge {
		display: inline-block; margin-bottom: 1.75rem;
		background: rgba(124,58,237,0.14); border: 1px solid rgba(167,139,250,0.38);
		color: #a78bfa; font-size: 0.78rem; font-weight: 700;
		padding: 0.32rem 1rem; border-radius: 9999px; letter-spacing: 0.04em;
	}
	h1 { font-size: clamp(2.4rem, 6vw, 4.5rem); font-weight: 900; line-height: 1.1; color: #f1f5f9; margin-bottom: 1.5rem; }
	.gradient-text {
		background: linear-gradient(135deg, #a78bfa, #38bdf8, #818cf8);
		-webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
	}
	.hero-sub { font-size: 1.05rem; color: #94a3b8; line-height: 1.75; margin-bottom: 2.5rem; max-width: 620px; margin-left: auto; margin-right: auto; }
	.hero-cta { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; margin-bottom: 3.5rem; }
	.btn-primary {
		background: linear-gradient(135deg, #7c3aed, #4f46e5); color: #fff;
		padding: 0.875rem 2rem; border-radius: 9999px; font-weight: 700; font-size: 1rem; text-decoration: none;
		box-shadow: 0 8px 28px rgba(124,58,237,0.38); transition: transform 0.2s, box-shadow 0.2s; will-change: transform;
	}
	.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 12px 36px rgba(124,58,237,0.55); }
	.btn-ghost {
		background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.14);
		color: #e2e8f0; padding: 0.875rem 2rem; border-radius: 9999px;
		font-weight: 600; font-size: 1rem; text-decoration: none; transition: background 0.2s, border-color 0.2s;
	}
	.btn-ghost:hover { background: rgba(255,255,255,0.09); border-color: rgba(255,255,255,0.28); }
	.hero-stats { display: flex; align-items: center; justify-content: center; gap: 2rem; flex-wrap: wrap; }
	.stat { display: flex; flex-direction: column; align-items: center; }
	.stat-num { font-size: 1.75rem; font-weight: 800; color: #f1f5f9; }
	.stat-label { font-size: 0.78rem; color: #64748b; margin-top: 0.2rem; }
	.stat-div { width: 1px; height: 38px; background: rgba(255,255,255,0.1); }
	.scroll-hint {
		position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
		display: flex; flex-direction: column; align-items: center; gap: 0.3rem;
		color: #475569; font-size: 0.72rem; z-index: 2;
		animation: bounce 2.2s ease-in-out infinite;
	}
	@keyframes bounce {
		0%, 100% { transform: translateX(-50%) translateY(0); }
		50% { transform: translateX(-50%) translateY(7px); }
	}
	@media (max-width: 640px) { .stat-div { display: none; } }
	@media (prefers-reduced-motion: reduce) {
		.hero-content { transition: none; opacity: 1; transform: none; }
		.scroll-hint { animation: none; }
		.canvas-web { display: none; }
	}
</style>
