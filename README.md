# Personal AI Knowledge Base

A local, privacy-first knowledge base system that allows you to upload documents (Markdown, PDF, Text) and chat with your knowledge using natural language.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

## Features

- 📁 **Multiple File Support**: Upload PDF, Markdown, TXT, DOCX, and HTML files
- 🧠 **AI-Powered Q&A**: Ask questions and get answers based on your documents
- 🔒 **Privacy First**: All data stored locally, no cloud uploads
- 🎨 **Modern UI**: Clean and intuitive interface built with React + TailwindCSS
- 🚀 **Fast Vector Search**: Powered by ChromaDB for efficient document retrieval

## Tech Stack

### Backend
- **Express.js** - Web framework
- **TypeScript** - Type-safe development
- **ChromaDB** - Local vector database
- **Claude API** - AI language model
- **pdf-parse** - PDF text extraction
- **mammoth** - DOCX text extraction

### Frontend
- **React 18** - UI library
- **Vite** - Build tool
- **TypeScript** - Type-safe development
- **TailwindCSS** - Styling
- **Zustand** - State management
- **React Router** - Navigation

## Prerequisites

- Node.js 16+ and npm
- Claude API key (get one from [Anthropic](https://www.anthropic.com/api))
- Modern web browser

## Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd personal-knowledge-base
   ```

2. **Set up environment variables**
   ```bash
   # Copy the example file
   cp .env.example .env

   # Edit .env and add your Claude API key
   CLAUDE_API_KEY=your_api_key_here
   ```

3. **Install backend dependencies**
   ```bash
   cd server
   npm install
   ```

4. **Install frontend dependencies**
   ```bash
   cd ../client
   npm install
   ```

## Usage

### Development Mode

1. **Start the backend server**
   ```bash
   cd server
   npm run dev
   ```
   The server will run on `http://localhost:3000`

2. **Start the frontend development server**
   ```bash
   cd client
   npm run dev
   ```
   The app will be available at `http://localhost:5173`

3. **Open your browser** and navigate to `http://localhost:5173`

### Production Mode

1. **Build the frontend**
   ```bash
   cd client
   npm run build
   ```

2. **Start the production server**
   ```bash
   cd server
   npm run build
   npm start
   ```

## Project Structure

```
personal-knowledge-base/
├── client/                 # Frontend React app
│   ├── src/
│   │   ├── components/     # React components
│   │   ├── services/       # API services
│   │   ├── store/          # State management
│   │   └── App.tsx
│   └── package.json
│
├── server/                 # Backend Express server
│   ├── src/
│   │   ├── routes/         # API routes
│   │   ├── services/       # Business logic
│   │   └── config/         # Configuration
│   └── package.json
│
├── data/                   # Local data storage
│   ├── documents/          # Uploaded files
│   └── chroma/             # Vector database
│
├── .env.example
└── README.md
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/upload` | POST | Upload a document file |
| `/api/query` | POST | Ask a question about your documents |
| `/api/documents` | GET | Get all uploaded documents |
| `/api/documents/:id` | DELETE | Delete a document |
| `/health` | GET | Health check |

## How It Works

1. **Upload Documents**: Upload your knowledge files (PDF, Markdown, etc.)
2. **Text Extraction**: The system extracts text from your files
3. **Text Chunking**: Documents are split into smaller chunks for better processing
4. **Vector Embedding**: Each chunk is converted into a vector representation
5. **Vector Storage**: Vectors are stored in ChromaDB with metadata
6. **Natural Language Query**: Ask questions in natural language
7. **Semantic Search**: Find relevant document chunks
8. **AI Response**: Claude generates answers based on retrieved context

## Configuration

### Environment Variables

```env
# Claude API Configuration
CLAUDE_API_KEY=your_api_key_here

# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
CHROMA_PATH=./data/chroma
COLLECTION_NAME=knowledge_base

# Upload Configuration
MAX_FILE_SIZE=20971520  # 20MB
```

## Troubleshooting

### File Upload Fails

- **Check file size**: Maximum file size is 20MB
- **Check file type**: Only PDF, Markdown, TXT, DOCX, and HTML are supported
- **Check server logs**: Look for error messages in the backend console

### Questions Don't Return Answers

- **Check Claude API key**: Ensure your API key is valid in `.env`
- **Verify documents are uploaded**: Check the Documents tab
- **Check network connection**: Ensure you have internet access for Claude API

### Frontend Can't Connect to Backend

- **Check ports**: Backend should be on port 3000, frontend on 5173
- **Check proxy configuration**: Verify vite.config.ts proxy settings
- **Restart both servers**: Sometimes a fresh start helps

## Security Considerations

- **Local Storage**: All files and vectors stored locally on your machine
- **API Key Protection**: Your Claude API key is only used locally
- **No External Uploads**: No data is sent to external servers (except Claude API for embeddings)
- **File Validation**: Files are validated before processing

## Future Enhancements

- [ ] Support for more file formats
- [ ] Document summarization
- [ ] Advanced search filters
- [ ] User authentication
- [ ] Multi-user support
- [ ] Export/import functionality
- [ ] Offline mode with local embeddings

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Credits

- **ChromaDB**: Open-source vector database
- **Claude AI**: Powerful language model by Anthropic
- **React & Vite**: Modern web development tools

## Support

If you encounter any issues or have questions, please open an issue on GitHub.

---

Made with ❤️ for privacy-conscious knowledge management
