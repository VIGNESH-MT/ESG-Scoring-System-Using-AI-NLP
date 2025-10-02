# 🌱 ESG Scoring System Using AI & NLP

A comprehensive Python-based ESG (Environmental, Social, and Governance) scoring system that uses advanced AI and Natural Language Processing to analyze company performance from text data.

## 🚀 Features

- **FinBERT Sentiment Analysis**: Extract sentiment from company reports and news articles using state-of-the-art financial language models
- **ESG Scoring Pipeline**: Combine sentiment scores with ESG-specific metrics for comprehensive evaluation
- **Network Analysis**: Visualize company relationships and analyze ESG influence using NetworkX
- **Interactive Dashboard**: Streamlit-based web interface for easy data upload and visualization
- **Benchmarking**: Compare ESG performance against industry standards
- **Modular Architecture**: Clean, extensible codebase with separate modules for each component

## 📋 Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Features Overview](#features-overview)
- [API Reference](#api-reference)
- [Example Datasets](#example-datasets)
- [Contributing](#contributing)
- [License](#license)

## 🛠️ Installation

### Prerequisites

- Python 3.8 or higher
- pip package manager
- At least 4GB RAM (for FinBERT model)

### Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd esg-scoring-system
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Create necessary directories**
```bash
mkdir -p output models
```

4. **Download FinBERT model** (optional - will download automatically on first use)
```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification
tokenizer = AutoTokenizer.from_pretrained("ProsusAI/finbert")
model = AutoModelForSequenceClassification.from_pretrained("ProsusAI/finbert")
```

## 🚀 Quick Start

### 1. Run the Demo
```bash
python main.py --mode demo
```

### 2. Launch the Streamlit Dashboard
```bash
streamlit run streamlit_app.py
```

### 3. Analyze Your Own Data
```bash
python main.py --mode text --input your_data.csv --text-column content
```

## 📖 Usage

### Command Line Interface

The system provides a command-line interface for batch processing:

```bash
# Text analysis
python main.py --mode text --input data/company_reports.csv --text-column text_content

# Network analysis
python main.py --mode network --input data/relationships.csv

# Run demo
python main.py --mode demo
```

### Streamlit Dashboard

Launch the interactive dashboard:

```bash
streamlit run streamlit_app.py
```

The dashboard provides:
- **Text Analysis**: Upload CSV files and analyze ESG sentiment
- **Network Analysis**: Visualize company relationships and influence
- **Benchmarking**: Compare scores against industry standards
- **Sample Data Demo**: Explore with pre-loaded datasets

### Python API

Use the components programmatically:

```python
from src.sentiment_analyzer import ESGSentimentAnalyzer
from src.esg_scorer import ESGScorer
from src.network_analyzer import CompanyNetworkAnalyzer

# Initialize components
analyzer = ESGSentimentAnalyzer()
scorer = ESGScorer()
network = CompanyNetworkAnalyzer()

# Analyze text
text = "Apple is committed to carbon neutrality by 2030"
sentiment = analyzer.analyze_esg_sentiment(text)
print(sentiment)

# Calculate ESG score
esg_scores = scorer.calculate_overall_esg_score(sentiment['sentiment'])
print(esg_scores)
```

## 📁 Project Structure

```
esg-scoring-system/
├── src/                          # Source code modules
│   ├── __init__.py
│   ├── sentiment_analyzer.py     # FinBERT sentiment analysis
│   ├── esg_scorer.py            # ESG scoring pipeline
│   ├── network_analyzer.py      # NetworkX company relationships
│   └── utils.py                 # Utility functions
├── data/                        # Sample datasets
│   ├── sample_company_reports.csv
│   ├── sample_news_articles.csv
│   └── sample_company_relationships.csv
├── output/                      # Analysis results
├── models/                      # Cached models
├── examples/                    # Example scripts
├── streamlit_app.py            # Streamlit dashboard
├── main.py                     # Command-line interface
├── config.py                   # Configuration settings
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

## 🔧 Features Overview

### 1. FinBERT Sentiment Analysis

- **Model**: ProsusAI/finbert - specialized for financial text
- **Capabilities**: 
  - Sentiment classification (positive, negative, neutral)
  - ESG keyword detection and categorization
  - Batch processing for large datasets
  - Confidence scores and compound sentiment

### 2. ESG Scoring Pipeline

- **Scoring Components**:
  - Environmental (40% weight): Climate, emissions, sustainability
  - Social (30% weight): Employee relations, community impact
  - Governance (30% weight): Board structure, ethics, compliance
- **Features**:
  - Weighted scoring with customizable weights
  - Industry benchmarking
  - Score interpretation and ratings
  - Trend analysis over time

### 3. Network Analysis

- **NetworkX Integration**:
  - Company relationship mapping
  - Centrality measures (degree, betweenness, eigenvector)
  - ESG influence propagation
  - Community detection and clustering
- **Visualizations**:
  - Interactive network graphs
  - Centrality analysis plots
  - Risk propagation modeling

### 4. Interactive Dashboard

- **Streamlit Features**:
  - File upload and processing
  - Real-time analysis results
  - Interactive visualizations with Plotly
  - Export functionality
  - Multi-page navigation

## 📊 API Reference

### ESGSentimentAnalyzer

```python
class ESGSentimentAnalyzer:
    def analyze_sentiment(text: str) -> Dict[str, float]
    def analyze_esg_sentiment(text: str) -> Dict[str, any]
    def analyze_dataframe(df: pd.DataFrame, text_column: str) -> pd.DataFrame
```

### ESGScorer

```python
class ESGScorer:
    def calculate_overall_esg_score(sentiment_data: Dict) -> Dict[str, float]
    def score_dataframe(df: pd.DataFrame) -> pd.DataFrame
    def generate_esg_report(df: pd.DataFrame, company_name: str) -> Dict
```

### CompanyNetworkAnalyzer

```python
class CompanyNetworkAnalyzer:
    def add_company(company_id: str, company_data: Dict)
    def add_relationship(company1: str, company2: str, relationship_type: str, weight: float)
    def calculate_esg_influence_scores() -> Dict[str, float]
    def get_network_statistics() -> Dict
```

## 📈 Example Datasets

The system includes sample datasets for testing:

### Company Reports (`data/sample_company_reports.csv`)
- 10 sample sustainability and ESG reports
- Companies: Apple, Microsoft, Tesla, ExxonMobil, JPMorgan, etc.
- Columns: company_name, report_type, date, text_content

### News Articles (`data/sample_news_articles.csv`)
- 10 ESG-related news articles
- Positive and negative sentiment examples
- Columns: company_name, headline, date, content, source

### Company Relationships (`data/sample_company_relationships.csv`)
- 15 company relationship mappings
- Relationship types: competitor, supplier, customer, partner
- Columns: company1, company2, relationship_type, strength, description

## 🎯 Use Cases

### 1. Investment Analysis
- Analyze ESG performance of potential investments
- Compare companies within industry sectors
- Track ESG trends over time

### 2. Risk Management
- Identify ESG-related risks in supply chains
- Monitor sentiment changes in real-time
- Assess reputational risk factors

### 3. Compliance Monitoring
- Track ESG disclosure quality
- Monitor regulatory compliance
- Generate ESG performance reports

### 4. Research and Academia
- Study ESG sentiment patterns
- Analyze network effects in ESG performance
- Benchmark scoring methodologies

## ⚙️ Configuration

Customize the system behavior by modifying `config.py`:

```python
# Model settings
FINBERT_MODEL = "ProsusAI/finbert"
MAX_TEXT_LENGTH = 512

# ESG category weights
ESG_WEIGHTS = {
    'environmental': 0.4,
    'social': 0.3,
    'governance': 0.3
}

# ESG keywords for categorization
ESG_CATEGORIES = {
    'environmental': ['climate', 'carbon', 'emission', 'renewable'],
    'social': ['employee', 'diversity', 'community', 'safety'],
    'governance': ['board', 'ethics', 'compliance', 'transparency']
}
```

## 🔍 Advanced Usage

### Custom ESG Weights

```python
from src.esg_scorer import ESGScorer

# Custom weights for specific analysis
custom_weights = {
    'environmental': 0.6,  # Higher emphasis on environmental
    'social': 0.2,
    'governance': 0.2
}

scorer = ESGScorer(weights=custom_weights)
```

### Batch Processing

```python
import pandas as pd
from src.sentiment_analyzer import ESGSentimentAnalyzer

# Load large dataset
df = pd.read_csv('large_dataset.csv')

# Process in batches
analyzer = ESGSentimentAnalyzer()
results = analyzer.analyze_esg_dataframe(df, 'text_column')
```

### Network Risk Analysis

```python
from src.network_analyzer import CompanyNetworkAnalyzer

analyzer = CompanyNetworkAnalyzer()
# ... build network ...

# Analyze risk propagation
risk_scores = analyzer.calculate_esg_risk_propagation('COMPANY_A', 85.0)
print(risk_scores)
```

## 🚨 Troubleshooting

### Common Issues

1. **Model Loading Errors**
   - Ensure sufficient RAM (4GB+)
   - Check internet connection for model download
   - Try clearing model cache: `rm -rf ~/.cache/huggingface/`

2. **Memory Issues**
   - Reduce batch size in config
   - Process data in smaller chunks
   - Use CPU instead of GPU if memory limited

3. **Import Errors**
   - Verify all dependencies installed: `pip install -r requirements.txt`
   - Check Python version (3.8+ required)
   - Ensure src directory in Python path

### Performance Optimization

- **Use GPU**: Install PyTorch with CUDA support for faster processing
- **Batch Processing**: Process multiple texts simultaneously
- **Model Caching**: Models are cached after first download
- **Parallel Processing**: Use multiprocessing for large datasets

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and add tests
4. Commit your changes: `git commit -am 'Add feature'`
5. Push to the branch: `git push origin feature-name`
6. Submit a pull request

### Development Setup

```bash
# Install development dependencies
pip install -r requirements.txt
pip install pytest black flake8

# Run tests
pytest tests/

# Format code
black src/ streamlit_app.py main.py

# Lint code
flake8 src/ streamlit_app.py main.py
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **FinBERT Model**: ProsusAI for the financial sentiment analysis model
- **Streamlit**: For the excellent web app framework
- **NetworkX**: For network analysis capabilities
- **Hugging Face**: For transformer model hosting and tools

## 📞 Support

For questions, issues, or contributions:

- Create an issue on GitHub
- Check the documentation
- Review example notebooks
- Join our community discussions

---

**Built with ❤️ for ESG analysis and sustainable investing**
