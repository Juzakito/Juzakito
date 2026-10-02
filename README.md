# Juzakito
<picture>
 <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Juzakito/Juzakito/main/dark.svg">
 <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Juzakito/Juzakito/main/light.svg">
 <img alt="Juzaki Juzakito" src="https://raw.githubusercontent.com/Juzakito/Juzakito/main/light.svg">
</picture>
<div align="center">
<img width="100%" src="https://streak-stats.demolab.com/?user=Juzakito&hide_border=true&background=0A101F&stroke=22D3EE&ring=A78BFA&fire=10B981&currStreakLabel=22D3EE&sideLabels=94A3B8&currStreakNum=F8FAFC&sideNums=F8FAFC&dates=64748B&titleColor=22D3EE&card_width=1180" alt="streak" />
<br/>
<img width="49%" src="https://github-readme-stats-is8o.vercel.app/api?username=Juzakito&show_icons=true&count_private=true&include_all_commits=true&hide_rank=true&hide_border=true&title_color=22D3EE&icon_color=A78BFA&text_color=94A3B8&bg_color=0A101F&card_width=500" alt="stats" />
<img width="49%" src="https://github-readme-stats-is8o.vercel.app/api/top-langs/?username=Juzakito&layout=compact&langs_count=8&hide_border=true&title_color=22D3EE&text_color=94A3B8&bg_color=0A101F&card_width=500" alt="top langs" />
</div>
<div align="center">
<a href="https://www.linkedin.com/in/jmgonzalezz/">
  <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
</a>
&nbsp;&nbsp;
<a href="https://joseg-dev.vercel.app/">
  <img src="https://img.shields.io/badge/Portfolio-0A101F?style=for-the-badge&logo=vercel&logoColor=22D3EE&labelColor=0A101F" alt="Portfolio" />
</a>
&nbsp;&nbsp;
<a href="mailto:jmgonzalez.contact@gmail.com">
  <img src="https://img.shields.io/badge/Email-0A101F?style=for-the-badge&logo=gmail&logoColor=10B981&labelColor=0A101F" alt="Email" />
</a>
</div>
<div align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Juzakito/Juzakito/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Juzakito/Juzakito/output/github-snake.svg" />
  <img alt="Snake eating my contributions" src="https://raw.githubusercontent.com/Juzakito/Juzakito/output/github-snake.svg" />
</picture>
</div>
name: Generate Snake Animation
on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:
  push:
    branches: [main]
jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - name: Generate snake SVGs
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg?palette=github-light&color_snake=0891B2&color_dots=#ebedf0,#a5b4fc,#818cf8,#6366f1,#0891B2
            dist/github-snake-dark.svg?palette=github-dark&color_snake=10B981&color_dots=#2d3343,#4b5563,#7C3AED,#A78BFA,#22D3EE
      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
          commit_message: "Update snake animation [skip ci]"
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
