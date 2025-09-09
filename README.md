# Scraper B3

A high-performance Python pipeline to collect, process, and store Brazilian stock market (B3) data from StatusInvest and TradingView. Built for research and educational purposes with multithreading support for faster data collection.

## Features
- **Comprehensive Data Collection**: Scrapes 50+ financial metrics from StatusInvest and TradingView
- **Sector Information**: Gets sector, sub-sector, and segment classification
- **Historical Analysis**: Captures tag along rights, historical returns, dividends, and dividend yields
- **Performance Indicators**: Calculates fundamentalist indicators (Graham Price, Bazin Price, SGR, EBIT, etc.)
- **Multithreading Support**: Parallel processing with configurable worker threads for faster execution
- **Data Processing**: Cleans and normalizes data automatically with fragmentation-free operations
- **Multiple Export Formats**: Stores results in JSONL and MySQL formats
- **Timestamped Records**: Adds scrape timestamp for each record
- **Dynamic Columns**: Handles annual data (liquidity, dividends, revenue) across multiple years

## Requirements
- Python 3.10+
- MySQL Server 8.0+
- Chrome/Chromium browser
- Required Python packages (see `requirements.txt`)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/heitorrosa/scraper-b3
   cd scraper-b3
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create environment configuration:
   ```bash
   # Create .env file with your MySQL credentials
   MYSQL_USER=your_username
   MYSQL_PASSWORD=your_password
   MYSQL_HOST=localhost
   MYSQL_DATABASE=scraper_b3
   ```

## Usage

### Basic Usage
```bash
python src/scraper.py
```

### Configuration Options
Edit the script configuration section to customize:

```python
# Script Configuration
saveToMYSQL = True      # Export to MySQL database
saveAsJSONL = True      # Export to JSON file
MAX_WORKERS = 6         # Number of parallel threads (adjust based on your system)
```

## Data Sources
- **StatusInvest**: Financial metrics, sector data, TAG along, dividends, revenue data
- **TradingView**: Historical performance and returns data

## Output Structure

### JSON Export (`b3_stocks.json`)
```json
{
  "TICKER": "PETR4",
  "SETOR": "Petróleo, Gás e Biocombustíveis",
  "SUBSETOR": "Petróleo",
  "SEGMENTO": "Exploração, Refino e Distribuição",
  "PRECO": 34.21,
  "DY": 8.73,
  "TAG ALONG": 100,
  "RENT_12_MESES": 28.5,
  "RENT_MEDIA_5_ANOS": 15.2,
  "DY_MEDIO_5_ANOS": 9.1,
  "PRECO_DE_GRAHAM": 45.67,
  "PRECO_DE_BAZIN": 52.34,
  "EBIT": 123456789.0,
  "SGR": 12.5,
  "DIVIDENDOS_2023": 2.34,
  "DIVIDENDOS_2022": 2.10,
  "DY_2023": 7.89,
  "DY_2022": 6.45,
  "RECEITA_LIQUIDA_2023": 987654321.0,
  "LUCRO_LIQUIDO_2023": 123456789.0,
  "TIME": "2024-12-09 14:30:00"
}
```

### MySQL Export
Data is stored in the `b3_stocks` table with the same structure as JSON, automatically handling:
- Data type conversion
- NULL values for missing data
- Timestamp indexing
- Incremental updates

## File Structure
```
scraper-b3/
├── src/
│   ├── scraper.py              # Main multithreaded script
│   ├── scraper-singlethread.py # Single-threaded version
│   └── cache/                  # Temporary download files
├── .env                        # Database configuration
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

## License
GPL 3.0 MODIFIED Mansa Team's License. See LICENSE for details.