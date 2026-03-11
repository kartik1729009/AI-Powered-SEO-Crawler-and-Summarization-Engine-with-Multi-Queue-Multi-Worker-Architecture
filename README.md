AI-Powered SEO Crawler & Summarization Engine
An intelligent distributed web crawler and SEO analysis platform that collects website performance metrics, generates AI-based summaries, and maintains fresh analytics through a multi-queue worker architecture.
The system demonstrates modern backend engineering concepts such as task orchestration, distributed queues, rate-limited crawling, scheduled recrawling, and AI-driven summarization.
Project Overview
Modern websites constantly change, making SEO monitoring a continuous process. Manual analysis tools are slow, limited, and often fail to maintain updated insights.
This project solves that problem by building an automated SEO intelligence pipeline that:
Crawls websites safely
Collects performance metrics
Generates AI summaries
Continuously refreshes stale data
Displays analytics in a dashboard
The system uses distributed job processing with Redis queues to process large workloads efficiently.
Key Features
Intelligent Web Crawling
Domain-aware crawling
Respectful rate limiting
URL deduplication
Distributed Queue Architecture
Separate queues for different tasks:
URL crawling
Stale page recrawling
AI summarization
SEO analytics
Each queue is processed by dedicated workers.
Google PageSpeed Insights Integration
Collects:
Performance score
SEO score
Accessibility score
Best practices metrics
Using the API from Google.
AI Content Summarization
Uses NLP models from platforms like:
Hugging Face
Cohere
to generate human-readable summaries of page content.
Scheduler for Data Freshness
A background scheduler:
identifies stale pages
re-queues them automatically
keeps analytics up-to-date
Fault Tolerance
Retry mechanism
Dead-letter queues
Structured logging
Analytics Dashboard
Displays:
crawl results
performance metrics
AI summaries
queue statistics
Supports report export (CSV/PDF).
System Architecture
The project uses a distributed pipeline architecture.
User Input (URLs)
        │
        ▼
API Server
        │
        ▼
Redis Queue System
        │
 ┌───────────────┬───────────────┬───────────────┐
 ▼               ▼               ▼               ▼
Crawl Worker   Analytics Worker   AI Worker   Scheduler
 │               │                 │            │
 ▼               ▼                 ▼            ▼
Website        PageSpeed API     AI Model   Stale Page Check
Content
        │
        ▼
Database
        │
        ▼
Dashboard & Reports
Tech Stack
Backend
Node.js
Express.js
Queue System
BullMQ
Redis
Database
MongoDB
AI / NLP
Hugging Face
Cohere / DeepSeek (optional)
APIs
Google PageSpeed Insights
Frontend
React.js
Project Structure
seo-crawler-engine
│
├── src
│   ├── controller
│   │   ├── crawl
│   │   ├── analytics
│   │   └── aiSummary
│   │
│   ├── workers
│   │   ├── crawl.worker.ts
│   │   ├── analytics.worker.ts
│   │   └── aiSummary.worker.ts
│   │
│   ├── queues
│   │   ├── crawl.queue.ts
│   │   ├── analytics.queue.ts
│   │   └── summary.queue.ts
│   │
│   ├── scheduler
│   │   └── stalePageScheduler.ts
│   │
│   ├── models
│   │   ├── domainPage.model.ts
│   │   └── domainNode.model.ts
│   │
│   └── utils
│       ├── rateLimiter.ts
│       ├── logger.ts
│       └── dbUtils.ts
│
├── dashboard
├── docker
├── .env
└── README.md
Installation
1. Clone Repository
git clone https://github.com/yourusername/seo-crawler-engine.git

cd seo-crawler-engine
2. Install Dependencies
npm install
3. Start Redis
The queue system requires Redis.
Install Redis locally or run using Docker:
docker run -p 6379:6379 redis
Redis acts as the job broker for BullMQ queues.
4. Configure Environment Variables
Create a .env file in the root directory.
Example:
PORT=5000

MONGO_URI=mongodb://localhost:27017/seoCrawler

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

PAGESPEED_API_KEY=your_google_api_key

AI_API_KEY=your_ai_provider_key
Running the Project
You must start multiple services.
Start Backend Server
npm run dev
or
npm start
Start Queue Workers
Each queue has a dedicated worker.
Run them in separate terminals.
Crawl worker:
npm run worker:crawl
Analytics worker:
npm run worker:analytics
AI summary worker:
npm run worker:summary
Start Scheduler
The scheduler handles stale pages.
npm run scheduler
Example API Usage
Submit a new website to crawl.
POST /api/crawl
Request body:
{
  "url": "https://example.com"
}
This will:
enqueue URL
crawl page
fetch SEO metrics
generate AI summary
Workflow
1️⃣ User submits URL
2️⃣ URL placed in crawl queue
3️⃣ Crawl worker fetches content
4️⃣ Analytics worker collects PageSpeed data
5️⃣ AI worker generates summary
6️⃣ Results stored in database
7️⃣ Scheduler refreshes stale pages
Evaluation Metrics
System correctness is demonstrated using:
Task success rate
Queue processing time
Retry rate
Crawl throughput
Summary completeness
Learning Outcomes
This project demonstrates knowledge of:
Distributed system design
Queue-based task processing
Rate-limited web crawling
Scheduler architecture
AI integration in backend systems
Fault-tolerant processing pipelines
Future Improvements
Keyword extraction
Topic clustering
Advanced SEO scoring
Kubernetes-based worker scaling
Real-time monitoring dashboard
Author
Kartik Sundriyal
Final Year Computer Science Project
License
This project is licensed under the MIT License.
How to Start the Project (Quick Summary)
# install dependencies
npm install

# start redis
docker run -p 6379:6379 redis

# start backend
npm run dev

# start workers
npm run worker:crawl
npm run worker:analytics
npm run worker:summary

# start scheduler
npm run scheduler
