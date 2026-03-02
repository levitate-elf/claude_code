# Personal AI Knowledge Base - Setup Instructions

## Quick Start Guide

### Step 1: Prerequisites

Make sure you have the following installed:
- **Node.js 16+** (Download from https://nodejs.org/)
- **npm** (comes with Node.js)
- **Claude API Key** (Get from https://www.anthropic.com/api)

### Step 2: Configure Environment

1. Copy the environment file:
   ```bash
   copy .env.example .env
   ```

2. Open `.env` in a text editor and add your Claude API key:
   ```env
   CLAUDE_API_KEY=sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx
   ```

### Step 3: Install Dependencies

You have two options:

#### Option A: Use the setup script (Windows)
```bash
setup.bat
```

#### Option B: Manual installation
```bash
# Install backend dependencies
cd server
npm install

# Install frontend dependencies
cd ../client
npm install
```

### Step 4: Start Development Servers

#### Option A: Use the start script (Windows)
```bash
start-dev.bat
```
This will open two terminal windows - one for backend and one for frontend.

#### Option B: Manual start

Terminal 1 - Backend:
```bash
cd server
npm run dev
```

Terminal 2 - Frontend:
```bash
cd client
npm run dev
```

### Step 5: Access the Application

Open your browser and go to:
```
http://localhost:5173
```

## Using the Application

### Upload Documents

1. Click on the **Upload** tab
2. Either:
   - Click "Select Files" and choose your files, OR
   - Drag and drop files into the upload area
3. Supported file types:
   - PDF (.pdf)
   - Markdown (.md)
   - Text (.txt)
   - Word (.docx)
   - HTML (.html)
4. Click "Upload All Files"

### Ask Questions

1. Click on the **Chat** tab
2. Type your question in the input box
3. Press Enter or click the send button
4. The AI will search your documents and provide an answer
5. Sources are shown below each answer

### Manage Documents

1. Click on the **Documents** tab
2. View all uploaded documents
3. Click the trash icon to delete a document

## Test with Example Document

We've included an example document for testing:

```bash
# Upload example-doc.md through the UI
# Then ask questions like:
- "What is artificial intelligence?"
- "What are the types of AI?"
- "What is machine learning?"
- "What ethical considerations should we keep in mind with AI?"
```

## Troubleshooting

### "Cannot find module" errors
Run `npm install` in both server and client directories.

### "Port already in use" errors
- Backend port 3000 is in use: Change PORT in .env
- Frontend port 5173 is in use: Change port in client/vite.config.ts

### "Invalid API key" errors
- Verify your CLAUDE_API_KEY in .env is correct
- Make sure there are no extra spaces or quotes

### File upload fails
- Check file size (max 20MB)
- Check file extension (must be supported format)
- Check browser console for errors

### No answer returned from queries
- Verify documents are uploaded (check Documents tab)
- Check that Claude API key is valid
- Check backend console for errors

## Production Deployment

### Build the application

1. Build frontend:
   ```bash
   cd client
   npm run build
   ```

2. Build backend:
   ```bash
   cd server
   npm run build
   ```

3. Start production server:
   ```bash
   cd server
   npm start
   ```

### Environment for Production

Update `.env` for production:
```env
NODE_ENV=production
PORT=8080  # or your preferred port
```

## Project Structure Overview

```
personal-knowledge-base/
├── client/                    # React frontend
│   ├── src/
│   │   ├── components/        # UI components
│   │   │   ├── Upload/        # File upload component
│   │   │   ├── Chat/          # Chat interface
│   │   │   ├── DocumentList/  # Document list
│   │   │   └── Layout/        # Main layout
│   │   ├── services/          # API services
│   │   ├── store/             # State management
│   │   └── App.tsx            # Main app
│   └── package.json
│
├── server/                    # Express backend
│   ├── src/
│   │   ├── routes/            # API routes
│   │   │   ├── upload.ts      # File upload
│   │   │   ├── query.ts       # AI queries
│   │   │   └── documents.ts   # Document management
│   │   ├── services/          # Business logic
│   │   │   ├── fileProcessor.ts  # File parsing
│   │   │   ├── vectorStore.ts    # Vector database
│   │   │   └── chatService.ts    # AI chat
│   │   └── config/            # Configuration
│   │       └── database.ts    # ChromaDB setup
│   └── package.json
│
├── data/                      # Local data storage
│   ├── documents/             # Uploaded files
│   └── chroma/                # Vector database
│
├── .env.example               # Environment template
├── README.md                  # Main documentation
└── setup.bat / start-dev.bat  # Windows scripts
```

## Key Features Explained

### 1. File Processing
- Files are uploaded and stored locally in `data/documents/`
- Text is extracted based on file type (PDF, DOCX, etc.)
- Documents are split into chunks for better search accuracy
- Each chunk is converted to a vector embedding

### 2. Vector Database (ChromaDB)
- Stores vector embeddings of document chunks
- Enables semantic search (understands meaning, not just keywords)
- Persists data locally in `data/chroma/`
- Fast similarity search for relevant content

### 3. AI Question Answering
- User questions are converted to vectors
- System searches for most similar document chunks
- Claude AI generates answers based on retrieved context
- Sources are shown for transparency

### 4. Privacy and Security
- All files stored locally on your machine
- No data sent to external servers (except Claude API for AI)
- Your Claude API key never leaves your machine
- Open source and auditable code

## Customization

### Change chunk size
Edit `server/src/services/fileProcessor.ts`:
```typescript
private chunkSize: number = 800;      // Change this value
private chunkOverlap: number = 100;   // Change this value
```

### Change number of search results
Edit `server/src/routes/query.ts`:
```typescript
const { query, topK = 5 } = req.body;  // Change default value
```

### Add more file types
Edit `server/src/routes/upload.ts`:
```typescript
const allowedTypes = ['.pdf', '.md', '.txt', '.docx', '.html', '.htm'];
// Add more extensions here
```

## Support and Contributing

If you encounter issues:
1. Check this guide and README.md
2. Review error messages in browser console and terminal
3. Open an issue on GitHub

Contributions are welcome! Feel free to submit pull requests.

## License

MIT License - See LICENSE file for details
