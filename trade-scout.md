# TradeScout: AI-Powered Import/Export Intelligence Platform

**TradeScout** is a next-generation web intelligence tool that allows users to find potential buyers, sellers, importers, or exporters worldwide simply by entering a product name and a location.

By leveraging Artificial Intelligence (Google Gemini) for query optimization and real-time data scraping technologies (SerpAPI/Google Maps), it delivers contact information, addresses, and activity details of companies in seconds.

## Purpose and Vision

The primary goal of this project is to automate the market research process for companies currently engaged in or looking to enter international trade.

**Future Roadmap:**

* ** Excel/CSV Export:** Ability to download hundreds of rows of company data in Excel format with a single click.
* ** Real-Time Tax & Customs Regulations:** Instant display of customs duty rates and trade restrictions between two selected countries (e.g., Turkey -> Germany).
* ** Big Data Processing:** Listing hundreds or even thousands of potential leads per search and integration with CRM systems.

---

## Architecture & Extensibility

One of TradeScout's core strengths is its **modular design**, built to adapt to changing technology needs without rewriting the entire codebase.

* ** Pluggable LLM Interface:** The system is not locked into a single AI provider. It uses an abstract base class (`BaseLLMModel`) for query generation.
* *Current Implementation:* Google Gemini Pro.
* *Easy Swap:* You can switch to **OpenAI (GPT-4)**, **Anthropic (Claude)**, or even local open-source models (Llama 3, Mistral) simply by adding a new class that inherits from `BaseLLMModel` and updating one line of configuration.


* **Modular Services:** Key components like the Scraper Service and Database Handler are decoupled.
* Need to switch from Supabase to a local PostgreSQL or MongoDB? Just implement the database interface.
* Want to use a different scraping provider instead of SerpAPI? The `ScraperService` is designed to support multiple backends.



---

## Technologies Used

The project is built on a modern, scalable, and microservices-oriented technology stack:

* **Backend:** Python, FastAPI
* **Frontend:** Streamlit (Fast and interactive UI)
* **AI & LLM:** Google Gemini Pro (Interchangeable)
* **Scraping:** SerpAPI (Google Maps & Local Results)
* **Database:** Supabase (PostgreSQL - Persistent data storage)
* **Cache:** Redis (Accelerating repeated searches and reducing API costs)
* **DevOps:** Docker & Docker Compose

---

## Project Structure

```text
.
├── app/
│   ├── api/v1/          # API Endpoints (Search router, etc.)
│   ├── core/            # Core configuration (Logger, etc.)
│   ├── db/              # Database and Cache connections (Supabase, Redis)
│   ├── models/          # Pydantic data models (BusinessResult, SearchResponse)
│   ├── services/        # Business logic layer
│   │   ├── llm_models/  # Base classes for easy LLM swapping
│   │   ├── search_fields/ # Dynamic search fields (Subject, Location)
│   │   ├── query_builder.py # AI query builder
│   │   ├── scraper_service.py # SerpAPI integration
│   │   └── search_service.py # Search orchestration
│   └── main.py          # FastAPI entry point
├── frontend/
│   └── app_ui.py        # Streamlit user interface
├── logs/                # Application logs
├── .env                 # Environment variables (API keys)
├── docker-compose.yml   # Docker service definitions
├── Dockerfile           # Backend container definition
└── requirements.txt     # Python dependencies

```

---

## Installation & Setup

The easiest way to run the project locally is using Docker.

### 1. Prerequisites

Clone the repository and navigate to the root directory:

```bash
git clone https://github.com/yourusername/trade-scout.git
cd trade-scout

```

### 2. Environment Configuration (.env)

Create a `.env` file in the root directory and populate it with your specific API keys:

```ini
# --- Google AI (Gemini) ---
GOOGLE_API_KEY=Your_Gemini_API_Key

# --- SerpAPI (Google Maps Scraping) ---
SERPAPI_API_KEY=Your_SerpAPI_Key

# --- Supabase (Database) ---
SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_KEY=Your_Supabase_Anon_Key

# --- Redis (Cache) ---
REDIS_HOST=redis
REDIS_PORT=6379
REDIS_PASSWORD=mysecretpassword
CACHE_EXPIRATION=3600

# --- App Settings ---
LOG_LEVEL=INFO
FASTAPI_URL=http://app:8000

```

### 3. Running with Docker (Recommended)

Launch the entire system (Backend, Frontend, and Redis) with a single command:

```bash
docker-compose up --build

```

Once completed:

* **Frontend (Streamlit):** Accessible at `http://localhost:8501`
* **Backend (FastAPI Swagger):** API documentation available at `http://localhost:8000/docs`

---

## Usage Scenario

1. **Open the Interface:** Navigate to `http://localhost:8501` in your browser.
2. **Input Data:**
* **Subject:** The product or sector you are looking for (e.g., "Organic Hazelnut Exporters" or "Textile Importers").
* **Location:** Target Market (e.g., "Hamburg, Germany" or "Global").


3. **Search:** Click the "Search" button.
* The system first uses **Gemini AI** to construct the most effective search term.
* **Redis Cache** is checked; if the search was done before, data is retrieved instantly.
* If not in cache, **SerpAPI** scans Google Maps for live data.
* Results are saved to the **Supabase** database and displayed on the screen.



---

## Development Notes

### AI Query Builder & Customization

Simple keywords entered by the user (e.g., "Hazelnuts", "Germany") are sent to the active LLM via `app/services/query_builder.py`. The system is designed to allow developers to modify the prompt engineering or switch the underlying model without touching the rest of the application logic.

### Database Schema (Supabase)

Data is stored in the `search_results` table. The table is automatically created if it does not exist when the application starts (`app/db/db.py`).

### Caching Strategy

Redis is used to prevent incurring repeated API costs (SerpAPI and Gemini) for the exact same queries. The default cache duration is 1 hour (`CACHE_EXPIRATION`).

---

## Contributing

1. Fork this repository.
2. Create a new feature branch (`git checkout -b feature/new-feature`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the branch (`git push origin feature/new-feature`).
5. Open a Pull Request.

---

## License

This project is licensed under the [MIT](https://choosealicense.com/licenses/mit/) License.

---

> **About This Project**
> This platform was engineered with **flexibility and ease of customization** at its core. It is designed to empower any corporation or business to initiate or accelerate their export/import market analysis with minimal technical friction.
> *Please note: **TradeScout is currently under active development.*** New features, performance optimizations, and integrations are being added regularly to further streamline global trade intelligence.
