<!DOCTYPE html>
<html lang="zh">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no"/>
<title>Stamp Maker</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:wght@400;600&family=Playfair+Display:wght@400;600&family=Courier+Prime&family=Cinzel:wght@400;600&family=Noto+Serif+SC:wght@400;600&family=Noto+Sans+SC:wght@400;700&family=Ma+Shan+Zheng&display=swap" rel="stylesheet"/>
<!-- OPPO Sans via 自托管 CDN -->
<style>
@font-face{font-family:'OPPO Sans';font-weight:400;font-style:normal;
  src:url('https://cdn.jsdelivr.net/gh/wordshub/free-font@master/assets/font/O/OPPOSans-R.ttf') format('truetype')}
@font-face{font-family:'OPPO Sans';font-weight:700;font-style:normal;
  src:url('https://cdn.jsdelivr.net/gh/wordshub/free-font@master/assets/font/O/OPPOSans-B.ttf') format('truetype')}
</style>
<script src="https://cdn.jsdelivr.net/npm/exifr@7.1.3/dist/full.umd.js"></script>
<script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;background:#111;-webkit-font-smoothing:antialiased}
body{font-family:'Helvetica Neue',Helvetica,Arial,sans-serif;color:#ddd}
#app{max-width:480px;margin:0 auto;min-height:100vh;display:flex;flex-direction:column}
button{-webkit-tap-highlight-color:transparent}
select,input{-webkit-appearance:none;appearance:none}
@keyframes spin{from{transform:rotate(0)}to{transform:rotate(360deg)}}
.spin{animation:spin 1s linear infinite;display:inline-block}
</style>
</head>
<body>
<div id="app"></div>
<script>
/* ─── STATE ─── */
const SEASONS={en:['SPRING','SUMMER','AUTUMN','WINTER'],zh:['春','夏','秋','冬']}
const M2S=[3,3,0,0,0,1,1,1,2,2,2,3]
const now=new Date()
const initSeason=()=>({en:SEASONS.en[M2S[now.getMonth()]],zh:SEASONS.zh[M2S[now.getMonth()]]})

const FONTS=[
  /* 英文 */
  {label:'EB Garamond（英文衬线）', val:"'EB Garamond',serif"},
  {label:'Playfair Display（英文衬线）', val:"'Playfair Display',serif"},
  {label:'Helvetica（英文无衬线）', val:"'Helvetica Neue',Helvetica,Arial,sans-serif"},
  {label:'Courier（英文等宽）', val:"'Courier Prime',monospace"},
  {label:'Cinzel（英文古典）', val:"'Cinzel',serif"},
  /* 中文 */
  {label:'OPPO Sans（中文无衬线）', val:"'OPPO Sans','Noto Sans SC',sans-serif"},
  {label:'Noto Sans SC（思源黑体）', val:"'Noto Sans SC',sans-serif"},
  {label:'Noto Serif SC（思源宋体）', val:"'Noto Serif SC',serif"},
  {label:'Ma Shan Zheng（马善政楷体）', val:"'Ma Shan Zheng',cursive"},
]
const PBG   =['#3D4EBF','#8B5A2B','#7A1F1F','#1A3A2A','#2C2C3A','#F5EDD6','#111111','#C8B8A2']
const PSTAMP=['#F5EDD6','#D4A96A','#C84B31','#EEEEEE','#1C1C1C','#E8D5B0','#A8C4BC','#3D4EBF']
const PTEXT =['#FFFFFF','#1C1C1C','#3D4EBF','#8B5A2B','#C84B31','#F5EDD6','#D4A96A','#888888']
const RATIOS=[
  {id:'1:1',  label:'1:1',     w:280,r:1},
  {id:'3:4',  label:'3:4 竖',  w:260,r:3/4},
  {id:'4:3',  label:'4:3 横',  w:320,r:4/3},
  {id:'9:16', label:'9:16 竖', w:240,r:9/16},
  {id:'16:9', label:'16:9 横', w:340,r:16/9},
]

const s=initSeason()
const state={
  image:null,bg:'#3D4EBF',stampColor:'#F5EDD6',textColor:'#1C1C1C',
  font:FONTS[5].val,year:String(now.getFullYear()),
  seasonEn:s.en,seasonZh:s.zh,
  cityZh:'城市名',cityEn:'CITY NAME',
  showText:true,panel:'color',ratio:RATIOS[1],
  geoStatus:'idle',
}

/* ─── STAMP PATH
   锯齿向内凹入，保证邮票矩形边界 = sW × sH，不会超出容器
─── */
function stampPath(W,H,inset=0,r=3.5){
  // 锯齿圆心在边界线上，半圆向内凹
  const x0=inset, y0=inset, w=W-inset*2, h=H-inset*2
  const hStep=w/Math.max(4,Math.round(w/(r*2*2.1)))
  const vStep=h/Math.max(4,Math.round(h/(r*2*2.1)))
  const tN=Math.round(w/hStep), sN=Math.round(h/vStep)
  const hs=w/tN, vs=h/sN

  let d=`M ${x0+r} ${y0}`
  // top — 半圆向下（凹入）
  for(let i=0;i<tN;i++){
    const x=x0+i*hs+hs/2
    d+=` L ${x-r} ${y0} A ${r} ${r} 0 0 1 ${x+r} ${y0}`
  }
  d+=` L ${x0+w-r} ${y0} Q ${x0+w} ${y0} ${x0+w} ${y0+r}`
  // right — 半圆向左（凹入）
  for(let i=0;i<sN;i++){
    const y=y0+i*vs+vs/2
    d+=` L ${x0+w} ${y-r} A ${r} ${r} 0 0 0 ${x0+w} ${y+r}`
  }
  d+=` L ${x0+w} ${y0+h-r} Q ${x0+w} ${y0+h} ${x0+w-r} ${y0+h}`
  // bottom — 半圆向上（凹入）
  for(let i=tN-1;i>=0;i--){
    const x=x0+i*hs+hs/2
    d+=` L ${x+r} ${y0+h} A ${r} ${r} 0 0 1 ${x-r} ${y0+h}`
  }
  d+=` L ${x0+r} ${y0+h} Q ${x0} ${y0+h} ${x0} ${y0+h-r}`
  // left — 半圆向右（凹入）
  for(let i=sN-1;i>=0;i--){
    const y=y0+i*vs+vs/2
    d+=` L ${x0} ${y+r} A ${r} ${r} 0 0 1 ${x0} ${y-r}`
  }
  d+=` L ${x0} ${y0+r} Q ${x0} ${y0} ${x0+r} ${y0} Z`
  return d
}

/* ─── RENDER ─── */
function render(){
  const {image,bg,stampColor,textColor,font,year,seasonEn,seasonZh,
         cityZh,cityEn,showText,panel,ratio,geoStatus}=state

  const PAD=18, BI=11
  const imgW=ratio.w-PAD*2
  const imgH=Math.round(imgW/ratio.r)
  const tzH=showText?68:0
  const sW=ratio.w
  const sH=PAD+imgH+(showText?8:0)+tzH+PAD
  // 背景画布：邮票四周各留 28px
  const MARGIN=28
  const cW=sW+MARGIN*2, cH=sH+MARGIN*2

  const pOuter=stampPath(sW,sH,0,4)
  const pInner=stampPath(sW,sH,BI,3)
  const cityFS=Math.min(20,imgW/Math.max(cityZh.length,1)*1.1+4)

  const grain=`url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.055'/%3E%3C/svg%3E")`

  // geo bar
  let geoBar=''
  if(geoStatus==='loading') geoBar=`<div style="background:#1A2A1A;border-top:1px solid #2A3A2A;padding:8px 16px;font-size:10px;color:#4CAF50;letter-spacing:.12em;display:flex;align-items:center;gap:6px"><span class="spin">◌</span> 正在从照片 GPS 读取位置…</div>`
  else if(geoStatus==='found') geoBar=`<div style="background:#1A2A1A;border-top:1px solid #2A3A2A;padding:8px 16px;font-size:10px;color:#4CAF50;letter-spacing:.12em">📍 已自动识别位置 · 可在「文字」标签修改</div>`
  else if(geoStatus==='none') geoBar=`<div style="background:#1E1E1E;border-top:1px solid #2A2A2A;padding:8px 16px;font-size:10px;color:#555;letter-spacing:.12em">照片无 GPS 信息 · 请手动输入城市</div>`

  // color dots
  const dots=(presets,key)=>presets.map(c=>{
    const a=state[key]===c
    return `<button onclick="setColor('${key}','${c}')" style="width:26px;height:26px;border-radius:50%;background:${c};border:${a?'2px solid #fff':'2px solid transparent'};outline:${a?'2px solid #555':'none'};cursor:pointer;flex-shrink:0;padding:0"></button>`
  }).join('')

  const crow=(label,key,presets)=>`
    <div style="margin-bottom:16px">
      <div style="font-size:9px;letter-spacing:.18em;color:#666;margin-bottom:7px;text-transform:uppercase">${label}</div>
      <div style="display:flex;gap:6px;align-items:center;flex-wrap:wrap">
        ${dots(presets,key)}
        <input type="color" value="${state[key]}" oninput="setColor('${key}',this.value)"
          style="width:32px;height:26px;border:none;background:none;cursor:pointer;padding:0;flex-shrink:0"/>
      </div>
    </div>`

  const colorPanel=`
    ${crow('背景色','bg',PBG)}
    ${crow('邮票色','stampColor',PSTAMP)}
    ${crow('文字色','textColor',PTEXT)}
    <div>
      <div style="font-size:9px;letter-spacing:.18em;color:#666;margin-bottom:7px;text-transform:uppercase">字体</div>
      <select onchange="setState('font',this.value)"
        style="width:100%;background:#222;border:1px solid #2E2E2E;color:#eee;padding:8px 9px;font-size:12px;border-radius:3px;cursor:pointer">
        ${FONTS.map(f=>`<option value="${f.val}"${state.font===f.val?' selected':''}>${f.label}</option>`).join('')}
      </select>
    </div>`

  const geoBadge=geoStatus==='loading'
    ?`<span style="font-size:8px;padding:1px 6px;border-radius:10px;background:#1E3A1E;color:#4CAF50;margin-left:6px">定位中…</span>`
    :geoStatus==='found'
    ?`<span style="font-size:8px;padding:1px 6px;border-radius:10px;background:#1E3A1E;color:#4CAF50;margin-left:6px">📍 自动识别</span>`
    :''

  const field=(label,key,badge='',upper=false)=>`
    <div style="margin-bottom:12px;flex:1">
      <div style="display:flex;align-items:center;margin-bottom:5px">
        <span style="font-size:9px;letter-spacing:.15em;color:#666;text-transform:uppercase">${label}</span>${badge}
      </div>
      <input value="${state[key].replace(/"/g,'&quot;')}"
        oninput="setState('${key}',${upper?'this.value.toUpperCase()':'this.value'})"
        style="width:100%;background:#222;border:1px solid #2E2E2E;color:#eee;padding:7px 9px;font-size:13px;border-radius:3px;outline:none"/>
    </div>`

  const textPanel=`
    <div style="display:flex;gap:10px">${field('年份','year')}<div style="flex:1"></div></div>
    <div style="display:flex;gap:10px">${field('季节 EN','seasonEn')}${field('季节 ZH','seasonZh')}</div>
    ${field('城市（中文）','cityZh',geoBadge)}
    ${field('城市（英文）','cityEn','',true)}
    <div style="display:flex;align-items:center;gap:8px;margin-top:4px">
      <input type="checkbox" id="st" ${showText?'checked':''}
        onchange="setState('showText',this.checked)"
        style="accent-color:#fff;width:15px;height:15px"/>
      <label for="st" style="font-size:10px;letter-spacing:.1em;color:#666;cursor:pointer">显示文字区域</label>
    </div>`

  const ratioPanel=`
    <div>
      <div style="font-size:9px;letter-spacing:.18em;color:#666;margin-bottom:7px;text-transform:uppercase">尺寸比例</div>
      <div style="display:flex;gap:6px;flex-wrap:wrap">
        ${RATIOS.map(r=>`<button onclick="setRatio('${r.id}')"
          style="padding:7px 12px;background:${state.ratio.id===r.id?'#fff':'#222'};color:${state.ratio.id===r.id?'#111':'#666'};border:1px solid ${state.ratio.id===r.id?'#fff':'#333'};border-radius:3px;font-size:10px;letter-spacing:.1em;cursor:pointer;white-space:nowrap">
          ${r.label}</button>`).join('')}
      </div>
    </div>`

  const panels={color:colorPanel,text:textPanel,ratio:ratioPanel}
  const tabs=[['color','颜色 / 字体'],['text','文字'],['ratio','比例']]

  document.getElementById('app').innerHTML=`
    <!-- header -->
    <div style="display:flex;align-items:center;justify-content:space-between;padding:14px 16px 10px;border-bottom:1px solid #1E1E1E;background:#161616;position:sticky;top:0;z-index:10">
      <div style="font-size:12px;font-weight:700;letter-spacing:.25em;color:#fff;text-transform:uppercase">Stamp Maker</div>
      <button onclick="document.getElementById('filein').click()"
        style="background:#222;border:1px solid #333;color:#aaa;padding:6px 16px;font-size:11px;letter-spacing:.12em;border-radius:3px;cursor:pointer">
        ${image?'换图':'+ 上传图片'}
      </button>
      <input id="filein" type="file" accept="image/*" style="display:none" onchange="handleFile(this)"/>
    </div>

    <!-- preview：overflow hidden 改为 visible，用 padding 撑开 -->
    <div style="display:flex;align-items:center;justify-content:center;padding:20px 0;background:#111">
      <div id="stamp-export"
        style="background:${bg};width:${cW}px;height:${cH}px;display:flex;align-items:center;justify-content:center;flex-shrink:0;border-radius:6px;box-shadow:0 8px 40px rgba(0,0,0,.55)">
        <div style="position:relative;width:${sW}px;height:${sH}px">
          <svg width="${sW}" height="${sH}" style="position:absolute;top:0;left:0;overflow:visible">
            <path d="${pOuter}" fill="${stampColor}"/>
            <path d="${pInner}" fill="none" stroke="${textColor}" stroke-width=".7" opacity=".28"/>
          </svg>
          <!-- image -->
          <div style="position:absolute;top:${PAD}px;left:${PAD}px;width:${imgW}px;height:${imgH}px;overflow:hidden">
            ${image
              ?`<img src="${image}" style="width:100%;height:100%;object-fit:cover;display:block"/>`
              :`<div style="width:100%;height:100%;background:rgba(0,0,0,.07);display:flex;align-items:center;justify-content:center;font-family:${font};color:${textColor};opacity:.35;font-size:10px;letter-spacing:.15em">UPLOAD IMAGE</div>`
            }
            <div style="position:absolute;inset:0;pointer-events:none;background-image:${grain};mix-blend-mode:multiply"></div>
          </div>
          <!-- text -->
          ${showText?`
          <div style="position:absolute;top:${PAD+imgH+8}px;left:${PAD}px;width:${imgW}px;height:${tzH}px;display:flex;flex-direction:column;align-items:center;justify-content:center;font-family:${font};color:${textColor};gap:4px">
            <div style="font-size:8.5px;letter-spacing:.22em;opacity:.6">${year} · ${seasonEn} · ${seasonZh}</div>
            <div style="font-size:${cityFS}px;font-weight:600;letter-spacing:.04em;line-height:1.15;text-align:center">${cityZh}</div>
            <div style="font-size:8px;letter-spacing:.2em;opacity:.55;text-align:center">${cityEn}</div>
          </div>`:''}
        </div>
      </div>
    </div>

    ${geoBar}

    <!-- controls -->
    <div style="background:#161616;border-top:1px solid #1E1E1E;flex:1;display:flex;flex-direction:column">
      <div style="display:flex;border-bottom:1px solid #1E1E1E">
        ${tabs.map(([k,v])=>`<button onclick="setPanel('${k}')"
          style="flex:1;padding:12px 0;font-size:10px;letter-spacing:.12em;background:${panel===k?'#1E1E1E':'transparent'};border-bottom:${panel===k?'2px solid #fff':'2px solid transparent'};color:${panel===k?'#fff':'#555'};border:none;cursor:pointer;text-transform:uppercase">
          ${v}</button>`).join('')}
      </div>
      <div style="padding:18px 16px 24px;overflow-y:auto">${panels[panel]||''}</div>
    </div>

    <!-- export -->
    <div style="padding:12px 16px 32px;background:#111;border-top:1px solid #1A1A1A">
      <button id="expbtn" onclick="doExport()"
        style="width:100%;padding:14px 0;background:#fff;color:#111;border:none;font-size:11px;letter-spacing:.22em;font-weight:700;text-transform:uppercase;border-radius:3px;cursor:pointer">
        导出 PNG
      </button>
    </div>
  `
}

/* ─── ACTIONS ─── */
function setState(k,v){state[k]=v;render()}
function setColor(k,v){state[k]=v;render()}
function setPanel(p){state.panel=p;render()}
function setRatio(id){state.ratio=RATIOS.find(r=>r.id===id);render()}

async function handleFile(input){
  const file=input.files[0];if(!file)return
  const reader=new FileReader()
  reader.onload=ev=>{state.image=ev.target.result;render()}
  reader.readAsDataURL(file)
  // exif date
  try{
    const all=await exifr.parse(file,{pick:['DateTimeOriginal','CreateDate']})
    const dt=all?.DateTimeOriginal||all?.CreateDate
    if(dt){const d=dt instanceof Date?dt:new Date(dt);if(!isNaN(d)){state.year=String(d.getFullYear());const m=d.getMonth();state.seasonEn=SEASONS.en[M2S[m]];state.seasonZh=SEASONS.zh[M2S[m]]}}
  }catch(e){}
  // gps
  state.geoStatus='loading';render()
  try{
    const gps=await exifr.gps(file)
    if(!gps?.latitude){state.geoStatus='none';render();return}
    const [r1,r2]=await Promise.all([
      fetch(`https://nominatim.openstreetmap.org/reverse?lat=${gps.latitude}&lon=${gps.longitude}&format=json&accept-language=zh-CN`),
      fetch(`https://nominatim.openstreetmap.org/reverse?lat=${gps.latitude}&lon=${gps.longitude}&format=json&accept-language=en`)
    ])
    const [d1,d2]=await Promise.all([r1.json(),r2.json()])
    const a1=d1.address||{},a2=d2.address||{}
    const zh=a1.city||a1.town||a1.village||a1.county||a1.state||''
    const en=(a2.city||a2.town||a2.village||a2.county||a2.state||'').toUpperCase()
    if(zh)state.cityZh=zh
    if(en)state.cityEn=en
    state.geoStatus=zh?'found':'none'
  }catch(e){state.geoStatus='none'}
  render()
}

async function doExport(){
  const btn=document.getElementById('expbtn')
  btn.textContent='导出中…';btn.style.background='#ccc';btn.disabled=true
  try{
    const el=document.getElementById('stamp-export')
    const canvas=await html2canvas(el,{scale:3,useCORS:true,backgroundColor:null})
    const a=document.createElement('a')
    a.download=`stamp-${state.cityEn.replace(/\s/g,'_')}.png`
    a.href=canvas.toDataURL('image/png');a.click()
  }catch(e){alert('导出失败，请截图保存')}
  btn.textContent='导出 PNG';btn.style.background='#fff';btn.disabled=false
}

render()
</script>
</body>
</html>
