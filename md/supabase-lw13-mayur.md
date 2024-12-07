---
marp: true
paginate: true
transition: dissolve 400ms
theme: uncover
class: invert
size: 16:9
style: |
  img {background-color: transparent!important;}
  a:hover, a:active, a:focus {text-decoration: none;}
  header a {color: #148ec8 !important; font-size: 24px;}
  footer {color: #148ec8;}
  /* ⬇️ Mark the image of "1" in every pages as morphable image named as "one" ⬇️ */
  img[alt="1"] {
    view-transition-name: one;
    contain: layout; /* required */
  }

  img[alt="2"] {
    view-transition-name: two;
    contain: layout; /* required */
  }

  /* Generic image styling for number icons */
  img:is([alt="1"], [alt="2"], [alt="3"]) {
    height: 64px;
    position: relative;
    top: -0.1em;
    vertical-align: middle;
    width: 64px;
  }

  @keyframes marp-transition-dissolve {
      from {
        opacity: 1;
      }
      to {
        opacity: 0;
      }
  }
header: '[Supabase and pgVector](#1 " ")'
footer: 'Slides by [Mayur](https://mayurgohil.com)'
---
# RAG with Supabase and pgvector
---
# Mayur Gohil
![1 w:200 h:200](https://blr1.digitaloceanspaces.com/mayur-media/IMG_3151-2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=DO00ZTM7JENB7T6MT7EH%2F20241206%2Fblr1%2Fs3%2Faws4_request&X-Amz-Date=20241206T095440Z&X-Amz-Expires=259200&X-Amz-SignedHeaders=host&X-Amz-Signature=138111f369ee8fba9ad387ffafb738911de4493d180902556f16d164d2167cce)
<!-- <style>
  img {
    border-radius: 50%; /* Makes the image round */
    width: 256px; /* Ensures the width is consistent */
    height: 256px; /* Ensures the height is consistent */
    object-fit: cover; /* Ensures the image covers the area */
  }
</style> -->
#### [mayurgohil.com](https://mayurgohil.com)
#### Software Engineering @ [Atyantik Technologies](https://atyantik.com)
---
## Topics:
- Introduction to Vector Databases
- Supabase & PGVector Overview
- Setting Up a Supabase Project
- Demo with PGVector

---
## What Are Vectors and Vector Databases?
---
![1 w:1024 h:512](https://mayur-media.blr1.digitaloceanspaces.com/Screenshot%202024-12-06%20at%204.13.48%E2%80%AFPM.png)
---
---
## Word Embedding Models:
- Transform words into numerical vectors, capturing semantic relationships in a continuous vector space.
---
## Popular Embedding Models:
- [Word2Vec](https://en.wikipedia.org/wiki/Word2vec?utm_source=chatgpt.com)
- [GloVe](https://en.wikipedia.org/wiki/GloVe?utm_source=chatgpt.com)
- [BERT](https://en.wikipedia.org/wiki/BERT_%28language_model%29?utm_source=chatgpt.com)
--- 
![1 w:700 h:350](https://mayur-media.blr1.digitaloceanspaces.com/Screenshot%202024-12-05%20at%201.31.09%E2%80%AFPM.png)
d = √(x2−x1)2+(y2−y1)2
---
---
## [Vector database]() indexes and stored vector embeddings for fast retrival and similarity search
---
## Challenges in Vector Databases
- Storing high-dimensional vectors and performing similarity searches across thousands of them can be computationally intensive and slow due to the complexity of distance calculations.
---
## How Can We Address This Challenge?
---
- Indexing is a fundamental component of a vector database, serving as a data structure that streamlines the search process.
- It is a dedicated field of research with various methods available for calculating and implementing indexing.
- Learn more about indexing [link](https://www.analyticsvidhya.com/blog/2024/07/indexing-algorithms-in-vector-databases/?utm_source=chatgpt.com).
---
## Example:
#### [E-commerce recommendation systems]()
- Represent products and user preferences as vectors.
- Perform rapid similarity searches for personalized recommendations
---
### Introduction to SUPABASE
---
- Open-source Backend as a Service (BaaS) platform built on PostgreSQL.
- Provides RESTful APIs, GraphQL APIs, real-time subscriptions, authentication, storage, and edge functions.
---
### Integration with PG Vector:
- Facilitates storage and querying of vector embeddings.
- Simplifies data architecture and improves performance.
---
## Supabase PG Vector [Features](https://supabase.com/features/vector-database?utm_source=chatgpt.com)
- Unified Data Storage
- Efficient Similarity Search
- Advanced Querying Capabilities
- Scalability
- Seamless AI Integration
- Real-Time Updates
---
## Setting Up a Supabase Project
--- 
1. Sign Up/In: Visit the Supabase [website](https://supabase.com) and create an account

2. Create a [Project](https://database.new)
---
## Demo project
---
[https://github.com/mayur161019/EmbedInbox.git](https://github.com/mayur161019/EmbedInbox.git)
---
---
## SQL code:
- Ensure the pgvector extension is enabled.
```sql
CREATE EXTENSION IF NOT EXISTS vector;
```
---
- Create the emails table.
```sql
CREATE TABLE emails ( id SERIAL PRIMARY KEY, -- Unique ID for each email 
subject TEXT NOT NULL, -- Subject of the email 
sender TEXT NOT NULL, -- Email address of the sender 
recipient TEXT[] NOT NULL, -- Array of recipients 
cc TEXT[], -- Optional CC recipients 
bcc TEXT[], -- Optional BCC recipients 
body TEXT NOT NULL, -- Full body of the email (raw content) 
created_at TIMESTAMPTZ DEFAULT NOW() -- Timestamp when the email was sent or received 
);
```
---
- Create the email_sections table.
```sql
CREATE TABLE email_sections ( id SERIAL PRIMARY KEY, -- Unique ID for each section 
email_id INT NOT NULL REFERENCES emails(id) ON DELETE CASCADE, -- Reference to parent email 
section_content TEXT NOT NULL, -- Content of the section (chunk) 
embedding VECTOR(1536), -- Embedding of the section 
section_order INT, -- Order of the section in the original email 
created_at TIMESTAMPTZ DEFAULT NOW() -- Timestamp for the section 
);
```
---
- Create an HNSW index on the section embeddings using the correct operator class.
```sql
CREATE INDEX section_embedding_hnsw_idx 
ON email_sections USING hnsw (embedding vector_cosine_ops);
```

---
## Why Supabase is Ideal for AI applications
---
- Supabase Vector integrates the pgvector extension into PostgreSQL, enabling the storage, indexing, and querying of vector embeddings alongside traditional relational data.
- [Pincode vs Supabase pgvector](https://supabase.com/blog/pgvector-vs-pinecone?utm_source=chatgpt.com)
---
## Thank You!
---
#### Questions?

 