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

## Bonus Part

To answer this question, we began by selecting a set of initial "training/queries" queries to create a 
document of 100 results, with 50 top doc scores from each query. We then computed BM25 scores for 
these 50 top documents and normalized them to a range of (0,1). Using these normalized BM25 scores, 
we computed the cosine similarity scores, and finally, we combined the BM25 and cosine similarity 
results using the formula:

                      alpha*BM25 + (1-alpha) * q_d_cosine_similarity

Through this formula we determined the optimal value for alpha, which maximized the @MAP20 
metric, and applied this value to the test query dataset. Overall, this methodology allowed us to 
effectively combine BM25 and cosine similarity scores to improve retrieval performance on both the 
training and test datasets.

10 values of alpha that were taken for the training queries were:

                    [0.1, 0.2, 0,3, 0,4, 0,5, 0.6, 0,7, 0,8, 0.9, 1.0]
