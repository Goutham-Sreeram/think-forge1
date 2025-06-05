<script>
	import { onMount } from 'svelte';
	import { Application } from '@splinetool/runtime';
	import { tick } from 'svelte';

	let loading = true;
	let ticker = 0;
	let tickerInterval;

	function startTicker() {
		ticker = 0;
		tickerInterval = setInterval(() => {
			ticker = (ticker + Math.floor(Math.random() * 7) + 1) % 100;
		}, 30);
	}

	function stopTicker() {
		clearInterval(tickerInterval);
		ticker = 100;
	}

	onMount(() => {
		startTicker();
		const canvas = document.getElementById('canvas3d');
		if (canvas) {
			const app = new Application(canvas);
			app.load('https://prod.spline.design/WCczSWoOoZu-FQCo/scene.splinecode').then(() => {
				stopTicker();
				setTimeout(() => { loading = false; }, 400);
			});
		}
	});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cal+Sans&family=Phudu:wght@300..900&display=swap');
body, :global(html) {
	margin: 0;
	padding: 0;
	font-family: 'Cal Sans', Arial, sans-serif;
	background: #fff;
	overflow: hidden;
	height: 100vh;
}
.header, .nav, .nav a, .contact-btn, .main-content, .status, .headline, .subheadline, .desc, .connect-btn, .preloader, .preloader-inner, .ticker, .ticker-label {
	font-family: 'Cal Sans', Arial, sans-serif !important;
}
.spline-bg {
	position: fixed;
	top: 0;
	left: 0;
	width: 100vw;
	height: 100vh;
	z-index: 0;
	pointer-events: none;
}
#canvas3d {
	width: 100vw;
	height: 100vh;
	display: block;
	background: transparent;
	pointer-events: auto;
}
.header {
	position: absolute;
	top: 0;
	left: 0;
	width: 100vw;
	display: flex;
	justify-content: space-between;
	align-items: flex-start;
	padding: 32px 56px 0 32px;
	z-index: 10;
}
.logo {
	width: 156px;
	height: 156px;
	
}
.logo img {
	width: 100%;
	height: 100%;
	object-fit: contain;
}
.nav {
	display: flex;
	gap: 36px;
	align-items: center;
	margin-top: 12px;
}
.nav a {
	text-decoration: none;
	color: #ffffff;
	font-size: 1.15rem;
	font-weight: 400;
	transition: color 0.2s;
	padding: 6px 0;
}
.nav a:hover {
	color: #e53935;
}
.contact-btn {
	background: #000;
	color: #fff;
	border: none;
	border-radius: 8px;
	padding: 10px 22px;
	font-size: 1rem;
	font-weight: 400;
	margin-left: 5px;
	cursor: pointer;
	transition: background 0.2s;
	box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}
.contact-btn:hover {
	background: #e53935;
}
.main-content {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	z-index: 2;
	display: flex;
	flex-direction: column;
	align-items: center;
	width: 100vw;
	max-width: 100vw;
	box-sizing: border-box;
	padding: 0 24px;
}
.status {
	display: flex;
	align-items: center;
	gap: 8px;
	font-size: 1.1rem;
	margin-bottom: 18px;
	background: #fff;
	padding: 6px 18px;
	border-radius: 16px;
	box-shadow: 0 2px 8px rgba(0,0,0,0.04);
}
.status-dot {
	width: 10px;
	height: 10px;
	background: #2ecc40;
	border-radius: 50%;
	display: inline-block;
}
.headline {
	font-size: 3.5rem;
	font-weight: 400;
	text-align: center;
	line-height: 1.1;
	margin-bottom: 0.1em;
	color: #fff;
}
.subheadline {
	font-size: 2.5rem;
	font-weight: 400;
	text-align: center;
	margin-bottom: 0.2em;
	color: #fff;
}
.headline .tech, .subheadline .tech {
	color: #e53935;
	font-weight: 400;
}
.desc {
	font-size: 1.1rem;
	text-align: center;
	margin-bottom: 2.5em;
	color: #cecece;
	max-width: 480px;
}
.connect-btn {
	background: #fff;
	color: #000;
	border: none;
	border-radius: 12px;
	padding: 18px 38px;
	font-size: 1.35rem;
	font-weight: 400;
	box-shadow: 0 2px 12px rgba(0,0,0,0.08);
	cursor: pointer;
	transition: background 0.2s, color 0.2s;
}
.connect-btn:hover {
	background: #e53935;
	color: #fff;
}
.preloader {
	position: fixed;
	top: 0; left: 0; width: 100vw; height: 100vh;
	background: #fff;
	z-index: 100;
	display: flex;
	align-items: center;
	justify-content: center;
	transition: opacity 0.5s;
}
.preloader-inner {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 18px;
}
.ticker {
	font-family: 'Cal Sans', Arial, sans-serif;
	font-size: 3.5rem;
	color: #000000;
	transition: color 0.2s;
}
.ticker-label {
	font-size: 1.1rem;
	color: #222;
	font-weight: 500;
	letter-spacing: 0.04em;
}
.preloader[hidden] {
	opacity: 0;
	pointer-events: none;
}
@media (max-width: 900px) {
	.header { padding: 18px 10px 0 10px; }
	.logo { width: 90px; height: 90px; }
	.headline { font-size: 2.1rem; }
	.subheadline { font-size: 1.2rem; }
	.main-content { padding: 0 10px; }
}
</style>

{#if loading}npm install @splinetool/runtime
<div class="preloader">
	<div class="preloader-inner">
		<div class="ticker">{ticker}%</div>
		<div class="ticker-label">Loading Experience...</div>
	</div>
</div>
{/if}

<div class="spline-bg">
	<canvas id="canvas3d"></canvas>
</div>
<div class="header">
	<div class="logo">
		<img src="/icon-tfb.png" alt="Think Forge Global Logo" style="width:100%;height:100%;object-fit:contain;" />
	</div>
	<nav class="nav">
		<a href="#">Blog</a>
		<a href="#">About</a>
		<a href="#">Services</a>
		<a href="#">Client</a>
		<a href="#">Work</a>
		<button class="contact-btn">Contact us</button>
	</nav>
</div>
<div class="main-content">
	<div class="status"><span class="status-dot"></span> Available for New Projects</div>
	<div class="headline">Forging Smarter Growth</div>
	<div class="subheadline">Through <span class="tech">Technology</span></div>
	<div class="desc">We don't just create tech, we solve your brand's biggest challenges</div>
	<button class="connect-btn">Connect With Us</button>
</div>
