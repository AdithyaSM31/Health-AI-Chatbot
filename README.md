# Health AI Chatbot 🏥🤖

A Medical AI Chatbot powered by Retrieval Augmented Generation (RAG) that provides medical information and answers health-related questions using advanced AI technologies.

## Features

- 💬 Interactive chat interface for medical queries
- 🔍 RAG-based information retrieval from medical documents
- 🤖 Powered by Google Gemini 1.5 Flash LLM
- 📚 Vector storage using Pinecone for efficient document search
- 🎨 Clean and responsive web interface

## Technologies Used

- **Backend**: Flask (Python)
- **LLM**: Google Gemini 1.5 Flash
- **Embeddings**: HuggingFace Sentence Transformers (all-MiniLM-L6-v2)
- **Vector Database**: Pinecone
- **Framework**: LangChain
- **Document Processing**: PyPDF

## Prerequisites

- Python 3.11+
- Pinecone API Key
- Google API Key (for Gemini)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/AdithyaSM31/Health-AI-Chatbot.git
cd Health-AI-Chatbot
```

2. Create a virtual environment:
```bash
python -m venv myenv
```

3. Activate the virtual environment:
- Windows:
```bash
myenv\Scripts\activate
```
- Linux/Mac:
```bash
source myenv/bin/activate
```

4. Install required packages:
```bash
pip install -r requirements.txt
```

5. Create a `.env` file in the root directory and add your API keys:
```env
PINECONE_API_KEY=your_pinecone_api_key_here
GOOGLE_API_KEY=your_google_api_key_here
```

## Usage

1. Start the Flask application:
```bash
python app.py
```

2. Open your web browser and navigate to:
```
http://localhost:8080
```

3. Start asking medical questions in the chat interface!

## Project Structure

```
Health-AI-Chatbot/
├── app.py                 # Main Flask application
├── store_index.py        # Script to create vector index
├── requirements.txt      # Python dependencies
├── setup.py             # Setup configuration
├── .env                 # Environment variables (not in repo)
├── Data/                # Medical documents (PDF)
├── src/
│   ├── helper.py        # Helper functions for document processing
│   ├── prompt.py        # System prompts for the chatbot
│   └── __init__.py
├── static/              # CSS and static files
│   ├── style.css
│   └── styles.css
├── templates/           # HTML templates
│   └── chat.html
└── research/           # Research notebooks and experiments
    └── trials.ipynb
```

## How It Works

1. **Document Processing**: Medical documents (PDFs) are loaded and split into chunks
2. **Embedding**: Text chunks are converted to vector embeddings using HuggingFace models
3. **Vector Storage**: Embeddings are stored in Pinecone for efficient similarity search
4. **Query Processing**: User questions are embedded and similar document chunks are retrieved
5. **Response Generation**: Retrieved context + user question are sent to Gemini LLM for answer generation

## Important Notes

⚠️ **Disclaimer**: This chatbot is for informational purposes only and should not be used as a substitute for professional medical advice, diagnosis, or treatment. Always consult with a qualified healthcare provider for medical concerns.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

**Adithya SM**
- GitHub: [@AdithyaSM31](https://github.com/AdithyaSM31)

## Acknowledgments

- Medical documents used for training the RAG system
- LangChain community for the excellent framework
- Google for Gemini API
- Pinecone for vector database services
