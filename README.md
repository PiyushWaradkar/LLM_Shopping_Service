# Email Classification and Shopping Response Pipeline

This repository provides a complete pipeline for classifying customer emails and generating relevant, intelligent responses using Large Language Models (LLMs), regex, keywords, FAISS-based vector search, and translation for multilingual support.

# ✨ Features

  LLM Email Classification with Structured Prompts
  
  Fallback Mechanisms Using Regex and Keyword Rules
  
  Order Handling: Details Extraction + Product Recommendation
  
  Inquiry Handling: Embedding Search + Language Translation
  
  LLM-Driven Response Generation
  
  Spreadsheet Updates for Tracking


# ⚙️ Components and Functions

  1. LLM Connectivity
  
    verify_ollama()
    
    Checks if the Ollama LLM API is reachable using a test prompt.
  
  2. Data Loading
  
  load_data()
  
    Loads products and emails from Google Sheets using public links.
  
  3. Email Classification
  
    EmailClassifier
    
    Uses ollama_generate() to classify each email.
    
    Falls back on _regex_classification() and _keyword_fallback() when LLM fails.
  
  4. Order Handling Path
  
    _extract_order_details()
    
    Extracts product names, quantities, and customer intent.
    
    _suggest_alternatives()
    
    Uses FAISS for semantic similarity search on product embeddings.
    
    generate_order_response()
    
    Uses LLM to generate a structured, friendly response based on matched and alternative products.
  
  5. Product Inquiry Path
  
    handle_inquiry()
    
    Detects email language
    
    Translates non-English text
    
    Embedding-based search using product descriptions
    
    Generates final response using LLM
  
  6. Spreadsheet Update
  
    generate_spreadsheet()
    
    Outputs processed results (responses, classifications, metadata) to an Excel file using openpyxl

📂 Requirements

  Python 3.10+
  
  Libraries: pandas, numpy, faiss-cpu, requests, openpyxl, tqdm
  
  Install dependencies:
  
  pip install pandas numpy faiss-cpu requests openpyxl tqdm

📃 Example Usage

  verify_ollama()
  products, emails = load_data()
  classifier = EmailClassifier()
  classified = classifier.classify_all(emails)
  # Automatically routes to order or inquiry flow based on classification

🔍 Notes

  The Ollama endpoint must be publicly accessible and valid for the model to respond
  
  Product embeddings can be extended with domain-specific data
  
  Translation layer enables internationalization
  
  Designed to scale with more use-case types by adding routing logic

