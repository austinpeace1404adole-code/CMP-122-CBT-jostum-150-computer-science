# CMP-122-CBT-jostum-150-computer-science
A CBT web app for BSc computer science 
<!DOCTYPE html>
<html lang="en"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>CMP 122 CBT Practice</title>
<style>
:root{box-sizing:border-box;
      padding-top:
      env(safe-area-inset-top,0px);
      padding-bottom:
      env(safe-area-inset-bottom,0px);
      --bg:#f6f7fb;--card:#fff;
      --tx:#1b1f2a;--mu:#5d6475;
      --pr:#3b5bdb;--ok:#2b8a3e;
      --okb:#ebfbee;--no:#c92a2a;
      --nob:#fff0f0;--bd:#d9dce6}
@media 
  (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#12141b;--card:#1c1f2a;--tx:#eceef5;--mu:#9aa1b5;--pr:#748ffc;--ok:#69db7c;--okb:#16301d;--no:#ff8787;--nob:#3a1b1b;--bd:#323750}}
:root[data-theme="dark"]{--bg:#12141b;--card:#1c1f2a;--tx:#eceef5;--mu:#9aa1b5;--pr:#748ffc;--ok:#69db7c;--okb:#16301d;--no:#ff8787;--nob:#3a1b1b;--bd:#323750}
html{scroll-padding-top:env(safe-area-inset-top,0px)}

  *{box-sizing:border-box}body{margin:0;background:var(--bg);color:var(--tx);font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif}
.w
  {max-width:640px;margin:0 auto;padding:16px}
.c
  {background:var(--card);border:1px solid var(--bd);border-radius:14px;padding:18px;margin-bottom:14px}
h1
  {font-size:22px;margin:0 0 6px}p{color:var(--mu);line-height:1.5;margin:6px 0}
.bar
  {height:6px;background:var(--bd);border-radius:9px;overflow:hidden;margin:8px 0}.bar i{display:block;height:100%;background:var(--pr);transition:width .3s}
.top
  {display:flex;justify-content:space-between;font-size:14px;color:var(--mu)}
.q
  {font-size:18px;font-weight:600;line-height:1.4;margin:10px 0 14px}
.o
  {display:block;width:100%;text-align:left;padding:13px;margin:8px 0;border:1.5px solid var(--bd);background:var(--card);color:var(--tx);border-radius:10px;font-size:16px;cursor:pointer}
.o:disabled
  {cursor:default}.o.ok{border-color:var(--ok);background:var(--okb)}.o.no{border-color:var(--no);background:var(--nob)}
.b
  {background:var(--pr);color:#fff;border:0;border-radius:10px;padding:13px 20px;font-size:16px;cursor:pointer;width:100%;margin-top:8px}
.b.s
  {background:transparent;color:var(--pr);border:1.5px solid var(--pr)}
.ex
  {margin-top:12px;padding:12px;border-radius:10px;font-size:15px;line-height:1.5}
.ex.ok
  {background:var(--okb);color:var(--ok)}.ex.no{background:var(--nob);color:var(--no)}.ex span{color:var(--tx);display:block;margin-top:6px}
.big
  {font-size:48px;font-weight:700;text-align:center;margin:8px 0}
.r
  {padding:10px 0;border-top:1px solid var(--bd);font-size:14px}.r b{display:block;margin-bottom:3px}
</style>
</head>
  <body>
    <div class="w" id="app"></div>
<script>
// [question, CORRECT answer, wrong1, wrong2, wrong3, explanation]
const Q=[
["What is the base of the hexadecimal number system?","16","8","10","2","Hexadecimal uses 16 symbols: 0–9 and A–F, so its base is 16."],
["Which digits does the octal system use?","0 – 7","0 – 8","0 – 9","0 – F","Octal is base 8, so digits run from 0 to 7."],
["In 572₁₀, what is the positional value of digit 5?","500","50","5","5000","572 = (5×10²)+(7×10¹)+(2×10⁰). The 5 is in the 10² position, so 5×100 = 500."],
["Convert 1011₂ to decimal.","11","9","13","10","(1×2³)+(0×2²)+(1×2¹)+(1×2⁰) = 8+0+2+1 = 11."],
["Convert 745₈ to decimal.","485","445","525","465","(7×8²)+(4×8¹)+(5×8⁰) = 448+32+5 = 485."],
["Convert 2F₁₆ to decimal.","47","37","57","32","F = 15. (2×16)+(15×1) = 32+15 = 47."],
["Which of these is NOT a valid binary number?","1201","1010","1111","0001","Binary only allows 0 and 1. The digit 2 in 1201 makes it invalid."],
["In hexadecimal, what is the decimal value of B?","11","10","12","13","A=10, B=11, C=12, D=13, E=14, F=15."],
["Why do computers mainly use the binary system?","Digital circuits have two states: ON (1) and OFF (0)","Binary is easier for humans to read","Binary uses more digits","Decimal is not mathematical","Digital circuits are built from switches with two states, ON = 1 and OFF = 0."],
["Which of these is a valid octal number?","745","789","2F","1982","Octal digits are only 0–7. 789 and 1982 contain 8 or 9; 2F contains F."],
["Convert 25₁₀ to binary.","11001","10011","11010","10101","25÷2=12 r1, 12÷2=6 r0, 6÷2=3 r0, 3÷2=1 r1, 1÷2=0 r1. Read upward: 11001."],
["Convert 10110₂ to decimal.","22","20","24","26","(1×16)+(0×8)+(1×4)+(1×2)+(0×1) = 16+4+2 = 22."],
["Convert 125₁₀ to octal.","175₈","157₈","571₈","205₈","125÷8=15 r5, 15÷8=1 r7, 1÷8=0 r1. Read upward: 175."],
["Convert 254₁₀ to hexadecimal.","FE","EF","FF","EE","254÷16=15 r14 (E), 15÷16=0 r15 (F). Read upward: FE."],
["Convert 110101₂ to octal.","65₈","56₈","53₈","35₈","Group in 3s from the right: 110 | 101 = 6 | 5 = 65."],
["Convert 10111101₂ to hexadecimal.","BD","DB","AD","BE","Group in 4s: 1011 | 1101 = B | D = BD."],
["Convert 101101₂ to decimal.","45","43","47","41","32+0+8+4+0+1 = 45."],
["Convert 276₁₀ to hexadecimal.","114","141","10C","11A","276÷16=17 r4, 17÷16=1 r1, 1÷16=0 r1. Read upward: 114."],
["Convert 7A₁₆ to binary.","01111010","10101111","01111100","01011010","Convert each hex digit to 4 bits: 7 = 0111, A = 1010. So 01111010."],
["Represent the decimal number 93 in binary.","1011101","1101101","1011011","1111001","93 = 64+16+8+4+1 → 1011101. (Division: 93÷2 gives remainders 1,0,1,1,1,0,1 read upward.)"],
["Represent the decimal number 93 in octal.","135₈","153₈","531₈","115₈","93÷8=11 r5, 11÷8=1 r3, 1÷8=0 r1. Read upward: 135."],
["Represent the decimal number 93 in hexadecimal.","5D","D5","59","5E","93÷16=5 r13 (D), 5÷16=0 r5. Read upward: 5D."],
["Convert octal 17 to binary (3 bits per digit).","001111","010111","111001","011011","1 = 001 and 7 = 111, so 001 111."],
["What is the largest decimal value a 4-bit binary number can hold?","15","8","16","31","1111₂ = 8+4+2+1 = 15 (range is 0 to 2⁴−1)."],
["Convert 11111111₂ to hexadecimal.","FF","EE","F0","1F","1111 | 1111 = F | F = FF."],
["In BCD, how many bits represent each decimal digit?","4","3","7","8","Each digit 0–9 is encoded using 4 binary bits."],
["Write 59₁₀ in BCD.","0101 1001","111011","0101 1010","1001 0101","5 = 0101 and 9 = 1001, so 0101 1001."],
["What decimal number is BCD 0111 0010?","72","114","27","82","0111 = 7 and 0010 = 2, so the number is 72."],
["What is the decimal ASCII code for character 'A'?","65","64","66","97","'A' = 65, which is 1000001 in binary. Lowercase 'a' is 97."],
["What is 7-bit ASCII binary for 'A'?","1000001","1000010","0100000","1000000","65₁₀ = 64+1 = 1000001₂."],
["What is the ASCII decimal code for 'C'?","67","66","68","99","A=65, B=66, C=67."],
["What is the ASCII decimal code for 'M'?","77","75","76","78","M is the 13th letter: 65+12 = 77."],
["What is the ASCII decimal code for the character '7'?","55","7","48","57","Digit '0' is 48, so '7' = 48+7 = 55."],
["How many bits does standard ASCII use?","7","4","8","16","Standard ASCII is 7-bit (128 characters). Extended ASCII uses 8 bits."],
["Which range holds the ASCII control characters?","0 – 31","0 – 127","32 – 127","128 – 255","The first 32 characters (codes 0–31) are unprintable control codes."],
["What is the decimal ASCII code of ESC (Escape)?","27","13","10","32","From the table, ESC is decimal 27 (hex 1B, octal 033)."],
["What is the decimal ASCII code of CR (Carriage Return)?","13","10","8","9","CR = 13 (hex 0D). LF (Line Feed) is 10."],
["Which control character has ASCII code 7?","BEL (Bell/Alert)","BS (Backspace)","HT (Tab)","ESC (Escape)","Code 7 is BEL, the bell/alert. BS=8, HT=9."],
["What is the key feature of Gray code?","Successive values differ by only one bit","Each digit uses 4 bits","It uses 7 bits","It uses base 8","In Gray (reflected binary) code, consecutive values change in exactly one bit."],
["What is the Gray code for decimal 2?","0011","0010","0110","0001","Binary 0010 → Gray: keep MSB 0, then 0⊕0=0, 0⊕1=1, 1⊕0=1 → 0011."],
["What is the Gray code for decimal 5?","0111","0101","0110","0100","Binary 0101 → 0, 0⊕1=1, 1⊕0=1, 0⊕1=1 → 0111."],
["What is the Gray code for decimal 15?","1000","1111","1110","1100","Binary 1111 → 1, 1⊕1=0, 0, 0 → 1000."],
["What is the Gray code for decimal 8?","1100","1000","1110","0100","Binary 1000 → 1, 1⊕0=1, 0, 0 → 1100."],
["What is the Gray code for decimal 10?","1111","1010","1110","1011","Binary 1010 → 1, 1⊕0=1, 0⊕1=1, 1⊕0=1 → 1111."],
["What is the Gray code for decimal 7?","0100","0111","0110","0101","Binary 0111 → 0, 0⊕1=1, 1⊕1=0, 1⊕1=0 → 0100."],
["What is the Gray code for decimal 12?","1010","1100","1110","0110","Binary 1100 → 1, 1⊕1=0, 1⊕0=1, 0⊕0=0 → 1010."],
["Gray code is widely used in:","Rotary encoders and Karnaugh maps","Word processing","Printing only","Decimal addition","Because only one bit changes at a time, it reduces errors in encoders and is used in K-maps."],
["An AND gate outputs 1 only when:","All inputs are 1","Any input is 1","Inputs differ","All inputs are 0","AND multiplies inputs: output is 1 only if every input is 1."],
["What is 1 + 0 in Boolean OR?","1","0","10","Undefined","OR outputs 1 if any input is 1."],
["What is the NOT of 0?","1","0","10","Undefined","NOT inverts its input: ¬0 = 1 and ¬1 = 0."],
["What is the output of a NAND gate when both inputs are 1?","0","1","Undefined","Same as input A","NAND = NOT(AND). AND(1,1)=1, so NAND = 0."],
["What is the output of a NOR gate when both inputs are 0?","1","0","Undefined","Same as input A","NOR = NOT(OR). OR(0,0)=0, so NOR = 1."],
["What is the output of an XOR gate when both inputs are 1?","0","1","Undefined","10","XOR is 1 only if inputs differ. Both equal → 0."],
["What is the output of an XNOR gate when both inputs are 1?","1","0","Undefined","10","XNOR is 1 when inputs are the same."],
["Which gates are called universal gates?","NAND and NOR","AND and OR","XOR and XNOR","NOT and Buffer","NAND and NOR can implement every other gate."],
["An XOR gate outputs 1 when:","Inputs differ","Inputs are the same","Both inputs are 1","Both inputs are 0","XOR = exclusive OR: true only if exactly one input is 1."],
["What is the output of XNOR when A = 0 and B = 1?","0","1","Undefined","01","Inputs differ, so XNOR (the opposite of XOR) gives 0."],
["A NAND gate is equivalent to:","An AND gate followed by NOT","An OR gate followed by NOT","A NOT gate followed by AND","An XOR followed by NOT","NAND = AND then NOT. NOR = OR then NOT."],
["Which Boolean expression represents XOR?","xy′ + x′y","xy + x′y′","x + y","(xy)′","XOR = xy′ + x′y (1 when inputs differ). xy + x′y′ is XNOR."],
["What is the output of a NOR gate when inputs are 1 and 0?","0","1","Undefined","10","OR(1,0)=1, NOT of 1 = 0."],
["The algebraic function of a Buffer is:","F = x","F = x′","F = x + y","F = xy","A buffer passes its input unchanged: F = x."],
["The symbol ⊕ represents which gate?","XOR","XNOR","NAND","NOR","A ⊕ B is the XOR (exclusive-OR) expression."],
["Who developed Boolean Algebra?","George Boole","Charles Babbage","Alan Turing","Blaise Pascal","English mathematician George Boole (1815–1864)."],
["How many fundamental Boolean operations are there?","3 (AND, OR, NOT)","2","4","7","The three fundamental operations are AND, OR and NOT."],
["Identity law: A + 0 = ?","A","0","1","A′","Adding 0 does not change A (identity law)."],
["Null law: A + 1 = ?","1","A","0","A′","If one OR input is 1, the output is always 1."],
["Inverse law: A + A′ = ?","1","0","A","A′","Either A or A′ is always 1, so the OR is 1."],
["Inverse law: A · A′ = ?","0","1","A","A′","A and A′ can never both be 1, so the AND is 0."],
["Idempotent law: A + A = ?","A","2A","1","0","Boolean: 1+1 = 1 and 0+0 = 0, so A + A = A."],
["Null law: A · 0 = ?","0","A","1","A′","AND with 0 always gives 0."],
["Identity law: A · 1 = ?","A","1","0","A′","AND with 1 leaves A unchanged."],
["If A = 1, what is A′ (the prime/NOT of A)?","0","1","A","Undefined","A′ is the complement of A, so 1 becomes 0."]
];
const app=document.getElementById('app');
let qs,i,sc,wrong;
const sh=a=>{a=a.slice();
             for(let k=a.length-1;k>0;k--)
             {const j=Math.random()*(k+1)|0;[a[k],a[j]]=[a[j],a[k]]}return a};
function start(){app.innerHTML=`<div class="c"><h1>CMP 122 CBT Practice</h1><p>${Q.length} questions: number systems, conversions, BCD/ASCII/Gray codes, logic gates and Boolean algebra.</p><p>Tap an answer to see if it is right or wrong, plus the full solution.</p><button class="b" onclick="go(Q.length)">Start all ${Q.length} questions</button><button class="b s" onclick="go(20)">Quick test (20 random)</button></div>`}
function go(n){qs=sh(Q).slice(0,n);i=0;sc=0;wrong=[];show()}
function show(){const q=qs[i];const opts=sh(q.slice(1,5));
app.innerHTML=`<div class="c"><div class="top"><span>Question ${i+1} of ${qs.length}</span><span>Score: ${sc}</span></div><div class="bar"><i style="width:${i/qs.length*100}%"></i></div><div class="q">${q[0]}</div><div id="os">${opts.map((o,k)=>`<button class="o" data-v="${k}">${String.fromCharCode(65+k)}. ${o}</button>`).join('')}</div><div id="fb"></div></div>`;
document.querySelectorAll('.o').forEach((b,k)=>b.onclick=()=>pick(b,opts[k],q))}
function pick(b,v,q){const good=v===q[1];if(good)sc++;else wrong.push(q);
document.querySelectorAll('.o').forEach((x,k)=>{x.disabled=true;const t=x.textContent.slice(3);if(t===q[1])x.classList.add('ok');else if(x===b)x.classList.add('no')});
document.getElementById('fb').innerHTML=`<div class="ex ${good?'ok':'no'}"><b>${good?'✓ Correct!':'✗ Wrong. Correct answer: '+q[1]}</b><span>${q[5]}</span></div><button class="b" onclick="next()">${i+1<qs.length?'Next question':'See results'}</button>`}
function next(){i++;i<qs.length?show():end()}
function end(){const p=Math.round(sc/qs.length*100);
app.innerHTML=`<div class="c"><h1>Results</h1><div class="big">${sc} / ${qs.length}</div><p style="text-align:center">${p}% — ${p>=70?'Excellent work!':p>=50?'Good, keep practising.':'Revise the handbook and try again.'}</p><button class="b" onclick="go(qs.length)">Retake</button><button class="b s" onclick="start()">Home</button></div>`+
(wrong.length?`<div class="c"><h1>Review of mistakes</h1>${wrong.map(q=>`<div class="r"><b>${q[0]}</b>Answer: ${q[1]}<br><span style="color:var(--mu)">${q[5]}</span></div>`).join('')}</div>`:'')}
start();
</script></body></html>
