import { useState, useEffect } from "react";

const TECH_CATALOG = [
  { label:"HTML5",         logo:"html5",           color:"#E34F26", text:"#fff" },
  { label:"CSS3",          logo:"css3",             color:"#1572B6", text:"#fff" },
  { label:"JavaScript",    logo:"javascript",       color:"#F7DF1E", text:"#000" },
  { label:"TypeScript",    logo:"typescript",       color:"#3178C6", text:"#fff" },
  { label:"Python",        logo:"python",           color:"#3776AB", text:"#fff" },
  { label:"Go",            logo:"go",               color:"#00ADD8", text:"#fff" },
  { label:"Rust",          logo:"rust",             color:"#000000", text:"#fff" },
  { label:"Java",          logo:"java",             color:"#007396", text:"#fff" },
  { label:"C++",           logo:"cplusplus",        color:"#00599C", text:"#fff" },
  { label:"C#",            logo:"csharp",           color:"#239120", text:"#fff" },
  { label:"Swift",         logo:"swift",            color:"#FA7343", text:"#fff" },
  { label:"Kotlin",        logo:"kotlin",           color:"#7F52FF", text:"#fff" },
  { label:"Ruby",          logo:"ruby",             color:"#CC342D", text:"#fff" },
  { label:"PHP",           logo:"php",              color:"#777BB4", text:"#fff" },
  { label:"Dart",          logo:"dart",             color:"#0175C2", text:"#fff" },
  { label:"Scala",         logo:"scala",            color:"#DC322F", text:"#fff" },
  { label:"R",             logo:"r",                color:"#276DC3", text:"#fff" },
  { label:"React",         logo:"react",            color:"#20232A", text:"#61DAFB" },
  { label:"Next.js",       logo:"nextdotjs",        color:"#000000", text:"#fff" },
  { label:"Vue",           logo:"vuedotjs",         color:"#4FC08D", text:"#fff" },
  { label:"Svelte",        logo:"svelte",           color:"#FF3E00", text:"#fff" },
  { label:"Angular",       logo:"angular",          color:"#DD0031", text:"#fff" },
  { label:"Astro",         logo:"astro",            color:"#FF5D01", text:"#fff" },
  { label:"Nuxt",          logo:"nuxtdotjs",        color:"#00DC82", text:"#fff" },
  { label:"Vite",          logo:"vite",             color:"#646CFF", text:"#fff" },
  { label:"TailwindCSS",   logo:"tailwindcss",      color:"#06B6D4", text:"#fff" },
  { label:"Three.js",      logo:"threedotjs",       color:"#000000", text:"#fff" },
  { label:"Flutter",       logo:"flutter",          color:"#02569B", text:"#fff" },
  { label:"WordPress",     logo:"wordpress",        color:"#21759B", text:"#fff" },
  { label:"React Router",  logo:"reactrouter",      color:"#CA4245", text:"#fff" },
  { label:"Node.js",       logo:"nodedotjs",        color:"#339933", text:"#fff" },
  { label:"Express",       logo:"express",          color:"#000000", text:"#fff" },
  { label:"FastAPI",       logo:"fastapi",          color:"#009688", text:"#fff" },
  { label:"Django",        logo:"django",           color:"#092E20", text:"#fff" },
  { label:"Flask",         logo:"flask",            color:"#000000", text:"#fff" },
  { label:"NestJS",        logo:"nestjs",           color:"#E0234E", text:"#fff" },
  { label:"Spring",        logo:"spring",           color:"#6DB33F", text:"#fff" },
  { label:"Laravel",       logo:"laravel",          color:"#FF2D20", text:"#fff" },
  { label:"LiveWire",      logo:"laravel",          color:"#FB70A9", text:"#fff" },
  { label:"PostgreSQL",    logo:"postgresql",       color:"#4169E1", text:"#fff" },
  { label:"MySQL",         logo:"mysql",            color:"#4479A1", text:"#fff" },
  { label:"MongoDB",       logo:"mongodb",          color:"#47A248", text:"#fff" },
  { label:"Redis",         logo:"redis",            color:"#DC382D", text:"#fff" },
  { label:"SQLite",        logo:"sqlite",           color:"#003B57", text:"#fff" },
  { label:"Supabase",      logo:"supabase",         color:"#3ECF8E", text:"#000" },
  { label:"Prisma",        logo:"prisma",           color:"#2D3748", text:"#fff" },
  { label:"MariaDB",       logo:"mariadb",          color:"#003545", text:"#fff" },
  { label:"AWS",           logo:"amazonaws",        color:"#FF9900", text:"#000" },
  { label:"Azure",         logo:"microsoftazure",   color:"#0078D4", text:"#fff" },
  { label:"GCP",           logo:"googlecloud",      color:"#4285F4", text:"#fff" },
  { label:"Vercel",        logo:"vercel",           color:"#000000", text:"#fff" },
  { label:"Netlify",       logo:"netlify",          color:"#00C7B7", text:"#fff" },
  { label:"Heroku",        logo:"heroku",           color:"#430098", text:"#fff" },
  { label:"Docker",        logo:"docker",           color:"#2496ED", text:"#fff" },
  { label:"Kubernetes",    logo:"kubernetes",       color:"#326CE5", text:"#fff" },
  { label:"Firebase",      logo:"firebase",         color:"#FFCA28", text:"#000" },
  { label:"DigitalOcean",  logo:"digitalocean",     color:"#0080FF", text:"#fff" },
  { label:"GitHub Actions",logo:"githubactions",    color:"#2088FF", text:"#fff" },
  { label:"TensorFlow",    logo:"tensorflow",       color:"#FF6F00", text:"#fff" },
  { label:"PyTorch",       logo:"pytorch",          color:"#EE4C2C", text:"#fff" },
  { label:"Pandas",        logo:"pandas",           color:"#150458", text:"#fff" },
  { label:"NumPy",         logo:"numpy",            color:"#013243", text:"#fff" },
  { label:"Scikit-learn",  logo:"scikitlearn",      color:"#F7931E", text:"#fff" },
  { label:"HuggingFace",   logo:"huggingface",      color:"#FFD21F", text:"#000" },
  { label:"Git",           logo:"git",              color:"#F05032", text:"#fff" },
  { label:"GitHub",        logo:"github",           color:"#181717", text:"#fff" },
  { label:"Figma",         logo:"figma",            color:"#F24E1E", text:"#fff" },
  { label:"Adobe",         logo:"adobe",            color:"#FF0000", text:"#fff" },
  { label:"Canva",         logo:"canva",            color:"#00C4CC", text:"#fff" },
  { label:"Postman",       logo:"postman",          color:"#FF6C37", text:"#fff" },
  { label:"NPM",           logo:"npm",              color:"#CB3837", text:"#fff" },
  { label:"GraphQL",       logo:"graphql",          color:"#E10098", text:"#fff" },
  { label:"Twilio",        logo:"twilio",           color:"#F22F46", text:"#fff" },
  { label:"Jira",          logo:"jira",             color:"#0052CC", text:"#fff" },
  { label:"Power BI",      logo:"powerbi",          color:"#F2C811", text:"#000" },
  { label:"Cisco",         logo:"cisco",            color:"#1BA0D7", text:"#fff" },
];

const CATEGORIES = [
  { name:"Languages",   keys:["HTML5","CSS3","JavaScript","TypeScript","Python","Go","Rust","Java","C++","C#","Swift","Kotlin","Ruby","PHP","Dart","Scala","R"] },
  { name:"Frontend",    keys:["React","Next.js","Vue","Svelte","Angular","Astro","Nuxt","Vite","TailwindCSS","Three.js","Flutter","WordPress","React Router","LiveWire"] },
  { name:"Backend",     keys:["Node.js","Express","FastAPI","Django","Flask","NestJS","Spring","Laravel"] },
  { name:"Database",    keys:["PostgreSQL","MySQL","MongoDB","Redis","SQLite","Supabase","Prisma","MariaDB"] },
  { name:"Cloud/DevOps",keys:["AWS","Azure","GCP","Vercel","Netlify","Heroku","Docker","Kubernetes","Firebase","DigitalOcean","GitHub Actions"] },
  { name:"AI/ML",       keys:["TensorFlow","PyTorch","Pandas","NumPy","Scikit-learn","HuggingFace"] },
  { name:"Tools",       keys:["Git","GitHub","Figma","Adobe","Canva","Postman","NPM","GraphQL","Twilio","Jira","Power BI","Cisco"] },
];

const VIBES = [
  { id:"builder",     label:"⚒️ Builder",        color:"#f59e0b" },
  { id:"researcher",  label:"🔬 Researcher",      color:"#6366f1" },
  { id:"hacker",      label:"🕶️ Hacker",          color:"#10b981" },
  { id:"designer",    label:"🎨 Designer",        color:"#ec4899" },
  { id:"open-source", label:"🌐 Open Sourcerer",  color:"#3b82f6" },
  { id:"learner",     label:"📚 Eternal Learner", color:"#f97316" },
];

const STAT_THEMES = ["tokyonight","radical","merko","gruvbox","onedark","cobalt","synthwave","dracula","prussian","monokai","shades-of-purple","nightowl","highcontrast","calm","vue-dark","buefy"];

const getTech = (label) => TECH_CATALOG.find(t => t.label === label);

function generateReadme({ name, username, title, bio, vibe, techs, twitter, linkedin, website, statsTheme, currentWork, funFact, showStreak, showTopLangs }) {
  const vibeLabel = VIBES.find(v => v.id === vibe)?.label || "";
  const safeUser = (username || "yourusername").replace(/[^a-zA-Z0-9_-]/g, "");

  const techBadges = techs.map(label => {
    const t = getTech(label);
    if (!t) return `![${label}](https://img.shields.io/badge/${encodeURIComponent(label)}-333?style=for-the-badge)`;
    const bg = t.color.replace("#", "");
    const logoColor = t.text.replace("#", "");
    return `![${t.label}](https://img.shields.io/badge/${encodeURIComponent(t.label)}-${bg}?style=for-the-badge&logo=${t.logo}&logoColor=${logoColor})`;
  }).join(" ");

  const socials = [
    website && `[![Portfolio](https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=vercel&logoColor=white)](${website})`,
    linkedin && `[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/${linkedin})`,
    twitter && `[![X](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/${twitter})`,
  ].filter(Boolean).join(" ");

  return [
    `<div align="center">`,
    ``,
    `# ${name || "Your Name"} ${vibeLabel}`,
    `### ${title || "Full Stack Developer · AI Enthusiast · Open Source Contributor"}`,
    ``,
    `<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&pause=1000&color=6366F1&center=true&vCenter=true&width=600&lines=${encodeURIComponent(bio || "Building things that matter.")}" alt="Typing SVG" />`,
    ``,
    socials,
    ``,
    `</div>`,
    ``,
    `---`,
    ``,
    `## 🧠 About Me`,
    ``,
    "```ts",
    `const ${safeUser} = {`,
    currentWork ? `  currentlyBuilding: "${currentWork}",` : null,
    `  alwaysLearning: true,`,
    `  openToCollaborate: true,`,
    funFact ? `  funFact: "${funFact}",` : null,
    `  contact: "${twitter ? `https://x.com/${twitter}` : `https://github.com/${safeUser}`}",`,
    `};`,
    "```",
    ``,
    techs.length > 0 ? `## 🛠️ Tech Stack` : null,
    techs.length > 0 ? `` : null,
    techs.length > 0 ? `<div align="center">` : null,
    techs.length > 0 ? `` : null,
    techs.length > 0 ? techBadges : null,
    techs.length > 0 ? `` : null,
    techs.length > 0 ? `</div>` : null,
    techs.length > 0 ? `` : null,
    `## 📊 GitHub Stats`,
    ``,
    `<div align="center">`,
    ``,
    `<img height="160" src="https://github-readme-stats.vercel.app/api?username=${safeUser}&show_icons=true&theme=${statsTheme}&hide_border=true&count_private=true" />`,
    showTopLangs ? `<img height="160" src="https://github-readme-stats.vercel.app/api/top-langs/?username=${safeUser}&layout=compact&theme=${statsTheme}&hide_border=true" />` : null,
    showStreak ? `<br/>` : null,
    showStreak ? `<img src="https://github-readme-streak-stats.herokuapp.com/?user=${safeUser}&theme=${statsTheme}&hide_border=true" />` : null,
    ``,
    `</div>`,
    ``,
    `---`,
    ``,
    `<div align="center">`,
    `<img src="https://komarev.com/ghpvc/?username=${safeUser}&style=flat-square&color=6366f1" alt="Profile views" />`,
    `</div>`,
  ].filter(l => l !== null).join("\n");
}

function Inp({ label, value, onChange, placeholder, rows }) {
  const s = { width:"100%", background:"rgba(255,255,255,0.05)", border:"1px solid rgba(255,255,255,0.1)", borderRadius:7, padding:"9px 12px", color:"#e2e8f0", fontSize:12, outline:"none", boxSizing:"border-box", fontFamily:"inherit", resize: rows ? "vertical" : "none" };
  return (
    <div style={{ marginBottom:12 }}>
      <div style={{ fontSize:9, fontWeight:700, letterSpacing:"0.12em", color:"#475569", textTransform:"uppercase", marginBottom:5 }}>{label}</div>
      {rows ? <textarea value={value} onChange={e=>onChange(e.target.value)} placeholder={placeholder} rows={rows} style={s}/> : <input value={value} onChange={e=>onChange(e.target.value)} placeholder={placeholder} style={s}/>}
    </div>
  );
}

function Sec({ title, children }) {
  return (
    <div style={{ marginBottom:24 }}>
      <div style={{ display:"flex", alignItems:"center", gap:8, marginBottom:12 }}>
        <div style={{ width:18, height:1, background:"linear-gradient(90deg,#6366f1,transparent)" }}/>
        <span style={{ fontSize:9, fontWeight:700, letterSpacing:"0.14em", color:"#6366f1", textTransform:"uppercase" }}>{title}</span>
      </div>
      {children}
    </div>
  );
}

export default function App() {
  const [name, setName] = useState("Erickson Kipkemoi");
  const [username, setUsername] = useState("Ericksonmutai");
  const [title, setTitle] = useState("Software Engineer · AI Builder · Web Dev");
  const [bio, setBio] = useState("Building exceptional digital experiences for the web, mobile & AI");
  const [vibe, setVibe] = useState("builder");
  const [techs, setTechs] = useState([
    "HTML5","Python","JavaScript","Go","TypeScript","Dart","AWS","Azure","Heroku",
    "Firebase","Vercel","Netlify","DigitalOcean","Node.js","Next.js","FastAPI","React",
    "WordPress","Vite","TailwindCSS","Flutter","Flask","NPM","React Router","LiveWire",
    "Express","MySQL","MongoDB","Prisma","Redis","Supabase","SQLite","MariaDB",
    "Adobe","Figma","Canva","NumPy","Pandas","TensorFlow","PyTorch",
    "GitHub","Git","Kubernetes","Twilio","Postman","Cisco","Power BI","Jira","Docker"
  ]);
  const [search, setSearch] = useState("");
  const [cat, setCat] = useState("Languages");
  const [twitter, setTwitter] = useState("mutaierickson");
  const [linkedin, setLinkedin] = useState("briankerio");
  const [website, setWebsite] = useState("https://briankerio.netlify.app");
  const [statsTheme, setStatsTheme] = useState("tokyonight");
  const [currentWork, setCurrentWork] = useState("An AI Powered Farming Solution");
  const [funFact, setFunFact] = useState("I learn by building, not reading");
  const [showStreak, setShowStreak] = useState(true);
  const [showTopLangs, setShowTopLangs] = useState(true);
  const [copied, setCopied] = useState(false);
  const [tab, setTab] = useState("edit");

  const readme = generateReadme({ name, username, title, bio, vibe, techs, twitter, linkedin, website, statsTheme, currentWork, funFact, showStreak, showTopLangs });

  const displayTechs = search
    ? TECH_CATALOG.filter(t => t.label.toLowerCase().includes(search.toLowerCase()))
    : TECH_CATALOG.filter(t => CATEGORIES.find(c => c.name === cat)?.keys.includes(t.label));

  function toggleTech(label) {
    setTechs(prev => prev.includes(label) ? prev.filter(x => x !== label) : [...prev, label]);
  }

  function copy() {
    navigator.clipboard.writeText(readme);
    setCopied(true);
    setTimeout(() => setCopied(false), 2000);
  }

  useEffect(() => {
    const s = document.createElement("style");
    s.textContent = `
      @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Syne:wght@400;600;700;800&display=swap');
      *{margin:0;padding:0;box-sizing:border-box;} body{background:#07090f;}
      ::-webkit-scrollbar{width:4px;height:4px;}
      ::-webkit-scrollbar-thumb{background:rgba(99,102,241,0.3);border-radius:2px;}
      input::placeholder,textarea::placeholder{color:rgba(148,163,184,0.3);}
      input:focus,textarea:focus{border-color:rgba(99,102,241,0.55)!important;}
      .tbtn:hover{border-color:rgba(99,102,241,0.4)!important;}
    `;
    document.head.appendChild(s);
    return () => document.head.removeChild(s);
  }, []);

  const panel = { background:"rgba(255,255,255,0.02)", border:"1px solid rgba(255,255,255,0.06)", borderRadius:12, padding:20, height:"100%", overflowY:"auto" };

  return (
    <div style={{ minHeight:"100vh", background:"#07090f", color:"#e2e8f0", fontFamily:"'Syne',sans-serif", padding:18 }}>
      {/* Header */}
      <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between", marginBottom:16, flexWrap:"wrap", gap:10 }}>
        <div style={{ display:"flex", alignItems:"center", gap:10 }}>
          <div style={{ width:4, height:26, background:"linear-gradient(180deg,#6366f1,#a855f7)", borderRadius:2 }}/>
          <span style={{ fontSize:18, fontWeight:800 }}>README<span style={{color:"#6366f1"}}>.forge</span></span>
          <span style={{ fontSize:9, color:"#1e293b", fontWeight:700, letterSpacing:"0.1em" }}>GITHUB PROFILE BUILDER</span>
        </div>
        <div style={{ display:"flex", background:"rgba(255,255,255,0.04)", border:"1px solid rgba(255,255,255,0.07)", borderRadius:8, padding:3, gap:2 }}>
          {["edit","preview"].map(t => (
            <button key={t} onClick={() => setTab(t)} style={{
              padding:"5px 16px", borderRadius:6, border:"none", cursor:"pointer",
              background: tab===t ? "#6366f1" : "transparent",
              color: tab===t ? "#fff" : "#475569",
              fontSize:10, fontWeight:700, letterSpacing:"0.08em", textTransform:"uppercase", transition:"all 0.18s",
            }}>{t}</button>
          ))}
        </div>
      </div>

      <div style={{ display:"grid", gridTemplateColumns: tab==="preview" ? "1fr" : "1fr 1fr", gap:14, height:"calc(100vh - 72px)" }}>
        {/* EDIT PANEL */}
        {tab === "edit" && (
          <div style={panel}>
            <Sec title="Identity">
              <Inp label="Full Name" value={name} onChange={setName} placeholder="Erickson Kipkemoi"/>
              <Inp label="GitHub Username" value={username} onChange={setUsername} placeholder="Ericksonmutai"/>
              <Inp label="Headline" value={title} onChange={setTitle} placeholder="Software Engineer · AI Builder"/>
              <Inp label="Animated Bio" value={bio} onChange={setBio} placeholder="Building things that matter…" rows={2}/>
            </Sec>

            <Sec title="Vibe">
              <div style={{ display:"flex", flexWrap:"wrap", gap:6 }}>
                {VIBES.map(v => (
                  <button key={v.id} onClick={() => setVibe(v.id)} style={{
                    padding:"5px 12px", borderRadius:6, border:`1.5px solid ${vibe===v.id ? v.color : "rgba(255,255,255,0.08)"}`,
                    background: vibe===v.id ? `${v.color}18` : "transparent",
                    color: vibe===v.id ? v.color : "#475569",
                    fontSize:11, fontWeight:600, cursor:"pointer", transition:"all 0.15s",
                  }}>{v.label}</button>
                ))}
              </div>
            </Sec>

            <Sec title="Tech Stack — click to toggle">
              {/* Selected preview */}
              <div style={{ display:"flex", flexWrap:"wrap", gap:5, padding:"10px", background:"rgba(0,0,0,0.35)", borderRadius:8, border:"1px solid rgba(255,255,255,0.05)", marginBottom:12, minHeight:40 }}>
                {techs.length === 0 && <span style={{color:"#1e293b",fontSize:11,alignSelf:"center"}}>No techs selected</span>}
                {techs.map(label => {
                  const t = getTech(label);
                  if (!t) return null;
                  return (
                    <span key={label} onClick={() => toggleTech(label)} title="Remove" style={{
                      display:"inline-flex", alignItems:"center", gap:4,
                      background: t.color, color: t.text,
                      borderRadius:4, padding:"2px 8px",
                      fontSize:10, fontWeight:800, letterSpacing:"0.05em",
                      cursor:"pointer", fontFamily:"'JetBrains Mono',monospace",
                      boxShadow:`0 0 6px ${t.color}66`,
                    }}>
                      {t.label} <span style={{opacity:0.55,fontSize:11,lineHeight:1}}>×</span>
                    </span>
                  );
                })}
              </div>

              {/* Search */}
              <input value={search} onChange={e => setSearch(e.target.value)} placeholder="🔍 Search technologies…"
                style={{ width:"100%", background:"rgba(255,255,255,0.05)", border:"1px solid rgba(255,255,255,0.09)", borderRadius:7, padding:"7px 11px", color:"#e2e8f0", fontSize:12, outline:"none", boxSizing:"border-box", marginBottom:9, fontFamily:"'Syne',sans-serif" }}
              />

              {/* Category tabs */}
              {!search && (
                <div style={{ display:"flex", flexWrap:"wrap", gap:4, marginBottom:10 }}>
                  {CATEGORIES.map(c => (
                    <button key={c.name} onClick={() => setCat(c.name)} style={{
                      padding:"3px 10px", borderRadius:5, border:`1px solid ${cat===c.name ? "#6366f1" : "rgba(255,255,255,0.07)"}`,
                      background: cat===c.name ? "rgba(99,102,241,0.15)" : "rgba(255,255,255,0.02)",
                      color: cat===c.name ? "#818cf8" : "#334155",
                      fontSize:9, fontWeight:700, cursor:"pointer", letterSpacing:"0.08em", textTransform:"uppercase",
                    }}>{c.name}</button>
                  ))}
                </div>
              )}

              {/* Tech grid — colorful badges just like the screenshot */}
              <div style={{ display:"flex", flexWrap:"wrap", gap:5 }}>
                {displayTechs.map(tech => {
                  const sel = techs.includes(tech.label);
                  return (
                    <span key={tech.label} onClick={() => toggleTech(tech.label)} className="tbtn" style={{
                      display:"inline-flex", alignItems:"center", gap:5,
                      background: sel ? tech.color : "rgba(255,255,255,0.03)",
                      color: sel ? tech.text : "#475569",
                      border: `1.5px solid ${sel ? tech.color : "rgba(255,255,255,0.08)"}`,
                      borderRadius:5, padding:"4px 11px",
                      fontSize:11, fontWeight:800, letterSpacing:"0.05em",
                      cursor:"pointer", transition:"all 0.14s",
                      fontFamily:"'JetBrains Mono',monospace",
                      boxShadow: sel ? `0 0 10px ${tech.color}55` : "none",
                    }}>
                      {sel && <span style={{fontSize:9}}>✓</span>}
                      {tech.label}
                    </span>
                  );
                })}
              </div>
            </Sec>

            <Sec title="Socials">
              <Inp label="Twitter / X handle" value={twitter} onChange={setTwitter} placeholder="mutaierickson"/>
              <Inp label="LinkedIn handle" value={linkedin} onChange={setLinkedin} placeholder="briankerio"/>
              <Inp label="Portfolio URL" value={website} onChange={setWebsite} placeholder="https://yoursite.com"/>
            </Sec>

            <Sec title="Content">
              <Inp label="Currently Building" value={currentWork} onChange={setCurrentWork} placeholder="An AI Powered Farming Solution"/>
              <Inp label="Fun Fact" value={funFact} onChange={setFunFact} placeholder="I debug with console.log and I'm proud"/>
            </Sec>

            <Sec title="GitHub Stats">
              <div style={{ fontSize:9, fontWeight:700, letterSpacing:"0.12em", color:"#475569", textTransform:"uppercase", marginBottom:8 }}>Theme</div>
              <div style={{ display:"flex", flexWrap:"wrap", gap:4, marginBottom:14 }}>
                {STAT_THEMES.map(t => (
                  <span key={t} onClick={() => setStatsTheme(t)} style={{
                    padding:"3px 9px", borderRadius:4, fontSize:10, fontWeight:700,
                    border:`1px solid ${statsTheme===t ? "#6366f1" : "rgba(255,255,255,0.07)"}`,
                    background: statsTheme===t ? "rgba(99,102,241,0.18)" : "rgba(255,255,255,0.02)",
                    color: statsTheme===t ? "#818cf8" : "#334155",
                    cursor:"pointer", fontFamily:"'JetBrains Mono',monospace", letterSpacing:"0.04em",
                  }}>{t}</span>
                ))}
              </div>
              <div style={{ display:"flex", gap:18 }}>
                {[["Streak",showStreak,setShowStreak],["Top Langs",showTopLangs,setShowTopLangs]].map(([lbl,val,set]) => (
                  <label key={lbl} style={{ display:"flex", alignItems:"center", gap:8, cursor:"pointer", fontSize:11, color:"#64748b" }}>
                    <div onClick={() => set(v=>!v)} style={{ width:32, height:17, borderRadius:9, background: val?"#6366f1":"rgba(255,255,255,0.09)", position:"relative", transition:"background 0.2s", flexShrink:0 }}>
                      <div style={{ position:"absolute", top:2, left: val?15:2, width:13, height:13, borderRadius:"50%", background:"white", transition:"left 0.2s" }}/>
                    </div>
                    {lbl}
                  </label>
                ))}
              </div>
            </Sec>
          </div>
        )}

        {/* OUTPUT PANEL */}
        <div style={panel}>
          <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between", marginBottom:12 }}>
            <div style={{ display:"flex", alignItems:"center", gap:10 }}>
              <span style={{ fontSize:9, fontWeight:700, letterSpacing:"0.12em", color:"#1e293b", textTransform:"uppercase" }}>📋 README.md</span>
              <span style={{ fontSize:9, color:"#1e293b" }}>{techs.length} techs</span>
            </div>
            <button onClick={copy} style={{
              padding:"6px 18px", borderRadius:7, border:"none",
              background: copied ? "rgba(16,185,129,0.15)" : "#6366f1",
              color: copied ? "#10b981" : "#fff",
              fontSize:10, fontWeight:700, cursor:"pointer", letterSpacing:"0.08em",
              transition:"all 0.2s", boxShadow: copied ? "none" : "0 0 16px rgba(99,102,241,0.4)",
            }}>{copied ? "✓ COPIED!" : "COPY README"}</button>
          </div>

          {/* Tech Stack visual preview */}
          {techs.length > 0 && (
            <div style={{ marginBottom:14, padding:14, background:"rgba(0,0,0,0.45)", borderRadius:10, border:"1px solid rgba(255,255,255,0.05)" }}>
              <div style={{ fontSize:9, fontWeight:700, letterSpacing:"0.12em", color:"#334155", textTransform:"uppercase", marginBottom:10 }}>🛠️ Tech Stack Preview (as it appears on GitHub)</div>
              <div style={{ display:"flex", flexWrap:"wrap", gap:6 }}>
                {techs.map(label => {
                  const t = getTech(label);
                  if (!t) return null;
                  return (
                    <span key={label} style={{
                      display:"inline-flex", alignItems:"center", gap:5,
                      background: t.color, color: t.text,
                      borderRadius:5, padding:"5px 12px",
                      fontSize:11, fontWeight:800, letterSpacing:"0.06em",
                      fontFamily:"'JetBrains Mono',monospace",
                      boxShadow:`0 1px 6px ${t.color}55`,
                    }}>
                      {t.label}
                    </span>
                  );
                })}
              </div>
            </div>
          )}

          <pre style={{
            background:"rgba(0,0,0,0.55)", border:"1px solid rgba(255,255,255,0.04)",
            borderRadius:10, padding:16, fontSize:10.5, lineHeight:1.8,
            fontFamily:"'JetBrains Mono',monospace", color:"#475569",
            overflowX:"auto", whiteSpace:"pre-wrap", wordBreak:"break-all",
          }}>{readme}</pre>

          <div style={{ marginTop:12, padding:13, background:"rgba(99,102,241,0.05)", border:"1px solid rgba(99,102,241,0.12)", borderRadius:9 }}>
            <p style={{ fontSize:10, color:"#6366f1", fontWeight:700, marginBottom:6 }}>📌 How to use</p>
            <ol style={{ paddingLeft:15, color:"#334155", fontSize:10, lineHeight:2.4 }}>
              <li>Copy the markdown above</li>
              <li>On GitHub, create a repo named <code style={{ background:"rgba(255,255,255,0.07)", padding:"1px 5px", borderRadius:3, color:"#818cf8" }}>{username||"yourusername"}</code> (same as your username)</li>
              <li>Create <code style={{ background:"rgba(255,255,255,0.07)", padding:"1px 5px", borderRadius:3, color:"#818cf8" }}>README.md</code> and paste the content</li>
              <li>Commit → profile is now 🔥</li>
            </ol>
          </div>
        </div>
      </div>
    </div>
  );
}
