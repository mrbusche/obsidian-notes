https://www.manning.com/books/a-simple-guide-to-retrieval-augmented-generation
through Chapter 4

- As the name implied, Retrieve Augmented Generation, in three steps

  - Retrieves relevant information from a data source external to the LLMs
  - Augments that external information as an input to the LLM
  - Then, the LLM Generates a more accurate result

- The technique of retrieving relevant information from an external source, augmenting that information as an input to the LLM, thereby enabling the LLM to generate an accurate response is called Retrieval Augmented Generation.

- LLMs can be, generally, thought of as a next token (loosely, next word) prediction model. They are machine learning models that have learned from massive datasets of human-generated text, finding statistical patterns to replicate human-like language abilities. (edited)

- WHAT ARE MODEL PARAMETERS? You may have heard that Large Language Models have billions and trillions of parameters. GPT-4 has 1.76 trillion parameters. Meta’s Llama models come in three different sizes and are denoted as 7B, 13B and 70B models. These are nothing but the number of parameters

- Giving “examples” within the prompt has emerged to be one of the most effective techniques to guide the LLM responses. This is also known as Few Shot Learning (FSL)

- In essence, it meant creating a ChatGPT like system for proprietary or non-public data with three main objectives.

1. Make LLMs respond with up-to-date information.
2. Make LLMs respond with factually accurate information.
3. Make LLMs aware of proprietary information.

- In May 2020, Lewis et al in their paper, Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks (https://arxiv.org/abs/2005.11401), explored the recipe for RAG - models which combine pre-trained ‘parametric and ‘non-parametric’ memory for language generation. Let us pay some attention to these terms ‘parametric’ and ‘non-parametric’.

- This information that is external to the LLM, but can be provided to the LLM is termed “non-parametric”

- This again is a five step process as shown below.

1. Connect to previously identified external sources
2. Extract documents and parse text from these documents
3. Break down long pieces of text into smaller manageable pieces
4. Convert these small pieces into a suitable format
5. Store this information

- Caching : Caching is the process in which certain data is stored in cache memory for faster retrieval. LLM caching is slightly different from regular caching. The LLM responses to queries are stored in a semantic cache. Next time, a similar query is asked, the response from the cache is retrieved instead of sending the query through the complete RAG pipeline. This improves the performance of the system by reducing the time it takes to respond, by reducing the cost of LLM inferencing and by reducing the load on the LLM service.

- Embeddings are vector representations of data. As a general definition, embeddings are data that has been transformed into n-dimensional matrices. A word embedding is a vector representation of words.

- text-embedding-3-small is the latest small embedding model of 1536 dimensions released in January 2024. The flexibility it provides over ada-002 model is that users can adjust the size of the dimensions according to their needs

- Gemini Embeddings Model by Google text-embedding-004 (last updated in April 2024) is the model offered by Google Gemini. It offers elastic embeddings size up to 768 dimensions and can be accessed via the Gemini API

- One of the most common measures of similarity is Cosine Similarity. Cosine similarity is calculated as the cosine value of the angle between the two vectors. Recall from trigonometry that cosine of parallel lines i.e. angle=0° is 1 and cosine of a right angle i.e. 90° is 0. On the other end, the cosine of opposite lines i.e. angle =180° is -1. Therefore, the cosine similarity lies between -1 and 1 where unrelated terms have a value close to 0, and related terms have a value close to 1. Terms that are opposite in meaning have a value of -1.

- Data Loading is comprised of four steps

  - Connecting to the source.
  - Extracting and parsing text.
  - Reviewing and updating metadata.
  - Cleaning and transforming data.

- Prompt engineering can be defined as the technique of giving instructions to an LLM to attain a desired outcome.

- Counterfactual Robustness: Sometimes the information in the knowledge base might itself be inaccurate. A high-quality RAG system should be able to address this and reject known inaccuracies in the retrieved information. This ability is Counterfactual Robustness

- Precision@k is a variation of precision that measures the proportion of relevant documents amongst the top ‘k’ retrieved results. It is particularly important because it focusses on the top results rather than all the retrieved documents. For RAG it is important because only the top results are most likely to be used for augmentation. For example, if you restrict your RAG system to use only the top 5 retrieved documents for context augmentation, Precision@5 will be the metric to calculate.

- Automated RAG evaluation system, or ARES, is a framework developed by researchers at Stanford University and Databricks. Like RAGAs, ARES uses an LLM as a judge approach for evaluations. Both request a language model to classify answer relevance, context relevance and faithfulness for a given query. However, there are some differences.
	- RAGAs relies on heuristically written prompts that are sent to the LLM for evaluation. ARES, on the other hand, trains a classifier using a language model.
	- RAGAs aggregates the responses from the LLM to arrive at a score. ARES provides confidence intervals for the scores leveraging a framework called Prediction-Powered Inference (PPI)
	- RAGAs generates a simple synthetic question-context-answer dataset for evaluation from the documents. ARES generate synthetic datasets comprising both positive and negative examples of query-passage-answer triples.
- ARES requires more data than we saw above with RAGAs. To leverage ARES, you need three datasets –
	- In-Domain Passage Set: This is a collection of passages relevant to the specific domain being evaluated. The passages should be suitable for generating queries and answers. In our case, it will be the documents that we created from the Wikipedia article.
	- Human Preference Validation Set: A minimum of approximately 150 annotated data points is required. This set is used to validate the preferences of human annotators regarding the relevance of the generated query-passage-answer triples.
	- Few-Shot Examples: At least five examples of in-domain queries and answers are needed. These examples help prompt the large language models (LLMs) during the synthetic data generation process.

Advanced RAG techniques
Advanced techniques in RAG have continued to emerge since the earliest experiments with Naïve RAG. There are three stages in which we can discuss these techniques –
1. Pre-retrieval Stage: Like the name suggests, there are certain interventions that can be employed before the retriever comes into action. This broadly covers two aspects
	1. Index Optimization – The way documents are stored in the knowledge base
	2. Query Optimization – Optimizing the user query so it aligns better to the retrieval and generation tasks
2. Retrieval Stage: Certain strategies can improve the recall and precision of the retrieval process. This goes beyond the capability of the underlying retrieval algorithms that we discussed in Chapter 4.
3. Post-retrieval Stage: Once the information has been retrieved, the context can be further optimized to better align with the generation task and the downstream LLM
With techniques employed at these three stages, the Advanced RAG process follows a ‘Rewrite then Retrieve then Re-rank then Read’ frameworks. Two additional components of Rewrite and Re-rank are added, and the Retrieve component is enhanced in comparison with Naïve RAG.
![[Pasted image 20241109145257.png]]

We have noted that the retrieval stage of Naïve RAG suffers from low recall and low precision –irrelevant information is retrieved and not all relevant information is retrieved. This can happen, largely because of two reasons –
- Knowledge Base is not suited for retrieval: If the information in the knowledge base is not stored in a manner that is easy to search through, then the quality of retrieval will remain suboptimal. To address this, Index Optimization is done in the indexing pipeline for more efficient storage of the knowledge base.
- Retriever doesn’t completely understand the input query: In generative AI applications, the control over the user query is, generally, limited. The level of details a user provides is subjective. The retriever sometimes may misunderstand or not completely understand the context of the user query. Query Optimization addresses this aspect of the challenge with the Naïve RAG.

**Chunk Optimization**
We discussed in Chapter 3, the significance of chunking in the indexing pipeline. Chunking large documents into smaller segments plays a crucial role in retrieval and handling the context length limits of LLMs. There are certain techniques that aim for better chunking and efficient retrieval of the chunks like –
	- Chunk Size Optimization: The size of the chunks can have a significant impact on the quality of the RAG system. While large sized chunks provide better context, they also carry a lot of noise. Smaller chunks, on the other hand, have precise information but they might miss important information. For instance, consider a legal document that's 10,000 words long. If we chunk it into 1,000-word segments, each chunk might contain multiple legal clauses, making it hard to retrieve specific information. Conversely, chunking it into 200-word segments allows for more precise retrieval of individual clauses, but may lose the context provided by surrounding clauses. Experimenting with chunk sizes can help find the optimal balance for accurate retrieval. The processing time also depends on the size of the chunk. Chunk size, therefore, has a significant impact on retrieval accuracy, processing speed and storage efficiency. The ideal chunk size varies with the use case and depends on balancing factors like document types and structure, complexity of user query and the desired response time. There is no one size fits all approach towards optimizing chunk sizes. Experimentation and evaluation of different chunk sizes on metrics like faithfulness, relevance, response time (as discussed in chapter 5) can help in identifying the optimal chunk size for the RAG system. Chunk size optimization may require periodic reassessment as data, or requirements change

Fetch Surrounding Chunks: In this technique, chunks are created at a granular level, say, at a sentence level and when a relevant chunk of text is found in response to a query, the system retrieves not only that chunk but also the surrounding chunks. This makes the search granular but also performs contextual expansion by retrieving adjacent chunks. It is useful in long form content like books and reports where information flows across paragraphs and sections. This technique also adds a layer of processing cost and latency to the system. Apart from that, there is a possibility of diluting the relevance as the neighboring chunks may contain noise

**Reverse Hypothetical Document Embeddings** - One particularly useful technique is Reverse Hypothetical Document Embeddings. It involves using a language model to generate potential queries that could be answered by each document or chunk. These synthetic queries are then added to the metadata. During retrieval, the system compares the user's query with these synthetic queries to find the most relevant chunks

Fine-tuning embedding models allows you to optimize vector representations for your specific domain or task, leading to more accurate retrieval of relevant context. Fine-tuning is a slightly complex process since it requires curation of training dataset and resources for recalculating the embeddings model. In case you’re dealing with highly specialized domains where the vocabulary is different from commonly spoken languages, you should consider fine-tuning the embedding model for your domain

**Query Expansion**
Multi-query expansion: In this approach, multiple variations of the original query are generated using an LLM and each variant query is used to search and retrieve chunks from the knowledge base. For a query ‘How does climate change affect polar bears?’, multi-query expansion might generate ‘Impact of global warming on polar bears’, ‘What are the consequences of climate change for polar bear habitats?’. Let us look at a simple example of multi-query generation using GPT 4o-mini model

```python
original_query="How does climate change affect polar bears?"
num=5

expansion_prompt=f"Generate {num} variations of the following query: {original_query}. Respond in JSON format."

from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(
  model="gpt-4o-mini", 
  messages= [ 
    {"role": "user", "content": expansion_prompt} 
  ], 
  response_format={ "type": "json_object" } )

expanded_queries=response.choices[0].message.content
```

HyDE: Hypothetical document embedding or HyDE is a technique where the language model first generates a hypothetical answer to the user's query without accessing the knowledge base. This generated answer is then used to perform a similarity search against the document embeddings in the knowledge base, effectively retrieving documents that are similar to the hypothetical answer rather than the query itself. Below is an example that generates hypothetical document embeddings.