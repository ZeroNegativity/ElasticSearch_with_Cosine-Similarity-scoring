# ElasticSearch_with_Cosine-Similarity-scoring
To begin, we established the Elastic Search configuration. Next, we proceeded to read the "documents" 
from the wikiIR collection and indexed them using the pre-configured Elastic Search setup. 
Subsequently, we read a "test/queries" document and generated a list of the top 20 BM25 scores for 
each of the 100 documents in the testing document. Finally, we evaluated the results by comparing the 
generated document with the "testing/qrels" document.

We utilized pre-existing documents that had been scored with the BM25 algorithm and applied the 
SentenceTransformer model ("msmarco-distilbert-cos-v5") to them. This model uses an encoder to 
convert sentences into embeddings, which can be used to calculate similarity scores between them. 
We then used the utils.cos sim function to compute cosine similarity scores for each query-document 
pair in the set, and re-evaluated the scores based on the new similarity values obtained from the 
SentenceTransformer model.
