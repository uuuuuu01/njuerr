# Visit https://github.com/lowlighter/metrics#-documentation for full reference
name: Metrics
on:
  # Schedule updates (each hour)
  schedule: [{cron: "0 * * * *"}]
  # Lines below let you run workflow manually and on each commit
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
          # The following scopes are required:
          #  - public_access (default scope)
          # The following additional scopes may be required:
          #  - read:org      (for organization related metrics)
          #  - read:user     (for user related data)
          #  - read:packages (for some packages related data)
          #  - repo          (optional, if you want to include private repositories)
          token: ${{ secrets.METRICS_TOKEN }}

          # Options
          template: classic
          base: header, activity, community, repositories, metadata
          config_timezone: Asia/Shanghai
          plugin_achievements: yes
          plugin_achievements_display: detailed
          plugin_achievements_secrets: yes
          plugin_achievements_threshold: C
          plugin_notable: yes
          plugin_notable_from: organization
          plugin_notable_types: commit
          plugin_stargazers: yes
          plugin_stargazers_charts: yes
          plugin_stargazers_charts_type: classic
          plugin_wakatime: yes
          plugin_wakatime_days: 7
          plugin_wakatime_limit: 5
          plugin_wakatime_repositories_visibility: all
          plugin_wakatime_sections: time, projects, projects-graphs, languages, languages-graphs, editors, os
          plugin_wakatime_url: https://wakatime.com
          plugin_wakatime_user: current
