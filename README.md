# Evaluation-of-IR-Models
Implementing the VSM,DFR and BM25 models in IR 

Using the following Similarity class in the schema.xml file we can implement 
the Vector Space Model as a global configuration :
<similarity class="solr.ClassicSimilarityFactory"/>

After re-indexing the train.json provided for the above configured schema.xml file for 
the core on solr, we run the TREC_eval to get the MAP and nDCG values for the test 
queries provided to us along with their manual judgement file qrel.txt
./trec_eval -q -c -M1000 ../qrel.txt ../vsm.txt | grep map
./trec_eval -q -c -M 1000 -m ndcg ../qrel.txt ../vsm.txt

BM25 Model
Using the following Similarity class in the schema.xml file we can implement BM25 model :
<similarity class="solr.BM25SimilarityFactory"> <str name="b">0.75</str>
<str name="k1">1.2</str>
</similarity>
We use the below to get the BM25 MAP values and nDCG values for the default configuration :
./trec_eval -q -c -M1000 ../qrel.txt ../bm25.txt | grep map ./trec_eval -q -c -M 1000 -m ndcg ../qrel.txt ../bm25.txt

DFR - Divergence From Randomness
Using the following Similarity class in the schema.xml file we can implement BM25 model :
<similarity class="solr.DFRSimilarityFactory"> <str name="c">1.0</str>
<str name="normalization">H1</str>
<str name="afterEffect">B</str>
<str name="basicModel">G</str> </similarity>
We use the below to get the BM25 MAP values and nDCG values for the default configuration :
./trec_eval -q -c -M1000 ../qrel.txt ../dfr.txt | grep map
./trec_eval -q -c -M 1000 -m ndcg ../qrel.txt ../dfr.txt
