🇮🇳 Bharat Biz Agent
A backend Telegram-bot and web service that powers a business order tracking and invoice generation agent for the “Bharat Biz” ecosystem. This project integrates with Telegram to accept commands from users, track sales, update inventory, and generate PDF invoices.

📌 Overview
Bharat Biz Agent is an AI-ready agent application built with Python and Flask that:


📦 Runs a Telegram-based bot for selling products


📊 Tracks orders and revenue in an Excel file


📑 Generates professional invoices (PDF) per order


🧠 Logs events and inventory status


🖥️ Provides a simple dashboard interface


The main backend service runs via Flask and continuously polls Telegram for bot commands to handle inventory and orders.

🚀 Features
✅ Telegram chatbot interface for product browsing and purchasing
✅ Inventory control and order tracking
✅ PDF invoice generation with styling and branding
✅ Excel-based sales record keeping
✅ Flask API to expose current state & admin endpoints
✅ Dashboard HTML for quick visualization

🛠️ Built With
ComponentPurposePythonCore backend logicFlaskHTTP API / dashboardTelegram Bot APIChat interfaceopenpyxlExcel sales ledgerFPDFPDF invoice creationFlask-CORSCross-origin API access

📥 Installation


Clone the repository
git clone https://github.com/comandoaman/bharat-biz-agent.git
cd bharat-biz-agent



Create & activate Python virtual environment
python3 -m venv venv
source venv/bin/activate



Install requirements
pip install -r requirements.txt



Configure environment


Add your Telegram bot token inside server.py:
BOT_TOKEN = "<your_bot_token_here>"





Run the server
python server.py




🧩 Usage
Telegram Bot


Type /start to initialize interaction with the bot


Use /stock to view available products


Send product names to purchase


After purchase, the bot generates an invoice PDF and sends it


Admin API Endpoints
EndpointMethodDescription/dataGETReturns current inventory, revenue, orders, logs/update-inventoryPOSTUpdate stock for a given product/reset-logsPOSTClears logs
Example request to update inventory:
curl -X POST http://localhost:5001/update-inventory \
  -H "Content-Type: application/json" \
  -d '{"id": 101, "stock": 5}'


🧾 Invoicing and Records


Invoices are auto-generated in the invoices/ folder


Sales are logged into store_orders.xlsx



📁 Project Structure
bharat-biz-agent/
├── Dashboard.html      # Minimal HTML dashboard
├── server.py           # Main backend & bot logic
├── store_orders.xlsx   # Excel sales record (auto-generated)
├── invoices/           # Generated invoices (PDF)
├── requirements.txt    # Python dependencies
├── Dockerfile          # (Optional container config)
└── Project Overview.mp4 # Demo/overview video




🐳 Running with Docker

This project includes a Dockerfile so you can run the Bharat Biz Agent in a containerized environment without manually installing dependencies.

📦 1. Build the Docker Image

From the project root directory (where the Dockerfile exists):

docker build -t bharat-biz-agent .


This will:

Use the Python base image

Install dependencies from requirements.txt

Copy the application files

Expose the Flask port

🚀 2. Run the Container
docker run -d \
  -p 5001:5001 \
  --name bharat-biz-agent \
  bharat-biz-agent


-d → Run in detached mode

-p 5001:5001 → Maps container port to your local machine

--name → Assigns container name

The app will be available at:

http://localhost:5001

🔐 3. Passing Telegram Bot Token (Recommended)

Instead of hardcoding the bot token in server.py, modify the app to use environment variables:

Update server.py
import os
BOT_TOKEN = os.environ.get("BOT_TOKEN")

Run with Environment Variable
docker run -d \
  -p 5001:5001 \
  -e BOT_TOKEN=your_telegram_bot_token_here \
  --name bharat-biz-agent \
  bharat-biz-agent

📂 4. Persisting Data (Recommended)

To keep invoices and Excel data after container restarts:

docker run -d \
  -p 5001:5001 \
  -e BOT_TOKEN=your_token_here \
  -v $(pwd)/invoices:/app/invoices \
  -v $(pwd)/store_orders.xlsx:/app/store_orders.xlsx \
  --name bharat-biz-agent \
  bharat-biz-agent


This mounts:

Local invoices/ folder

Local store_orders.xlsx file

So data survives container removal.

🛑 Stopping the Container
docker stop bharat-biz-agent


Remove container:

docker rm bharat-biz-agent


Remove image:

docker rmi bharat-biz-agent

🧱 Optional: Using Docker Compose

Create a docker-compose.yml:

version: "3.9"
services:
  bharat-biz-agent:
    build: .
    ports:
      - "5001:5001"
    environment:
      - BOT_TOKEN=your_telegram_bot_token_here
    volumes:
      - ./invoices:/app/invoices
      - ./store_orders.xlsx:/app/store_orders.xlsx


Run:

docker-compose up --build -d




