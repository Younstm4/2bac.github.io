<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Bac 2027 — Study Planner</title>
<style>
:root{
  --paper:#FCFCFA;
  --ink:#1F2430;
  --ink-2:#4A5365;
  --ink-3:#818B9C;
  --rule:#E6E8EC;
  --rule-soft:#F0F1F4;

  --maths:#3D7A34;
  --physics:#4B45B8;
  --chemistry:#067A6E;
  --svt:#B06010;
  --philosophy:#9A2B62;

  --gold:#B8892B;
  --break-bg:#F6F5F1;
  --rev-bg:#F7F4EC;

  --sans:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  --serif:Georgia,"Iowan Old Style","Palatino Linotype",Palatino,serif;
  --ar:"Noto Naskh Arabic","Geeza Pro","Al Bayan","Times New Roman",serif;
  --gut:18px;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{-webkit-text-size-adjust:100%}
body{
  margin:0;background:var(--paper);color:var(--ink);
  font-family:var(--sans);font-size:16px;line-height:1.5;padding:0 0 64px;
}
.wrap{max-width:720px;margin:0 auto;padding:0 var(--gut)}

header{padding:26px 0 6px}
.kicker{font-size:13px;color:var(--ink-3)}
h1{font-family:var(--serif);font-weight:400;font-size:30px;line-height:1.15;
   margin:2px 0 0;letter-spacing:-.01em}
h1 em{font-style:normal;color:var(--ink-3)}

.ruler-block{margin:22px 0 8px}
.ruler{display:flex;align-items:flex-end;gap:2px;height:52px;
  padding-bottom:9px;border-bottom:1px solid var(--rule)}
.tick{flex:1 1 0;min-width:0;border:0;padding:0;cursor:pointer;background:none;
  display:flex;align-items:flex-end;justify-content:center;height:100%}
.tick i{display:block;width:100%;border-radius:1px;background:#D2D6DE;
  transition:background .2s ease,transform .2s ease}
.tick[data-p="break"] i{height:26%}
.tick[data-p="lessons"] i{height:62%}
.tick[data-p="revision"] i{height:86%;background:transparent;box-shadow:inset 0 0 0 1.5px #CBBF9E}
.tick[data-p="exam"] i{height:100%;background:var(--ink)}
.tick[data-p="after"] i{height:22%}
.tick.past i{background:#9AA3B2}
.tick.past[data-p="revision"] i{background:#DCCFA8;box-shadow:none}
.tick.now i{background:var(--gold);box-shadow:none}
.tick:focus-visible{outline:2px solid var(--ink);outline-offset:2px;border-radius:2px}
.tick:hover i{transform:scaleY(1.06);transform-origin:bottom}

.ruler-axis{display:flex;justify-content:space-between;
  font-size:11.5px;color:var(--ink-3);padding-top:7px}
.legend{display:flex;flex-wrap:wrap;gap:14px;font-size:12.5px;color:var(--ink-3);margin-top:12px}
.legend span{display:inline-flex;align-items:center;gap:6px}
.legend b{display:block;width:9px;border-radius:1px;background:#9AA3B2}
.legend .l1 b{height:9px}
.legend .l2 b{height:13px;box-shadow:inset 0 0 0 1.5px #CBBF9E;background:#DCCFA8}
.legend .l3 b{height:15px;background:var(--ink)}

.count{display:flex;align-items:baseline;gap:11px;flex-wrap:wrap;
  margin:20px 0 4px;padding-bottom:20px;border-bottom:1px solid var(--rule)}
.count .big{font-family:var(--serif);font-size:46px;line-height:1;letter-spacing:-.02em}
.count .txt{font-size:14.5px;color:var(--ink-2);max-width:36ch}

.now-panel{margin:24px 0 6px}
.panel-head{display:flex;align-items:baseline;justify-content:space-between;gap:12px;margin-bottom:12px}
.panel-head h2{font-size:14px;font-weight:600;margin:0}
.panel-head .when{font-size:13px;color:var(--ink-3);white-space:nowrap}

.subj{display:flex;gap:12px;padding:11px 0;border-top:1px solid var(--rule-soft)}
.subj:first-of-type{border-top:1px solid var(--rule)}
.subj .bar{width:3px;border-radius:2px;flex:0 0 3px;align-self:stretch}
.subj .body{min-width:0;flex:1}
.subj .name{font-size:12px;font-weight:600;margin-bottom:2px}
.subj .what{font-size:15px;line-height:1.42}
.subj .what.none{color:var(--ink-3)}
.ar{font-family:var(--ar);font-size:17px;line-height:1.75;direction:rtl;text-align:right}
.gloss{font-size:12.5px;color:var(--ink-3);direction:ltr;text-align:left;margin-top:1px}

.c-maths{background:var(--maths)} .n-maths{color:var(--maths)}
.c-physics{background:var(--physics)} .n-physics{color:var(--physics)}
.c-chemistry{background:var(--chemistry)} .n-chemistry{color:var(--chemistry)}
.c-svt{background:var(--svt)} .n-svt{color:var(--svt)}
.c-philosophy{background:var(--philosophy)} .n-philosophy{color:var(--philosophy)}

.tabs{position:sticky;top:0;z-index:20;background:var(--paper);
  display:flex;gap:6px;margin-top:30px;
  padding:14px var(--gut) 10px;
  margin-left:calc(-1 * var(--gut));margin-right:calc(-1 * var(--gut));
  border-bottom:1px solid var(--rule)}
.tab{font:inherit;font-size:14px;border:0;background:none;color:var(--ink-3);
  padding:7px 12px;border-radius:7px;cursor:pointer}
.tab[aria-selected="true"]{background:var(--ink);color:#fff}
.tab:focus-visible{outline:2px solid var(--ink);outline-offset:2px}

.weeks{margin-top:8px}
.wk{border-bottom:1px solid var(--rule);padding:18px 0;scroll-margin-top:74px}
.wk-top{display:flex;align-items:baseline;gap:12px;margin-bottom:12px}
.wk-no{font-family:var(--serif);font-size:26px;line-height:1;color:var(--ink-3);
  min-width:34px;font-variant-numeric:tabular-nums}
.wk-meta{flex:1;min-width:0}
.wk-dates{font-size:15px;font-weight:600}
.wk-note{font-size:13px;color:var(--ink-2);margin-top:2px}
.wk.current{background:#FFFDF6;margin:0 -14px;padding:18px 14px;border-radius:10px;
  border:1px solid #EADFC0}
.wk.current .wk-no{color:var(--gold)}
.flag{display:inline-block;font-size:11.5px;padding:2px 8px;border-radius:20px;
  background:#F1F2F5;color:var(--ink-2);margin-left:auto;white-space:nowrap}
.flag.now{background:var(--gold);color:#fff}
.flag.exam{background:var(--ink);color:#fff}
.wk.rest{background:var(--break-bg);margin:0 -14px;padding:14px;border-radius:10px;border-bottom:0}
.wk.rest + .wk{border-top:1px solid var(--rule)}
.wk.rest .wk-no{color:#B8BDC7}
.wk.revise{background:var(--rev-bg);margin:0 -14px;padding:18px 14px;border-radius:10px;border-bottom:0}
.wk.revise + .wk{border-top:1px solid var(--rule)}

.sub-block{margin:26px 0 34px}
.sub-head{display:flex;align-items:baseline;gap:10px;margin-bottom:4px}
.sub-head h3{font-size:19px;margin:0;font-weight:600}
.sub-head .pct{margin-left:auto;font-size:13px;color:var(--ink-3);font-variant-numeric:tabular-nums}
.meter{height:3px;background:var(--rule);border-radius:2px;overflow:hidden;margin:8px 0 4px}
.meter i{display:block;height:100%;width:0;transition:width .35s ease}
.unit{font-size:12px;font-weight:600;color:var(--ink-3);
  padding:18px 0 7px;border-bottom:1px solid var(--rule-soft)}
.les{display:flex;gap:12px;align-items:flex-start;
  padding:12px 0;border-bottom:1px solid var(--rule-soft);cursor:pointer}
.les input{appearance:none;-webkit-appearance:none;margin:2px 0 0;flex:0 0 19px;
  width:19px;height:19px;border:1.5px solid #C3C9D4;border-radius:5px;background:#fff;
  cursor:pointer;position:relative;transition:border-color .15s,background .15s}
.les input:checked{background:currentColor;border-color:currentColor}
.les input:checked::after{content:"";position:absolute;left:5.5px;top:2px;width:5px;height:10px;
  border:solid #fff;border-width:0 2px 2px 0;transform:rotate(42deg)}
.les input:focus-visible{outline:2px solid var(--ink);outline-offset:2px}
.les .t{flex:1;min-width:0;font-size:15px;line-height:1.4;color:var(--ink)}
.les .d{font-size:12.5px;color:var(--ink-3);white-space:nowrap;padding-top:2px;
  font-variant-numeric:tabular-nums}
.les.done .t{color:var(--ink-3);text-decoration:line-through;text-decoration-color:#C3C9D4}
.les .opt{font-size:12px;color:var(--ink-3);display:block;margin-top:2px}

.dates .row{display:flex;gap:14px;padding:13px 0;border-bottom:1px solid var(--rule-soft)}
.dates .when{flex:0 0 118px;font-size:13px;color:var(--ink-2);font-variant-numeric:tabular-nums}
.dates .what{flex:1;font-size:15px;line-height:1.4}
.dates .row.key .what{font-weight:600}
.dates .row.key .when{color:var(--ink)}
.dates .sub{display:block;font-size:12.5px;color:var(--ink-3);margin-top:1px;font-weight:400}

.note{font-size:13.5px;color:var(--ink-2);line-height:1.6;background:#fff;
  border:1px solid var(--rule);border-radius:10px;padding:14px 16px;margin:22px 0}
.note b{font-weight:600;color:var(--ink)}
.reset{font:inherit;font-size:12.5px;background:none;border:0;color:var(--ink-3);
  text-decoration:underline;cursor:pointer;padding:6px 0;margin-top:6px}
[hidden]{display:none !important}

@media (max-width:430px){
  :root{--gut:15px}
  h1{font-size:26px}
  .count .big{font-size:40px}
  .dates .when{flex:0 0 96px}
}
@media (prefers-reduced-motion:reduce){*{transition:none !important;animation:none !important}}
</style>
</head>
<body>
<div class="wrap">

<header>
  <div class="kicker">2<sup>ème</sup> Bac — Sciences Physiques</div>
  <h1>Your year to the Watani <em>2026 / 2027</em></h1>
</header>

<div class="ruler-block">
  <div class="ruler" id="ruler" role="group" aria-label="The plan, one bar per week"></div>
  <div class="ruler-axis"><span>Sep</span><span>Nov</span><span>Jan</span><span>Mar</span><span>May</span><span>Jun</span></div>
  <div class="legend">
    <span class="l1"><b></b>Break</span>
    <span class="l1"><b style="height:15px"></b>Lessons</span>
    <span class="l2"><b></b>Revision</span>
    <span class="l3"><b></b>Exam</span>
  </div>
</div>

<div class="count">
  <div class="big" id="cd">—</div>
  <div class="txt" id="cdTxt"></div>
</div>

<section class="now-panel">
  <div class="panel-head">
    <h2 id="nowTitle">This week</h2>
    <div class="when" id="nowDates"></div>
  </div>
  <div id="nowBody"></div>
</section>

<nav class="tabs" role="tablist" aria-label="Views">
  <button class="tab" role="tab" aria-selected="true"  data-view="weeks">Weeks</button>
  <button class="tab" role="tab" aria-selected="false" data-view="subjects">Subjects</button>
  <button class="tab" role="tab" aria-selected="false" data-view="dates">Key dates</button>
</nav>

<div id="v-weeks" class="weeks"></div>
<div id="v-subjects" hidden></div>
<div id="v-dates" class="dates" hidden></div>

</div>

<script>
"use strict";

/* ─────────────────────────── the year ─────────────────────────── */
const START = new Date(2026, 8, 21);   // Mon 21 Sep 2026 — week 1 of this plan
const EXAM  = new Date(2027, 5, 1);    // Tue 1 Jun 2027
const NW = 39;
const LAST_TEACHING = 26;              // week 26 ends Sun 21 Mar 2027

const BREAKS = {
  5:"Autumn break, 18–25 Oct",
  12:"Second break, 6–13 Dec",
  19:"Mid-year break, 24–31 Jan",
  27:"Spring break, 21–28 Mar",
  34:"May break, 9–16 May"
};

const NOTES = {
  1:"Your plan starts here.",
  7:"Green March holiday, Friday 6 Nov. First class tests land around now.",
  9:"Independence Day, Wednesday 18 Nov.",
  15:"New Year's Day, Friday 1 Jan.",
  17:"Independence Manifesto 11 Jan, Amazigh New Year 14 Jan. Second round of class tests.",
  18:"End of the first term.",
  22:"Ramadan begins around 18 February.",
  24:"Class tests, second term.",
  26:"Aïd al-Fitr around 20 March. Last teaching week of the syllabus.",
  27:"Syllabus finished. Rest, then revision starts Monday 29 March.",
  32:"Labour Day, Saturday 1 May.",
  33:"Mock exam season.",
  36:"Lessons officially end Saturday 29 May.",
  37:"National exam, Tuesday 1 to Thursday 3 June.",
  39:"Results published Saturday 19 June."
};

const D = n => { const d = new Date(START); d.setDate(d.getDate() + (n-1)*7); return d; };
const DAY = ["Sun","Mon","Tue","Wed","Thu","Fri","Sat"];
const MON = ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"];
const fmt  = d => DAY[d.getDay()]+" "+d.getDate()+" "+MON[d.getMonth()];
const fmtY = d => fmt(d)+" "+d.getFullYear();
function range(n){
  const a = D(n), b = new Date(a); b.setDate(b.getDate()+6);
  return fmt(a)+" – "+fmtY(b);
}
function phase(n){
  if (n === 37) return "exam";
  if (n >= 38) return "after";
  if (n >= 28) return BREAKS[n] ? "break" : "revision";
  return BREAKS[n] ? "break" : "lessons";
}

/* ─────────────────────────── the syllabus ───────────────────────────
   Lesson names stay in French, and in Arabic for Philosophy, because
   that is how they appear in your books. Everything else is English. */

const MATHS = [
 ["Limits, derivatives and sequences", [
  ["m1","Limites et continuité",1,2],
  ["m2","Dérivation et étude des fonctions",3,4],
  ["m3","Suites numériques",6,7]]],
 ["Primitives and logarithms", [
  ["m4","Fonctions primitives",8,8],
  ["m5","Fonctions logarithmiques",9,11]]],
 ["Complex numbers and exponentials", [
  ["m6","Nombres complexes — partie 1",13,14],
  ["m7","Fonctions exponentielles",15,17],
  ["m8","Nombres complexes — partie 2",18,18]]],
 ["Integration and differential equations", [
  ["m9","Calcul intégral",20,21],
  ["m10","Équations différentielles",22,22]]],
 ["Space geometry and probability", [
  ["m11","Géométrie dans l'espace (produit scalaire, produit vectoriel)",23,24],
  ["m12","Dénombrement et probabilités",25,26]]]
];

const PHYSICS = [
 ["Waves", [
  ["p1","Les ondes mécaniques progressives",1,1],
  ["p2","Les ondes mécaniques progressives périodiques",2,2],
  ["p3","Propagation des ondes lumineuses (diffraction, dispersion)",3,3]]],
 ["Nuclear transformations", [
  ["p4","Décroissance radioactive",4,4],
  ["p5","Noyaux, masse et énergie",6,6]]],
 ["Electricity", [
  ["p6","Dipôle RC",7,8],
  ["p7","Dipôle RL",9,10],
  ["p8","Oscillations libres d'un circuit RLC série",11,13],
  ["p9","Circuit RLC série en régime sinusoïdal forcé",null,null,"Sciences Maths syllabus — ask your teacher whether you are examined on it"],
  ["p10","Ondes électromagnétiques",14,14],
  ["p11","Modulation d'amplitude",15,15]]],
 ["Mechanics", [
  ["p12","Lois de Newton",16,17],
  ["p13","Chute libre verticale et chute avec frottement",18,18],
  ["p14","Mouvements plans (projectile, particule chargée)",20,21],
  ["p15","Mouvement des satellites et des planètes",22,22],
  ["p16","Mouvement de rotation d'un solide autour d'un axe fixe",23,23],
  ["p17","Systèmes mécaniques oscillants (pendule élastique, pesant, torsion)",24,25],
  ["p18","Aspects énergétiques des oscillations mécaniques",26,26],
  ["p19","Atome et mécanique de Newton",26,26]]]
];

const CHEMISTRY = [
 ["Reaction rates", [
  ["c1","Transformations lentes et transformations rapides",1,1],
  ["c2","Suivi temporel d'une transformation — vitesse de réaction",2,2]]],
 ["Chemical equilibrium", [
  ["c3","Transformations chimiques s'effectuant dans les deux sens",4,4],
  ["c4","État d'équilibre d'un système chimique",6,7],
  ["c5","Transformations liées à des réactions acide-base",9,10],
  ["c6","Dosage acido-basique",13,14]]],
 ["Which way a reaction goes", [
  ["c7","Évolution spontanée d'un système chimique",16,16],
  ["c8","Transformations spontanées dans les piles et production d'énergie",18,18],
  ["c9","Transformations forcées (électrolyse)",21,21]]],
 ["Controlling a reaction", [
  ["c10","Réactions d'estérification et d'hydrolyse",23,24],
  ["c11","Contrôle de l'évolution d'un système chimique",26,26]]]
];

const SVT = [
 ["Energy from organic matter", [
  ["s1","Libération de l'énergie emmagasinée dans la matière organique (glycolyse, respiration, fermentation)",1,2],
  ["s2","Rôle du muscle strié squelettique dans la conversion de l'énergie",3,4]]],
 ["Genetic material", [
  ["s3","Notion de l'information génétique (mitose, ADN, réplication)",6,8],
  ["s4","Expression de l'information génétique (transcription, traduction)",9,11],
  ["s5","Transmission de l'information génétique par la reproduction sexuée (méiose, brassage, fécondation)",13,15],
  ["s6","Lois statistiques de la transmission des caractères héréditaires",16,18]]],
 ["Using organic and inorganic matter", [
  ["s7","Les ordures ménagères",20,20],
  ["s8","La pollution des milieux naturels",21,21],
  ["s9","Les matières radioactives et l'énergie nucléaire",22,22],
  ["s10","Contrôle de la qualité et de la salubrité des milieux naturels",23,23]]],
 ["Geology", [
  ["s11","Les chaînes de montagnes récentes et la tectonique des plaques",24,24],
  ["s12","Le métamorphisme et sa relation avec la tectonique des plaques",25,25],
  ["s13","La granitisation et sa relation avec le métamorphisme",26,26]]]
];

const PHILOSOPHY = [
 ["مجزوءة الوضع البشري — The human condition", [
  ["f1","مفهوم الشخص","The person","الشخص والهوية / الشخص بوصفه قيمة / الشخص بين الضرورة والحرية",1,2],
  ["f2","مفهوم الغير","The other","وجود الغير / معرفة الغير / العلاقة مع الغير",3,4],
  ["f3","مفهوم التاريخ","History","المعرفة التاريخية / التاريخ وفكرة التقدم / دور الإنسان في التاريخ",6,8]]],
 ["مجزوءة المعرفة — Knowledge", [
  ["f4","مفهوم النظرية والتجربة","Theory and experiment","التجربة والتجريب / العقلانية العلمية / معايير علمية النظريات العلمية",9,11],
  ["f5","مفهوم الحقيقة","Truth","الرأي والحقيقة / معايير الحقيقة / الحقيقة بوصفها قيمة",13,15]]],
 ["مجزوءة السياسة — Politics", [
  ["f6","مفهوم الدولة","The state","مشروعية الدولة وغاياتها / طبيعة السلطة السياسية / الدولة بين الحق والعنف",16,18],
  ["f7","مفهوم الحق والعدالة","Right and justice","الحق بين الطبيعي والوضعي / العدالة كأساس للحق / العدالة بين الإنصاف والمساواة",20,22]]],
 ["مجزوءة الأخلاق — Ethics", [
  ["f8","مفهوم الواجب","Duty","الواجب والإكراه / الوعي الأخلاقي / الواجب والمجتمع",23,24],
  ["f9","مفهوم السعادة","Happiness","تمثلات السعادة / السعادة والواجب / السعادة والرغبة",25,26]]]
];

const SUBJECTS = [
  {key:"maths",      label:"Maths",      data:MATHS},
  {key:"physics",    label:"Physics",    data:PHYSICS},
  {key:"chemistry",  label:"Chemistry",  data:CHEMISTRY},
  {key:"svt",        label:"SVT",        data:SVT},
  {key:"philosophy", label:"Philosophy", data:PHILOSOPHY, arabic:true}
];

/* revision plan, weeks 28–37 */
const REVISION = {
 28:{maths:"Limites, continuité, dérivation, étude de fonctions. Redo every exercise.",
     physics:"Ondes mécaniques et lumineuses + décroissance radioactive.",
     chemistry:"Cinétique: transformations lentes et rapides, vitesse de réaction.",
     svt:"Unit 1 in full: énergie et muscle strié squelettique.",
     philosophy:"الشخص والغير + منهجية تحليل النص"},
 29:{maths:"Suites numériques + fonctions primitives. Convergence proofs by hand.",
     physics:"Noyaux, masse et énergie + dipôles RC et RL.",
     chemistry:"État d'équilibre + réactions acide-base.",
     svt:"Information génétique et son expression — ADN, transcription, traduction.",
     philosophy:"التاريخ + النظرية والتجربة"},
 30:{maths:"Fonctions logarithmiques et exponentielles. The biggest exam block.",
     physics:"RLC libre, ondes électromagnétiques, modulation d'amplitude.",
     chemistry:"Dosage acido-basique + évolution spontanée.",
     svt:"Méiose, brassage, fécondation, lois statistiques. Genetics problems daily.",
     philosophy:"الحقيقة + منهجية السؤال"},
 31:{maths:"Nombres complexes, parties 1 et 2. Every geometric interpretation.",
     physics:"Lois de Newton, chute libre, mouvements plans, satellites.",
     chemistry:"Piles, électrolyse, estérification et hydrolyse.",
     svt:"Unit 3: ordures, pollution, radioactivité, qualité des milieux.",
     philosophy:"الدولة + الحق والعدالة"},
 32:{maths:"Calcul intégral, équations différentielles, géométrie dans l'espace, probabilités.",
     physics:"Rotation, oscillateurs, aspects énergétiques, atome et mécanique de Newton.",
     chemistry:"Contrôle de l'évolution + full formula sheet from memory.",
     svt:"Géologie: chaînes de montagnes, métamorphisme, granitisation.",
     philosophy:"الواجب + السعادة + منهجية القولة"},
 33:{maths:"National exams 2018–2020, timed, no notes.",
     physics:"National exams 2018–2020, timed.",
     chemistry:"Same papers — chemistry sections.",
     svt:"National exams 2018–2020.",
     philosophy:"الامتحانات الوطنية 2018 ← 2020"},
 34:{maths:"National exams 2021–2022. Rebuild anything you got wrong.",
     physics:"National exams 2021–2022.",
     chemistry:"Same papers — chemistry sections.",
     svt:"National exams 2021–2022.",
     philosophy:"الامتحانات الوطنية 2021 ← 2022 + حفظ المواقف"},
 35:{maths:"National exams 2023–2024 + your own formula sheet.",
     physics:"National exams 2023–2024 + formula sheet.",
     chemistry:"Same papers. Every equation balanced from memory.",
     svt:"National exams 2023–2024. Redraw every diagram from memory.",
     philosophy:"الامتحانات الوطنية 2023 ← 2024"},
 36:{maths:"National exams 2025–2026, full paper, exam conditions.",
     physics:"National exams 2025–2026, exam conditions.",
     chemistry:"Same papers, exam conditions.",
     svt:"National exams 2025–2026, exam conditions.",
     philosophy:"الامتحانات الوطنية 2025 ← 2026"},
 37:{maths:"Your notes only. Nothing new. Sleep.",
     physics:"Your notes only.",
     chemistry:"Your notes only.",
     svt:"Notes and diagrams only.",
     philosophy:"مراجعة المواقف والمفاهيم فقط"}
};

const KEYDATES = [
 ["Mon 21 Sep 2026","Your plan starts","",1],
 ["18–25 Oct 2026","Autumn break","Eight days",0],
 ["Late Oct – mid Nov","First class tests, term 1","Your school fixes the exact date",0],
 ["Fri 6 Nov 2026","Green March holiday","",0],
 ["Wed 18 Nov 2026","Independence Day","",0],
 ["6–13 Dec 2026","Second break","Eight days",0],
 ["Fri 1 Jan 2027","New Year's Day","",0],
 ["Mon 11 Jan 2027","Independence Manifesto Day","",0],
 ["Thu 14 Jan 2027","Amazigh New Year","",0],
 ["January 2027","Second class tests, term 1","Before the mid-year break",0],
 ["24–31 Jan 2027","Mid-year break","Eight days",0],
 ["~18 Feb 2027","Ramadan begins","Depends on the moon",0],
 ["March 2027","Class tests, term 2","",0],
 ["~20 Mar 2027","Aïd al-Fitr","Three or four days, depends on the moon",0],
 ["Sun 21 Mar 2027","Syllabus finished","Nothing new after this date — the whole point of the plan",1],
 ["21–28 Mar 2027","Spring break","Eight days",0],
 ["Apr – May 2027","Mock exam","Usually April or early May",0],
 ["Sat 1 May 2027","Labour Day","",0],
 ["9–16 May 2027","May break","Eight days",0],
 ["Sat 29 May 2027","Lessons end for 2ème Bac","Other year groups carry on to 26 June",0],
 ["1–3 Jun 2027","National exam","All streams",1],
 ["Sat 19 Jun 2027","Results","",1],
 ["1–3 Jul 2027","Resit session","",0]
];

/* ─────────────────────────── lookups ─────────────────────────── */
const byWeek = {};
const allLessons = {};
SUBJECTS.forEach(s=>{
  s.data.forEach(([unit,items])=>{
    items.forEach(it=>{
      const isPhil = !!s.arabic;
      const id = it[0], title = it[1];
      const sw = isPhil ? it[4] : it[2];
      const ew = isPhil ? it[5] : it[3];
      allLessons[id] = {subject:s.key, title, unit, sw, ew, gloss:isPhil?it[2]:null};
      if (sw == null) return;
      for (let w=sw; w<=ew; w++){
        if (BREAKS[w]) continue;
        let t = title;
        if (ew>sw && !isPhil) t += (w===ew ? " — finish it" : (w>sw ? " — keep going" : ""));
        let g = isPhil ? it[2] : null;
        if (g && ew>sw) g += (w===ew ? " — finish it" : (w>sw ? " — keep going" : ""));
        byWeek[w] = byWeek[w] || {};
        (byWeek[w][s.key] = byWeek[w][s.key] || []).push({t, ar:isPhil, gloss:g});
      }
    });
  });
});

const today = new Date(); today.setHours(0,0,0,0);
let CUR = Math.floor((today - START)/(7*864e5)) + 1;
CUR = Math.max(1, Math.min(NW, CUR));

/* ─────────────────────────── progress ─────────────────────────── */
const KEY = "bac2027:progress";
let done = {};
let storageOK = true;
async function loadProgress(){
  try{ const r = await window.storage.get(KEY); if (r && r.value) done = JSON.parse(r.value); }
  catch(e){}
}
async function saveProgress(){
  if (!storageOK) return;
  try{ await window.storage.set(KEY, JSON.stringify(done)); }catch(e){ storageOK = false; }
}

/* ─────────────────────────── render ─────────────────────────── */
function el(tag, cls, html){
  const n = document.createElement(tag);
  if (cls) n.className = cls;
  if (html != null) n.innerHTML = html;
  return n;
}
const esc = s => String(s).replace(/[&<>"]/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));

function drawRuler(){
  const r = document.getElementById("ruler");
  for (let n=1;n<=NW;n++){
    const p = phase(n);
    const b = el("button","tick");
    b.dataset.p = p; b.dataset.n = n;
    if (n < CUR) b.classList.add("past");
    if (n === CUR) b.classList.add("now");
    b.title = "Week "+n+" — "+range(n);
    b.setAttribute("aria-label","Week "+n+", "+range(n));
    b.appendChild(el("i"));
    b.addEventListener("click", ()=>{
      setView("weeks");
      const t = document.getElementById("wk"+n);
      if (t) t.scrollIntoView({behavior:"smooth", block:"start"});
    });
    r.appendChild(b);
  }
}

function drawCount(){
  const days  = Math.max(0, Math.round((EXAM - today)/864e5));
  const weeks = Math.max(0, Math.ceil(days/7));
  let teaching = 0;
  for (let n=CUR; n<=LAST_TEACHING; n++) if (phase(n)==="lessons") teaching++;
  document.getElementById("cd").textContent = days;
  document.getElementById("cdTxt").textContent =
    "days until the national exam on Tuesday 1 June 2027 — about " + weeks +
    " weeks, of which " + teaching + " are teaching weeks before the syllabus has to be finished.";
}

function subjRow(key, label, items){
  const row = el("div","subj");
  row.appendChild(el("div","bar c-"+key));
  const body = el("div","body");
  body.appendChild(el("div","name n-"+key, label));
  if (!items || !items.length){
    body.appendChild(el("div","what none","No new lesson. Spend the time on exercises."));
  } else {
    items.forEach(it=>{
      body.appendChild(el("div","what"+(it.ar?" ar":""), esc(it.t)));
      if (it.gloss) body.appendChild(el("div","gloss", esc(it.gloss)));
    });
  }
  row.appendChild(body);
  return row;
}

function weekContent(n){
  const p = phase(n);
  if (p === "break" && !REVISION[n]) return null;
  if (p === "after") return null;
  const frag = document.createDocumentFragment();
  SUBJECTS.forEach(s=>{
    const items = REVISION[n]
      ? [{t: REVISION[n][s.key], ar: s.key==="philosophy"}]
      : (byWeek[n]||{})[s.key];
    frag.appendChild(subjRow(s.key, s.label, items));
  });
  return frag;
}

function drawNow(){
  document.getElementById("nowTitle").textContent = "This week — week "+CUR+" of "+NW;
  document.getElementById("nowDates").textContent = range(CUR);
  const body = document.getElementById("nowBody");
  body.innerHTML = "";
  const c = weekContent(CUR);
  if (c) { body.appendChild(c); return; }
  let msg;
  if (phase(CUR) === "after")
    msg = "<b>It's done.</b> Results come out on Saturday 19 June.";
  else if (CUR === 27)
    msg = "<b>"+esc(BREAKS[27])+".</b> The syllabus is finished. Rest properly, then revision starts Monday 29 March.";
  else
    msg = "<b>"+esc(BREAKS[CUR]||"Break")+".</b> Nothing new is scheduled. Catch up if you are behind, otherwise actually rest.";
  body.appendChild(el("div","note", msg));
}

function drawWeeks(){
  const host = document.getElementById("v-weeks");
  for (let n=1;n<=NW;n++){
    const p = phase(n);
    const revising = p==="revision" || !!REVISION[n];
    const wk = el("div","wk"
      + (p==="break" && !REVISION[n] ? " rest" : "")
      + (revising ? " revise" : "")
      + (n===CUR ? " current" : ""));
    wk.id = "wk"+n;
    const top = el("div","wk-top");
    top.appendChild(el("div","wk-no", n));
    const meta = el("div","wk-meta");
    meta.appendChild(el("div","wk-dates", range(n)));
    const note = NOTES[n] || BREAKS[n] || "";
    if (note) meta.appendChild(el("div","wk-note", esc(note)));
    top.appendChild(meta);
    if (n===CUR) top.appendChild(el("span","flag now","This week"));
    else if (p==="exam") top.appendChild(el("span","flag exam","Exam"));
    else if (p==="break" && REVISION[n]) top.appendChild(el("span","flag","Break, keep revising"));
    else if (p==="revision") top.appendChild(el("span","flag","Revision"));
    else if (p==="break") top.appendChild(el("span","flag","Break"));
    else if (p==="after") top.appendChild(el("span","flag","After"));
    wk.appendChild(top);
    const c = weekContent(n);
    if (c) wk.appendChild(c);
    host.appendChild(wk);
  }
}

function drawSubjects(){
  const host = document.getElementById("v-subjects");
  host.innerHTML = "";
  host.appendChild(el("div","note",
    "Tick a lesson when you have <b>understood it and done at least three exercise sets</b> on it — "+
    "not when the teacher finished it. Ticks are saved on this device."));
  SUBJECTS.forEach(s=>{
    const block = el("div","sub-block");
    const head = el("div","sub-head");
    const h = el("h3", "n-"+s.key, s.label);
    head.appendChild(h);
    const pct = el("div","pct"); pct.id = "pct-"+s.key;
    head.appendChild(pct);
    block.appendChild(head);
    const m = el("div","meter"); const mi = el("i"); mi.id = "meter-"+s.key;
    mi.style.background = "var(--"+s.key+")";
    m.appendChild(mi); block.appendChild(m);

    s.data.forEach(([unit,items])=>{
      block.appendChild(el("div","unit", esc(unit)));
      items.forEach(it=>{
        const id = it[0], L = allLessons[id];
        const lab = el("label","les");
        lab.style.color = "var(--"+s.key+")";
        const cb = el("input"); cb.type = "checkbox"; cb.checked = !!done[id];
        if (done[id]) lab.classList.add("done");
        cb.addEventListener("change", ()=>{
          if (cb.checked) done[id] = 1; else delete done[id];
          lab.classList.toggle("done", cb.checked);
          updateMeters(); saveProgress();
        });
        lab.appendChild(cb);
        const t = el("div","t");
        if (s.arabic){
          t.appendChild(el("div","ar", esc(L.title)));
          t.appendChild(el("div","gloss", esc(L.gloss)+" — "+esc(it[3])));
        } else {
          t.appendChild(document.createTextNode(L.title));
          if (it[4]) t.appendChild(el("span","opt","Optional. "+esc(it[4])));
        }
        lab.appendChild(t);
        const due = L.sw == null ? "optional"
                  : fmt(new Date(D(L.ew).getTime() + 6*864e5));
        lab.appendChild(el("div","d","by "+due));
        block.appendChild(lab);
      });
    });
    host.appendChild(block);
  });
  const rb = el("button","reset","Clear all my ticks");
  rb.addEventListener("click", async ()=>{
    done = {};
    document.querySelectorAll(".les input").forEach(cb=>{
      cb.checked = false; cb.closest(".les").classList.remove("done");
    });
    updateMeters();
    try{ await window.storage.delete(KEY); }catch(e){}
  });
  host.appendChild(rb);
  updateMeters();
}

function updateMeters(){
  SUBJECTS.forEach(s=>{
    const ids = [];
    s.data.forEach(([u,items])=>items.forEach(it=>ids.push(it[0])));
    const n = ids.filter(i=>done[i]).length;
    const p = Math.round(n/ids.length*100);
    const pe = document.getElementById("pct-"+s.key);
    const me = document.getElementById("meter-"+s.key);
    if (pe) pe.textContent = n+" of "+ids.length+"  ·  "+p+"%";
    if (me) me.style.width = p+"%";
  });
}

function drawDates(){
  const host = document.getElementById("v-dates");
  KEYDATES.forEach(([when,what,sub,key])=>{
    const r = el("div","row"+(key?" key":""));
    r.appendChild(el("div","when", esc(when)));
    const w = el("div","what", esc(what));
    if (sub) w.appendChild(el("span","sub", esc(sub)));
    r.appendChild(w);
    host.appendChild(r);
  });
}

function setView(v){
  document.querySelectorAll(".tab").forEach(t=>
    t.setAttribute("aria-selected", String(t.dataset.view === v)));
  ["weeks","subjects","dates"].forEach(k=>
    document.getElementById("v-"+k).hidden = (k !== v));
}
document.querySelectorAll(".tab").forEach(t=>
  t.addEventListener("click", ()=>setView(t.dataset.view)));

(async function init(){
  await loadProgress();
  drawRuler();
  drawCount();
  drawNow();
  drawWeeks();
  drawSubjects();
  drawDates();
  setView("weeks");
})();
</script>
</body>
</html>
