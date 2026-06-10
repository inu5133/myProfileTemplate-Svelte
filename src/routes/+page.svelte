<script>
	import { onMount } from 'svelte';

	// Stats config
	const stats = [
		{ name: 'Strength (王道往く力)', value: 81, max: 100, desc: '王道を征くパワフルな肉体美' },
		{ name: 'Speed (イキスギ速度)', value: 114, max: 120, desc: '常人を置き去りにする速度' },
		{ name: 'Charisma (カリスマ性)', value: 514, max: 514, desc: 'ネット界を統一した圧倒的求心力' },
		{ name: 'Mystery (神秘性)', value: 999, max: 999, desc: '現在も行方不明という神話的ベール' },
		{ name: 'Voice Power (咆哮)', value: 88, max: 100, desc: '枕をデカくする迫真のボイス' }
	];

	// Quotes config
	const quotes = [
		{ text: '114514 (いいよ！こいよ！)', sub: 'Ii yo! Koi yo!', color: '#d49e2a', detail: '最も有名な王道の快諾フレーズ' },
		{ text: 'イキスギィ！イクイク！', sub: 'Iki sugii! Iku iku!', color: '#e5c158', detail: '限界を超え、感情が高ぶった際の絶叫' },
		{ text: 'ヌッ！', sub: 'Nu!', color: '#f4eacc', detail: '威厳に満ちた静かなる登場音' },
		{ text: 'やめてくれよぉ（絶望）', sub: 'Yamete kure yo', color: '#b87e1f', detail: '人間の持つ哀愁と繊細さを表す悲痛な叫び' },
		{ text: '冷えてるか～？', sub: 'Hieteru ka~?', color: '#d49e2a', detail: '他者を気遣う先輩としての深い慈愛' },
		{ text: '王道を往く', sub: 'Oudou wo yuku', color: '#e5c158', detail: '自らの生き様を示す哲学的なマニフェスト' }
	];

	// Theories config
	const theories = [
		{ title: '新説・野獣先輩女の子説', content: 'そのしなやかな身のこなしや一部の繊細な発言から、実は女の子なのではないかという説。ネットで熱心な考察が続いている。' },
		{ title: '野獣先輩惑星説', content: '地球の重力や自転周期、その他天文学的な数値が「114514」に完全に一致することから、野獣先輩は天体そのものであるとする壮大な宇宙的仮説。' },
		{ title: '野獣先輩光速説', content: '彼が放つ圧倒的なエネルギーと消滅の速さはアインシュタインの相対性理論を超越しており、光速を超えて宇宙を旅しているとする説。' },
		{ title: '野獣先輩救世主説', content: 'あらゆる人々の悲しみやネット上の混沌をすべてその身に引き受け、笑顔をもたらした現代の救世主（メシア）であるとする説。' }
	];

	// Timeline events
	const timeline = [
		{ year: '2001年', title: '伝説の始まり', desc: 'ビデオ作品にて、王道を征く孤高の存在としてデビュー。圧倒的な存在感を示す。' },
		{ year: '2007年', title: 'ネット文化との邂逅', desc: 'ニコニコ動画などの動画プラットフォームにおいて、その独特な発言や仕草が切り抜かれ一大ブームに。' },
		{ year: '2010年代', title: 'BB素材化と神格化', desc: 'あらゆるクリエイターによって素材として使用され、ネットミームの帝王として君臨。「114514」はネットの一般教養へ。' },
		{ year: '現代', title: '概念としての存在へ', desc: '姿を消したことでかえって神秘性が高まり、ネット文化の生ける伝説（あるいは概念）として崇められている。' }
	];

	// Client-side interactive states
	let selectedTheoryIndex = 0;
	let activeVisualizerQuote = '';
	let visualizerActive = false;
	let visualizerBars = Array(15).fill(0);
	let visualizerTimer;

	// Guestbook state
	let comments = [
		{ name: '王道を往く者', message: 'いいよ！こいよ！このサイト最高すぎるだろ！', date: '2026/06/10 18:15' },
		{ name: '通りすがりの一般兵', message: '冷えてるか～？冷えてるよ！', date: '2026/06/10 18:16' }
	];
	let newName = '';
	let newMessage = '';

	function playQuote(quote) {
		activeVisualizerQuote = quote.text;
		visualizerActive = true;
		
		// Animate audio-visualizer simulation bars
		if (visualizerTimer) clearInterval(visualizerTimer);
		visualizerTimer = setInterval(() => {
			visualizerBars = visualizerBars.map(() => Math.floor(Math.random() * 80) + 20);
		}, 100);

		// Stop simulation after 3 seconds
		setTimeout(() => {
			visualizerActive = false;
			activeVisualizerQuote = '';
			clearInterval(visualizerTimer);
			visualizerBars = Array(15).fill(0);
		}, 3000);
	}

	function addComment() {
		if (!newName.trim() || !newMessage.trim()) return;
		const now = new Date();
		const formattedDate = `${now.getFullYear()}/${String(now.getMonth() + 1).padStart(2, '0')}/${String(now.getDate()).padStart(2, '0')} ${String(now.getHours()).padStart(2, '0')}:${String(now.getMinutes()).padStart(2, '0')}`;
		comments = [...comments, { name: newName, message: newMessage, date: formattedDate }];
		newName = '';
		newMessage = '';
	}

	onMount(() => {
		return () => {
			if (visualizerTimer) clearInterval(visualizerTimer);
		};
	});
</script>

<div class="min-height-screen py-12 px-4 sm:px-6 lg:px-8">
	<!-- Navbar / Header -->
	<header class="max-w-6xl mx-auto flex items-center justify-between mb-16 border-b border-amber-500/10 pb-6">
		<div class="flex items-center gap-3">
			<div class="w-10 h-10 rounded-full border border-amber-500/30 flex items-center justify-center bg-amber-500/10 text-amber-400 font-bold text-lg">
				野
			</div>
			<span class="font-semibold text-lg tracking-wider text-amber-100">YAJU SENPAI ARCHIVE</span>
		</div>
		<div class="flex gap-6 text-sm text-gray-400">
			<a href="#profile" class="hover:text-amber-400 transition-colors">PROFILE</a>
			<a href="#quotes" class="hover:text-amber-400 transition-colors">SOUNDBOARD</a>
			<a href="#theories" class="hover:text-amber-400 transition-colors">THEORIES</a>
			<a href="#guestbook" class="hover:text-amber-400 transition-colors">GUESTBOOK</a>
		</div>
	</header>

	<main class="max-w-6xl mx-auto space-y-24">
		<!-- Hero Section -->
		<section class="grid grid-cols-1 md:grid-cols-12 gap-8 items-center pt-8">
			<div class="md:col-span-7 space-y-6">
				<div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/10 border border-amber-500/20 text-amber-400 text-xs font-semibold tracking-widest">
					<span class="w-2 h-2 rounded-full bg-amber-400 animate-ping"></span>
					LEGENDARY INTERNET ICON
				</div>
				<h1 class="text-5xl md:text-7xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-amber-400 via-yellow-200 to-amber-600 tracking-tight leading-none">
					野獣先輩 <br/>
					<span class="text-2xl md:text-3xl font-medium text-gray-400 tracking-normal">The Absolute Myth of Japanese Net Culture</span>
				</h1>
				<p class="text-gray-300 text-lg leading-relaxed max-w-xl">
					「いいよ！こいよ！」「冷えてるか～？」など、数々の伝説的フレーズとネットミームを生み出した孤高の存在。その正体は未だ厚い謎に包まれており、現代のネットシーンにおいては一種の概念、あるいは神格として語り継がれています。
				</p>
				<div class="flex gap-4 pt-4">
					<a href="#quotes" class="px-6 py-3 rounded-lg bg-gradient-to-r from-amber-500 to-amber-600 text-black font-bold tracking-wider hover:from-amber-400 hover:to-amber-500 transition-all duration-300 transform hover:-translate-y-0.5 shadow-lg shadow-amber-500/20">
						ボイスを再生する
					</a>
					<a href="#theories" class="px-6 py-3 rounded-lg border border-amber-500/20 text-amber-400 font-semibold tracking-wider hover:bg-amber-500/10 transition-all duration-300">
						説を考察する
					</a>
				</div>
			</div>
			<div class="md:col-span-5 flex justify-center">
				<div class="relative w-80 h-80 md:w-96 md:h-96 rounded-2xl overflow-hidden glass-panel flex items-center justify-center p-6 border-amber-500/20 group">
					<div class="absolute inset-0 bg-gradient-to-tr from-amber-500/10 to-transparent opacity-50"></div>
					<img src="/beast.png" alt="Legendary Beast Crest" class="w-full h-full object-contain animate-float group-hover:scale-105 transition-transform duration-700" />
				</div>
			</div>
		</section>

		<!-- Profile & Stats Grid -->
		<section id="profile" class="space-y-8 scroll-mt-24">
			<div class="border-l-4 border-amber-500 pl-4">
				<h2 class="text-3xl font-bold tracking-wider text-amber-100">BASIC STATUS</h2>
				<p class="text-gray-400 text-sm">野獣先輩の基本スペック・ステータスHUD</p>
			</div>
			
			<div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
				<!-- Bio Details Card -->
				<div class="glass-panel p-8 rounded-2xl space-y-6 lg:col-span-1 border-amber-500/20">
					<h3 class="text-xl font-bold text-amber-400 border-b border-amber-500/10 pb-3">登録プロフィール</h3>
					<ul class="space-y-4 text-sm">
						<li class="flex justify-between border-b border-white/5 pb-2">
							<span class="text-gray-400">通称</span>
							<span class="font-semibold text-gray-200">野獣先輩、田所、鈴木</span>
						</li>
						<li class="flex justify-between border-b border-white/5 pb-2">
							<span class="text-gray-400">身長</span>
							<span class="font-semibold text-gray-200">170 cm</span>
						</li>
						<li class="flex justify-between border-b border-white/5 pb-2">
							<span class="text-gray-400">体重</span>
							<span class="font-semibold text-gray-200">74 kg</span>
						</li>
						<li class="flex justify-between border-b border-white/5 pb-2">
							<span class="text-gray-400">誕生日</span>
							<span class="font-semibold text-gray-200">8月10日 (野獣の日)</span>
						</li>
						<li class="flex justify-between border-b border-white/5 pb-2">
							<span class="text-gray-400">属性</span>
							<span class="font-semibold text-gray-200">光 / 王道 / 迫真</span>
						</li>
					</ul>
					<div class="bg-amber-500/5 p-4 rounded-xl border border-amber-500/10 text-xs leading-relaxed text-amber-300">
						<strong>※ステータス考察:</strong> 全体的に筋肉質で均整の取れた体躯を持ち、威圧感と包容力を兼ね備える完璧なバランス型。
					</div>
				</div>

				<!-- Stats Progress Card -->
				<div class="glass-panel p-8 rounded-2xl space-y-6 lg:col-span-2 border-amber-500/20">
					<h3 class="text-xl font-bold text-amber-400 border-b border-amber-500/10 pb-3">戦闘能力評価 (PARAM)</h3>
					<div class="space-y-5">
						{#each stats as stat}
							<div class="space-y-1">
								<div class="flex justify-between text-sm">
									<span class="font-semibold text-amber-100">{stat.name}</span>
									<span class="text-amber-400 font-bold">{stat.value} / {stat.max}</span>
								</div>
								<div class="w-full bg-[#181613] h-3 rounded-full overflow-hidden border border-white/5">
									<div class="bg-gradient-to-r from-amber-600 to-amber-400 h-full rounded-full transition-all duration-1000" style="width: {(stat.value / stat.max) * 100}%"></div>
								</div>
								<p class="text-gray-400 text-xs">{stat.desc}</p>
							</div>
						{/each}
					</div>
				</div>
			</div>
		</section>

		<!-- Soundboard Section -->
		<section id="quotes" class="space-y-8 scroll-mt-24">
			<div class="border-l-4 border-amber-500 pl-4">
				<h2 class="text-3xl font-bold tracking-wider text-amber-100">LEGENDARY SOUNDBOARD</h2>
				<p class="text-gray-400 text-sm">名言・フレーズを選択して脳内再生（エフェクト付き）</p>
			</div>

			<!-- Dynamic Visualizer Screen -->
			<div class="w-full glass-panel p-6 rounded-2xl border-amber-500/20 flex flex-col items-center justify-center min-h-[140px] text-center relative overflow-hidden">
				{#if visualizerActive}
					<div class="absolute inset-0 bg-amber-500/5 pointer-events-none"></div>
					<div class="text-amber-400 font-extrabold text-2xl md:text-3xl mb-4 animate-bounce tracking-widest">
						「{activeVisualizerQuote}」
					</div>
					<!-- Fake Equalizer Visualizer -->
					<div class="flex gap-1 items-end justify-center h-12 w-full max-w-xs">
						{#each visualizerBars as barHeight}
							<div class="w-1 bg-amber-500 rounded-t transition-all duration-100" style="height: {barHeight}%"></div>
						{/each}
					</div>
				{:else}
					<div class="text-gray-500 italic text-sm">
						ボイスフレーズをタップすると、波形シミュレーターが起動します
					</div>
				{/if}
			</div>

			<!-- Quote Buttons Grid -->
			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
				{#each quotes as quote}
					<button 
						onclick={() => playQuote(quote)}
						class="text-left glass-panel p-5 rounded-xl border-amber-500/15 hover:bg-amber-500/5 transition-all duration-300 transform hover:-translate-y-1 focus:outline-none focus:ring-2 focus:ring-amber-500/50 flex flex-col justify-between h-32"
					>
						<div>
							<span class="text-xs text-amber-500/70 tracking-wider font-semibold uppercase">{quote.sub}</span>
							<p class="text-lg font-bold text-amber-100 mt-1">{quote.text}</p>
						</div>
						<p class="text-gray-400 text-xs mt-2 border-t border-white/5 pt-2">{quote.detail}</p>
					</button>
				{/each}
			</div>
		</section>

		<!-- Theories / Myths section -->
		<section id="theories" class="grid grid-cols-1 lg:grid-cols-12 gap-8 scroll-mt-24">
			<div class="lg:col-span-4 space-y-6">
				<div class="border-l-4 border-amber-500 pl-4">
					<h2 class="text-3xl font-bold tracking-wider text-amber-100">THEORIES</h2>
					<p class="text-gray-400 text-sm">ネット上でまことしやかに囁かれる諸説</p>
				</div>
				<p class="text-gray-300 text-sm leading-relaxed">
					野獣先輩はあまりにも多面的な魅力を持つため、有志による天文学的・歴史的・言語学的アプローチからの研究が進んでおり、毎年新たな「新説」が誕生しています。
				</p>

				<!-- Theory Selector List -->
				<div class="space-y-2">
					{#each theories as theory, index}
						<button 
							onclick={() => selectedTheoryIndex = index}
							class="w-full text-left p-3 rounded-lg border text-sm transition-all {selectedTheoryIndex === index ? 'bg-amber-500/20 border-amber-500 text-amber-200' : 'bg-transparent border-white/5 text-gray-400 hover:bg-white/5'}"
						>
							{theory.title}
						</button>
					{/each}
				</div>
			</div>

			<div class="lg:col-span-8">
				<div class="glass-panel p-8 rounded-2xl border-amber-500/20 h-full flex flex-col justify-between">
					<div class="space-y-4">
						<div class="inline-flex px-3 py-1 rounded bg-amber-500/10 border border-amber-500/20 text-amber-400 text-xs font-semibold">
							RESEARCH THEORY #{selectedTheoryIndex + 1}
						</div>
						<h3 class="text-2xl font-bold text-amber-200">{theories[selectedTheoryIndex].title}</h3>
						<p class="text-gray-300 leading-relaxed text-base">
							{theories[selectedTheoryIndex].content}
						</p>
					</div>
					<div class="border-t border-amber-500/10 pt-4 mt-8 flex justify-between items-center text-xs text-gray-500">
						<span>出典: 民俗学およびインターネットアーカイブより</span>
						<span class="text-amber-500/50">STATUS: HYPOTHESIS</span>
					</div>
				</div>
			</div>
		</section>

		<!-- Timeline Section -->
		<section class="space-y-8">
			<div class="border-l-4 border-amber-500 pl-4">
				<h2 class="text-3xl font-bold tracking-wider text-amber-100">HISTORY TIMELINE</h2>
				<p class="text-gray-400 text-sm">神話の成立から現在に至る軌跡</p>
			</div>

			<div class="relative border-l border-amber-500/20 ml-4 pl-8 space-y-12">
				{#each timeline as item}
					<div class="relative group">
						<!-- Dot indicator -->
						<div class="absolute -left-[37px] top-1.5 w-4 h-4 rounded-full bg-[#0b0a0a] border border-amber-500 flex items-center justify-center">
							<div class="w-1.5 h-1.5 rounded-full bg-amber-500 group-hover:scale-150 transition-transform"></div>
						</div>
						
						<div class="glass-panel p-6 rounded-xl border-amber-500/10 hover:border-amber-500/30 transition-all max-w-3xl">
							<span class="text-xs font-bold text-amber-400 tracking-widest">{item.year}</span>
							<h4 class="text-lg font-bold text-amber-100 mt-1">{item.title}</h4>
							<p class="text-gray-300 text-sm mt-2 leading-relaxed">{item.desc}</p>
						</div>
					</div>
				{/each}
			</div>
		</section>

		<!-- Guestbook Section -->
		<section id="guestbook" class="space-y-8 scroll-mt-24">
			<div class="border-l-4 border-amber-500 pl-4">
				<h2 class="text-3xl font-bold tracking-wider text-amber-100">GUESTBOOK (BBS)</h2>
				<p class="text-gray-400 text-sm">迫真のメッセージを残していってくれよぉ</p>
			</div>

			<div class="grid grid-cols-1 lg:grid-cols-12 gap-8">
				<!-- Form -->
				<div class="lg:col-span-5 glass-panel p-6 rounded-2xl border-amber-500/20 space-y-4 h-fit">
					<h3 class="text-lg font-bold text-amber-400">メッセージ投稿</h3>
					<div class="space-y-3">
						<div>
							<label for="name" class="block text-xs text-gray-400 mb-1">お名前</label>
							<input 
								type="text" 
								id="name" 
								bind:value={newName} 
								placeholder="例: 田所こうじ" 
								class="w-full bg-[#181613] border border-amber-500/20 rounded-lg p-2.5 text-sm text-gray-200 focus:outline-none focus:border-amber-500"
							/>
						</div>
						<div>
							<label for="message" class="block text-xs text-gray-400 mb-1">メッセージ</label>
							<textarea 
								id="message" 
								bind:value={newMessage} 
								rows="3" 
								placeholder="例: イキスギィ！" 
								class="w-full bg-[#181613] border border-amber-500/20 rounded-lg p-2.5 text-sm text-gray-200 focus:outline-none focus:border-amber-500 resize-none"
							></textarea>
						</div>
						<button 
							onclick={addComment} 
							class="w-full py-2.5 rounded-lg bg-amber-500 text-black font-bold text-sm tracking-widest hover:bg-amber-400 transition-colors"
						>
							書き込む
						</button>
					</div>
				</div>

				<!-- Comments List -->
				<div class="lg:col-span-7 glass-panel p-6 rounded-2xl border-amber-500/20 space-y-4 max-h-[360px] overflow-y-auto">
					<h3 class="text-lg font-bold text-amber-400">書き込み一覧</h3>
					<div class="space-y-3">
						{#each comments as comment}
							<div class="p-4 rounded-lg bg-white/5 border border-white/5 space-y-2">
								<div class="flex justify-between items-center text-xs">
									<span class="font-bold text-amber-200">{comment.name}</span>
									<span class="text-gray-500">{comment.date}</span>
								</div>
								<p class="text-sm text-gray-300 leading-relaxed">{comment.message}</p>
							</div>
						{/each}
					</div>
				</div>
			</div>
		</section>
	</main>

	<footer class="max-w-6xl mx-auto mt-24 pt-8 border-t border-amber-500/10 text-center text-xs text-gray-500 space-y-2">
		<p>© 2026 Yaju Senpai Archive. This website is a premium unofficial fan parody.</p>
		<p class="text-amber-500/30">1145148101919810</p>
	</footer>
</div>
