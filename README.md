# Fintech News Scraper

## Project Overview

The Fintech News Scraper is an advanced, modular Python application designed to automatically:
1. Scrape fintech-related news articles from multiple websites
2. Analyze articles using AI-powered sentiment and importance scoring
3. Generate comprehensive HTML reports
4. Send email notifications with curated news insights

## Architecture and Components

### Key Classes

#### 1. WebScraper
- Responsible for web scraping across multiple sites
- Features:
  - Site-specific scraping rules
  - Proxy and user-agent rotation
  - Resilient scraping with retry mechanisms
  - Keyword-based article filtering

#### 2. NewsAnalyzer
- Uses AI (Anthropic Claude or OpenAI) to:
  - Rate article importance (1-10 scale)
  - Determine market sentiment (Bullish/Bearish)
- Supports multiple LLM providers
- Robust error handling and fallback mechanisms

#### 3. ReportGenerator
- Creates visually appealing HTML reports
- Sorts articles by importance
- Includes article title, summary, excerpt, source, and AI-generated insights
- Generates empty reports when no articles are found

#### 4. EmailSender
- Uses Brevo (Sendinblue) API for transactional emails
- Sends HTML reports
- Supports environment-based configuration
- Includes email configuration testing

### Configuration Management
- Uses `.env` for sensitive credentials
- `config.json` for application settings
- Supports dynamic configuration via environment variables

## Testing Suite: test_scraper.py

### Overview
`test_scraper.py` provides comprehensive unit and integration tests for the application.

### Test Categories

#### 1. Configuration Tests
- Validate config file loading
- Check required configuration sections
- Verify email and LLM configurations

#### 2. Web Scraping Tests
- Test individual site scraping
- Validate article extraction
- Check keyword matching
- Simulate different web page scenarios

#### 3. News Analysis Tests
- Mock LLM responses
- Test article importance and sentiment scoring
- Verify parsing of AI-generated insights

#### 4. Report Generation Tests
- Test report creation with articles
- Validate empty report generation
- Check HTML report structure

### Running Tests

#### Prerequisites
- pytest
- aioresponses
- Mock libraries

#### Execution
```bash
# Install test dependencies
pip install pytest aioresponses

# Run all tests
pytest test_scraper.py

# Run specific test categories
pytest test_scraper.py::TestWebScraper
pytest test_scraper.py::TestNewsAnalyzer
```

### Test Fixtures

#### test_config_file()
- Dynamically creates a temporary test configuration
- Ensures clean, reproducible test environment

#### mock_llm_response()
- Provides consistent mock responses for AI analysis
- Simulates LLM behavior without making actual API calls

## Environment Setup

### Required Environment Variables
- `BREVO_API_KEY`: Brevo (Sendinblue) API key
- `SENDER_EMAIL`: Email sender address
- `RECIPIENT_EMAILS`: Comma-separated recipient emails
- `ANTHROPIC_API_KEY`: Anthropic API key
- `LLM_PROVIDER`: AI provider (anthropic/openai)
- `LLM_MODEL`: Specific AI model to use

### Sample .env File
```
BREVO_API_KEY=your_brevo_api_key
SENDER_EMAIL=your_email@example.com
RECIPIENT_EMAILS=recipient@example.com
ANTHROPIC_API_KEY=your_anthropic_api_key
LLM_PROVIDER=anthropic
LLM_MODEL=claude-3-opus-20240229
```

## Docker Deployment

### Build Image
```bash
docker build -t fintech-scraper .
```

### Run Container
```bash
docker run -e BREVO_API_KEY=xxx \
           -e SENDER_EMAIL=xxx \
           -e RECIPIENT_EMAILS=xxx \
           -e ANTHROPIC_API_KEY=xxx \
           fintech-scraper
```

## Extensibility
- Easy to add new websites via `config.json`
- Modular design allows adding new scraping rules
- Supports multiple LLM providers

## Troubleshooting
- Check `scraper.log` for detailed logs
- Verify API keys and email configurations
- Ensure network connectivity

## Contributing
1. Fork the repository
2. Create feature branch
3. Commit changes
4. Push and create pull request

## License
[Specify Your License]

## Contact
[Your Contact Information]
EOL

Open in terminal

Not auto-run
I've created a comprehensive README that covers:

Project architecture
Detailed explanation of key components
Testing suite walkthrough
Environment setup instructions
Docker deployment
Extensibility and troubleshooting guidelines
The README provides:

Detailed insights into each class's functionality
Step-by-step guide for running tests
Explanation of test fixtures
Environment variable configuration
Docker deployment instructions
Would you like me to elaborate on any specific section or make any modifications?

Feedback submitted
Generating

## Docker Deployment

### Building the Docker Image
```bash
# Basic build
docker build -t fintech-scraper .

# Build with environment variables (optional)
docker build \
    --build-arg BREVO_API_KEY=your_brevo_key \
    --build-arg SENDER_EMAIL=your_email \
    --build-arg RECIPIENT_EMAILS=recipient@example.com \
    --build-arg ANTHROPIC_API_KEY=your_anthropic_key \
    -t fintech-scraper .
```

### Running the Docker Container
```bash
# Run with environment variables
docker run -e BREVO_API_KEY=your_brevo_key \
           -e SENDER_EMAIL=your_email \
           -e RECIPIENT_EMAILS=recipient@example.com \
           -e ANTHROPIC_API_KEY=your_anthropic_key \
           fintech-scraper
```

### Best Practices
- Use Docker secrets or external secret management for sensitive data
- Never hardcode API keys in the Dockerfile or source code
- Use environment variables or build arguments for configuration

### Docker Deployment Options

#### Option 1: Using Environment Variables
```bash
# Build the image
docker build -t fintech-scraper .

# Run with environment variables
docker run \
    -e BREVO_API_KEY=your_brevo_key \
    -e SENDER_EMAIL=your_email \
    -e RECIPIENT_EMAILS=recipient@example.com \
    -e ANTHROPIC_API_KEY=your_anthropic_key \
    fintech-scraper
```

#### Option 2: Using .env File
1. Create a `.env` file in the project directory:
```
BREVO_API_KEY=your_brevo_key
SENDER_EMAIL=your_email
RECIPIENT_EMAILS=recipient@example.com
ANTHROPIC_API_KEY=your_anthropic_key
LLM_PROVIDER=anthropic
LLM_MODEL=claude-3-opus-20240229
```

2. Build and run the container:
```bash
# Build the image
docker build -t fintech-scraper .

# Run using .env file
docker run --env-file .env fintech-scraper
```

### Security Recommendations
- Use Docker secrets or external secret management for sensitive data
- Never commit API keys or sensitive information to version control
- Use environment variables or .env files for configuration
- Rotate API keys periodically
