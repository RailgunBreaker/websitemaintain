# WordPress Website Setup Guide

This is a basic guide to set up your own WordPress site with a custom domain and server.

---

## 1. Domain

- [ ] Register a domain through a registrar (e.g., Namecheap, Google Domains, GoDaddy).
- [ ] Set up DNS settings:
  - [ ] Create an A record pointing to your server's public IP address. (1xx.1xx.1xxx)
- [ ] Install SSL certificate to enable HTTPS access:
  - [ ] Buy an SSL certificate (free) from the registrar.

---

## 2. Server

- [ ] Rent a cloud server in Amsterdam (AMS) for free (if possible):
  - Options: AWS EC2,  choose Ubantu or CentOS, a normal Linux System
- [ ] Secure your server:
  - [ ] Set up SSH key authentication.
  - [ ] Enable UFW firewall (open only ports 22, 80, 443).

---

## 3. Install Web Server Environment

Choose one environment:

- [ ] **LEMP stack** (Linux + Nginx + MySQL/MariaDB + PHP)
- **OR**
- [ ] **LAMP stack** (Linux + Apache + MySQL/MariaDB + PHP)

Install:
- [ ] Web server (Nginx or Apache)
- [ ] Database (MySQL or MariaDB)
- [ ] PHP and necessary PHP extensions

Check if the web server and PHP are working (test with a simple PHP page).

---

## 4. Install WordPress

- [ ] Download the latest WordPress package from [wordpress.org](https://wordpress.org/).
- [ ] Unzip and move WordPress files into the web server root directory (`/var/www/html` or your custom path).
- [ ] Set correct file permissions:
  - `sudo chown -R www-data:www-data /path/to/wordpress`
- [ ] Create a database and user for WordPress:
  - Use MySQL commands or a tool like phpMyAdmin.
- [ ] Configure `wp-config.php` with database info.
- [ ] Complete WordPress setup through the web installer (access via your domain).

---

## 5. Connect Your API (Optional)

If you need to insert your API into WordPress:

- [ ] Create a simple WordPress plugin **or**
- [ ] Edit the `functions.php` file of your theme.
- [ ] Use WordPress HTTP functions like:
  - `wp_remote_get()`
  - `wp_remote_post()`
- [ ] (Recommended) Cache API responses to avoid slowing down your site.

---

## 6. Final Check

- [ ] Test if your domain properly loads your WordPress site.
- [ ] Check if SSL (HTTPS) is working.
- [ ] Ensure your WordPress dashboard is accessible.
- [ ] Monitor your server resource usage occasionally (e.g., CPU, RAM).
# SSH Connection (Windows) and Basic Linux Operations

## 5. SSH Connection from Windows

- [ ] Install an SSH client:
  - or use Window Terminal
  - log in using connect `<username>@ur domain(or ip address)`
- [ ] Obtain server's public IP address.
- [ ] Open PuTTY and configure:
  - Host Name: `<your_server_ip>`
  - Port: `22`
  - Connection type: SSH
- [ ] Login with:
  - Username: `ubuntu` (or whatever the cloud provider specifies)
  - Private key file (if using key authentication)

---

## 6. Basic Linux Commands

- [ ] Update server packages:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```
- [ ] Install basic software packages:
  ```bash
  sudo apt install nginx mysql-server php-fpm php-mysql unzip
  ```
- [ ] Navigate between directories:
  ```bash
  cd /path/to/directory
  ls -al
  ```
- [ ] Create and edit files:
  ```bash
  nano filename.txt
  ```
- [ ] Restart services:
  ```bash
  sudo systemctl restart nginx
  sudo systemctl restart mysql
  ```
- Go to the previous directory
```bash
cd ../
```
- Restart 
```bash
reboot
```
---

# Upload Files from Your Computer to Your Server using FileZilla

## 7. Install and Connect FileZilla

- [ ] Download and install [FileZilla Client](https://filezilla-project.org/).
- [ ] Open FileZilla and set up a new site in Site Manager:
  - Host: `<your_server_ip>`
  - Port: `22`
  - Protocol: SFTP - SSH File Transfer Protocol
  - Logon Type: Normal (for password) or Key File (for SSH Key)
  - Username: `ur name`
  - Password or private key as needed.
- [ ] Connect to your server.

## 8. Upload Files

- [ ] Local computer files appear on the left.
- [ ] Server files appear on the right.
- [ ] Drag and drop files to upload into your server directories.

---
# AI System for Real-Time Multilingual News Tracking and Alerts

## System Architecture Overview

- **Modular Microservices Design:**  
  Split into distinct services for ingestion, NLP analysis, storage, and notification. Each service can scale and update independently.
- **Pipeline Workflow:**  
  1. **News Ingestion Service** collects data from global, Nikkei, and corporate sources.  
  2. **NLP Analysis Service** performs language detection, entity recognition, and importance classification.  
  3. **Database** stores parsed articles with metadata.  
  4. **Notification Service** pushes alerts via API.
- **Entity-Focused Filtering:**  
  Identify mentions of the target company (e.g., Mitsubishi Corporation, ticker 8058.T) and related economic/sector terms to filter only relevant news.
- **Multilingual NLP Integration:**  
  Process Japanese and English natively (no translation), using language‐appropriate tokenizers and a shared multilingual model (e.g. mBERT or XLM-RoBERTa).
- **High-Level Data Flow:**  
  1. Sources publish news  
  2. Ingestion polls or receives events  
  3. Text cleaning & analysis  
  4. Importance classification  
  5. API‐based notification dispatch

## Data Sources and APIs

- **Worldwide News Feeds:**  
  Use NewsAPI, RSS feeds from Reuters, Bloomberg, BBC, etc., filtering by company name and keywords.
- **Japanese News (Nikkei & Others):**  
  Subscribe to Nikkei’s RSS/API, NHK Biz, Jiji Press, and Ministry releases; optionally scrape if no API is provided.
- **Corporate News:**  
  Monitor official IR sites, TDnet disclosures, and press‐release feeds for first‐party announcements.
- **Connector Layer:**  
  Normalize all inputs (title, timestamp, source, language, snippet) via REST API calls, RSS parsing, or scraper bots.
- **Trusted-Source Whitelist:**  
  Maintain a list of approved domains and APIs; discard or flag unknown sources.

## Fake News Detection Mechanisms

- **Source Verification:**  
  Only ingest from whitelisted, reputable publishers and official channels.
- **Cross-Source Cross-Check:**  
  For high‐impact articles, verify that multiple trusted outlets report the same story.
- **Content Analysis for Red Flags:**  
  Use an NLP classifier or rule‐based checks to detect sensational or inconsistent language.
- **Official Source Priority:**  
  Tag direct press releases or government bulletins as highly reliable.
- **Adaptive Blacklist/Whitelist:**  
  Continuously update source lists based on observed reliability and user feedback.

## News Importance Analysis and Color Coding

- **Automated Content Scoring:**  
  Analyze subject matter, financial figures, entity relationships, and past impact patterns to assign a raw significance score.
- **Classification Model:**  
  Map scores to three categories via a fine-tuned transformer or supervised classifier:  
  - **Red:** Major events (e.g. earnings surprises, M&A, regulatory changes)  
  - **Yellow:** Moderate updates (e.g. product launches, partnerships)  
  - **Green:** Minor or routine news (e.g. conference attendance, small appointments)
- **Rule-Based Overrides:**  
  Apply heuristic rules (e.g. any “merger” keyword → at least Yellow) to catch edge cases.
- **Contextual Analysis:**  
  Factor in company‐sector‐economy relationships (e.g. GDP changes may jump from Green to Yellow if tightly correlated).
- **Color Tagging:**  
  Store & expose the color label in the database and notification payload.

## Real-Time Monitoring and Notification

- **Continuous Polling & Eventing:**  
  Poll RSS/API feeds every 1–2 minutes or subscribe to webhooks/streaming APIs where available.
- **Low-Latency Processing:**  
  Use message queues (Kafka/RabbitMQ) and horizontally‐scaled workers to keep end-to-end processing under 5 minutes.
- **Notification Dispatcher:**  
  On classification, emit an internal “notification event” containing title, snippet, source, timestamp, and color.
- **API-Based Delivery:**  
  - **Webhooks/APIs** for website or third-party apps (REST or WebSocket/SSE)  
  - **Email** via SendGrid/SES for inbox alerts  
  - **Mobile Push** via FCM/APNs for iOS & Android  
  - **Web Push** (Push API + service workers) for browser notifications  
  - **Messaging Apps** (LINE Notify, Telegram Bot API) for chat alerts

## Deployment Strategy

- **Cloud Infrastructure:**  
  Containerize services with Docker, orchestrate on Kubernetes (auto-scaling, rolling updates).
- **Serverless Components:**  
  Use AWS Lambda / GCP Cloud Functions for scheduled ingestion or webhook triggers.
- **Data Storage:**  
  - Relational DB (PostgreSQL/MySQL) for metadata & subscriptions  
  - Elasticsearch for full-text search & historical queries  
  - Redis for caching & pub/sub
- **CI/CD & Monitoring:**  
  Automate tests & deployments with GitHub Actions; monitor metrics (Prometheus/Grafana) and logs (ELK or cloud logs).
- **Frontend Hosting:**  
  Deploy a static or single‐page app (React/Vue) on AWS Amplify, Netlify, or CloudFront + S3.

## Tech Stack Recommendations

- **Language & Frameworks:**  
  - **Python** (data pipeline, NLP, FastAPI)  
  - **Node.js** (optional ingestion or real-time API server)  
- **NLP & ML:**  
  - Hugging Face Transformers (mBERT/XLM-RoBERTa)  
  - spaCy + GiNZA (Japanese) / standard tokenizers (English)  
  - scikit-learn for initial fake-news classifiers
- **Databases & Queues:**  
  - PostgreSQL/MySQL, MongoDB or Elasticsearch  
  - Redis, Kafka, or RabbitMQ
- **Notification SDKs:**  
  - SendGrid or Amazon SES (email)  
  - Firebase Admin SDK (push)  
  - LINE Messaging API, python-telegram-bot
- **DevOps & Infra:**  
  - Docker & Kubernetes  
  - Terraform or CloudFormation for infra as code  
  - Prometheus, Grafana, ELK for monitoring & logging

## Challenges and Mitigation

1. **Multilingual NLP Complexity**  
   - Use proven multilingual models and language-specific preprocessors (MeCab, SudachiPy).  
2. **Source Coverage vs. Noise**  
   - Strict entity filters, de-duplication logic, & adaptive source lists.  
3. **Real-Time Performance**  
   - Async I/O, in-memory processing, and auto-scaling worker pools.  
4. **Misclassification Risks**  
   - Hybrid ML + rule-based checks; feedback loop via impact correlation.  
5. **Integration & API Changes**  
   - Configurable adapters; fallback scrapers; regular maintenance.  
6. **Misinformation**  
   - Cross-source checks; flag unverified items; whitelist official channels.  
7. **Notification Fatigue**  
   - User preferences (e.g. Red-only); bundling minor alerts into digests.  
8. **Security & Reliability**  
   - HTTPS, encrypted keys, auth for APIs; multi-region deployment & automated recovery.

## Useful Links
- Linux Syntax(https://www.youtube.com/watch?v=16d2lHc0Pe8)
- Wordpress (https://www.youtube.com/watch?v=kYY88h5J86A&pp=0gcJCdgAo7VqN5tD)
- Domain, DNS, (https://www.youtube.com/watch?v=1JBCKNIT2Ys)
- SSL Certificate (https://www.youtube.com/watch?v=NZzcDsG-LxE)
- AWS EC2(https://www.youtube.com/watch?v=BFCBitHQI-Q)