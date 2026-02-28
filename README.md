# Vectorless RAG with PageIndex

A reasoning-based Retrieval-Augmented Generation (RAG) system that uses **tree-structured document indexing** instead of traditional vector embeddings.

## What is Vectorless RAG?

Unlike traditional RAG systems that rely on vector embeddings and similarity search, vectorless RAG:
- Parses documents into a **hierarchical tree structure** (nodes and sub-nodes)
- Uses **reasoning-based retrieval** through tree searching
- Provides **traceable paths** showing exactly why a section was selected
- Enables more interpretable and explainable document retrieval

## Features

- 🌲 Tree-based document structuring with PageIndex
- 🧠 Reasoning-driven retrieval using LLM tree traversal
- 🔍 Transparent retrieval paths showing selected nodes and reasoning
- ⚡ Fast query response times
- 🏥 Tested on healthcare documents (extensible to any domain)

## Architecture

1. **Document Indexing**: PDF is parsed and organized into a tree structure with nodes and sub-nodes
2. **Query Processing**: User query is analyzed against the tree structure
3. **Reasoning Retrieval**: LLM reasons about which nodes are relevant
4. **Context Extraction**: Text from relevant nodes is extracted
5. **Answer Generation**: LLM generates final answer based on retrieved context

## Prerequisites

- Python 3.8+
- PageIndex API key ([Get one here](https://dash.pageindex.ai/api-keys))
- Google Gemini API key ([Get one here](https://ai.google.dev/))

## Installation

1. Clone or download this repository

2. Install required packages:
```bash
pip3 install pageindex python-dotenv google-genai
```

3. Create a `.env` file in the project root:
```env
PAGEINDEX_API_KEY=your_pageindex_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
```

## Usage

1. Place your PDF document in the project directory and update the `pdf_path` in the notebook

2. Run the notebook cells sequentially:
   - **Cell 1**: Initialize PageIndex client
   - **Cell 2**: Set up Gemini LLM
   - **Cell 3**: Submit document for indexing
   - **Cell 4**: View the tree structure
   - **Cell 5**: Define query and search the tree
   - **Cell 6**: View reasoning and retrieved nodes
   - **Cell 7**: Extract relevant content
   - **Cell 8**: Generate final answer

3. Customize your query:
```python
query = "What are the conclusions in this document?"
```

## Example Output

### Tree Structure
The system creates a hierarchical representation of your document with nodes for major sections and sub-nodes for subsections.

### Reasoning Process
The LLM provides transparent reasoning about why specific nodes were selected:
```
"The user is asking about conclusions. Node X contains the 'Conclusion' section title, 
and Node Y contains summary findings that relate to conclusions..."
```

### Retrieved Nodes
Clear mapping of which document sections were selected:
```
Node ID: abc123    Page: 15    Title: Conclusions and Future Work
Node ID: def456    Page: 14    Title: Discussion of Results
```

## How It Works

### Traditional RAG vs Vectorless RAG

| Traditional RAG | Vectorless RAG |
|----------------|----------------|
| Vector embeddings | Tree structure |
| Cosine similarity | Reasoning-based search |
| Black box retrieval | Transparent node selection |
| Flat document chunks | Hierarchical organization |

### Key Advantages

1. **Transparency**: See exactly which sections were retrieved and why
2. **Structure Awareness**: Respects document hierarchy and organization
3. **Reasoning Capability**: LLM can make logical decisions about relevance
4. **No Embedding Required**: Eliminates embedding model dependencies

## Configuration

### Change LLM Model
Modify the `call_llm` function to use a different model:
```python
response = client.models.generate_content(
    model="gemini-2.0-flash-exp",  # or another model
    contents=prompt,
)
```

### Adjust Tree Search Prompt
Customize the `search_prompt` in Cell 5 to change how the LLM reasons about node selection.

## Project Structure

```
vectorless-rag/
├── rag.ipynb           # Main notebook with complete pipeline
├── sample.pdf          # Your document to analyze
├── .env               # API keys (not committed to git)
└── README.md          # This file
```

## Use Cases

- 📄 Long-form document analysis (research papers, reports)
- 📋 Policy and compliance document Q&A
- 🏥 Healthcare document retrieval
- 📚 Technical manual navigation
- 📊 Structured data extraction from PDFs

## Limitations

- Requires PageIndex API subscription
- Best suited for well-structured documents
- Tree creation time depends on document size
- Reasoning quality depends on LLM capabilities

## Future Enhancements

- [ ] Benchmark against vector-based RAG systems
- [ ] Support multiple document types (Word, HTML, Markdown)
- [ ] Caching layer for repeated queries
- [ ] Interactive visualization of tree structure
- [ ] Multi-document querying

## Contributing

Feel free to fork this project and submit pull requests for improvements!

## License

MIT

## Acknowledgments

- [PageIndex](https://pageindex.ai) - For the vectorless RAG infrastructure
- [Google Gemini](https://ai.google.dev/) - For LLM capabilities

---

**Built with 🧠 and 🌲 by exploring reasoning-based retrieval methods**
