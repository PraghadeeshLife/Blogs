Hi All, This is Praghadeesh. I recently created a program called DocumentGPT build with open source technologies and frameworks such as Reflex, Supabase (Postgres), Langchain.
DocumentGPT uses LLM Models to answer any questions related to the document upload in the form of PDF or TEXT file.

![image](https://github.com/PraghadeeshLife/Blogs/assets/102030901/58b554a5-d720-4556-ac83-a1e8be7d0e31)

In this blog, let's have a sneak peek into the working of DocumentGPT

The concept behind the DocumentGPT is something called Context Injection.

What is Context Injection?
In simple words, context injection is as simple as feeding the required texts as context to the LLM and trying to obtain the answer in a single prompt.

![image](https://github.com/PraghadeeshLife/Blogs/assets/102030901/1a6fed53-f5f3-4df7-9ea2-aebcf850f41e)
The above is an example of Context Injection in which as a part of the prompt the relevant text has been fed and the model answers the question based on the context provided.


But the limitation with Context Injection is that, we can't provide it with the entire data as the LLM has a limitation of maximum number of tokens it can process.
The Limitation is overcome by the use of Vector Databases and Embeddings, which essentially allows us to provide the prompt with only relevant information based on the query the user has asked for.

How do we decide which pieces of texts are relevant to be injected as context?
This is where the embeddings model come into play, the embedding models let us to convert the textual information into a vector array that has some meaningful information.
They are dense vector representations of words where words with similar meanings or contexts are represented by vectors that are closer to each other in the embedding space. 
This allows machine learning algorithms to capture semantic relationships between words,
These vector representation of texts are stored in the Vector Databases.

![image](https://github.com/PraghadeeshLife/Blogs/assets/102030901/d57a4350-624d-4dcc-b5eb-48bed3fefeb2)

In the above picture, the word dog and puppy lies closer meaning these words are used in similar situations and the vectors for these would be close to each other and similar.
While this is just a 2 dimensional representation, the embedding models could generate vectors ranging from dimension of 300 and above thousand. In this case, we use the OpenAI embedding model
and it has a dimension of about 1536.

![image](https://github.com/PraghadeeshLife/Blogs/assets/102030901/9692ba1b-063d-438c-8bcd-81451ab448f7)


Let's have a look at the Steps in which the above is done
- Reading the TEXT or PDF files as texts
- Breaking the texts into smaller chunks
- Using the embeddings on the chunks of texts to generate the vectors
- The generated vector and the relevant text is stored in the Vector Database
- On user entering a question, the question is fed to embedding model and the corresponding vector for the question is obtained
- The question's vector is compared with the vectors present in the vector database with the help of similarity search algorithms
- Based on the ranking of texts using similarity search algorithm, the relevant chunks of information is passed in the prompt along with the question asked.
- The LLM Model then answers the question based on the relevant information provided.

