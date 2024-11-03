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
