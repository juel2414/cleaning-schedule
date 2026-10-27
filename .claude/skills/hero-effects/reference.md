# 히어로 효과 원본 코드 (오늘분량 landing.js · landing.css)

## 1) landing.js — 글자 쪼개기 · "o" SVG

```js
const LP_BIG_O = '<svg viewBox="0 0 100 100" class="lp-big-o" aria-hidden="true"><path class="lp-o-ring" d="M51.62 3.68 A46.35 46.35 0 0 1 71.56 91.03" fill="none" stroke="#141414" stroke-width="7.3"/><path class="lp-o-arc" pathLength="100" d="M66.89 88.45 A42 42 0 0 1 33.11 88.45" fill="none" stroke="#3B5BA5" stroke-width="16"/><path class="lp-o-ring" d="M28.44 91.03 A46.35 46.35 0 0 1 48.38 3.68" fill="none" stroke="#141414" stroke-width="2.4"/></svg>';

/* 첫 화면 효과용: 글자 하나씩 감싸기 (아래에서 잘려 올라오는 효과) */
function lpChars(text, start) {
  return [...text].map((ch, i) => `<span class="lp-char" style="--i:${start + i}"><span>${ch}</span></span>`).join('');
}
/* 제목 단어 하나씩 감싸기 (흐림에서 또렷하게) */
function lpWords(text) {
  return text.split(' ').map((w, i) => `<span class="lp-word" style="--i:${i}">${w}</span>`).join(' ');
}

/**
 * 랜딩 페이지 그리기
 * options: {
 *   lang: 'ko' | 'en',
 *   onLogin: () => Promise,     // Google 로그인 시작
```

## 2) landing.js — 히어로 마크업 (renderLanding 안)

```js
      <header class="lp-hero" id="lp-top">
        <div class="lp-hero-bloom" aria-hidden="true"><i class="lp-bloom-a"></i><i class="lp-bloom-b"></i><i class="lp-bloom-c"></i><i class="lp-bloom-d"></i></div>
        <div class="lp-hero-lines" aria-hidden="true">
          <i class="lp-line-v" style="--x:20%;--d:.15s"></i><i class="lp-line-v" style="--x:50%;--d:.3s"></i><i class="lp-line-v" style="--x:80%;--d:.45s"></i>
          <i class="lp-line-h" style="--y:96px;--d:0s"></i><i class="lp-line-h lp-line-h-mid" style="--d:.25s"></i><i class="lp-line-h lp-line-h-low" style="--d:.4s"></i>
          <span class="lp-dust"></span>
        </div>
        <div class="lp-hero-glow" aria-hidden="true"></div>
        <div class="lp-topbar">
          <a href="#" class="lp-brand" data-lp-scroll="lp-top" aria-label="${E(T.brandLabel)}">
            <span class="lp-brand-tile"><img src="${LP_ASSETS.markLight}" alt=""></span>
            ${landingWordmark('md', false)}
          </a>
          <nav class="lp-nav">${navLinks('lp-nav-link')}</nav>
          <div class="lp-top-right">
            <div class="lp-lang" role="group" aria-label="${E(T.langLabel)}">
              <button type="button" data-lang="ko" class="${lang === 'ko' ? 'is-on' : ''}" aria-pressed="${lang === 'ko'}">KO</button>
              <button type="button" data-lang="en" class="${lang === 'en' ? 'is-on' : ''}" aria-pressed="${lang === 'en'}">EN</button>
            </div>
            <button type="button" class="lp-login" data-action="google-login">${E(T.login)}<span class="lp-login-arrow">↗</span></button>
          </div>
        </div>

        <h1 class="lp-hero-title"><span class="lp-dot"></span><span>${lpWords(E(T.heroTitle))}</span></h1>
        <div class="lp-wm-wrap">
          <div class="lp-big-wordmark" aria-hidden="true">
            <span class="lp-big-today">${lpChars('Today', 0)}<span class="lp-char" style="--i:5"><span class="lp-apos">’</span></span>${lpChars('s', 6)}</span>
            <span class="lp-big-dose">${lpChars('D', 7)}<span class="lp-char lp-char-o" style="--i:8"><span>${LP_BIG_O}</span></span>${lpChars('se', 9)}</span>
            <img class="lp-hero-mini" src="${LP_ASSETS.hero}" alt="">
          </div>
          <div class="lp-big-wordmark lp-wm-shine" aria-hidden="true">
            <span class="lp-big-today">${lpChars('Today', 0)}<span class="lp-char" style="--i:5"><span class="lp-apos">’</span></span>${lpChars('s', 6)}</span>
            <span class="lp-big-dose">${lpChars('D', 7)}<span class="lp-char lp-char-o" style="--i:8"><span>${LP_BIG_O}</span></span>${lpChars('se', 9)}</span>
          </div>
        </div>

        <div class="lp-hero-row">
          <div class="lp-hero-left">
            <p class="lp-hero-sub">${E(T.heroSub)}</p>
            <div class="lp-cta-row">
              ${googleBtn('lp-cta')}
              <button type="button" class="lp-install" data-action="app-install" title="${E(T.installSub)}">
                <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 4v11"/><path d="m7.5 10.5 4.5 4.5 4.5-4.5"/><path d="M5 19.5h14"/></svg>${E(T.install)}
              </button>
            </div>
            <p class="lp-alert" data-lp-alert hidden></p>
          </div>
          <img class="lp-hero-illus" src="${LP_ASSETS.hero}" alt="${E(T.illusAlt)}">
          <div class="lp-hero-right">
            <div class="lp-today-card">
              <div class="lp-today-head"><b>${E(T.todayCard)}</b><span>${E(T.todayDate)}</span></div>
              <div class="lp-today-bar"><div></div></div>
              ${T.todayItems.map((text, i) => `<div class="lp-today-item ${i < 2 ? 'is-done' : ''}"><span class="lp-check"></span>${E(text)}</div>`).join('')}
            </div>
          </div>
        </div>
      </header>

```

## 3) landing.js — 첫 화면 효과 · 아래 섹션 효과

```js
/* =========================================================================
 * 첫 화면 효과 (21st 참고 · 순수 JS/CSS, React·애니메이션 라이브러리 없음)
 *  - 등장: 큰 글자 아래에서 잘려 올라오기 · 제목 단어 흐림→또렷 · 나머지 차례로 떠오르기 · o의 파란 반달 그리기
 *  - 오늘 분량 카드: 항목이 하나씩 체크되고 막대가 차오름
 *  - 마우스: 손그림·카드·큰 글자가 깊이를 달리해 살짝 움직임(시차) · 배경 점무늬가 커서를 따라 비침 · 시작 버튼이 커서를 따라옴
 *  - 스크롤: 큰 글자가 위로 떠오르며 옅어짐
 *  움직임 줄이기 설정이면 아무 효과도 넣지 않는다.
 * ========================================================================= */
function initLandingHeroFx(landing) {
  const hero = landing && landing.querySelector('.lp-hero');
  if (!hero) return;
  const reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if (reduce) return;
  hero.classList.add('lp-fx');

  // 오늘 분량 카드: 처음엔 비워 두었다가 하나씩 체크
  const items = [...hero.querySelectorAll('.lp-today-item')];
  const doneIdx = items.map((el, i) => (el.classList.contains('is-done') ? i : -1)).filter((i) => i >= 0);
  items.forEach((el) => el.classList.remove('is-done'));
  const bar = hero.querySelector('.lp-today-bar div');
  if (bar) bar.style.width = '0%';

  const start = () => requestAnimationFrame(() => requestAnimationFrame(() => hero.classList.add('is-in')));
  if (document.fonts && document.fonts.ready) {
    Promise.race([document.fonts.ready, new Promise((r) => setTimeout(r, 1200))]).then(start);
  } else start();

  const timers = [];
  doneIdx.forEach((i, n) => {
    timers.push(setTimeout(() => {
      if (!hero.isConnected) return;
      items[i].classList.add('is-done');
      if (bar) bar.style.width = `${Math.round(((n + 1) / items.length) * 100 * 0.93)}%`;
    }, 1900 + n * 750));
  });

  // 마우스 시차 · 점무늬 빛
  let raf = 0;
  let px = 0;
  let py = 0;
  hero.addEventListener('pointermove', (e) => {
    if (e.pointerType === 'touch') return;
    const r = hero.getBoundingClientRect();
    px = ((e.clientX - r.left) / r.width) * 2 - 1;
    py = ((e.clientY - r.top) / r.height) * 2 - 1;
    hero.style.setProperty('--gx', `${e.clientX - r.left}px`);
    hero.style.setProperty('--gy', `${e.clientY - r.top}px`);
    if (!raf) raf = requestAnimationFrame(() => {
      raf = 0;
      hero.style.setProperty('--px', px.toFixed(3));
      hero.style.setProperty('--py', py.toFixed(3));
    });
  });
  hero.addEventListener('pointerleave', () => {
    hero.style.setProperty('--px', '0');
    hero.style.setProperty('--py', '0');
  });

  // 시작 버튼: 커서를 살짝 따라온다
  const cta = hero.querySelector('.lp-cta');
  if (cta) {
    cta.addEventListener('pointermove', (e) => {
      const r = cta.getBoundingClientRect();
      const dx = (e.clientX - (r.left + r.width / 2)) / r.width;
      const dy = (e.clientY - (r.top + r.height / 2)) / r.height;
      cta.style.transform = `translate(${(dx * 10).toFixed(1)}px, ${(dy * 8).toFixed(1)}px)`;
    });
    cta.addEventListener('pointerleave', () => { cta.style.transform = ''; });
  }

  // 스크롤: 첫 화면을 지나는 만큼 0 → 1
  let sraf = 0;
  const onScroll = () => {
    if (!hero.isConnected) { window.removeEventListener('scroll', onScroll); timers.forEach(clearTimeout); return; }
    if (sraf) return;
    sraf = requestAnimationFrame(() => {
      sraf = 0;
      const h = hero.offsetHeight || window.innerHeight;
      const sy = Math.min(1, Math.max(0, window.scrollY / h));
      hero.style.setProperty('--sy', sy.toFixed(3));
    });
  };
  window.addEventListener('scroll', onScroll, { passive: true });
}

/* =========================================================================
 * 아래 섹션 등장 효과 (순수 JS/CSS) — 화면에 들어올 때 한 번씩
 *  - 제목: 아래에서 잘려 올라오기
 *  - 예전 방식: 줄이 차례로 들어오고 취소선이 그어진다 → 오늘분량 1·2·3이 하나씩 튀어나온다
 *  - 계산기: 하루 분량 숫자가 0부터 올라간다, 말풍선이 톡 튀어나온다
 *  - 없앤 세 가지: 글자 위 파란 취소선이 그어지고, 카드가 반대쪽에서 들어온다
 *    (목차 줄이 차례로 · 달력 칸이 하루씩 채워짐 · 원래 계획은 밀려나고 새 계획이 올라옴)
 *  - 이런 분들: 그림 알약이 하나씩 튀어나오고 아래 칸이 차례로 올라온다
 *  - 자주 묻는 질문 · 마지막: 차례로 떠오르기
 * ========================================================================= */
function initLandingScrollFx(landing) {
  if (!landing || !('IntersectionObserver' in window)) return;
  const reduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
  if (reduce) return;
  landing.classList.add('lp-sfx');
  // 차례 번호 매기기
  const order = (sel) => landing.querySelectorAll(sel).forEach((el, i) => el.style.setProperty('--ri', i));
  order('.lp-old li');
  order('.lp-new-step');
  order('.lp-toc-row');
  order('.lp-strip span');
  order('.lp-who-sentence .lp-pill');
  order('.lp-who-item');
  order('.lp-faq-item');
  order('.lp-days .lp-day');

  // 계산기 숫자: 0부터 지금 값까지 올라간다 (한 번만)
  const countUp = () => {
    const el = landing.querySelector('[data-lp-perday]');
    const target = Number(el && el.textContent);
    if (!el || !Number.isFinite(target) || target <= 0) return;
    const t0 = performance.now();
    const step = (now) => {
      const k = Math.min(1, (now - t0) / 1100);
      const eased = 1 - Math.pow(1 - k, 3);
      if (el.dataset.lpTouched) return; // 사용자가 값을 바꾸면 멈춘다
      el.textContent = String(Math.round(target * eased));
      if (k < 1) requestAnimationFrame(step);
      else el.textContent = String(target);
    };
    el.textContent = '0';
    requestAnimationFrame(step);
  };
  landing.querySelectorAll('[data-lp-amount], [data-lp-weeks], [data-lp-day]').forEach((x) => {
    x.addEventListener('input', () => { const el = landing.querySelector('[data-lp-perday]'); if (el) el.dataset.lpTouched = '1'; });
    x.addEventListener('click', () => { const el = landing.querySelector('[data-lp-perday]'); if (el) el.dataset.lpTouched = '1'; });
  });

  const targets = landing.querySelectorAll('.lp-why, .lp-calc, .lp-h-remove, .lp-rm-row, .lp-who, .lp-story, .lp-faq-main, .lp-end');
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (!entry.isIntersecting) return;
      entry.target.classList.add('is-seen');
      if (entry.target.classList.contains('lp-calc')) setTimeout(countUp, 350);
      io.unobserve(entry.target);
    });
  }, { threshold: 0.22, rootMargin: '0px 0px -8% 0px' });
  targets.forEach((el) => io.observe(el));
}
```

## 4) landing.css — 효과 전부 (첫 화면 효과 ~ 아래 섹션 효과)

```css
/* ===== 첫 화면 효과 (21st 참고 · CSS 트랜지션) — .lp-fx는 움직임 줄이기 설정이 아닐 때만 붙는다 ===== */
.lp-char { display: inline-block; }
.lp-char > span { display: inline-block; }
.lp-char-o > span { display: inline; }
.lp-hero { position: relative; }

.lp-hero-glow { position: absolute; inset: 0; z-index: 0; pointer-events: none; opacity: 0; transition: opacity .5s ease;
  background-image: radial-gradient(rgba(20, 20, 20, .22) 1px, transparent 1.5px); background-size: 22px 22px;
  -webkit-mask-image: radial-gradient(300px circle at var(--gx, 50%) var(--gy, 40%), #000 0%, transparent 70%);
  mask-image: radial-gradient(300px circle at var(--gx, 50%) var(--gy, 40%), #000 0%, transparent 70%); }
.lp-fx:hover .lp-hero-glow { opacity: 1; }

/* 1. 큰 글자: 아래에서 잘려 올라오기 (Vertical Cut Reveal) */
.lp-fx .lp-char > span { transform: translateY(.42em); clip-path: inset(100% -40% -60% -40%); opacity: 0;
  transition: transform .95s cubic-bezier(.2, .8, .2, 1), clip-path .95s cubic-bezier(.2, .8, .2, 1), opacity .5s ease;
  transition-delay: calc(260ms + var(--i) * 60ms); }
.lp-fx.is-in .lp-char > span { transform: none; clip-path: inset(-60% -40% -60% -40%); opacity: 1; }
/* o: 고리가 다이얼처럼 네 번 '딱딱' 끊어 돌다가 정확히 멈춘다 */
.lp-fx .lp-big-o { transform: rotate(-120deg); transform-origin: 50% 50%; }
.lp-fx.is-in .lp-big-o { animation: lpDial .9s .75s both; }
@keyframes lpDial {
  0% { transform: rotate(-120deg); animation-timing-function: cubic-bezier(.8, 0, .2, 1); }
  20% { transform: rotate(-90deg); animation-timing-function: steps(1, end); }
  25% { transform: rotate(-90deg); animation-timing-function: cubic-bezier(.8, 0, .2, 1); }
  45% { transform: rotate(-60deg); animation-timing-function: steps(1, end); }
  50% { transform: rotate(-60deg); animation-timing-function: cubic-bezier(.8, 0, .2, 1); }
  70% { transform: rotate(-30deg); animation-timing-function: steps(1, end); }
  75% { transform: rotate(-30deg); animation-timing-function: cubic-bezier(.8, 0, .2, 1); }
  100% { transform: rotate(0deg); }
}
/* 파란 반달: 다이얼이 멈추며 '탁' 한 뒤, 천천히 부드럽게 차오른다 */
.lp-fx .lp-o-arc { stroke-dasharray: 100; stroke-dashoffset: 100; opacity: .35;
  transition: stroke-dashoffset 1.4s cubic-bezier(.22, 1, .36, 1) 1.75s, opacity .9s ease 1.75s; }
.lp-fx.is-in .lp-o-arc { stroke-dashoffset: 0; opacity: 1; }
.lp-fx.is-in .lp-char-o > span { animation: lpClick .22s 1.62s both; }
@keyframes lpClick { 0% { transform: scale(1); } 40% { transform: scale(1.045); } 100% { transform: scale(1); } }

/* 2. 제목: 단어가 흐림에서 또렷하게 */
.lp-fx .lp-word { display: inline-block; opacity: 0; filter: blur(10px); transform: translateY(10px);
  transition: opacity .7s ease, filter .7s ease, transform .7s cubic-bezier(.2, .8, .2, 1); transition-delay: calc(80ms + var(--i) * 90ms); }
.lp-fx.is-in .lp-word { opacity: 1; filter: none; transform: none; }
.lp-fx .lp-dot { transform: scale(0); transition: transform .5s cubic-bezier(.3, 1.6, .5, 1) .05s; }
.lp-fx.is-in .lp-dot { transform: none; }

/* 3. 나머지: 차례로 떠오르기 */
.lp-fx .lp-hero-sub, .lp-fx .lp-cta, .lp-fx .lp-hero-illus, .lp-fx .lp-today-card, .lp-fx .lp-topbar { opacity: 0; translate: 0 18px;
  transition: opacity .8s ease, translate .9s cubic-bezier(.2, .8, .2, 1), transform .25s ease-out, background .15s; }
.lp-fx .lp-topbar { translate: 0 -10px; transition-delay: 0s; }
.lp-fx .lp-hero-sub { transition-delay: .95s, .95s, 0s, 0s; }
.lp-fx .lp-cta { transition-delay: 1.05s, 1.05s, 0s, 0s; }
.lp-fx .lp-hero-illus { transition-delay: 1.15s, 1.15s, 0s, 0s; }
.lp-fx .lp-today-card { transition-delay: 1.3s, 1.3s, 0s, 0s; }
.lp-fx.is-in .lp-hero-sub, .lp-fx.is-in .lp-cta, .lp-fx.is-in .lp-hero-illus, .lp-fx.is-in .lp-today-card, .lp-fx.is-in .lp-topbar { opacity: 1; translate: 0 0; }

/* 4. 오늘 분량 카드: 하나씩 체크 · 막대 차오름 */
.lp-fx .lp-today-bar div { transition: width .7s cubic-bezier(.2, .8, .2, 1); }
.lp-fx .lp-check { transition: background .25s ease, border-color .25s ease, transform .35s cubic-bezier(.3, 1.8, .5, 1); }
.lp-fx .lp-today-item { transition: color .3s ease; }
.lp-fx .lp-today-item.is-done .lp-check { transform: scale(1.12); animation: lpPop .4s cubic-bezier(.3, 1.8, .5, 1); }
@keyframes lpPop { 0% { transform: scale(.6); } 100% { transform: scale(1); } }

/* 5. 마우스 시차 (깊이: 카드 > 손그림 > 큰 글자) · 6. 스크롤하면 큰 글자가 떠오르며 옅어짐 */
.lp-fx .lp-big-wordmark { transform: translate3d(calc(var(--px, 0) * -6px), calc(var(--py, 0) * -4px + var(--sy, 0) * -70px), 0) scale(calc(1 - var(--sy, 0) * .05));
  opacity: calc(1 - var(--sy, 0) * .55); transition: transform .35s ease-out; }
.lp-fx.is-in .lp-hero-illus { transform: translate3d(calc(var(--px, 0) * 14px), calc(var(--py, 0) * 10px), 0); }
.lp-fx.is-in .lp-today-card { transform: translate3d(calc(var(--px, 0) * 22px), calc(var(--py, 0) * 16px), 0) rotateX(calc(var(--py, 0) * -4deg)) rotateY(calc(var(--px, 0) * 5deg)); transform-style: preserve-3d; }
.lp-fx .lp-hero-right { perspective: 900px; }
.lp-fx .lp-cta { transition-property: opacity, translate, transform, background; }
.lp-fx.is-in .lp-cta:hover { box-shadow: 0 10px 26px -12px rgba(20, 20, 20, .6); }

@media (max-width: 760px) {
  .lp-fx .lp-big-wordmark { transform: translate3d(0, calc(var(--sy, 0) * -40px), 0); }
  .lp-fx.is-in .lp-today-card, .lp-fx.is-in .lp-hero-illus { transform: none; }
  .lp-hero-glow { display: none; }
}

/* ===== 첫 화면 배경: 번지는 빛 (21st Animated Gradient · Bloom · Silk 계열 참고, 순수 CSS) =====
   종이 회색 위에 파랑 · 연파랑 · 흰빛 덩어리가 천천히 흐르고, 옅은 필름 질감을 얹는다. 마우스를 따라 살짝 밀린다. */
.lp-hero-bloom { position: absolute; inset: 0; z-index: 0; overflow: hidden; pointer-events: none;
  transform: translate3d(calc(var(--px, 0) * -24px), calc(var(--py, 0) * -18px), 0); transition: transform .8s ease-out; }
.lp-hero-bloom i { position: absolute; display: block; border-radius: 50%; filter: blur(70px); opacity: .9; will-change: transform; }
.lp-bloom-a { width: 46vw; height: 46vw; left: -8vw; top: -14vw; background: radial-gradient(circle at 40% 40%, rgba(59, 91, 165, .38), rgba(59, 91, 165, 0) 68%); animation: lpBloomA 26s ease-in-out infinite alternate; }
.lp-bloom-b { width: 40vw; height: 40vw; right: -6vw; top: 8vh; background: radial-gradient(circle at 50% 50%, rgba(223, 228, 239, .95), rgba(223, 228, 239, 0) 70%); animation: lpBloomB 22s ease-in-out infinite alternate; }
.lp-bloom-c { width: 36vw; height: 36vw; left: 30vw; bottom: -18vw; background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, .9), rgba(255, 255, 255, 0) 68%); animation: lpBloomC 30s ease-in-out infinite alternate; }
.lp-bloom-d { width: 28vw; height: 28vw; right: 14vw; bottom: -6vw; background: radial-gradient(circle at 50% 50%, rgba(59, 91, 165, .26), rgba(59, 91, 165, 0) 70%); animation: lpBloomD 24s ease-in-out infinite alternate; }
@keyframes lpBloomA { 0% { transform: translate(0, 0) scale(1); } 50% { transform: translate(14vw, 10vh) scale(1.12); } 100% { transform: translate(4vw, 22vh) scale(.95); } }
@keyframes lpBloomB { 0% { transform: translate(0, 0) scale(1); } 50% { transform: translate(-12vw, 14vh) scale(1.08); } 100% { transform: translate(-4vw, -6vh) scale(1.15); } }
@keyframes lpBloomC { 0% { transform: translate(0, 0) scale(1); } 50% { transform: translate(-16vw, -14vh) scale(1.1); } 100% { transform: translate(10vw, -8vh) scale(.9); } }
@keyframes lpBloomD { 0% { transform: translate(0, 0) scale(.9); } 50% { transform: translate(-20vw, -24vh) scale(1.15); } 100% { transform: translate(-8vw, -10vh) scale(1); } }
/* 필름 질감 */
.lp-hero-bloom::after { content: ''; position: absolute; inset: -50%; opacity: .07; mix-blend-mode: multiply;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E"); }
/* 처음엔 빛도 서서히 켜진다 */
.lp-fx .lp-hero-bloom { opacity: 0; transition: opacity 1.6s ease .2s, transform .8s ease-out; }
.lp-fx.is-in .lp-hero-bloom { opacity: 1; }
@media (prefers-reduced-motion: reduce) { .lp-hero-bloom i { animation: none; } }
@media (max-width: 760px) {
  .lp-hero { overflow: hidden; }
  .lp-hero-bloom i { filter: blur(50px); }
  .lp-bloom-a { width: 110vw; height: 110vw; left: -40vw; top: -30vw; }
  .lp-bloom-b { width: 90vw; height: 90vw; right: -40vw; top: 30vh; }
  .lp-bloom-c, .lp-bloom-d { width: 80vw; height: 80vw; }
}

.lp-hero > *:not(.lp-hero-glow):not(.lp-hero-bloom):not(.lp-hero-lines) { position: relative; z-index: 1; }

/* ===== 첫 화면 가는 선 격자 + 먼지 (21st Hero Minimalism 참고 · 밝은 종이에 맞게 뒤집음) =====
   화면을 가로지르는 가는 선이 하나씩 그어져 격자를 만들고, 아주 작은 먼지가 천천히 떠다닌다. */
.lp-hero-lines { position: absolute; inset: 0; z-index: 0; pointer-events: none; overflow: hidden; }
.lp-hero-lines i { position: absolute; display: block; background: rgba(20, 20, 20, .09); }
.lp-line-v { top: 0; bottom: 0; left: var(--x); width: 1px; transform-origin: 50% 0; }
.lp-line-h { left: 0; right: 0; top: var(--y); height: 1px; transform-origin: 0 50%; }
.lp-line-h-mid { top: auto; bottom: 46%; }
.lp-line-h-low { top: auto; bottom: clamp(150px, 26vh, 300px); }
.lp-fx .lp-line-v { transform: scaleY(0); transition: transform 1.6s cubic-bezier(.65, 0, .35, 1) var(--d); }
.lp-fx .lp-line-h { transform: scaleX(0); transition: transform 1.6s cubic-bezier(.65, 0, .35, 1) var(--d); }
.lp-fx.is-in .lp-line-v, .lp-fx.is-in .lp-line-h { transform: none; }
/* 먼지: 작은 점 두 겹이 서로 다른 속도로 떠다닌다 */
.lp-dust, .lp-dust::after { position: absolute; inset: -20%; display: block; opacity: .55;
  background-image: radial-gradient(rgba(20, 20, 20, .35) .8px, transparent 1.2px), radial-gradient(rgba(59, 91, 165, .45) .9px, transparent 1.3px);
  background-size: 173px 151px, 229px 197px; background-position: 0 0, 61px 89px; animation: lpDust 60s linear infinite; }
.lp-dust::after { content: ''; inset: 0; opacity: .7; background-size: 113px 131px, 157px 139px; background-position: 37px 11px, 97px 53px; animation-duration: 90s; animation-direction: reverse; }
@keyframes lpDust { from { transform: translate3d(0, 0, 0); } to { transform: translate3d(-6%, -10%, 0); } }
.lp-fx .lp-dust { opacity: 0; transition: opacity 2s ease 1s; }
.lp-fx.is-in .lp-dust { opacity: .55; }
@media (prefers-reduced-motion: reduce) { .lp-dust, .lp-dust::after { animation: none; } }
@media (max-width: 760px) { .lp-line-v[style*="50%"] { display: none; } .lp-line-h-mid { display: none; } }

/* ===== 메인 타이틀을 한 번 휩싸고 사라지는 빛 (o 애니메이션이 끝난 뒤) =====
   같은 글자를 겹쳐 두고, 비스듬한 빛 띠가 지나간 자리만 밝게 빛나게 한다. */
.lp-wm-wrap { position: relative; }
.lp-wm-shine { display: none; }
.lp-fx .lp-wm-shine { display: flex; position: absolute !important; left: 0; right: 0; top: 0; pointer-events: none; z-index: 2;
  color: #f7f9ff; text-shadow: 0 0 14px rgba(159, 179, 224, .7), 0 0 3px rgba(255, 255, 255, .6);
  -webkit-mask-image: linear-gradient(100deg, transparent 36%, #000 47%, #000 53%, transparent 64%);
  mask-image: linear-gradient(100deg, transparent 36%, #000 47%, #000 53%, transparent 64%);
  -webkit-mask-size: 260% 100%; mask-size: 260% 100%; -webkit-mask-repeat: no-repeat; mask-repeat: no-repeat;
  -webkit-mask-position: 130% 0; mask-position: 130% 0; opacity: 0; }
/* 파란 반달이 반쯤 차오르면(2.05초 · 처음에 빠르게 차오르는 곡선) 시작 */
.lp-fx.is-in .lp-wm-shine { animation: lpWrapLight 1.6s cubic-bezier(.45, 0, .2, 1) 2.05s both; }
@keyframes lpWrapLight {
  0% { -webkit-mask-position: 130% 0; mask-position: 130% 0; opacity: 0; }
  12% { opacity: .62; }
  80% { opacity: .62; }
  100% { -webkit-mask-position: -30% 0; mask-position: -30% 0; opacity: 0; }
}
/* 겹친 글자는 처음부터 다 보이는 상태 (등장 효과 · 다이얼 없이) */
.lp-fx .lp-wm-shine .lp-char > span { transform: none; clip-path: none; opacity: 1; transition: none; }
.lp-fx .lp-wm-shine .lp-big-o, .lp-fx.is-in .lp-wm-shine .lp-big-o { transform: none; animation: none; filter: drop-shadow(0 0 8px rgba(159, 179, 224, .7)); }
.lp-fx .lp-wm-shine .lp-char-o > span { animation: none !important; }
.lp-fx .lp-wm-shine .lp-big-o path { stroke: #f7f9ff; }
.lp-fx .lp-wm-shine .lp-o-arc { stroke-dashoffset: 0; opacity: 1; transition: none; }
/* 빛이 지나갈 때 글자 주변도 은은하게 밝아진다 */
.lp-fx .lp-wm-wrap::after { content: ''; position: absolute; inset: -10% -4%; pointer-events: none; z-index: 1; opacity: 0;
  background: radial-gradient(60% 70% at 50% 55%, rgba(159, 179, 224, .22), transparent 70%); }
.lp-fx.is-in .lp-wm-wrap::after { animation: lpHalo 1.8s ease 2.1s both; }
@keyframes lpHalo { 0% { opacity: 0; } 45% { opacity: 1; } 100% { opacity: 0; } }

/* =========================================================================
 * 아래 섹션 등장 효과 — .lp-sfx(움직임 줄이기 아님)일 때만, 화면에 들어오면 .is-seen
 * ========================================================================= */
.lp-sfx { --ease-out: cubic-bezier(.2, .8, .2, 1); --ease-io: cubic-bezier(.65, 0, .35, 1); }
/* 제목: 아래에서 잘려 올라오기 */
.lp-sfx .lp-why .lp-h-xl, .lp-sfx .lp-calc .lp-h-lg, .lp-sfx .lp-h-remove, .lp-sfx .lp-faq-main .lp-h-lg, .lp-sfx .lp-end h2 {
  clip-path: inset(0 0 100% 0); transform: translateY(28px); transition: clip-path 1s var(--ease-out), transform 1s var(--ease-out); }
.lp-sfx .is-seen .lp-h-xl, .lp-sfx .is-seen .lp-h-lg, .lp-sfx .lp-h-remove.is-seen, .lp-sfx .lp-end.is-seen h2 { clip-path: inset(-10% -5% -20% -5%); transform: none; }

/* 왜: 예전 방식 줄이 차례로 들어오고 취소선이 그어진다 */
.lp-sfx .lp-old li { opacity: 0; transform: translateX(-24px); transition: opacity .6s ease, transform .7s var(--ease-out); transition-delay: calc(.25s + var(--ri) * .12s); }
.lp-sfx .lp-why.is-seen .lp-old li { opacity: 1; transform: none; }
.lp-sfx .lp-old-text { text-decoration: none; background: linear-gradient(var(--ink), var(--ink)) no-repeat 0 56% / 0% 2.5px; transition: background-size .5s var(--ease-io); transition-delay: calc(.9s + var(--ri, 0) * .14s); }
.lp-sfx .lp-old li .lp-old-text { transition-delay: inherit; }
.lp-sfx .lp-why.is-seen .lp-old-text { background-size: 100% 2.5px; }
.lp-sfx .lp-old li:nth-child(1) .lp-old-text { transition-delay: 1s; }
.lp-sfx .lp-old li:nth-child(2) .lp-old-text { transition-delay: 1.12s; }
.lp-sfx .lp-old li:nth-child(3) .lp-old-text { transition-delay: 1.24s; }
.lp-sfx .lp-old li:nth-child(4) .lp-old-text { transition-delay: 1.36s; }
.lp-sfx .lp-old li:nth-child(5) .lp-old-text { transition-delay: 1.48s; }
/* 오늘분량 1·2·3이 하나씩 튀어나온다 */
.lp-sfx .lp-new { opacity: 0; transform: translateY(30px) scale(.98); transition: opacity .7s ease .15s, transform .9s var(--ease-out) .15s; }
.lp-sfx .lp-why.is-seen .lp-new { opacity: 1; transform: none; }
.lp-sfx .lp-new-step { opacity: 0; transform: translateY(18px); transition: opacity .5s ease, transform .6s cubic-bezier(.3, 1.6, .5, 1); transition-delay: calc(1.7s + var(--ri) * .22s); }
.lp-sfx .lp-why.is-seen .lp-new-step { opacity: 1; transform: none; }

/* 계산기: 떠오르기 · 요일 칸 차례로 · 말풍선 톡 */
.lp-sfx .lp-calc-main, .lp-sfx .lp-calc-side { opacity: 0; transform: translateY(32px); transition: opacity .8s ease, transform .9s var(--ease-out); }
.lp-sfx .lp-calc-side { transition-delay: .15s; }
.lp-sfx .lp-calc.is-seen .lp-calc-main, .lp-sfx .lp-calc.is-seen .lp-calc-side { opacity: 1; transform: none; }
.lp-sfx .lp-day { opacity: 0; transform: scale(.6); transition: opacity .3s ease, transform .4s cubic-bezier(.3, 1.6, .5, 1), background .15s, color .15s; transition-delay: calc(.4s + var(--ri) * .06s), calc(.4s + var(--ri) * .06s), 0s, 0s; }
.lp-sfx .lp-calc.is-seen .lp-day { opacity: 1; transform: none; }
.lp-sfx .lp-bubble { opacity: 0; transform: translateY(8px) scale(.7); transform-origin: 0 100%; transition: opacity .3s ease 1.4s, transform .5s cubic-bezier(.3, 1.7, .5, 1) 1.4s; }
.lp-sfx .lp-calc.is-seen .lp-bubble { opacity: 1; transform: none; }

/* 없앤 세 가지: 파란 취소선이 그어지고, 카드가 반대쪽에서 들어온다 */
.lp-sfx .lp-rm-copy { opacity: 0; transform: translateY(26px); transition: opacity .7s ease, transform .8s var(--ease-out); }
.lp-sfx .lp-rm-row.is-seen .lp-rm-copy { opacity: 1; transform: none; }
.lp-sfx .lp-rm-word { text-decoration: none; background: linear-gradient(var(--blue), var(--blue)) no-repeat 0 58% / 0% var(--rm-line, 6px); transition: background-size .6s var(--ease-io) .55s; }
.lp-sfx .lp-rm-word-2 { --rm-line: 8px; }
.lp-sfx .lp-rm-word-3 { --rm-line: 5px; background-position: 0 52%; }
.lp-sfx .lp-rm-row.is-seen .lp-rm-word { background-size: 100% var(--rm-line, 6px); }
.lp-sfx .lp-rm-left > :last-child { opacity: 0; transform: translateX(60px); transition: opacity .8s ease .2s, transform 1s var(--ease-out) .2s; }
.lp-sfx .lp-rm-right > :first-child { opacity: 0; transform: translateX(-60px); transition: opacity .8s ease .2s, transform 1s var(--ease-out) .2s; }
.lp-sfx .lp-rm-row.is-seen > :last-child, .lp-sfx .lp-rm-row.is-seen > :first-child { opacity: 1; transform: none; }
.lp-sfx .lp-toc-row { opacity: 0; transform: translateY(8px); transition: opacity .4s ease, transform .5s var(--ease-out); transition-delay: calc(.7s + var(--ri) * .13s); }
.lp-sfx .lp-rm-row.is-seen .lp-toc-row { opacity: 1; transform: none; }
.lp-sfx .lp-strip span { transform: scaleY(0); transform-origin: 50% 100%; transition: transform .35s cubic-bezier(.3, 1.4, .5, 1); transition-delay: calc(.7s + var(--ri) * .07s); }
.lp-sfx .lp-rm-row.is-seen .lp-strip span { transform: none; }
.lp-sfx .lp-replan-old { transition: transform .9s var(--ease-out) .5s, opacity .6s ease .5s; transform: rotate(0deg) translateX(40px); opacity: 0; }
.lp-sfx .lp-rm-row.is-seen .lp-replan-old { transform: rotate(-3deg); opacity: 1; }
.lp-sfx .lp-replan-new { transition: transform 1s cubic-bezier(.3, 1.3, .5, 1) .85s, opacity .5s ease .85s; transform: translateY(50px) rotate(3deg); opacity: 0; }
.lp-sfx .lp-rm-row.is-seen .lp-replan-new { transform: none; opacity: 1; }
.lp-sfx .lp-rm-left > .lp-replan { transform: none; opacity: 1; }

/* 이런 분들: 그림 알약이 하나씩 튀어나오고, 아래 칸이 차례로 */
.lp-sfx .lp-who-sentence { opacity: 0; transform: translateY(24px); transition: opacity .8s ease, transform .9s var(--ease-out); }
.lp-sfx .lp-who.is-seen .lp-who-sentence { opacity: 1; transform: none; }
.lp-sfx .lp-pill { transform: scale(0) rotate(-8deg); transition: transform .6s cubic-bezier(.3, 1.6, .5, 1); transition-delay: calc(.35s + var(--ri) * .18s); }
.lp-sfx .lp-who.is-seen .lp-pill { transform: none; }
.lp-sfx .lp-accent { background: linear-gradient(transparent 62%, rgba(59, 91, 165, .22) 62%) no-repeat 0 0 / 0% 100%; transition: background-size .8s var(--ease-io) 1.3s; }
.lp-sfx .lp-who.is-seen .lp-accent { background-size: 100% 100%; }
.lp-sfx .lp-who-item { opacity: 0; transform: translateY(26px); transition: opacity .6s ease, transform .7s var(--ease-out); transition-delay: calc(1s + var(--ri) * .12s); }
.lp-sfx .lp-who.is-seen .lp-who-item { opacity: 1; transform: none; }

/* 이야기 · 자주 묻는 질문 · 마지막 */
.lp-sfx .lp-story { opacity: 0; transform: translateY(30px); transition: opacity .9s ease, transform 1s var(--ease-out); }
.lp-sfx .lp-story.is-seen { opacity: 1; transform: none; }
.lp-sfx .lp-faq-item { opacity: 0; transform: translateY(16px); transition: opacity .5s ease, transform .6s var(--ease-out); transition-delay: calc(.35s + var(--ri) * .1s); }
.lp-sfx .lp-faq-main.is-seen .lp-faq-item { opacity: 1; transform: none; }
.lp-sfx .lp-end .lp-cta { opacity: 0; transform: translateY(20px) scale(.96); transition: opacity .6s ease .45s, transform .7s cubic-bezier(.3, 1.5, .5, 1) .45s; }
.lp-sfx .lp-end.is-seen .lp-cta { opacity: 1; transform: none; }
@media (max-width: 760px) {
  /* 휴대폰: 옆에서 들어오는 대신 아래에서 (가로 넘침 방지) */
  .lp-sfx .lp-rm-left > :last-child, .lp-sfx .lp-rm-right > :first-child { transform: translateY(30px); }
  .landing { overflow-x: clip; }
}
/* 취소선은 글자 길이만큼만 */
.lp-sfx .lp-old-text { justify-self: start; width: fit-content; }
.lp-sfx .lp-rm-word { align-self: flex-start; justify-self: start; width: fit-content; }
.lp-sfx .lp-accent { background-image: linear-gradient(transparent 64%, rgba(59, 91, 165, .14) 64%); }
@media (max-width: 760px) { .lp-sfx .lp-rm-right .lp-rm-word { align-self: flex-end; } }

/* =========================================================================
```
