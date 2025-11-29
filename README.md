import React, { useState } from "react";
import { PieChart, Pie, Cell, Tooltip, ResponsiveContainer, BarChart, Bar, XAxis, YAxis } from "recharts";
import { motion } from "framer-motion";

// === Dipta's Interactive README Preview ===
// Default data lives below — replace with your real GitHub stats.
// Features:
// - Animated header and sections (Framer Motion)
// - Language usage pie chart (Recharts)
// - Contribution heatmap grid with animation
// - Repos table with animated rows
// - Export button to download README.md generated from the content

const languageDataDefault = [
  { name: "Python", value: 42 },
  { name: "C++", value: 28 },
  { name: "C", value: 15 },
  { name: "JavaScript", value: 10 },
  { name: "Other", value: 5 },
];

const contributionsDefault = Array.from({ length: 90 }).map((_, i) => ({
  day: i + 1,
  count: Math.floor(Math.random() * 6),
}));

const reposDefault = [
  { name: "Salinity-Sentinel", desc: "Smart Soil Monitoring System", stars: 42, lang: "Python" },
  { name: "Offline-Game", desc: "Personal hobby offline game", stars: 18, lang: "C++" },
  { name: "Net-Analyzer", desc: "Network packet analyzer (WIP)", stars: 7, lang: "C" },
];

const COLORS = ["#FF6B6B", "#FFD93D", "#6BCB77", "#4D96FF", "#845EC2"];

export default function DiptaReadmePreview() {
  const [langData, setLangData] = useState(languageDataDefault);
  const [contribs, setContribs] = useState(contributionsDefault);
  const [repos] = useState(reposDefault);

  function generateMarkdown() {
    // Build a clean markdown README from the current state
    const header = `# Hi, I'm Dipta 👾\nAI/ML & Cybersecurity Enthusiast | CSE Student\n\n`;

    const about = `### 🧬 About Me\n- Studying CSE (B.Tech)\n- Interested in cybersecurity, AI/ML, systems\n- Love building tools and solving problems\n\n`;

    const skills = `### 🛠️ Skills\n- Languages: ${langData.map((l) => l.name).join(", ")}\n- Tools: Git, VS Code\n- Domains: Cybersecurity, Machine Learning, Algorithms\n\n`;

    const projects = `### 🔥 Current Project\n- Salinity-Sentinel — A Smart Soil Monitoring System for Coastal Bangladesh\n- Offline game development (personal hobby project)\n\n`;

    const future = `### 🚀 Future Projects\n- IoT-based security system\n- Network packet analyzer\n- AI-based phishing detector\n- OSINT automation tool\n\n`;

    const contact = `### 📩 Contact\n- Email: yourmail@example.com\n- LinkedIn: your-profile\n\n`;

    const langSection = `---\n\n### 📊 Language usage (approx)\n${langData
      .map((l) => `- ${l.name}: ${l.value}%`)
      .join("\n")}\n\n`;

    const contribSection = `---\n\n### 📈 Contributions (recent 90 days sample)\nSee the contribution graph on my profile for full history.\n\n`;

    const tableHeader = `---\n\n### 📋 Repositories snapshot\n\n| Repo | Description | Stars | Main Language |\n|---|---|---:|---|\n`;

    const tableRows = repos.map((r) => `| ${r.name} | ${r.desc} | ${r.stars} | ${r.lang} |`).join("\n");

    return header + about + skills + projects + future + contact + langSection + contribSection + tableHeader + tableRows + "\n";
  }

  function downloadReadme() {
    const md = generateMarkdown();
    const blob = new Blob([md], { type: "text/markdown" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = "README.md";
    a.click();
    URL.revokeObjectURL(url);
  }

  return (
    <div className="p-6 max-w-4xl mx-auto font-sans">
      <motion.header
        initial={{ y: -40, opacity: 0 }}
        animate={{ y: 0, opacity: 1 }}
        transition={{ duration: 0.6 }}
        className="mb-6"
      >
        <div className="flex items-center gap-4">
          <div className="w-20 h-20 rounded-2xl bg-gradient-to-br from-purple-500 via-pink-500 to-yellow-400 flex items-center justify-center text-white text-2xl font-bold shadow-2xl">
            DD
          </div>
          <div>
            <h1 className="text-3xl font-extrabold">Hi, I'm Dipta <span className="animate-pulse">👾</span></h1>
            <p className="text-sm mt-1">AI/ML & Cybersecurity Enthusiast | CSE Student</p>
          </div>
        </div>
      </motion.header>

      <motion.section
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ delay: 0.2 }}
        className="grid grid-cols-1 md:grid-cols-3 gap-6"
      >
        <div className="md:col-span-2 bg-white/30 p-4 rounded-2xl shadow-lg">
          <h2 className="text-xl font-semibold mb-3">🧬 About Me</h2>
          <p>Studying CSE (B.Tech)</p>
          <p>Interested in cybersecurity, AI/ML, systems</p>
          <p>Love building tools and solving problems</p>

          <div className="mt-6">
            <h3 className="font-semibold">🔥 Current Project</h3>
            <ul className="list-disc list-inside">
              <li>Salinity-Sentinel — A Smart Soil Monitoring System for Coastal Bangladesh</li>
              <li>Offline game development (personal hobby project)</li>
            </ul>
          </div>

          <div className="mt-4">
            <h3 className="font-semibold">🚀 Future Projects</h3>
            <ul className="list-disc list-inside">
              <li>IoT-based security system</li>
              <li>Network packet analyzer</li>
              <li>AI-based phishing detector</li>
              <li>OSINT automation tool</li>
            </ul>
          </div>

          <div className="mt-4 flex gap-3">
            <button onClick={downloadReadme} className="px-4 py-2 rounded-lg shadow-md bg-gradient-to-r from-blue-500 to-purple-600 text-white font-semibold">
              Export README.md
            </button>
            <button
              onClick={() => setContribs(contributionsDefault.map(c => ({...c, count: Math.floor(Math.random()*6)})))}
              className="px-4 py-2 rounded-lg shadow-md bg-white/20 border border-white/30 text-white font-medium"
            >
              Randomize sample contributions
            </button>
          </div>
        </div>

        <div className="bg-white/10 p-4 rounded-2xl shadow-lg">
          <h3 className="font-semibold mb-2">📩 Contact</h3>
          <p>Email: yourmail@example.com</p>
          <p>LinkedIn: your-profile</p>

          <div className="mt-4">
            <h3 className="font-semibold mb-2">📊 Language Usage</h3>
            <div style={{ width: "100%", height: 200 }}>
              <ResponsiveContainer width="100%" height={200}>
                <PieChart>
                  <Pie data={langData} dataKey="value" nameKey="name" outerRadius={60} label>
                    {langData.map((entry, index) => (
                      <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                    ))}
                  </Pie>
                  <Tooltip />
                </PieChart>
              </ResponsiveContainer>
            </div>

            <div className="mt-2 text-xs opacity-80">
              Percentages show rough distribution of languages used across your public repos.
            </div>
          </div>
        </div>
      </motion.section>

      <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.4 }} className="mt-6">
        <h2 className="text-xl font-semibold mb-3">📈 Contribution heatmap (last 90 days)</h2>
        <div className="w-full bg-white/5 p-4 rounded-xl">
          <div className="grid grid-cols-18 gap-1">
            {contribs.map((c, i) => {
              const colorIndex = Math.min(c.count, 4);
              const shades = ["#ebedf0", "#c6e48b", "#7bc96f", "#239a3b", "#196127"];
              return (
                <motion.div
                  key={i}
                  initial={{ opacity: 0, scale: 0.6 }}
                  animate={{ opacity: 1, scale: 1 }}
                  transition={{ delay: i * 0.01 }}
                  title={`Day ${c.day}: ${c.count} contributions`}
                  className="w-6 h-6 rounded-sm"
                  style={{ background: shades[colorIndex] }}
                />
              );
            })}
          </div>
        </div>
      </motion.section>

      <motion.section initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.6 }} className="mt-6">
        <h2 className="text-xl font-semibold mb-3">📋 Repositories snapshot</h2>
        <div className="overflow-x-auto bg-white/5 p-4 rounded-xl">
          <table className="min-w-full text-left">
            <thead>
              <tr>
                <th className="pb-2">Repository</th>
                <th className="pb-2">Description</th>
                <th className="pb-2">Stars</th>
                <th className="pb-2">Language</th>
              </tr>
            </thead>
            <tbody>
              {repos.map((r, i) => (
                <motion.tr key={r.name} initial={{ opacity: 0, x: -20 }} animate={{ opacity: 1, x: 0 }} transition={{ delay: 0.05 * i }} className="border-t border-white/5">
                  <td className="py-3 font-medium">{r.name}</td>
                  <td className="py-3 text-sm opacity-90">{r.desc}</td>
                  <td className="py-3">{r.stars}</td>
                  <td className="py-3">{r.lang}</td>
                </motion.tr>
              ))}
            </tbody>
          </table>
        </div>
      </motion.section>

      <motion.footer initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: 0.8 }} className="mt-8 text-center text-sm opacity-80">
        Built with ❤️ — edit the sample data at the top of this file to match your real stats, then export README.md.
      </motion.footer>
    </div>
  );
}
