https://www.manning.com/books/knowledge-graph-enhanced-rag
through Chapter 5 (chapter 4 hasn't be published)

- A knowledge graph is a data structure that uses nodes to represent concepts and entities, and relationships to connect these nodes.

- One problem with LLMs is that they are trained to give assertive and confident answers even when their answers might contain invalid information.

- Limitations of LLMs

  1. Bias in Responses: LLMs can sometimes generate biased responses, reflecting biases present in the training data.
  2. Lack of Understanding and Context: LLMs, despite their complexity, do not truly understand the text. They process language based on patterns learned from data, which means they can miss nuances and contextual subtleties.
  3. Vulnerability to Prompt Injection: LLMs are susceptible to prompt injection attacks, where malicious users craft inputs to manipulate the model into generating inappropriate, biased, or harmful responses. This vulnerability poses significant challenges for ensuring the security and integrity of LLM applications in real-world scenarios

- When using a vector index, the retriever method is often refered to as a approximate nearest neighbor (ANN) search. This is because the vector index doesn’t find the exact nearest neighbors, but it finds vectors that is very close to the nearest neighbor. This is a trade-off between speed and accuracy. The vector index is much faster than a brute-force search, but it’s not as accurate.

- The result from a semantic classification of text is called an embedding. Any text you want to match using vector similarity search must be converted into an embedding. This is done using an embedding model, and it’s important to remember that the embedding model needs to stay the same throughout the RAG application.

- Embeddings are lists of numbers, and the length of the list is called the embedding dimension. The embedding dimension is important because it determines how much information the embedding can hold. The higher the embedding dimension, the more computationally expensive it is to work with the embedding both when generating the embedding as well as when performing vector similarity search.

- The generator is the second component of a RAG application. It uses the information found by the retriever to generate a response. The generator is often a large language model, but one benefit of RAG over fine-tuning or relying on a model’s base knowledge is that the models don’t need to be as large.

- Fulltext search is a text search method in databases that has existed for a long time. It searches for matches in the data via keywords, and not by similarity in a vector space. To find a match in a fulltext search, the search term must be an exact match to a word in the data.

- A RAG application consists of a retriever and a generator. The retriever finds relevant information, and the generator uses that information to create a response

- 3.1 outlines a process where a user’s query is transformed to improve document retrieval outcomes, a technique known as step-back prompting. In the scenario presented, the user poses a detailed question regarding Estella Leopold’s educational history during a specific timeframe. This initial question is then processed by a language model such as GPT-4 with query rewriting capabilities, which rephrases it into a more general inquiry about Estella Leopold’s educational background. The purpose of this step is to cast a wider net during the search process, as the rewritten query is more likely to align with a range of documents that may contain the required information.

- As mentioned, the step-back prompting is a query rewriting technique that aims to improve the accuracy of vector retrieval. An example from the original paper [Zheng et al., 2023] demonstrates this process: the specific query "Which team did Thierry Audel play for from 2007 to 2008?" is broadened to "Which teams did Thierry Audel play for in his career?" to improve vector search precision and consequently the accuracy of the generated answers. By transforming a detailed question into a broader, high-level query, step-back prompting reduces the complexity of the vector search process. The idea is that broader queries typically encompass a more comprehensive range of information, making it easier for the model to identify relevant facts without getting bogged down by the specifics.

An agentic RAG system is a system where a variety of retrieval agents are available to retrieve the data needed to answer the user question.

In successful agentic RAG systems a few foundational parts are needed:
- Query Rewriter: The ability to rewrite the user input into one or more atomic questions ot tasks that more easily can be routed to the right retrievers.
- Retriever Router: A function that takes in the user question(s) and returns the best retriever(s) to use.
- Retriever Agents: The actual retrievers that can be used to retrieve the data needed to answer the user question(s).
- Answer Critic: A function that takes in the answers from the retrievers and checks if the original question is answered correctly.

Agentic RAG is useful when we have a variety of data sources and we want to use the best data source for the job. Or when data data source is very broad or complex and we might need specialized retrievers to get the data we need in a consistent way

This is where agentic RAG can be useful. We can have a variety of retrievers available and use the best retriever for the job. In a production environment, this is very useful to keep the performance of the system high and the quality of the answers consistent.

The Query Rewriter has two main tasks which is to divide the user input into atomic questions or tasks and to rewrite the user input into a format that is very clear and easy to understand for the Retriever Router.

Note that the LLM can’t make actual calls to your retrievers, it can only make a decision on which retriever to use and what parameters to pass to the retriever. The actual call to the retriever needs to be done by the system that calls the LLM, which we’ll see in the next section.

The Retriever Router is the central part of the agentic RAG system. It’s job is to take in the user question(s) and return the best retriever(s) to use.
When implementing the Retriever Router we’ll use an LLM to help us with the task. We will provide the LLM with a list of retrievers and the user question(s) and the LLM will return the best retriever(s) to use to find the answer for each question.

One extra benefit of sending the questions in sequence is that we can use the answers from the previous questions to rewrite the next question. This can be useful if the user asks a follow up question that is dependent on the answer to the previous question.

- The main interface to an agentic RAG system is usually some kind of use case or retriever router which job is to find the best suited retriever (or retrievers) to perform the task at hand.