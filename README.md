<!--
  This is your PROFILE README. It goes in a repo named exactly after your
  username (e.g. github.com/priyanxu-oz/priyanxu-oz) so GitHub shows it on your profile.
  Widths 370/490 keep the portrait and info card the same height -- if you
  change the info card's height, re-match these.
-->
<div align="center">

<table>
<tr>
<td valign="top"><img src="./avi-ascii.svg" width="370" alt="ASCII portrait" /></td>
<td valign="top"><img src="./info-card.svg" width="490" alt="Experience, stack, highlights" /></td>
</tr>
</table>

## Priyanshu Singh

**AI Engineer · Open Source · Coffee · Protein**

[![Instagram](https://img.shields.io/badge/Instagram-priyanxuywrrr__-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/priyanxuywrrr_)

<br>

<!-- animated contribution graph, refreshed daily by the workflow -->
<img src="./contrib-heatmap.svg" width="860" alt="GitHub contribution graph" />

</div>
<svg viewBox="0 0 490 690" width="490" height="690" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <style>
      .card-bg { fill: #0d1117; }
      .accent  { fill: #ff8fa3; }
      .heading { fill: #ff8fa3; font-family: Consolas, 'DejaVu Sans Mono', monospace; font-size: 17px; font-weight: bold; }
      .label   { fill: #8b949e; font-family: Consolas, 'DejaVu Sans Mono', monospace; font-size: 13px; }
      .value   { fill: #e6edf3; font-family: Consolas, 'DejaVu Sans Mono', monospace; font-size: 13px; }
      .tag     { fill: #21262d; stroke: #ff8fa3; stroke-width: 1; rx: 12; }
      .tag-text{ fill: #ff8fa3; font-family: Consolas, 'DejaVu Sans Mono', monospace; font-size: 12px; }
      .divider { stroke: #21262d; stroke-width: 1; }
    </style>
  </defs>

  <rect class="card-bg" width="100%" height="100%" rx="12"/>
  <rect x="1" y="1" width="488" height="688" rx="12" fill="none" stroke="#21262d" stroke-width="1.5"/>

  <!-- header -->
  <text x="24" y="42" class="heading">$ whoami</text>
  <text x="24" y="68" fill="#e6edf3" font-family="Consolas, monospace" font-size="15">Priyanshu Singh</text>
  <text x="24" y="90" class="label">Student of Engineering · AI / CS</text>

  <line x1="24" y1="112" x2="466" y2="112" class="divider"/>

  <!-- focus -->
  <text x="24" y="140" class="heading">$ focus</text>
  <text x="40" y="164" class="value">→ Artificial Intelligence</text>
  <text x="40" y="186" class="value">→ Computer Science fundamentals</text>
  <text x="40" y="208" class="value">→ Open source contributions</text>

  <line x1="24" y1="230" x2="466" y2="230" class="divider"/>

  <!-- stack -->
  <text x="24" y="258" class="heading">$ stack</text>

  <g font-family="Consolas, 'DejaVu Sans Mono', monospace" font-size="12">
    <rect x="24" y="272" width="82" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="65" y="290" text-anchor="middle" class="tag-text">Python</text>

    <rect x="114" y="272" width="70" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="149" y="290" text-anchor="middle" class="tag-text">Java</text>

    <rect x="192" y="272" width="112" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="248" y="290" text-anchor="middle" class="tag-text">JavaScript</text>

    <rect x="312" y="272" width="80" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="352" y="290" text-anchor="middle" class="tag-text">Canva</text>
  </g>

  <line x1="24" y1="322" x2="466" y2="322" class="divider"/>

  <!-- interests -->
  <text x="24" y="350" class="heading">$ interests</text>
  <g font-family="Consolas, 'DejaVu Sans Mono', monospace" font-size="12">
    <rect x="24" y="364" width="100" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="74" y="382" text-anchor="middle" class="tag-text">Open Source</text>

    <rect x="132" y="364" width="76" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="170" y="382" text-anchor="middle" class="tag-text">Coffee</text>

    <rect x="216" y="364" width="86" height="28" rx="14" fill="#21262d" stroke="#ff8fa3"/>
    <text x="259" y="382" text-anchor="middle" class="tag-text">Protein</text>
  </g>

  <line x1="24" y1="406" x2="466" y2="406" class="divider"/>

  <!-- quote / footer -->
  <text x="24" y="434" class="heading">$ echo status</text>
  <text x="40" y="458" class="value">"Building, breaking, learning."</text>

  <!-- decorative ascii border accent at bottom -->
  <text x="24" y="660" fill="#30363d" font-family="Consolas, monospace" font-size="11" xml:space="preserve">-----------------------------------------------</text>
  <text x="24" y="678" class="label">github.com/priyanxu-oz</text>
</svg>
name: Generate contribution heatmap

on:
  schedule:
    - cron: "0 2 * * *"   # every day at 02:00 UTC
  workflow_dispatch: {}
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Generate animated contribution graph
        uses: Platane/snk@v3
        with:
          github_user_name: priyanxu-oz
          outputs: |
            contrib-heatmap.svg?color_snake=%23ff8fa3&color_dots=%2321262d,%232b3543,%233a4353,%234a5568,%23ff8fa3

      - name: Commit and push
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add contrib-heatmap.svg
          git diff --staged --quiet || git commit -m "chore: refresh contribution heatmap"
          git push
