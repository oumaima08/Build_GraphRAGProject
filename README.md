# 🧠 GraphRAG with Neo4j

A complete **GraphRAG (Graph Retrieval-Augmented Generation)** implementation that combines **LLMs, Knowledge Graphs, and Neo4j** to answer questions using connected and structured information.

### 🔄 Architecture

```text
Documents
    ↓
Chunking
    ↓
LLM Entity & Relationship Extraction
    ↓
Neo4j Knowledge Graph
    ↓
User Question
    ↓
Question → Cypher
    ↓
Graph Retrieval
    ↓
Retrieved Facts + Question → LLM
    ↓
Final Answer
```

## 🛠️ Technologies Used

| Tool                               | Purpose                                                     |
| ---------------------------------- | ----------------------------------------------------------- |
| **LangChain**                      | Orchestrates the complete GraphRAG pipeline                 |
| **Neo4j**                          | Stores and retrieves the Knowledge Graph                    |
| **Neo4j Aura**                     | Provides a cloud-hosted Neo4j database                      |
| **Groq**                           | Provides fast LLM inference                                 |
| **GPT-OSS-120B**                   | Extracts graph information and generates answers            |
| **LLMGraphTransformer**            | Converts text into **nodes and relationships**              |
| **GraphCypherQAChain**             | Converts natural-language questions into **Cypher queries** |
| **RecursiveCharacterTextSplitter** | Splits documents into manageable chunks                     |
| **Cypher**                         | Queries and traverses connected graph data                  |
| **Google Colab**                   | Development and execution environment                       |

## 🚀 Pipeline

### 1. 📄 Document Processing

Movie documents are created and divided into smaller **chunks** to make them easier for the LLM to process.

### 2. 🔗 Knowledge Graph Extraction

The LLM identifies entities such as **Person, Movie, and Genre**, then extracts relationships such as:

```text
(Person) ──[:DIRECTED]──> (Movie)
(Person) ──[:ACTED_IN]──> (Movie)
(Movie) ──[:IN_GENRE]──> (Genre)
```

### 3. 🗄️ Graph Storage

The extracted graph is stored in **Neo4j**, creating a connected Knowledge Graph that can be queried using Cypher.

### 4. 🔎 Graph Retrieval

Instead of retrieving only semantically similar text, GraphRAG **traverses relationships** to retrieve connected facts.

For example:

> Christopher Nolan → directed → Inception → acted in → Leonardo DiCaprio

### 5. 🤖 Question → Cypher → Answer

**GraphCypherQAChain** uses the Neo4j schema to transform a natural-language question into a Cypher query, executes it, and provides the retrieved facts to the LLM.

The LLM then generates the final answer based on the graph context.

## 🎯 Why GraphRAG?

Traditional RAG focuses mainly on **similarity-based document retrieval**. GraphRAG additionally captures **relationships between entities**, making it particularly useful for questions requiring multi-hop reasoning and connected information.

### 💡 Example

**Question:**

> Which movie did Christopher Nolan direct in 2010 and who acted in it?

**Graph reasoning:**

```text
Christopher Nolan
       ↓ DIRECTED
    Inception
       ↑ ACTED_IN
Leonardo DiCaprio
```

**Answer:**

> Inception, starring Leonardo DiCaprio.

## 📌 Key Takeaway

This project demonstrates how **LLMs + Knowledge Graphs + Neo4j** can create a structured RAG system capable of understanding and retrieving **relationships between entities**, rather than relying only on text similarity.
