# Reaktorimport React, { useState, useEffect, useRef } from "react";
import {
  Twitter,
  Linkedin,
  Instagram,
  Youtube,
  FileText,
  Upload,
  Link2,
  Sparkles,
  Copy,
  Check,
  ArrowRight,
  Mic,
  Video,
  FileAudio,
  ChevronRight,
  Zap,
  RefreshCw,
  Clock,
  ShieldCheck,
} from "lucide-react";

// ---------------------------------------------------------------------------
// DESIGN TOKENS
// ---------------------------------------------------------------------------
const COLORS = {
  bg: "#0B0E14",
  surface: "#141826",
  surfaceHover: "#1A1F30",
  border: "#242B3D",
  text: "#EDEAE3",
  textMuted: "#8C92A4",
  coral: "#FF6B4A",
  coralDim: "#FF6B4A20",
  gold: "#D4A857",
  green: "#4ADE80",
};

const PLATFORMS = [
  { key: "twitter", label: "X Thread", icon: Twitter, color: "#EDEAE3" },
  { key: "linkedin", label: "LinkedIn", icon: Linkedin, color: "#4F9DDE" },
  { key: "instagram", label: "Instagram", icon: Instagram, color: "#E1639B" },
  { key: "shorts", label: "YT Shorts", icon: Youtube, color: "#FF6B4A" },
  { key: "blog", label: "Blog SEO", icon: FileText, color: "#D4A857" },
];

// ---------------------------------------------------------------------------
// SHARED UI
// ---------------------------------------------------------------------------
function Logo({ size = 22 }) {
  return (
    <div className="flex items-center gap-2.5 select-none">
      <div
        className="relative flex items-center justify-center rounded-md"
        style={{
          width: size + 14,
          height: size + 14,
          background: `linear-gradient(135deg, ${COLORS.coral}, #C2452E)`,
        }}
      >
        <Zap size={size * 0.62} color="#0B0E14" strokeWidth={2.6} fill="#0B0E14" />
      </div>
      <span
        className="font-semibold tracking-tight"
        style={{ fontFamily: "Fraunces, serif", fontSize: size * 0.95, color: COLORS.text }}
      >
        Reaktor
      </span>
    </div>
  );
}

function PillButton({ children, onClick, variant = "primary", className = "", icon: Icon, ...props }) {
  const base =
    "inline-flex items-center justify-center gap-2 rounded-full font-medium transition-all duration-200 px-5 py-2.5 text-[14px] focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2";
  const styles = {
    primary: { background: COLORS.coral, color: "#0B0E14" },
    ghost: { background: "transparent", color: COLORS.text, border: `1px solid ${COLORS.border}` },
    subtle: { background: COLORS.surface, color: COLORS.text, border: `1px solid ${COLORS.border}` },
  };
  return (
    <button
      onClick={onClick}
      className={`${base} ${className} hover:brightness-110 active:scale-[0.98]`}
      style={{ ...styles[variant], outlineColor: COLORS.coral }}
      {...props}
    >
      {Icon && <Icon size={16} />}
      {children}
    </button>
  );
}

// ---------------------------------------------------------------------------
// LANDING: NAV
// ---------------------------------------------------------------------------
function Nav({ onLaunch }) {
  return (
    <header className="sticky top-0 z-50 backdrop-blur-md" style={{ background: "#0B0E14CC", borderBottom: `1px solid ${COLORS.border}` }}>
      <div className="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
        <Logo />
        <nav className="hidden md:flex items-center gap-8 text-[14px]" style={{ color: COLORS.textMuted }}>
          <a href="#how" className="hover:text-white transition-colors">How it works</a>
          <a href="#platforms" className="hover:text-white transition-colors">Platforms</a>
          <a href="#pricing" className="hover:text-white transition-colors">Pricing</a>
        </nav>
        <div className="flex items-center gap-3">
          <button className="hidden sm:block text-[14px] hover:text-white transition-colors" style={{ color: COLORS.textMuted }}>
            Log in
          </button>
          <PillButton onClick={onLaunch}>Try the dashboard</PillButton>
        </div>
      </div>
    </header>
  );
}

// ---------------------------------------------------------------------------
// LANDING: HERO — signature element (content splitting into platforms)
// ---------------------------------------------------------------------------
function Hero({ onLaunch }) {
  const [activeIdx, setActiveIdx] = useState(0);
  useEffect(() => {
    const id = setInterval(() => setActiveIdx((i) => (i + 1) % PLATFORMS.length), 1800);
    return () => clearInterval(id);
  }, []);

  return (
    <section className="relative overflow-hidden">
      <div
        className="absolute inset-0 pointer-events-none"
        style={{
          background: `radial-gradient(60% 50% at 50% 0%, ${COLORS.coral}14 0%, transparent 70%)`,
        }}
      />
      <div className="max-w-6xl mx-auto px-6 pt-20 pb-28 relative">
        <div className="max-w-2xl">
          <div
            className="inline-flex items-center gap-2 rounded-full px-3 py-1.5 mb-7 text-[13px]"
            style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}`, color: COLORS.gold }}
          >
            <Sparkles size={13} />
            Built for creators who publish everywhere
          </div>
          <h1
            className="text-[44px] sm:text-[58px] leading-[1.05] tracking-tight mb-6"
            style={{ fontFamily: "Fraunces, serif", color: COLORS.text }}
          >
            Record once.
            <br />
            <span style={{ color: COLORS.coral }}>Publish everywhere</span> by lunch.
          </h1>
          <p className="text-[18px] leading-relaxed mb-9 max-w-lg" style={{ color: COLORS.textMuted }}>
            Drop in a video, podcast, or blog post. Reaktor's own transcription and writing
            engines turn it into a thread, a LinkedIn post, captions, and a script — in your voice,
            without waiting on anyone else's servers to stay up.
          </p>
          <div className="flex flex-wrap items-center gap-4">
            <PillButton onClick={onLaunch} icon={ArrowRight} className="!px-6 !py-3 !text-[15px]">
              Repurpose your first piece
            </PillButton>
            <span className="text-[13px]" style={{ color: COLORS.textMuted }}>
              No card required · 3 free conversions
            </span>
          </div>
        </div>

        {/* Signature element: source -> platform branches */}
        <div className="mt-20 relative">
          <div className="flex flex-col lg:flex-row items-center gap-8 lg:gap-0">
            {/* Source node */}
            <div
              className="relative z-10 w-full lg:w-[280px] shrink-0 rounded-2xl p-5"
              style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}` }}
            >
              <div className="flex items-center gap-2 mb-3 text-[12px] uppercase tracking-wider" style={{ color: COLORS.textMuted, fontFamily: "JetBrains Mono, monospace" }}>
                <Video size={13} />
                Source · 14:32
              </div>
              <div className="text-[14px] leading-relaxed mb-4" style={{ color: COLORS.text }}>
                "...the real reason most creators burn out isn't content, it's the repurposing
                tax they pay on every single post..."
              </div>
              <div className="h-1.5 rounded-full overflow-hidden" style={{ background: COLORS.border }}>
                <div className="h-full rounded-full" style={{ width: "62%", background: COLORS.coral }} />
              </div>
            </div>

            {/* Connector */}
            <div className="hidden lg:flex flex-1 items-center justify-center px-2 relative h-[1px]">
              <svg width="100%" height="120" className="overflow-visible">
                {PLATFORMS.map((p, i) => {
                  const yTarget = (i - 2) * 44;
                  const active = i === activeIdx;
                  return (
                    <path
                      key={p.key}
                      d={`M 0 0 C 60 0, 60 ${yTarget}, 130 ${yTarget}`}
                      fill="none"
                      stroke={active ? COLORS.coral : COLORS.border}
                      strokeWidth={active ? 2 : 1}
                      style={{ transition: "stroke 0.4s, stroke-width 0.4s" }}
                    />
                  );
                })}
              </svg>
            </div>

            {/* Platform outputs */}
            <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-1 gap-3 w-full lg:w-[200px]">
              {PLATFORMS.map((p, i) => {
                const Icon = p.icon;
                const active = i === activeIdx;
                return (
                  <div
                    key={p.key}
                    className="rounded-xl px-4 py-3 flex items-center gap-2.5 transition-all duration-300"
                    style={{
                      background: active ? COLORS.coralDim : COLORS.surface,
                      border: `1px solid ${active ? COLORS.coral : COLORS.border}`,
                      transform: active ? "translateX(6px)" : "none",
                    }}
                  >
                    <Icon size={15} color={active ? COLORS.coral : COLORS.textMuted} />
                    <span className="text-[13px]" style={{ color: active ? COLORS.text : COLORS.textMuted, fontFamily: "JetBrains Mono, monospace" }}>
                      {p.label}
                    </span>
                  </div>
                );
              })}
            </div>
          </div>
        </div>
      </div>
    </section>
  );
}

// ---------------------------------------------------------------------------
// LANDING: RELIABILITY STRIP — the "won't flop because of third parties" pitch
// ---------------------------------------------------------------------------
function ReliabilityStrip() {
  const items = [
    { icon: ShieldCheck, title: "Self-hosted transcription", body: "Audio-to-text runs on infrastructure we own. No outside API to wait on." },
    { icon: RefreshCw, title: "Multi-model failover", body: "If one writing model slows down, your job switches to a backup automatically." },
    { icon: Clock, title: "99.9% generation uptime", body: "Tracked publicly. Outages are rare, and your drafts are never lost mid-job." },
  ];
  return (
    <section className="py-16" style={{ borderTop: `1px solid ${COLORS.border}`, borderBottom: `1px solid ${COLORS.border}`, background: COLORS.surface }}>
      <div className="max-w-6xl mx-auto px-6 grid sm:grid-cols-3 gap-10">
        {items.map((it, i) => {
          const Icon = it.icon;
          return (
            <div key={i} className="flex gap-4">
              <div className="shrink-0 w-10 h-10 rounded-lg flex items-center justify-center" style={{ background: COLORS.coralDim }}>
                <Icon size={18} color={COLORS.coral} />
              </div>
              <div>
                <div className="text-[15px] font-medium mb-1" style={{ color: COLORS.text }}>{it.title}</div>
                <div className="text-[13.5px] leading-relaxed" style={{ color: COLORS.textMuted }}>{it.body}</div>
              </div>
            </div>
          );
        })}
      </div>
    </section>
  );
}

// ---------------------------------------------------------------------------
// LANDING: HOW IT WORKS
// ---------------------------------------------------------------------------
function HowItWorks() {
  const steps = [
    { label: "Drop in your content", body: "Paste a YouTube link, upload audio, or paste a blog draft.", icon: Upload },
    { label: "Pick your platforms", body: "Choose where you publish. Reaktor matches tone and format to each.", icon: Sparkles },
    { label: "Edit and ship", body: "Every draft is editable inline. Copy, schedule, or export in one tap.", icon: Copy },
  ];
  return (
    <section id="how" className="py-28">
      <div className="max-w-6xl mx-auto px-6">
        <div className="mb-16 max-w-lg">
          <div className="text-[13px] uppercase tracking-wider mb-3" style={{ color: COLORS.gold, fontFamily: "JetBrains Mono, monospace" }}>
            How it works
          </div>
          <h2 className="text-[34px] leading-tight" style={{ fontFamily: "Fraunces, serif", color: COLORS.text }}>
            Three steps between you and a week of posts
          </h2>
        </div>
        <div className="grid md:grid-cols-3 gap-px rounded-2xl overflow-hidden" style={{ background: COLORS.border }}>
          {steps.map((s, i) => {
            const Icon = s.icon;
            return (
              <div key={i} className="p-8" style={{ background: COLORS.bg }}>
                <div className="flex items-center justify-between mb-8">
                  <Icon size={22} color={COLORS.coral} />
                  <span className="text-[13px]" style={{ color: COLORS.textMuted, fontFamily: "JetBrains Mono, monospace" }}>
                    0{i + 1}
                  </span>
                </div>
                <div className="text-[17px] font-medium mb-2" style={{ color: COLORS.text }}>{s.label}</div>
                <div className="text-[14px] leading-relaxed" style={{ color: COLORS.textMuted }}>{s.body}</div>
              </div>
            );
          })}
        </div>
      </div>
    </section>
  );
}

// ---------------------------------------------------------------------------
// LANDING: FOOTER CTA
// ---------------------------------------------------------------------------
function FooterCTA({ onLaunch }) {
  return (
    <section className="py-28 text-center px-6" style={{ borderTop: `1px solid ${COLORS.border}` }}>
      <h2 className="text-[36px] sm:text-[44px] leading-tight mb-6 max-w-2xl mx-auto" style={{ fontFamily: "Fraunces, serif", color: COLORS.text }}>
        Stop retyping the same idea five times.
      </h2>
      <PillButton onClick={onLaunch} icon={ArrowRight} className="!px-7 !py-3.5 !text-[15px] mx-auto">
        Open the dashboard
      </PillButton>
    </section>
  );
}

function LandingPage({ onLaunch }) {
  return (
    <div style={{ background: COLORS.bg, minHeight: "100vh" }}>
      <Nav onLaunch={onLaunch} />
      <Hero onLaunch={onLaunch} />
      <ReliabilityStrip />
      <HowItWorks />
      <FooterCTA onLaunch={onLaunch} />
      <footer className="py-8 text-center text-[13px]" style={{ color: COLORS.textMuted, borderTop: `1px solid ${COLORS.border}` }}>
        © 2026 Reaktor. Built for creators, not algorithms.
      </footer>
    </div>
  );
}

// ---------------------------------------------------------------------------
// DASHBOARD
// ---------------------------------------------------------------------------
const SAMPLE_OUTPUTS = {
  twitter: `1/ Most creators don't have a content problem. They have a repurposing problem.

2/ You spend 3 hours on a video. Then 2 more hours turning it into a thread, a caption, a post. The second part is where people quit.

3/ The fix isn't "post less." It's separating the thinking from the formatting.`,
  linkedin: `Most creators don't burn out from making content.

They burn out from the repurposing tax that comes after.

One video becomes a thread, a caption, a LinkedIn post, a script — and each one needs its own tone, length, and hook.

That's not creative work. That's overhead.

The creators who last separate the two: think once, format many times.`,
  instagram: `the real burnout isn't content.
it's everything you have to do AFTER you hit record. 🎬

swipe for the 3-step fix →`,
  shorts: `[HOOK - 0:00]
"You don't have a content problem."

[BEAT - 0:03]
"You have a repurposing problem."

[PAYOFF - 0:08]
Show the same idea reformatted 4 ways in 4 seconds, fast cuts.

[CTA - 0:14]
"Stop retyping. Link in bio."`,
  blog: `# Why Creator Burnout Is Really a Repurposing Problem

Most creators assume burnout comes from running out of ideas. It rarely does. What actually drains creators is the hidden "repurposing tax" — the hours spent reformatting one idea for five different platforms...

[Continue reading — 640 words, SEO-optimized for "creator burnout"]`,
};

function UploadPanel({ onGenerate, isGenerating }) {
  const [mode, setMode] = useState("link");
  const [val, setVal] = useState("");
  const tabs = [
    { key: "link", label: "Paste a link", icon: Link2 },
    { key: "upload", label: "Upload file", icon: Upload },
    { key: "text", label: "Paste text", icon: FileText },
  ];
  return (
    <div className="rounded-2xl p-6" style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}` }}>
      <div className="flex items-center gap-1 mb-5 p-1 rounded-lg w-fit" style={{ background: COLORS.bg }}>
        {tabs.map((t) => {
          const Icon = t.icon;
          const active = mode === t.key;
          return (
            <button
              key={t.key}
              onClick={() => setMode(t.key)}
              className="flex items-center gap-1.5 px-3.5 py-1.5 rounded-md text-[13px] transition-colors"
              style={{ background: active ? COLORS.surface : "transparent", color: active ? COLORS.text : COLORS.textMuted }}
            >
              <Icon size={13} />
              {t.label}
            </button>
          );
        })}
      </div>

      {mode === "upload" ? (
        <div
          className="rounded-xl flex flex-col items-center justify-center py-12 text-center cursor-pointer transition-colors"
          style={{ border: `1.5px dashed ${COLORS.border}` }}
          onClick={() => setVal("creator-podcast-ep12.mp3")}
        >
          <FileAudio size={26} color={COLORS.textMuted} className="mb-3" />
          <div className="text-[14px] mb-1" style={{ color: COLORS.text }}>
            {val || "Drop audio, video, or transcript here"}
          </div>
          <div className="text-[12.5px]" style={{ color: COLORS.textMuted }}>MP3, MP4, MOV, TXT — up to 2 hours</div>
        </div>
      ) : (
        <textarea
          value={val}
          onChange={(e) => setVal(e.target.value)}
          placeholder={mode === "link" ? "https://youtube.com/watch?v=..." : "Paste your blog post, script, or notes..."}
          rows={mode === "link" ? 2 : 6}
          className="w-full rounded-xl p-4 text-[14px] resize-none focus:outline-none"
          style={{ background: COLORS.bg, border: `1px solid ${COLORS.border}`, color: COLORS.text }}
        />
      )}

      <div className="flex items-center justify-between mt-5">
        <div className="flex items-center gap-1.5 text-[12.5px]" style={{ color: COLORS.textMuted }}>
          <Mic size={13} />
          Transcription runs on our own engine
        </div>
        <PillButton
          icon={isGenerating ? undefined : Sparkles}
          onClick={() => onGenerate(val || "creator-podcast-ep12.mp3")}
          disabled={isGenerating}
        >
          {isGenerating ? "Generating..." : "Repurpose this"}
        </PillButton>
      </div>
    </div>
  );
}

function PlatformTabs({ selected, onSelect, completedKeys }) {
  return (
    <div className="flex flex-wrap gap-2">
      {PLATFORMS.map((p) => {
        const Icon = p.icon;
        const active = selected === p.key;
        const done = completedKeys.includes(p.key);
        return (
          <button
            key={p.key}
            onClick={() => onSelect(p.key)}
            className="flex items-center gap-2 px-4 py-2.5 rounded-xl text-[13.5px] transition-all"
            style={{
              background: active ? COLORS.coralDim : COLORS.surface,
              border: `1px solid ${active ? COLORS.coral : COLORS.border}`,
              color: active ? COLORS.text : COLORS.textMuted,
              opacity: done ? 1 : 0.5,
            }}
          >
            <Icon size={14} color={active ? COLORS.coral : COLORS.textMuted} />
            {p.label}
            {done && <Check size={12} color={COLORS.green} />}
          </button>
        );
      })}
    </div>
  );
}

function OutputCard({ platformKey }) {
  const [copied, setCopied] = useState(false);
  const platform = PLATFORMS.find((p) => p.key === platformKey);
  const content = SAMPLE_OUTPUTS[platformKey];
  const Icon = platform.icon;

  const handleCopy = () => {
    setCopied(true);
    setTimeout(() => setCopied(false), 1600);
  };

  return (
    <div className="rounded-2xl p-6" style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}` }}>
      <div className="flex items-center justify-between mb-4">
        <div className="flex items-center gap-2">
          <Icon size={16} color={platform.color} />
          <span className="text-[13.5px] font-medium" style={{ color: COLORS.text }}>{platform.label}</span>
        </div>
        <button
          onClick={handleCopy}
          className="flex items-center gap-1.5 text-[12.5px] px-3 py-1.5 rounded-full transition-colors"
          style={{ background: COLORS.bg, color: copied ? COLORS.green : COLORS.textMuted, border: `1px solid ${COLORS.border}` }}
        >
          {copied ? <Check size={12} /> : <Copy size={12} />}
          {copied ? "Copied" : "Copy"}
        </button>
      </div>
      <textarea
        defaultValue={content}
        rows={platformKey === "blog" ? 7 : 6}
        className="w-full bg-transparent resize-none focus:outline-none text-[14px] leading-relaxed"
        style={{ color: COLORS.text, fontFamily: platformKey === "shorts" ? "JetBrains Mono, monospace" : "inherit" }}
      />
    </div>
  );
}

function Dashboard({ onBack }) {
  const [isGenerating, setIsGenerating] = useState(false);
  const [completedKeys, setCompletedKeys] = useState([]);
  const [selected, setSelected] = useState("twitter");
  const [hasGenerated, setHasGenerated] = useState(false);

  const handleGenerate = () => {
    setIsGenerating(true);
    setCompletedKeys([]);
    setHasGenerated(false);
    let i = 0;
    const order = PLATFORMS.map((p) => p.key);
    const interval = setInterval(() => {
      i += 1;
      setCompletedKeys(order.slice(0, i));
      if (i >= order.length) {
        clearInterval(interval);
        setIsGenerating(false);
        setHasGenerated(true);
        setSelected("twitter");
      }
    }, 420);
  };

  return (
    <div style={{ background: COLORS.bg, minHeight: "100vh" }}>
      <header className="sticky top-0 z-50" style={{ background: "#0B0E14EE", borderBottom: `1px solid ${COLORS.border}`, backdropFilter: "blur(8px)" }}>
        <div className="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">
          <button onClick={onBack}>
            <Logo size={20} />
          </button>
          <div className="flex items-center gap-3">
            <div className="hidden sm:flex items-center gap-1.5 text-[12.5px] px-3 py-1.5 rounded-full" style={{ background: COLORS.surface, color: COLORS.gold, border: `1px solid ${COLORS.border}` }}>
              <Sparkles size={12} />
              2 of 3 free conversions left
            </div>
            <PillButton variant="ghost">Upgrade</PillButton>
          </div>
        </div>
      </header>

      <main className="max-w-6xl mx-auto px-6 py-12">
        <div className="mb-8">
          <h1 className="text-[26px] mb-1.5" style={{ fontFamily: "Fraunces, serif", color: COLORS.text }}>
            New repurpose
          </h1>
          <p className="text-[14px]" style={{ color: COLORS.textMuted }}>
            Drop in content once. Get every format back in under a minute.
          </p>
        </div>

        <div className="grid lg:grid-cols-[380px_1fr] gap-8">
          <div className="space-y-5">
            <UploadPanel onGenerate={handleGenerate} isGenerating={isGenerating} />

            {(isGenerating || hasGenerated) && (
              <div className="rounded-2xl p-5" style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}` }}>
                <div className="text-[12.5px] uppercase tracking-wider mb-4" style={{ color: COLORS.textMuted, fontFamily: "JetBrains Mono, monospace" }}>
                  Generation status
                </div>
                <div className="space-y-3">
                  {PLATFORMS.map((p) => {
                    const done = completedKeys.includes(p.key);
                    const Icon = p.icon;
                    return (
                      <div key={p.key} className="flex items-center gap-3">
                        <div
                          className="w-6 h-6 rounded-full flex items-center justify-center shrink-0"
                          style={{ background: done ? COLORS.green + "20" : COLORS.bg, border: `1px solid ${done ? COLORS.green : COLORS.border}` }}
                        >
                          {done ? <Check size={12} color={COLORS.green} /> : <Icon size={11} color={COLORS.textMuted} />}
                        </div>
                        <span className="text-[13px]" style={{ color: done ? COLORS.text : COLORS.textMuted }}>
                          {p.label}
                        </span>
                      </div>
                    );
                  })}
                </div>
              </div>
            )}
          </div>

          <div>
            {!hasGenerated && !isGenerating ? (
              <div
                className="rounded-2xl h-full min-h-[400px] flex flex-col items-center justify-center text-center p-12"
                style={{ background: COLORS.surface, border: `1px dashed ${COLORS.border}` }}
              >
                <div className="w-12 h-12 rounded-xl flex items-center justify-center mb-5" style={{ background: COLORS.coralDim }}>
                  <Sparkles size={20} color={COLORS.coral} />
                </div>
                <div className="text-[16px] mb-2" style={{ color: COLORS.text }}>Your formats will land here</div>
                <div className="text-[13.5px] max-w-xs" style={{ color: COLORS.textMuted }}>
                  Add a link, file, or text on the left and hit Repurpose to see drafts for every platform.
                </div>
              </div>
            ) : (
              <div className="space-y-5">
                <PlatformTabs selected={selected} onSelect={setSelected} completedKeys={completedKeys} />
                {completedKeys.includes(selected) ? (
                  <OutputCard platformKey={selected} />
                ) : (
                  <div className="rounded-2xl h-[280px] flex items-center justify-center" style={{ background: COLORS.surface, border: `1px solid ${COLORS.border}` }}>
                    <div className="flex items-center gap-2 text-[13.5px]" style={{ color: COLORS.textMuted }}>
                      <div className="w-3.5 h-3.5 rounded-full border-2 animate-spin" style={{ borderColor: COLORS.border, borderTopColor: COLORS.coral }} />
                      Writing this one now...
                    </div>
                  </div>
                )}
              </div>
            )}
          </div>
        </div>
      </main>
    </div>
  );
}

// ---------------------------------------------------------------------------
// ROOT
// ---------------------------------------------------------------------------
export default function App() {
  const [view, setView] = useState("landing");

  return (
    <div style={{ fontFamily: "Inter, sans-serif" }}>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
        * { box-sizing: border-box; }
        body { margin: 0; }
        textarea::placeholder { color: #8C92A4; }
        button { cursor: pointer; font-family: inherit; }
      `}</style>
      {view === "landing" ? (
        <LandingPage onLaunch={() => setView("dashboard")} />
      ) : (
        <Dashboard onBack={() => setView("landing")} />
      )}
    </div>
  );
}
