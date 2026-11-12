<?php
/*
 * VOICE LAB — single-file PHP vocal practice analyzer
 * Requires PHP 8+ and HTTPS. Audio/video analysis runs locally in the browser.
 * MediaPipe model is downloaded by the browser from Google's model hosting.
 */
header('X-Content-Type-Options: nosniff');
header('Referrer-Policy: strict-origin-when-cross-origin');
?>
<!doctype html>
<html lang="fa" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<meta name="theme-color" content="#10111b">
<title>Voice Lab | Vocal Science</title>
<style>
:root{--bg:#0d0f18;--panel:#171a29;--line:#2b3046;--text:#f4f3fb;--muted:#a6a9bd;--accent:#b99cff;--good:#7ed9b0;--warn:#ffca78;--bad:#ff8f9b}
*{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--text);font-family:Tahoma,Arial,sans-serif;padding:18px}
main{max-width:1120px;margin:auto}header{text-align:center;padding:18px 0 24px}h1{margin:0;color:var(--accent);letter-spacing:2px;font-size:30px}header p,.muted{color:var(--muted);font-size:13px;line-height:1.9}
.toolbar{display:flex;gap:10px;flex-wrap:wrap;margin:12px 0 16px}.toolbar button{flex:1;min-width:145px}
button,select,input{font:inherit;color:var(--text);background:#252a40;border:1px solid #3a405c;border-radius:10px;padding:12px}
button{cursor:pointer;font-weight:bold}.primary{background:#7656b5;border-color:#7656b5}.stop{background:#653846}.secondary{background:#24283a}
button:disabled{opacity:.45;cursor:not-allowed}
.status{background:#20243a;border:1px solid var(--line);border-radius:12px;padding:12px;text-align:center;margin-bottom:15px;color:#d4c7ff}
.grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px}
.card{background:var(--panel);border:1px solid var(--line);border-radius:15px;padding:16px;margin-bottom:13px;min-width:0}
.card h2{font-size:15px;color:var(--accent);margin:0 0 13px}
.metric{text-align:center}.metric .num{font-size:29px;font-weight:bold;direction:ltr;color:white;overflow-wrap:anywhere}.metric small{display:block;color:var(--muted);margin-top:6px}
.two{display:grid;grid-template-columns:1.15fr .85fr;gap:13px}
canvas{width:100%;height:170px;background:#0b0d15;border-radius:9px;display:block}
video{width:100%;max-height:360px;object-fit:cover;border-radius:10px;background:#07080d;transform:scaleX(-1)}
.videoWrap{position:relative}.videoNote{font-size:12px;color:var(--muted);line-height:1.8}
.rows{display:grid;grid-template-columns:1fr 1fr;gap:8px}.row{display:flex;justify-content:space-between;gap:8px;border-bottom:1px solid var(--line);padding:9px 0;font-size:13px}.row b{direction:ltr;color:#d2c2ff}
.advice{font-size:14px;line-height:2.05;color:#e5e2f2;white-space:pre-line}.advice strong{color:var(--good)}
label{display:block;font-size:13px;color:var(--muted);margin:8px 0}select{width:100%}
.pill{display:inline-block;border:1px solid var(--line);padding:5px 9px;border-radius:20px;color:var(--muted);font-size:11px;margin:3px}
.warning{border-right:3px solid var(--warn);padding:8px 11px;background:#292317;border-radius:7px;color:#f3d9aa;font-size:12px;line-height:1.9}
footer{text-align:center;color:#777d94;font-size:11px;padding:18px}
@media(max-width:800px){.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.two{grid-template-columns:1fr}}
@media(max-width:430px){body{padding:11px}.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.metric .num{font-size:24px}.card{padding:12px}}
</style>
</head>
<body>
<main>
<header>
<h1>VOICE LAB</h1>
<p>تحلیل زنده آکوستیک صدا، واکه و حرکت دهان — پردازش داخل مرورگر</p>
</header>

<div class="status" id="status">برای شروع، اجازه میکروفون و دوربین را فعال کن.</div>
<div class="toolbar">
<button class="primary" id="start">شروع تحلیل زنده</button>
<button class="stop" id="stop" disabled>توقف</button>
<button class="secondary" id="reset">پاک‌کردن داده‌ها</button>
</div>

<section class="grid">
 <div class="card metric"><h2>فرکانس پایه F0</h2><div class="num" id="f0">—</div><small>Hz</small></div>
 <div class="card metric"><h2>نت تقریبی</h2><div class="num" id="note">—</div><small>نام نت و اکتاو</small></div>
 <div class="card metric"><h2>شدت نسبی</h2><div class="num" id="rms">—</div><small>RMS، نه بلندی کالیبره‌شده</small></div>
 <div class="card metric"><h2>تناوب‌مندی</h2><div class="num" id="periodicity">—</div><small>شاخص تقریبی autocorrelation</small></div>
</section>

<div class="two">
 <section class="card">
  <h2>نمودار فرکانس لحظه‌ای</h2>
  <canvas id="pitchChart"></canvas>
  <p class="muted">مقیاس نمودار تقریبی است؛ برای تمرین، یک نت راحت و بدون فشار انتخاب کن.</p>
 </section>
 <section class="card">
  <h2>طیف فرکانسی زنده</h2>
  <canvas id="spectrum"></canvas>
  <p class="muted">طیف FFT برای دیدن انرژی فرکانس‌هاست؛ قله‌های آن به‌تنهایی اندازه‌گیری معتبر فرمنت نیستند.</p>
 </section>
</div>

<div class="two">
 <section class="card">
  <h2>دوربین و ردیابی دهان</h2>
  <div class="videoWrap"><video id="video" playsinline muted></video></div>
  <div class="rows">
   <div class="row"><span>بازشدگی نسبی دهان</span><b id="mouth">—</b></div>
   <div class="row"><span>نسبت بازشدگی لب</span><b id="mouthRatio">—</b></div>
   <div class="row"><span>وضعیت ردیابی</span><b id="faceStatus">خاموش</b></div>
   <div class="row"><span>کیفیت فریم</span><b id="faceQuality">—</b></div>
  </div>
  <p class="videoNote">ردیابی با Face Landmarker انجام می‌شود. عدد بازشدگی، نسبت تصویریِ نسبی است و درصد واقعی بازشدن فک یا موقعیت زبان نیست. تصویر در این کد به سرور ارسال نمی‌شود.</p>
 </section>
 <section class="card">
  <h2>تحلیل کیفیت صوت و واکه</h2>
  <div class="row"><span>شاخص نویز/تناوب</span><b id="noiseIndex">—</b></div>
  <div class="row"><span>تخمین طیفی F1</span><b id="f1">در دسترس نیست</b></div>
  <div class="row"><span>تخمین طیفی F2</span><b id="f2">در دسترس نیست</b></div>
  <div class="row"><span>تخمین طیفی F3</span><b id="f3">در دسترس نیست</b></div>
  <label for="vowel">واکه‌ای که تمرین می‌کنی</label>
  <select id="vowel">
   <option value="آ">آ / A</option><option value="اِ">اِ / E</option>
   <option value="ای">ای / I</option><option value="اُ">اُ / O</option><option value="او">او / U</option>
  </select>
  <p class="muted">فرمنت‌ها در این نسخه به‌صورت قابل اتکا از نویز محیط و میکروفون معمولی جدا نشده‌اند؛ بنابراین عدد ساختگی نمایش داده نمی‌شود.</p>
 </section>
</div>

<section class="card">
 <h2>مربی قانون‌محور — بازخورد لحظه‌ای</h2>
 <div class="advice" id="coach">بعد از شروع، صدای راحت و کشیده‌ای اجرا کن تا تحلیل اولیه انجام شود.</div>
 <div style="margin-top:12px">
  <span class="pill">Mix coordination</span><span class="pill">SOVT</span><span class="pill">Vowel modification</span><span class="pill">CVT concepts</span>
 </div>
</section>

<section class="card">
 <h2>تمرین هدفمند</h2>
 <label for="exercise">تمرین</label>
 <select id="exercise">
  <option value="lip">لرزش لب (Lip trill)</option>
  <option value="straw">فونیشن با نی (Straw phonation)</option>
  <option value="ng">صدای ملایم NG</option>
  <option value="gee">الگوی کوتاه «گی» با حجم راحت</option>
  <option value="vowel">پله‌ای واکه انتخاب‌شده</option>
 </select>
 <p class="advice" id="exerciseInfo">تمرین را آرام، در محدوده راحت و بدون فشار انجام بده.</p>
</section>

<section class="card warning">
 <b>محدودیت و ایمنی:</b>
 این ابزار تشخیص پزشکی یا ارزیابی قطعی Mix Voice نیست. از روی میکروفون نمی‌توان میزان بسته‌شدن تارهای صوتی، فشار زیرگلوتی، وضعیت حنجره یا نیاز قطعی به «هوادار/بی‌هوا» خواندن را تشخیص داد. شاخص تناوب و نویز فقط سرنخ آکوستیکی‌اند و به میکروفون، اتاق، فاصله و شدت صدا وابسته‌اند. برای ارزیابی دقیق‌ترِ حنجره، معاینه متخصص گفتاردرمانی/حنجره و در صورت نیاز استروبوسکوپی لازم است. اگر درد، سوزش یا گرفتگی ایجاد شد، تمرین را متوقف کن؛ برای حذف هوا صدا را فشار نده.
</section>

<footer>VOICE LAB · Local browser processing · Single PHP file</footer>
</main>

<script type="module">
import { FilesetResolver, FaceLandmarker } from
 'https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.14';

const $ = id => document.getElementById(id);
let audioCtx=null, analyser=null, stream=null, source=null, raf=0;
let faceLandmarker=null, videoStream=null, faceTimer=0, active=false;
let pitchData=[], lastFaceTime=0;

const noteNames=['C','C#','D','D#','E','F','F#','G','G#','A','A#','B'];
function noteName(f){
 if(!f || f<40) return '—';
 const m=Math.round(69+12*Math.log2(f/440));
 return noteNames[(m%12+12)%12]+(Math.floor(m/12)-1);
}
function autoPitch(buf,sr){
 let rms=0; for(let i=0;i<buf.length;i++) rms+=buf[i]*buf[i];
 rms=Math.sqrt(rms/buf.length);
 if(rms<0.008) return {freq:null,rms,periodicity:0};
 const minLag=Math.floor(sr/1000), maxLag=Math.min(Math.floor(sr/65),buf.length-2);
 let best=-1,bestCorr=0;
 for(let lag=minLag;lag<=maxLag;lag++){
  let corr=0,n=0;
  for(let i=0;i<buf.length-lag;i+=2){corr+=buf[i]*buf[i+lag];n++;}
  corr/=Math.max(1,n);
  if(corr>bestCorr){bestCorr=corr;best=lag;}
 }
 return {freq:best>0?sr/best:null,rms,periodicity:Math.max(0,Math.min(1,bestCorr))};
}
function drawLine(canvas,arr,min,max){
 const c=canvas,ctx=c.getContext('2d'),dpr=devicePixelRatio||1;
 c.width=Math.max(1,c.clientWidth*dpr);c.height=170*dpr;
 const w=c.width,h=c.height;ctx.clearRect(0,0,w,h);
 ctx.strokeStyle='#292e43';ctx.lineWidth=1;
 for(let i=1;i<5;i++){ctx.beginPath();ctx.moveTo(0,h*i/5);ctx.lineTo(w,h*i/5);ctx.stroke();}
 if(arr.length<2)return;
 ctx.beginPath();ctx.strokeStyle='#b99cff';ctx.lineWidth=2.5*dpr;
 arr.forEach((v,i)=>{let x=i/(arr.length-1)*w,y=h-(v-min)/(max-min)*h;y=Math.max(3,Math.min(h-3,y));i?ctx.lineTo(x,y):ctx.moveTo(x,y);});
 ctx.stroke();
}
function drawSpectrum(){
 if(!analyser)return;
 const c=$('spectrum'),ctx=c.getContext('2d'),dpr=devicePixelRatio||1;
 c.width=Math.max(1,c.clientWidth*dpr);c.height=170*dpr;
 const w=c.width,h=c.height,arr=new Uint8Array(analyser.frequencyBinCount);
 analyser.getByteFrequencyData(arr);ctx.clearRect(0,0,w,h);
 const bins=Math.min(arr.length,Math.floor(5000*analyser.fftSize/audioCtx.sampleRate));
 const bw=w/bins;
 for(let i=1;i<bins;i++){
  const bh=arr[i]/255*h*.92;ctx.fillStyle='#9272d2';
  ctx.fillRect(i*bw,h-bh,Math.max(1,bw-1),bh);
 }
}
function coach(result){
 const vowel=$('vowel').value;
 if(!result.freq){
  $('coach').textContent='صدای قابل تحلیل نیست. فاصله میکروفون را ثابت نگه دار و یک صدای راحت و کشیده اجرا کن.';
  return;
 }
 const p=result.periodicity;
 let lines=[];
 if(p<0.35){
  lines.push('تناوب‌مندی پایین است. ممکن است سیگنال کم‌صدا، پرنویز، نفس‌آلود یا نامناسب برای ردیابی Pitch باشد؛ این شاخص به‌تنهایی نفس‌آلود بودن صدا را ثابت نمی‌کند.');
  lines.push('برای مقایسه، یک «وو» یا لرزش لب ملایم و راحت اجرا کن؛ صدایت را برای حذف هوا سفت یا فشرده نکن.');
 } else if(p<0.65){
  lines.push('تناوب‌مندی متوسط است. یک نت راحت را با حجم متوسط و بدون فشار چند ثانیه نگه دار و دوباره مقایسه کن.');
 } else {
  lines.push('سیگنال در این لحظه تناوب‌مندتر است. این به معنی میکس صحیح یا سلامت قطعی حنجره نیست.');
 }
 const target=Number($('target')?.value);
 if(target && result.freq){
  const cents=1200*Math.log2(result.freq/target);
  lines.push('فاصله از نت هدف: '+(cents>0?'+':'')+cents.toFixed(0)+' سنت. به جای فشار برای رسیدن به نت، با شدت راحت تمرین کن.');
 }
 lines.push('واکه انتخابی: '+vowel+'. تغییر شکل واکه باید تدریجی و متناسب با نت و سبک باشد؛ یک شکل دهان برای همه نت‌ها نسخه ثابت نیست.');
 $('coach').textContent=lines.join('\n\n');
}
function audioLoop(){
 if(!active||!analyser)return;
 const buf=new Float32Array(analyser.fftSize);
 analyser.getFloatTimeDomainData(buf);
 const r=autoPitch(buf,audioCtx.sampleRate);
 $('rms').textContent=(r.rms*100).toFixed(2);
 $('periodicity').textContent=(r.periodicity*100).toFixed(0)+'%';
 $('noiseIndex').textContent=((1-r.periodicity)*100).toFixed(0)+'% (تقریبی)';
 if(r.freq){
  $('f0').textContent=r.freq.toFixed(1);
  $('note').textContent=noteName(r.freq);
  pitchData.push(r.freq);if(pitchData.length>100)pitchData.shift();
 } else {$('f0').textContent='—';$('note').textContent='—';}
 drawLine($('pitchChart'),pitchData,60,1000);drawSpectrum();coach(r);
 raf=requestAnimationFrame(audioLoop);
}
function landmarkLoop(){
 if(!active||!faceLandmarker||$('video').readyState<2){faceTimer=requestAnimationFrame(landmarkLoop);return;}
 const now=performance.now();
 if(now-lastFaceTime>75){
  lastFaceTime=now;
  const result=faceLandmarker.detectForVideo($('video'),now);
  if(result.faceLandmarks?.length){
   const p=result.faceLandmarks[0];
   // MediaPipe Face Mesh lip landmarks: 13/14 inner upper/lower lip; 61/291 mouth corners.
   const dist=(a,b)=>Math.hypot(p[a].x-p[b].x,p[a].y-p[b].y);
   const opening=dist(13,14),width=dist(61,291);
   const ratio=width>0?opening/width:0;
   $('mouth').textContent=(ratio*100).toFixed(1)+'% نسبت تصویری';
   $('mouthRatio').textContent=ratio.toFixed(3);
   $('faceStatus').textContent='ردیابی فعال';
   $('faceQuality').textContent=(p[13].visibility??1).toFixed(2);
  } else {
   $('faceStatus').textContent='چهره پیدا نشد';$('mouth').textContent='—';$('mouthRatio').textContent='—';
  }
 }
 faceTimer=requestAnimationFrame(landmarkLoop);
}
async function start(){
 $('start').disabled=true;
 try{
  $('status').textContent='در حال درخواست دسترسی دوربین و میکروفون…';
  const combined=await navigator.mediaDevices.getUserMedia({
   audio:{echoCancellation:false,noiseSuppression:false,autoGainControl:false},
   video:{facingMode:'user',width:{ideal:1280},height:{ideal:720}}
  });
  stream=combined;
  $('video').srcObject=combined;
  await $('video').play();
  audioCtx=new (window.AudioContext||window.webkitAudioContext)();
  await audioCtx.resume();
  analyser=audioCtx.createAnalyser();analyser.fftSize=4096;analyser.smoothingTimeConstant=.25;
  source=audioCtx.createMediaStreamSource(combined);source.connect(analyser);
  $('status').textContent='در حال بارگذاری مدل ردیابی چهره…';
  const vision=await FilesetResolver.forVisionTasks(
   'https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.14/wasm'
  );
  faceLandmarker=await FaceLandmarker.createFromOptions(vision,{
   baseOptions:{modelAssetPath:'https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task',delegate:'GPU'},
   runningMode:'VIDEO',numFaces:1,
   outputFaceBlendshapes:false,outputFacialTransformationMatrixes:false
  });
  active=true;$('stop').disabled=false;
  $('status').textContent='تحلیل زنده فعال است — تصویر و صدا در همین مرورگر پردازش می‌شوند.';
  audioLoop();landmarkLoop();
 }catch(e){
  $('status').textContent='شروع نشد: '+(e.message||e)+' | HTTPS، مجوز دوربین/میکروفون و اتصال اینترنت را بررسی کن.';
  $('start').disabled=false;stop();
 }
}
function stop(){
 active=false;cancelAnimationFrame(raf);cancelAnimationFrame(faceTimer);
 if(stream)stream.getTracks().forEach(t=>t.stop());
 stream=null;$('video').srcObject=null;
 if(audioCtx){audioCtx.close();audioCtx=null;}
 analyser=null;source=null;faceLandmarker=null;
 $('stop').disabled=true;$('start').disabled=false;
 $('status').textContent='تحلیل متوقف شد.';
}
$('start').addEventListener('click',start);
$('stop').addEventListener('click',stop);
$('reset').addEventListener('click',()=>{
 pitchData=[];['f0','note','rms','periodicity','mouth','mouthRatio','noiseIndex'].forEach(id=>$(id).textContent='—');
 $('coach').textContent='داده‌ها پاک شدند. برای تحلیل دوباره شروع کن.';
});
const exerciseText={
 lip:'با لرزش لب، یک الگوی آرام و کوتاه در محدوده راحت اجرا کن. اگر لرزش سخت شد، نت یا شدت را کمتر کن.',
 straw:'با نی معمولی و بدون فشار، صدای یکنواخت و سپس سر خوردن آرام بین چند نت راحت را تمرین کن. فشار هوا را زیاد نکن.',
 ng:'صدای NG ملایم و کوتاه اجرا کن؛ فک و گردن را آزاد نگه دار و در صورت گرفتگی توقف کن.',
 gee:'«گی» را کوتاه و با حجم راحت اجرا کن؛ اگر صدا فشرده یا گلویی شد، شدت را کم کن یا تمرین را متوقف کن.',
 vowel:'واکه انتخاب‌شده را روی چند نت نزدیک و راحت اجرا کن و تغییرات Pitch و شکل دهان را مقایسه کن.'
};
$('exercise').addEventListener('change',()=>{$('exerciseInfo').textContent=exerciseText[$('exercise').value];});
$('vowel').addEventListener('change',()=>{coach({freq:Number($('f0').textContent)||null,periodicity:0.5});});
window.addEventListener('pagehide',stop);
</script>
</body>
</html>
