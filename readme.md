# Fixr Bot

An automated system for ticket purchasing on the Fixr platform, consisting of multiple interconnected components for event discovery, account management, and ticket acquisition.

## ⚠️ Important Legal and Ethical Notice

This project is for **educational and research purposes only**. Using this bot may:
- Violate Fixr's Terms of Service
- Be against venue policies
- Potentially be illegal in some jurisdictions
- Create unfair advantages over regular users

**Use at your own risk and responsibility.**

## 🏗️ Project Architecture

The system consists of four main components:

### 1. Web Scraper (`web_scraper/`)
- **Purpose**: Discovers and extracts event information from Fixr
- **Technology**: Python with BeautifulSoup and requests
- **Output**: `events.json` containing event dates, URLs, and IDs

### 2. Credential Generator (`credential_generator/`)
- **Purpose**: Generates realistic user credentials for account creation
- **Technology**: Python with pandas
- **Features**: 
  - Random name generation from CSV datasets
  - Secure password generation with words + numbers + symbols
  - Realistic birthday generation (2000-2004)
  - Phone number generation in format 7XX-XXX-XXXX
- **Output**: `credentials.csv` and `credentials_record.csv`

### 3. Account Creation (`account_creation/`)
- **Purpose**: Automates user account registration on Fixr
- **Technology**: Python with Selenium WebDriver
- **Features**: 
  - Automated form filling
  - Error handling with screenshot capture
  - Success tracking in CSV format
- **Output**: `unused_accounts.csv`

### 4. Ticket Purchasing (`main/`)
- **Purpose**: Core bot functionality for ticket acquisition
- **Technology**: Go with custom Fixr API package
- **Features**: 
  - Interactive event and ticket selection
  - Multi-account ticket purchasing
  - Real-time event detail fetching

## 📋 Prerequisites

### Software Requirements
- **Python 3.7+** with pip
- **Go 1.16+**
- **Google Chrome** or Chromium browser
- **ChromeDriver** (compatible with your Chrome version)

### Python Dependencies
```
pandas
selenium
requests
beautifulsoup4
```

### Go Dependencies
- `github.com/sneakypanda17/fixr` (Custom Fixr API package)

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/sneakypanda17/fixr_bot.git
   cd fixr_bot
   ```

2. **Set up Python environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Install Go dependencies**
   ```bash
   cd main/
   go mod tidy
   ```

4. **Download ChromeDriver**
   - Download from [ChromeDriver Downloads](https://chromedriver.chromium.org/)
   - Update the path in `account_creation/account_creation.py`

## 📚 Usage Workflow

### Step 1: Generate Credentials
```bash
cd credential_generator/
python credential_generator.py
```
This creates fake user credentials for account creation.

### Step 2: Scrape Events
```bash
cd web_scraper/
python web_scraper.py
```
This discovers available events and saves them to `events.json`.

### Step 3: Create Accounts
```bash
cd account_creation/
python account_creation.py
```
This automatically registers accounts on Fixr using generated credentials.

### Step 4: Purchase Tickets
```bash
cd main/
go run main.go
```
This runs the main bot for ticket purchasing using created accounts.

## 📁 Project Structure

```
fixr_bot/
├── web_scraper/
│   ├── web_scraper.py          # Event discovery script
│   └── events.json             # Scraped event data
├── credential_generator/
│   ├── raw_data/               # Name and word datasets
│   │   ├── firstnames.csv
│   │   ├── surnames.csv
│   │   └── words.csv
│   ├── credential_generator.py # Credential generation script
│   ├── credentials.csv         # Current batch credentials
│   └── credentials_record.csv  # Historical credential log
├── account_creation/
│   ├── account_creation.py     # Selenium automation script
│   └── unused_accounts.csv     # Successfully created accounts
├── main/
│   ├── main.go                 # Core ticket purchasing bot
│   └── main.exe                # Compiled executable
├── requirements.txt            # Python dependencies
├── .gitignore                  # Git ignore rules
├── LICENSE.txt                 # MIT License
└── README.md                   # This file
```

## ⚙️ Configuration

### ChromeDriver Path
Update the ChromeDriver path in `account_creation/account_creation.py`:
```python
chromedriver_path = r"C:\path\to\your\chromedriver.exe"
```

### Credential Generation
Modify `credential_generator.py` to adjust:
- Number of credentials generated
- Email domain (default: yahoo.com)
- Password complexity
- Phone number format

### Web Scraper Target
The scraper currently targets Timepiece organizer events. Modify the URL in `web_scraper.py` to target different organizers.

## 🔧 Technical Details

### Error Handling
- **Account Creation**: Screenshots saved on failure
- **Ticket Purchasing**: Graceful handling of login failures
- **Web Scraping**: HTTP status code validation

### Data Flow
1. Raw data (names, words) → Credential Generator
2. Generated credentials → Account Creation
3. Created accounts → Ticket Purchasing
4. Event data → Ticket Purchasing

### Security Considerations
- Passwords include words, numbers, and symbols
- User agents simulate real browser requests
- Chrome options configured for automated browsing

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/enhancement`)
3. Commit changes (`git commit -m 'Add enhancement'`)
4. Push to branch (`git push origin feature/enhancement`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the `LICENSE.txt` file for details.

## ⚠️ Disclaimer

This software is provided "as is" without warranty. The authors are not responsible for any misuse, damages, or legal consequences resulting from the use of this software. Users are solely responsible for ensuring their use complies with applicable laws and terms of service.

## 🔗 Dependencies

- [Selenium WebDriver](https://selenium-python.readthedocs.io/)
- [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/)
- [Pandas](https://pandas.pydata.org/)
- [Go](https://golang.org/)

---

**Note**: This project was created for educational purposes to demonstrate automation techniques. Please use responsibly and in accordance with all applicable terms of service and laws.
