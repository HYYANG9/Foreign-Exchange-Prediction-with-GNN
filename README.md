# GNN-FX-Prediction
This is a model for predicting the movement of foreign exchange(FX) rate in the future. We want to predict the movement of the price in the next five minutes, hour. The currency pairs we predict include AUDJPY, CADJPY, CHFJPY, EURJPY, GBPJPY, NZDJPY, SGDJPY, USDJPY and ZARJPY.    
Currency pairs' FX rate may have lead-lag effect with each other. For example, the sharp drop of USDJPY today may cause drop of EURJPY tomorrow. Capturing the lead-lag effect can improve the performance of FX prediction models. We caputre lead-lag effect by dealing with a graph containing different currency pairs and different time points. The label of a graph is the movement of the price at the time point that we want to predict. So the task is a graph classification task.  
After prediction, we use GNNExplainer to explain to result. By knowing the important sub-graphs and important node features, we may find out the lead-lag effect between currency pairs.
## Workflow
First, downlod all currency pairs form [HistData](https://www.histdata.com/download-free-forex-data/?/ninjatrader/1-minute-bar-quotes), compute technical indicators at each time point, including bollinger band, RSI, RCI, movement.  
Second, Prepare training graphs data and test graph data. We use the previous 18 hours currency pair datasets to formulate a graph, treating one hour one currency pair as a node, final price, return, risk, technical indicators as node features. Then compute similar scores between different nodes using DTW. If the similar score is above the threshold, there is a link between these two nodes. The label of a graph is decided by the return at the next time point that we want to predict. For example, if we want to predict next five minute's price movement, the label is decided by the return at the next minute.  
Third, use a Graph Convolutional Network(GCN) model to do graph classification.  
Fourth, use GNNExplainer to explain the results.


## File Description
Data_prepare: Pre-process all currency pairs.   
1_hour_prediction: Predict the movement of the price in the next hour. A graph is formulated using 2, 6 and 9 pairs seperately.   
5_minutes_prediction: Predict the movement of the price in the next five minutes. A graph is formulated using 2, 6 and 9 pairs seperately.   
GNNExplainer: Explain the result by giving the important sub-graph and important node features.

## Future Work
1. Find out lead-lag effect from the GNNExplainer's results.
2. Embed external information and input to GNN model such as Fed rate, government announcement... Only use the FX data itself is not enough.
3. Try other methods of graph formulation. For example, use different time windows, different ways of link formulation, more technical indicators....

## Acknowledgments
Thanks for the NOMURA Securities to give me the chance and resource to complete this project. At the same time, I am very appreciated for all the help I received from my mentor. 
