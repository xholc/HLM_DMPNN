# HLM_DMPNN
## excute codes in 1 -> 5

1.hyperparameter searching of GCN/ D_MPNN 因為兩個模型各自的參數不同分成兩個，參數細節請看註解與deepchem說明文件
把model對於testset的預測值轉變成classification，分成 unstable(<30 min)/ moderate (30-60 min)/ stable (> 60 min)三個classes，
並print 出Confusion Matrix/ classification_report/ matthews_corrcoef

2.進行各種data selection，可透過oversampling minor class實現 even class training，此處的class labels來自於不同clustering methods對於datasets的分類結果，
需要因為訓練model時需要輸入CSV所以2.5的output是CSV file，分成train/ test set CSV，找Maximal Common Structure(MCS)，有分成直接尋找，或是先抓出scaffold在找MCS

3.定義將SMILES轉換成igraph objects作為後續WWL graph kernels分析的input，此處將DMPNN node / edge feature 都存入graph中並並儲存igraph objects，
之後進行WWL graph kernels分析的主要流程，執行完後會獲得WWL distance matrix (in shape: N*N, N= number of samples of dataset)

4.load chosen WWL distance matrix as input 並使用各種ML methods（k-means, HDBSCAN, k-medoids)分析，
利用unstable(<30 min)/ moderate (30-60 min)/ stable (> 60 min) 的class資訊與cluster labels，
兩種labeling畫出MDS plot，以視覺化不同clustering methods對於WWL distance matrix的影響，與cluster labels如何在資料點間分布

5.用KL divergence來決定最終進行ML model時使用哪個fingerprint較為合適，之後參考註解就可以完成ML methods(RF, SVM, XGBoost)

