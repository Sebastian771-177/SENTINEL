# SENTINEL 
◈ Sentinel
AI-Powered SOC Assistant — IOC Triage & Analysis

Automating the most time-consuming part of Tier 1 SOC work: triaging indicators of compromise across multiple threat intelligence platforms and turning raw data into analyst-ready reports.


🔍 What It Does
Sentinel accepts any suspicious indicator — IP address, domain, file hash, or phishing email — and automatically queries public threat intelligence APIs, then uses the Anthropic Claude API to synthesize the results into a structured analyst report.
For each IOC, Sentinel produces:

Verdict — MALICIOUS / SUSPICIOUS / CLEAN / UNKNOWN
Severity rating — CRITICAL / HIGH / MEDIUM / LOW
VirusTotal results — malicious, suspicious, and harmless engine counts
AbuseIPDB score — abuse confidence score, ISP, country, Tor exit node detection
MITRE ATT&CK TTPs — mapped to the threat behavior
Key findings — most important data points synthesized across sources
Analyst recommendations — concrete next steps
False positive likelihood — helps prioritize triage queue
Phishing indicators — for email analysis (social engineering tactics, spoofed brands, link analysis)

Results are rendered as a color-coded HTML dashboard directly in Google Colab.

🛠 Technologies

Python 3.10+
Anthropic Claude API (claude-opus-4-5) — IOC synthesis and email phishing analysis
VirusTotal API — multi-engine malware and reputation scanning (free tier)
AbuseIPDB API — IP abuse reputation and reporting (free tier)
Google Colab — interactive notebook environment with HTML rendering


🚀 Getting Started
Run in Google Colab (recommended)

Upload sentinel_soc.py to Google Colab or paste cells manually
Click the 🔑 Secrets icon in the left sidebar
Add the following secrets:

Secret NameWhere to get itANTHROPIC_API_KEYconsole.anthropic.comVIRUSTOTAL_API_KEYvirustotal.com → Sign up → API KeyABUSEIPDB_API_KEYabuseipdb.com → Sign up → API Key

Toggle Notebook access ON for each secret
In Cell 10, set use_mock=False
Run all cells top to bottom


No API keys yet? Set use_mock=True in Cell 10 to run a full demo with simulated threat data.

Run locally
bashpip install anthropic requests
export ANTHROPIC_API_KEY=sk-ant-...
export VIRUSTOTAL_API_KEY=your-key
export ABUSEIPDB_API_KEY=your-key
python sentinel_soc.py

📊 Supported IOC Types
TypeExampleData SourcesIPv4 Address185.220.101.45VirusTotal + AbuseIPDBDomainpaypa1-secure.comVirusTotalMD5 Hash44d88612...VirusTotalSHA1 Hashda39a3ee...VirusTotalSHA256 Hashe3b0c442...VirusTotalEmail (full text)Paste raw emailClaude AI analysis
Sentinel auto-detects the IOC type — no configuration needed.

📁 Project Structure
sentinel/
├── sentinel_soc.py       # Main script (paste into Colab cells)
├── README.md             # This file
└── sentinel_output.json  # Generated after running — full analyst reports

💡 Why I Built This
SOC Tier 1 analysts spend a disproportionate amount of time on manual IOC triage — copying indicators between VirusTotal, AbuseIPDB, and other platforms, then writing up findings by hand. Sentinel compresses that workflow into a single tool.
The addition of Claude as a synthesis layer means analysts get a plain-English verdict with actionable next steps, not just raw numbers. This is especially valuable for junior analysts who may not yet have the experience to interpret conflicting signals across multiple platforms.

🔮 Roadmap

 AlienVault OTX integration
 Shodan lookup for IP infrastructure profiling
 STIX 2.1 export for SIEM ingestion
 Bulk IOC analysis from CSV input
 Spanish-language phishing email detection (integrates with Centinela OSINT)
 Slack/Teams alerting for high-severity findings


👤 Author
Sebastian Guerrero
CompTIA Security+ | Google Cybersecurity Certificate
B.A. International Relations | Fluent in Spanish
Based in Miami, FL

⚠️ Disclaimer
This tool is intended for educational and portfolio purposes only. Sample IOCs used in the demo are either simulated or reference publicly documented malicious indicators. Always follow your organization's policies and applicable laws when conducting threat intelligence activities.
