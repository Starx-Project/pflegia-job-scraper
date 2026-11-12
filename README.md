# Pflegia Job Scraper and Data Delivery Bot

Automation that collects recruiting data on a schedule, stores results in **Google Drive** and delivers them to the team as Excel files through a Telegram bot.

> The source code of this project is private (client work). This page describes what it does and how it is built. It handles only data the client is entitled to use, and no personal data is shown here.

## What it does
- **Collection:** browser-automation scrapers (Selenium and Playwright) gather listings and records from job platforms. For one source, a Playwright runner uses a persistent signed-in profile and collects data per province in sequence.
- **Resilient runs:** automatic re-login, timeouts, "idle after progress" detection, incremental saving after every record so a crash loses nothing, and one output folder per run.
- **Merge and de-duplication:** per-province Excel files are merged into a single sheet. Duplicates are removed by stable IDs, or by normalized phone number, name and email, and rows that have no useful data are dropped.
- **Google Drive publishing:** results are published to a shared Drive folder through the Drive API with a service account.
- **Telegram delivery bot:** two buttons (`/pflegia`, `/eestekhdam`). The first exports the latest Google Sheet from Drive as .xlsx. The second merges and de-duplicates the local scrape output on demand. The file is sent to the chat and temporary files are deleted.

## Stack
Python, Selenium, Node.js, Playwright, Telegraf, Google Drive API (googleapis), SheetJS (xlsx), systemd.

## How it is run
- Runs on a Linux server with scheduled jobs. The bot runs as a systemd service.
- Delivered and handed over with project documentation.

## Context
Built at Arika (2024 - 2026) as one of five production services I delivered and handed over.

## Contact
Amir Hossein Fotoohi - ahfotoohi@gmail.com - [LinkedIn](https://linkedin.com/in/amir-hossein-fotoohi-411429390)
