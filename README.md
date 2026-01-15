name: Metrics
on:
  # Schedule updates (every day at midnight)
  schedule: [{cron: "0 0 * * *"}]
  # Lines below let you run it manually
  workflow_dispatch:
  push: {branches: ["master", "main"]}

jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          # Your GitHub token
          token: ${{ secrets.METRICS_TOKEN }}

          # Options
          user: TheShivaji  # <-- YAHAN APNA USERNAME CHECK KAR LENA
          template: classic
          base: header, activity, community, repositories, metadata
          config_timezone: Asia/Kolkata
          
          # 1. 3D Isometric Calendar (Woh photo wala 3D graph)
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year
          
          # 2. Most Used Languages (Right side bar)
          plugin_languages: yes
          plugin_languages_ignored: >-
            html, css
          plugin_languages_details: bytes-size, percentage
          plugin_languages_limit: 8
          plugin_languages_analysis_timeout: 15
          
          # 3. PageSpeed (Performance wala meter) - Optional
          plugin_pagespeed: no # Ise 'yes' kar dena agar website ho to
          
          # 4. Habits (Activity Graph)
          plugin_habits: yes
          plugin_habits_charts_type: classic
          plugin_habits_days: 14
          plugin_habits_facts: yes
          plugin_habits_from: 200
          
          # 5. Tech Stack Icons (Niche wale icons)
          plugin_stack: yes
          plugin_stack_from: github.com/TheShivaji
          
          # 6. Introduction (Left side info)
          plugin_introduction: yes
          plugin_introduction_title: yes
