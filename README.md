# LegalBrief AI: Multi-Task Legal Document Analysis

An end-to-end NLP system for automated legal case classification and summarization, combining traditional ML classification with transformer-based abstractive summarization.

## Project Overview

LegalBrief AI is a production-ready legal tech application that analyzes legal case documents to:
1. **Classify** whether a case seeks class action status
2. **Categorize** cases into legal domain groups (Civil Rights, Criminal Justice, Social Welfare, Other)
3. **Summarize** lengthy legal documents into digestible briefs (long, short, or tiny formats)

The system processes raw legal text through custom NLP pipelines and delivers predictions via an interactive Streamlit web interface, containerized with Docker for easy deployment.

## Business Value

**For Legal Professionals:**
- **Time Savings**: Reduce document review time by 70%+ with automated summarization
- **Case Triage**: Instantly categorize incoming cases for proper routing to specialized teams
- **Risk Assessment**: Identify class action cases early for resource allocation

**For Law Firms:**
- **Scalability**: Process hundreds of cases simultaneously with batch inference
- **Consistency**: Eliminate human variability in initial case assessment
- **Cost Efficiency**: Reduce paralegal hours spent on preliminary document review

**Market Application:**
- Legal case management systems
- E-discovery platforms
- Court filing automation
- Legal research databases

## System Architecture

```
Legal Case Document (Raw Text)
         ↓
    Text Cleaning & Preprocessing
    (Domain-specific legal cleaning)
         ↓
    ┌────────────────────────────┐
    │   Multi-Task Prediction    │
    ├────────────────────────────┤
    │  1. Class Action Detection │ → Logistic Regression 
    │  2. Case Type Classification│ → Logistic Regression
    │  3. Abstractive Summarization│ → DistilBART Transformer
    └────────────────────────────┘
         ↓
    Streamlit Web Interface
    (Docker containerized)
```

## Summarization Model

**Model**: DistilBART-CNN-12-6 (Hugging Face)
- Distilled BART model fine-tuned on CNN/DailyMail
- Seq2Seq transformer for abstractive summarization

**Summarization Pipeline:**
1. Clean text with summarization-specific preprocessing
2. Chunk long documents (1,000 word chunks)
3. Summarize each chunk independently
4. Hierarchical summarization: combine chunk summaries → final summary
5. Post-processing: remove artifacts, normalize spacing

**Summary Styles:**
- **Long**: 350-600 tokens (comprehensive overview)
- **Short**: 100-250 tokens (executive summary)
- **Tiny**: 25-75 tokens (one-sentence brief)

**Optimization:**
- Batch processing for multiple documents
- GPU acceleration support
- Beam search (num_beams=4) for quality
- Repetition penalty (2.0) to reduce redundancy

##  Quick Start

### Installation & Running

```bash
# Clone the repository
git clone <repository-url>
cd LegalBrief-AI

# Build Docker image
docker build -t legalbrief-ai .

# Run the application
docker run -p 8501:8501 legalbrief-ai
```

Access the web interface at `http://localhost:8501`

### Using the Interactive Tool

1. **Input**: Paste text or upload a `.txt` file containing a legal case
2. **Select Summary Style**: Choose None, Long, Short, or Tiny
3. **Run Analysis**: Get instant predictions and optional summary
4. **Output**: 
   - Class Action Sought: Yes/No
   - Case Type Category
   - Generated summary (if requested)

##  Project Structure

```
LegalBrief-AI/
├── app/
│   ├── interactive_app.py          # Streamlit web interface
│   ├── model_runner.py             # Classification inference
│   ├── legal_summary.py            # Summarization pipeline
│   └── text_cleaning_module.py     # Text preprocessing utilities
├── notebook/
│   └── Text_Final_Modeling.ipynb   # Model training & evaluation
├── models/
│   ├── best_case_action_sought.joblib
│   └── best_case_type_model.joblib
├── Dockerfile                       # Container configuration
├── requirements.txt                 # Python dependencies
└── README.md
```

##  Tech Stack

- **ML/NLP**: scikit-learn, Transformers (Hugging Face), PyTorch
- **Data Processing**: pandas, NLTK
- **Web Framework**: Streamlit
- **Deployment**: Docker
- **Models**: Logistic Regression, DistilBART

  
## The Long Summarization Data Link

https://drive.google.com/file/d/1iUk9Fq2rtJ2SIcNO1VY-6L30-vK-CHVa/view?usp=drive_link

## The Short Summarization Data Link
https://drive.google.com/file/d/1KqHmN0MWO_J1phdk1bGQoQrVXZJ0fnkB/view?usp=drive_link

## The Short Summarization Data Link

https://drive.google.com/file/d/1chiBRz1A_6PmZnqnTFNEk0mP7yxzh_Am/view?usp=drive_link

## Link to the Presentation
https://nuwildcat-my.sharepoint.com/:p:/g/personal/jmf8305_ads_northwestern_edu/EbTW5CZuH4VHqQGCwAqHSngBz8HbnfYYBKxhg2znYX0hmw
