Hybrid GenAI Telegram Bot (RAG + Vision)
 Overview
This project is a Hybrid GenAI Telegram Bot that supports both:
 Text-based Question Answering (RAG)
 Image Captioning & Tag Generation (Vision AI)
The bot intelligently processes user input and routes it to the appropriate pipeline, enabling a multi-modal conversational experience.

Features
RAG (Retrieval-Augmented Generation)
/ask <query> — Answer questions from a local knowledge base
Semantic search using embeddings
MMR (Maximal Marginal Relevance) for diverse retrieval
MQR LLM Power to generate multiple similar query from user prompt to get accurate response.
CrossEncoder reranking for high-quality results
Vision AI
/image — Upload an image
Generates:
📸 Caption
🏷️ Tags/keywords

 System Architecture
               ┌────────────────────┐
                │   User Input       │
                └─────────┬──────────┘
                          │
        ┌─────────────────┴─────────────────┐
        │                                   │
   🧠 Text Query                       🖼️ Image Upload
        │                                   │
        ▼                                   ▼
  Embedding Model                   Vision Model (BLIP)
        │                                   │
        ▼                                   ▼
  Vector DB Retrieval                 Caption + Tags
        │
        ▼
   MMR (Diversity)
        │
        ▼
 CrossEncoder Reranking
        │
        ▼
     LLM Response
        │
        ▼
   Telegram Reply


 Models Used
🔹 Embedding Model
all-MiniLM-L6-v2
Fast and efficient for semantic similarity
🔹 Reranking Model
cross-encoder/ms-marco-MiniLM-L-6-v2
Improves relevance of retrieved documents
🔹 Vision Model
BLIP (Salesforce/blip-image-captioning-base)
CLIP for tag generation
Generates natural image descriptions
  LLM
OpenAI 
Used to generate final answers from retrieved context

 Database
SQLite used for:
Document storage
Embeddings
Lightweight and easy to deploy locally

 How It Works
 RAG Pipeline
Documents are split into chunks
Each chunk is converted into embeddings
Stored in SQLite database
At query time:
Query is embedded
Top-K documents retrieved
MMR applied for diversity
CrossEncoder reranks results
Context passed to LLM
Final answer returned to user

 Vision Pipeline
User uploads an image via /image
Image processed using BLIP model
Tags generated using CLIP
Model generates:
Caption
Tags 
Response sent back to user

 How to Run
1. Run all the code by using your Open AI API
2. Start the bot
http://t.me/AvivoTelBot


💬 Telegram Commands
/ask <query>   → Ask a question (RAG)
/image         → Upload image for captioning
/help          → Show usage instructions
/summarize          → Generate summary of last interaction.


📊 Key Design Decisions
Component
Choice
Reason
Embeddings
MiniLM
Fast + lightweight
Retrieval
Cosine + MMR + MQR
Balance of relevance + diversity + Precision 
Reranking
CrossEncoder
High precision results
Vision Model
BLIP
CLIP
Strong caption generation
Tag Generation
Database
SQLite
Simple and local



 Innovation Highlights
 Hybrid bot (Text + Image support)
 MMR+MQR -based retrieval (advanced technique)
 CrossEncoder reranking (production-level approach)
 Multi-stage retrieval pipeline
Streaming for continuous output from bot in flow.
Past 3 conversation history

 Future Improvements
Proper output format using any Parser
Can be deployed for seamless interaction
Tokens can be Secret 



 Example Usage
 RAG Query
Input:
/ask What is refund policy?

Output:
 Answer:
Our refund policy allows...

 Source:



 Image Input
Input:
(User uploads image)
Output:
📸 Caption:
A dog playing in the park

🏷️ Tags:
dog, park, outdoor


 Tech Stack
Python
sentence-transformers
SQLite / sqlite-vec
BLIP (HuggingFace Transformers)
python-telegram-bot


Developed as part of a GenAI assignment demonstrating:
Retrieval-Augmented Generation (RAG)
Computer Vision integration
Multi-modal AI system design


