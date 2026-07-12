name: GitHub Metrics Dashboard

on:
  schedule:
    - cron: "0 0 * * *"   # runs daily at midnight UTC
  workflow_dispatch:        # allows manual trigger from the Actions tab
  push:
    branches: [ main ]

jobs:
  metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          filename: metrics.svg
          token: ${{ secrets.METRICS_TOKEN }}
          user: RahulKumar-devhub

          # ---- Overall look ----
          template: classic
          config_timezone: Asia/Kolkata
          config_display: large
          base: header, activity, community, repositories, metadata

          # ---- Purple / black premium theme ----
          plugin_base_color: "#a855f7"
          config_gradient: "#0d0221, #6a0dad, #a855f7"

          # ---- Donut-style top languages chart ----
          plugin_languages: yes
          plugin_languages_donut: yes
          plugin_languages_limit: 8
          plugin_languages_threshold: 0%
          plugin_languages_categories: markup, programming

          # ---- Isometric contribution calendar ----
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year

          # ---- Coding habits (commit time patterns) ----
          plugin_habits: yes
          plugin_habits_charts_type: bar

          # ---- Achievements / rank badges ----
          plugin_achievements: yes
          plugin_achievements_display: compact
