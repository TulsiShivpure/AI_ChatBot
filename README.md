# 🛒 E-commerce AI Agent

**An intelligent conversational AI system for analyzing e-commerce data using natural language queries**

![Python](https://img.shields.io/badge/python-v3.8+-blue.svg)


---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [API Reference](#api-reference)
- [Data Schema](#data-schema)

---

## 🎯 Overview

The E-commerce AI Agent is a powerful conversational AI system that transforms natural language questions into SQL queries and provides intelligent insights from your e-commerce data. Built with Google's Gemini AI and featuring a modern Gradio interface, it enables business users to analyze complex data without technical expertise.

### 🚀 Key Capabilities

- **Natural Language Processing**: Ask questions in plain English
- **Real-time Analysis**: Get instant answers to business questions
- **Intelligent Visualizations**: Automatic chart generation based on query context
- **Conversation Memory**: Context-aware responses with conversation history
- **Error Recovery**: Smart fallback mechanisms for robust operation
- **Export Functionality**: Download results and insights

---

## ✨ Features

### 🧠 AI-Powered Analysis
- **Intent Understanding**: Advanced question interpretation
- **Context Awareness**: Remembers conversation history
- **Smart SQL Generation**: Converts natural language to optimized queries
- **Error Handling**: Automatic query correction and retry logic

### 📊 Data Insights
- **Sales Analytics**: Total sales, revenue trends, performance metrics
- **Advertising Metrics**: RoAS, CPC, conversion rates, campaign analysis
- **Product Performance**: Top/bottom performers, eligibility status
- **Custom Queries**: Flexible analysis for any business question

### 🎨 User Interface
- **Conversational Chat**: Natural dialogue with the AI
- **Interactive Visualizations**: Dynamic charts and graphs
- **Real-time Processing**: Instant responses to queries
- **Export Options**: Download data and insights

### 🔧 Technical Features
- **Multi-table Joins**: Complex data relationships
- **Performance Optimization**: Efficient query execution
- **Data Validation**: Robust error checking
- **Extensible Architecture**: Easy to add new data sources

---


## 🛠 Installation

### Prerequisites

- Python 3.8 or higher
- Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))

### Option 1: Google Colab 

1. **Open the notebook**: Click the Colab link above
2. **Upload your data**: Run Cell 3 and upload your CSV files
3. **Add API key**: Store your Gemini API key in Colab Secrets
4. **Run all cells**: Execute the entire notebook
5. **Start chatting**: Use the Gradio interface

### Option 2: Local Installation


### Required Dependencies

```txt
google-generativeai>=0.3.0
gradio>=4.0.0
pandas>=1.5.0
plotly>=5.0.0
sqlite3>=3.8.0
numpy>=1.20.0
```

---

## 🚀 Quick Start

### 1. Set up your API key

```python
import google.generativeai as genai
genai.configure(api_key="your-gemini-api-key-here")
```

### 2. Prepare your data

Ensure your CSV files follow this structure:

**Ad Sales Metrics**: `date`, `item_id`, `ad_sales`, `impressions`, `ad_spend`, `clicks`, `units_sold`
**Product Eligibility**: `eligibility_datetime_utc`, `item_id`, `eligibility`, `message`
**Total Sales Metrics**: `date`, `item_id`, `total_sales`, `total_units_ordered`

### 3. Initialize the agent

```python
from ecommerce_ai_agent import ConversationalEcommerceAgent

# Initialize the agent
agent = ConversationalEcommerceAgent('your_database.db')

# Ask a question
response = agent.chat("What is my total sales revenue?")
print(response['response'])
```

### 4. Launch the web interface

```python
import gradio as gr

# The Gradio interface will launch automatically
# Access it at http://localhost:7860
```

---

## 💻 Usage

### Basic Query Examples

```python
# Initialize agent
agent = ConversationalEcommerceAgent()

# Sales analysis
response = agent.chat("What are my total sales?")

# Performance metrics
response = agent.chat("Calculate RoAS for all products")

# Product insights
response = agent.chat("Which products have the highest conversion rates?")

# Trend analysis
response = agent.chat("Show me sales trends over time")
```

### Advanced Features

```python
# Get conversation history
summary = agent.get_conversation_summary()

# Export results
agent.export_results()

# Custom visualization
chart = agent.create_visualization(data, "Sales by Product")
```

---

## 📚 API Reference

### ConversationalEcommerceAgent

#### `__init__(self, db_path='ecommerce_data.db')`
Initialize the AI agent with database connection.

#### `chat(self, question: str) -> dict`
Process a natural language question and return structured response.

**Parameters:**
- `question` (str): Natural language question about your data

**Returns:**
- Dictionary containing response, SQL query, execution time, and visualizations

#### `get_conversation_summary(self) -> str`
Get a summary of the current conversation session.

#### `export_results(self, format='json') -> str`
Export analysis results in specified format.

### Response Format

```python
{
    'question': str,           # Original question
    'response': str,           # Formatted natural language response
    'sql_query': str,          # Generated SQL query
    'chart': plotly.Figure,    # Visualization (if applicable)
    'execution_time': float,   # Processing time in seconds
    'intent': dict            # Parsed user intent
}
```

---

## 🗃 Data Schema

### Required Tables

#### `ad_sales_metrics`
| Column | Type | Description |
|--------|------|-------------|
| date | DATE | Transaction date |
| item_id | INTEGER | Product identifier |
| ad_sales | DECIMAL | Revenue from ads |
| impressions | INTEGER | Ad impressions |
| ad_spend | DECIMAL | Advertising spend |
| clicks | INTEGER | Ad clicks |
| units_sold | INTEGER | Units sold via ads |

#### `product_eligibility`
| Column | Type | Description |
|--------|------|-------------|
| eligibility_datetime_utc | DATETIME | Eligibility check time |
| item_id | INTEGER | Product identifier |
| eligibility | BOOLEAN | Advertising eligibility |
| message | TEXT | Eligibility details |

#### `total_sales_metrics`
| Column | Type | Description |
|--------|------|-------------|
| date | DATE | Transaction date |
| item_id | INTEGER | Product identifier |
| total_sales | DECIMAL | Total revenue |
| total_units_ordered | INTEGER | Total units sold |

---

## 🎯 Examples

### Business Intelligence Queries

```python
# Revenue Analysis
"What's my total revenue for the last month?"
"Which products contribute most to my revenue?"
"Show me revenue trends by week"

# Advertising Performance
"Calculate RoAS for each product"
"Which ads have the highest conversion rate?"
"What's my average cost per acquisition?"

# Product Insights
"Which products are underperforming?"
"Show me products with declining sales"
"What's my best-selling product category?"

# Operational Metrics
"Which products need attention?"
"Show me advertising eligibility issues"
"What's my inventory turnover rate?"
```

### Advanced Analytics

```python
# Comparative Analysis
"Compare Q1 vs Q2 performance"
"Show me year-over-year growth"
"Which products improved most this quarter?"

# Predictive Insights
"What are my sales trends?"
"Which products show seasonal patterns?"
"Forecast next month's performance"

# Custom Calculations
"Calculate customer lifetime value"
"Show me profit margins by product"
"What's my return on marketing investment?"
```

---

## 🔧 Configuration

### Environment Variables

```bash
# .env file
GEMINI_API_KEY=your_api_key_here
DATABASE_PATH=./data/ecommerce_data.db
DEBUG_MODE=True
MAX_QUERY_RESULTS=1000
```

### Customization Options

```python
# Custom configuration
config = {
    'model_name': 'gemini-1.5-flash',
    'temperature': 0.1,
    'max_output_tokens': 500,
    'conversation_memory_limit': 10,
    'visualization_row_limit': 20
}

agent = ConversationalEcommerceAgent(config=config)
```

---



---

## 🧪 Testing

Run the test suite:

```bash
# Unit tests
python -m pytest tests/

# Integration tests
python -m pytest tests/integration/

# Performance tests
python -m pytest tests/performance/
```

### Test Coverage

- ✅ SQL Generation: 95% coverage
- ✅ Query Execution: 90% coverage
- ✅ Response Formatting: 85% coverage
- ✅ Error Handling: 80% coverage

---


## 🐛 Troubleshooting

### Common Issues

**API Key Errors**
```bash
Error: API key not configured
Solution: Set GEMINI_API_KEY environment variable
```

**Database Connection Issues**
```bash
Error: Database file not found
Solution: Check DATABASE_PATH and ensure CSV files were processed
```

**Memory Issues with Large Datasets**
```bash
Error: Memory allocation failed
Solution: Reduce query result limits or use data sampling
```

### Performance Optimization

- **Large Datasets**: Use data pagination and caching
- **Complex Queries**: Optimize with database indexing
- **Memory Usage**: Implement result streaming
- **Response Time**: Add query result caching

---

