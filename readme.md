# .NET installer comparison

**Variance:** observed minimum–maximum in ms, coefficient of variation (CV), and sample count (N). A single sample cannot establish variance.

**Caches Busted:** fresh-install headings refer to harness reset of the target installation and dotnetup archive cache. OS filesystem caches, CDN caches, and all machine-wide installer/package caches are not guaranteed cold or purged.

**Already-installed tables:** historical SDK-only second invocations against the installation left by the first pass. They do not use the current local optimized build. The Windows .NET 11 dotnetup/script batches have N=5 per telemetry setting; other cells generally have N=1. A verified WinGet no-applicable-update response is treated as a successful no-op.

**Legend:** 🟢 🥇 unique observed leader; 🟢 🤝 approximate/uncertain leaders (within 5% or 50 ms, overlapping observed ranges with medians less than 50% apart, or insufficient repeated data); 🔴 at least 50% slower than the lowest median. These are descriptive labels, not statistical significance claims. — means not measured.

**Comparability:** measurements span different days and tool builds. Windows .NET 11 runtime figures use fresh local-dotnetup and install-script runs with N=3 per telemetry setting. Other runtime figures are historical, including single-sample .NET 10 telemetry-on Windows and Apt results. The .NET 10 MSI payload is from an older SDK feature band than the portable tools; Apt uses its distro payload. Telemetry differences are not controlled causal effects. Unix here means Ubuntu under WSL, not all Unix systems.

The completed clean .NET 10 MSI trial is included. The earlier contaminated MSI trial is excluded. No completed .NET 10 WinGet install samples were available for this snapshot. Runtime measurements are dedicated runtime installs, not runtimes bundled with an SDK.

**Partial admin trials:** verified install rows are retained even if a later reset failed; failed resets and setup/download rows are not install timings. The WinGet SDK top-up batch followed a standalone-runtime trial: the SDK reset confirmed SDK absence, but the shared target runtime could remain installed. Its SDK timings are included with this shared-runtime caveat, not as proof that every bundled component was cold.
The .NET 11 MSI runtime telemetry-off cell has only one sample, so its variance is unknown.


## Shareable summary · .NET 11 · First Time Install

Telemetry off. Median install time; lower is better. Windows and Unix are separate comparisons.

| Installer | .NET 11 SDK Install (Telemetry Off) | .NET 11 Runtime Install (Telemetry Off) |
| --- | ---: | ---: |
| **🪟 Windows** | | |
| ☁️&nbsp;dotnetup | 🟢 🤝 11,764 ms | 🟢 🤝 2,175 ms |
| 📄&nbsp;Install&nbsp;Script | 🟢 🤝 11,430 ms | 3,254 ms |
| 🏗️&nbsp;MSI | 🔴 40,167 ms | 🔴 4,848 ms |
| 🪟&nbsp;WinGet | 🔴 47,025 ms | — |
| **🐧 Unix · WSL Ubuntu** | | |
| ☁️&nbsp;dotnetup | 🟢 🤝 8,608 ms | 🟢 🤝 2,032 ms |
| 📄&nbsp;Install&nbsp;Script | 🟢 🤝 7,532 ms | 🟢 🤝 2,567 ms |
| ⬇️&nbsp;Apt | 🔴 22,676 ms | 🔴 9,241 ms |


## .NET 11.0

![.NET 11.0 install-duration graphic](./comparison-11.0.svg)

### 🪟 Windows · .NET 11.0 · First Time Install · 1st run · Caches Busted

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) | Runtime (Telemetry Off) | Runtime - Telemetry Off (Variance) | Runtime - Telemetry On | Runtime Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 11,764 ms | 10,858–13,460 ms; CV 11.0%; N=3 | 🟢 🤝 15,468 ms | 11,962–18,975 ms; CV 32.1%; N=2 | 🟢 🤝 2,175 ms | 2,108–2,580 ms; CV 11.2%; N=3 | 🟢 🥇 2,170 ms | 1,729–2,204 ms; CV 13.0%; N=3 |
| 📄&nbsp;Install&nbsp;Script | 🟢 🤝 11,430 ms | 10,934–13,011 ms; CV 9.2%; N=3 | 🟢 🤝 13,887 ms | 13,539–14,235 ms; CV 3.5%; N=2 | 3,254 ms | 3,176–3,260 ms; CV 1.5%; N=3 | 🔴 3,653 ms | 3,258–4,060 ms; CV 11.0%; N=3 |
| 🏗️&nbsp;MSI | 🔴 40,167 ms | 36,813–43,522 ms; CV 11.8%; N=2 | 🔴 44,309 ms | 41,561–47,057 ms; CV 8.8%; N=2 | 🔴 4,848 ms | Unknown; N=1 | — | Not measured |
| 🪟&nbsp;WinGet | 🔴 47,025 ms | 44,963–49,087 ms; CV 6.2%; N=2 | 🔴 44,948 ms | 43,454–46,443 ms; CV 4.7%; N=2 | — | Not measured | — | Not measured |

### 🐧 Unix · WSL Ubuntu · .NET 11.0 · First Time Install · 1st run · Caches Busted

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) | Runtime (Telemetry Off) | Runtime - Telemetry Off (Variance) | Runtime - Telemetry On | Runtime Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 8,608 ms | 7,201–8,753 ms; CV 10.5%; N=3 | 10,918 ms | 10,499–11,336 ms; CV 5.4%; N=2 | 🟢 🤝 2,032 ms | 1,921–2,593 ms; CV 14.2%; N=4 | — | Not measured |
| 📄&nbsp;Install&nbsp;Script | 🟢 🤝 7,532 ms | 7,376–47,649 ms; CV 111.3%; N=3 | 🟢 🥇 9,736 ms | 9,604–9,868 ms; CV 1.9%; N=2 | 🟢 🤝 2,567 ms | 2,393–2,699 ms; CV 5.2%; N=4 | — | Not measured |
| ⬇️&nbsp;Apt | 🔴 22,676 ms | 22,436–27,239 ms; CV 8.5%; N=5 | 🔴 23,106 ms | 21,456–26,075 ms; CV 8.6%; N=5 | 🔴 9,241 ms | Unknown; N=1 | — | Not measured |

### Already-installed SDK · 2nd run

#### 🪟 Windows · .NET 11.0 · Install when the Install Already Exists · 2nd run

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 188 ms | 103–244 ms; CV 36.0%; N=5 | 🔴 1,149 ms | 996–1,306 ms; CV 11.7%; N=5 |
| 📄&nbsp;Install&nbsp;Script | 🔴 919 ms | 811–1,113 ms; CV 14.0%; N=5 | 857 ms | 792–947 ms; CV 7.5%; N=5 |
| 🏗️&nbsp;MSI | 🔴 2,139 ms | Unknown; N=1 | 🔴 2,351 ms | Unknown; N=1 |
| 🪟&nbsp;WinGet | 🔴 685 ms | Unknown; N=1 | 🟢 🤝 734 ms | Unknown; N=1 |

#### 🐧 Unix · WSL Ubuntu · .NET 11.0 · Install when the Install Already Exists · 2nd run

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 227 ms | Unknown; N=1 | 🟢 🤝 247 ms | Unknown; N=1 |
| 📄&nbsp;Install&nbsp;Script | 🔴 490 ms | Unknown; N=1 | 🔴 476 ms | Unknown; N=1 |
| ⬇️&nbsp;Apt | 🔴 2,614 ms | Unknown; N=1 | 🔴 2,444 ms | Unknown; N=1 |

### 🪟 Windows · Concurrent/batched scenario · .NET 11.0 cohort

**Three runtime majors: 9.0 + 10.0 + 11.0.** Historical first-install batch totals, N=5 per telemetry setting; these are not already-installed timings or single-runtime measurements. Dotnetup uses one multi-target command; Install Script runs three commands sequentially. The tools were benchmarked separately, not concurrently with each other. These older dotnetup builds do not represent the current local optimized executable. No matching WSL batch comparison is included.

| Installer | Execution | Runtime batch - Telemetry Off | Variance | Runtime batch - Telemetry On | Variance |
| --- | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 1 multi-target command | 🟢 🤝 4,567 ms | 3,656–4,744 ms; CV 9.9%; N=5 | 🟢 🤝 4,842 ms | 3,834–5,703 ms; CV 14.2%; N=5 |
| ☁️&nbsp;dotnetup&nbsp;(untracked) | 1 multi-target command | 🟢 🤝 3,793 ms | 3,704–4,111 ms; CV 4.4%; N=5 | 🟢 🤝 4,688 ms | 3,878–5,028 ms; CV 12.5%; N=5 |
| 📄&nbsp;Install&nbsp;Script | 3 sequential commands | 🔴 8,837 ms | 8,325–11,231 ms; CV 12.5%; N=5 | 🔴 9,683 ms | 8,331–10,683 ms; CV 11.2%; N=5 |

## .NET 10.0

![.NET 10.0 install-duration graphic](./comparison-10.0.svg)

### 🪟 Windows · .NET 10.0 · First Time Install · 1st run · Caches Busted

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) | Runtime (Telemetry Off) | Runtime - Telemetry Off (Variance) | Runtime - Telemetry On | Runtime Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🥇 29,849 ms | 29,499–30,199 ms; CV 1.7%; N=2 | 🟢 🤝 30,847 ms | 28,150–33,545 ms; CV 12.4%; N=2 | 🟢 🥇 1,728 ms | 1,417–2,710 ms; CV 34.6%; N=3 | 🟢 🤝 3,061 ms | Unknown; N=1 |
| 📄&nbsp;Install&nbsp;Script | 33,710 ms | 33,216–34,204 ms; CV 2.1%; N=2 | 🟢 🤝 37,523 ms | 31,888–43,158 ms; CV 21.2%; N=2 | 🔴 4,330 ms | 3,607–5,086 ms; CV 17.0%; N=3 | 4,249 ms | Unknown; N=1 |
| 🏗️&nbsp;MSI | 38,161 ms | 34,606–41,715 ms; CV 13.2%; N=2 | 35,273 ms | 34,262–36,285 ms; CV 4.1%; N=2 | — | Not measured | — | Not measured |
| 🪟&nbsp;WinGet | — | Not measured | — | Not measured | — | Not measured | — | Not measured |

### 🐧 Unix · WSL Ubuntu · .NET 10.0 · First Time Install · 1st run · Caches Busted

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) | Runtime (Telemetry Off) | Runtime - Telemetry Off (Variance) | Runtime - Telemetry On | Runtime Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🥇 7,555 ms | 5,592–9,517 ms; CV 36.7%; N=2 | 🟢 🥇 6,908 ms | 5,443–8,374 ms; CV 30.0%; N=2 | 🟢 🤝 2,276 ms | 1,656–2,781 ms; CV 25.2%; N=3 | — | Not measured |
| 📄&nbsp;Install&nbsp;Script | 🔴 11,563 ms | 10,585–12,541 ms; CV 12.0%; N=2 | 🔴 10,949 ms | 10,634–11,264 ms; CV 4.1%; N=2 | 🟢 🤝 2,701 ms | 2,262–2,979 ms; CV 13.6%; N=3 | — | Not measured |
| ⬇️&nbsp;Apt | 🔴 19,126 ms | 17,985–20,266 ms; CV 8.4%; N=2 | — | Not measured | 🔴 8,730 ms | Unknown; N=1 | — | Not measured |

### Already-installed SDK · 2nd run

#### 🪟 Windows · .NET 10.0 · Install when the Install Already Exists · 2nd run

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 132 ms | Unknown; N=1 | 979 ms | Unknown; N=1 |
| 📄&nbsp;Install&nbsp;Script | 🔴 916 ms | Unknown; N=1 | 🟢 🤝 843 ms | Unknown; N=1 |
| 🏗️&nbsp;MSI | — | Not measured | — | Not measured |
| 🪟&nbsp;WinGet | — | Not measured | — | Not measured |

#### 🐧 Unix · WSL Ubuntu · .NET 10.0 · Install when the Install Already Exists · 2nd run

| Installer | SDK - Telemetry Off | SDK - Telemetry Off (Variance) | SDK - Telemetry On | SDK - Telemetry On (Variance) |
| --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 🟢 🤝 265 ms | Unknown; N=1 | 🟢 🤝 303 ms | Unknown; N=1 |
| 📄&nbsp;Install&nbsp;Script | 🔴 509 ms | Unknown; N=1 | 🔴 609 ms | Unknown; N=1 |
| ⬇️&nbsp;Apt | 🔴 2,907 ms | Unknown; N=1 | 🔴 4,272 ms | Unknown; N=1 |

### 🪟 Windows · Concurrent/batched scenario · .NET 10.0 cohort

**Three runtime majors: 8.0 + 9.0 + 10.0.** Historical first-install batch totals, N=5 per telemetry setting; these are not already-installed timings or single-runtime measurements. Dotnetup uses one multi-target command; Install Script runs three commands sequentially. The tools were benchmarked separately, not concurrently with each other. These older dotnetup builds do not represent the current local optimized executable. No matching WSL batch comparison is included.

| Installer | Execution | Runtime batch - Telemetry Off | Variance | Runtime batch - Telemetry On | Variance |
| --- | --- | ---: | --- | ---: | --- |
| ☁️&nbsp;dotnetup | 1 multi-target command | 🟢 🤝 4,315 ms | 4,129–4,451 ms; CV 2.8%; N=5 | 🟢 🤝 3,914 ms | 3,420–4,964 ms; CV 15.2%; N=5 |
| ☁️&nbsp;dotnetup&nbsp;(untracked) | 1 multi-target command | 🟢 🤝 3,552 ms | 3,374–4,137 ms; CV 9.7%; N=5 | 🟢 🤝 3,586 ms | 3,414–4,483 ms; CV 11.5%; N=5 |
| 📄&nbsp;Install&nbsp;Script | 3 sequential commands | 🔴 10,463 ms | 9,228–13,049 ms; CV 15.8%; N=5 | 🔴 11,725 ms | 10,311–12,438 ms; CV 8.2%; N=5 |
