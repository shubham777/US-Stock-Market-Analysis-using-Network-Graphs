# US-Stock-Market-Analysis-using-Network-Graphs
## Overview:
This study presents a comprehensive network analysis of the S\&P 500 stocks from 2018 to 2022, with the aim of visualizing stock connectivity and its evolution over
time, particularly during the COVID-19 pandemic. Our methodology involved multiple steps, starting with the data collection of S\&P 500 stock prices, detrending the data by computing log returns, calculation of correlation matrices for multiple windows, and finally buliding a network using the Winner-Take-All (WTA) method, as
proposed in the referenced \href{https://www.researchgate.net/publication/222825530_A_network_perspective_of_the_stock_market}{paper}.

Leveraging the WTA method, we were able to construct an accurate and robust network that captured the connections among stocks effectively. The network analysis revealed key findings on degree distribution, scale-free properties, the average degree of the network over time, high-degree stocks in the network, and stocks with high betweenness centrality. Furthermore, we identified communities detected over time and measured the Jaccard similarity of these communities with sector codes, which allowed us to assess the extent to which the detected communities corresponded to real-world industry sectors. Visualizations of the network and its evolution provided valuable insights into stock market dynamics and stock interrelationships during the studied period.

By employing the WTA method and improving the data collection process, our research presented an enhanced and updated analysis of stock market networks. The
findings contributed to a deeper understanding of stock market behavior, especially during tumultuous periods like the COVID-19 pandemic, and offered potential
applications for investors, policymakers, and researchers seeking to explore the complex interactions within financial markets.

### We aim to answer following questions with this project:
1. What are the properties of the S&P 500 stock market network, such as degree distribution, average degree, clustering coefficient, betweenness centrality, and modularity over time?
2. Which stocks have high connectivity and centrality in the network, and how did their roles change during the COVID-19 pandemic period?
3. How did the community structure of the stock market network change over time, and how did it correspond to industry sectors?
4. How did the network structure and connectivity change during the COVID-19 pandemic period?
5. What insights can be gained from visualizing the network and its evolution during the studied period?

## Methodology:
### Data Collection:
The first step in our methodology was to collect historical price data for the S&P 500 stocks from January 2018 to December 2022. We used the Yahoo Finance API to download the daily stock prices for each stock in the S&P 500 index. To obtain the list of S&P 500 companies, we used Python code to scrape the list from the Wikipedia page for the S&P 500 index. 

### Data Detrending:
calculating correlations on stock prices is challenging due to the dynamic time series nature of the data and the presence of inherent trends. If the data is not properly normalized, false correlations may arise.  For this purpose we employ the concept of detrending. To prepare the stock price data for network analysis, the log price returns were calculated using the closing price data for each stock. The log price return is the difference between the natural logarithm of the closing price on a given day and the natural logarithm of the closing price on the previous day. 
<p align="center">
  <img width="500" src="https://user-images.githubusercontent.com/29313860/235371997-91e1d33a-d1e5-47f9-9df5-92473b5ac4b1.png">
</p>
<p align="center">Log price return variations</p>
### Computing Correlation Matrices:
The correlation matrices capture the pairwise correlations between the log-returns of the stocks and are used to construct the network.In this phase, we compute the Pearson correlation between the stocks' log returns. To investigate the dynamic properties of the networks, we divide the data into windows of a given width (T). The window width is equal to the number of daily results that are used to figure out how similar two stocks are. We then evaluated the mean correlation for window values of 21, 42, 63, 84, and 105 and then plotted the fluctuations in correlation to determine the ideal window length.
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372055-0b8f2269-5bf9-48c9-b296-83747d0f6a29.png">
</p>
<p align="center">Mean correlation for different window sizes</p>

### Network Construction:
We employ the following steps to create the graph and study the properties:

1. First, the modularity of the graph is calculated by considering the correlations between stock prices within a specific time frame.
2. A threshold value is then selected based on the maximum modularity value. This threshold value is used to create an edge list for the graph.
3. The graph is created using the NetworkX library and the community structure of the graph is determined using the Louvain algorithm. The attributes of the nodes in the graph, such as sector, degree centrality, closeness centrality, and betweenness centrality, are calculated and assigned.
4. Finally, various graph properties such as the number of nodes and edges, average clustering coefficient, average shortest path length, diameter, slope, and number of communities are calculated and stored in a DataFrame. These properties are used later to analyze the structure and dynamics of the graph.

## Network Analysis:
### Degree distribution and Scale-free properties:
We plotted a log-log scale and a histogram of the degree distribution. The plots created, show that most windows have scale-free features.

### Average network degree: 
We examined the evolution of the typical degree over time. Indicative of the volatile nature of the stock market, the Winner Takes All method reveals that this metric fluctuates considerably over time for the networks.The graph’s peaks correspond well with significant events such as the beginning of the COVID-19 pandemic in March 2020 (approximately 450 days from January 2018).
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372221-b1c404ea-c30a-4efd-b8ae-ffdba09b2700.png">
</p>

### High-degree stocks: 
We examined the network’s high-degree stocks at different windows to identify influential stocks that can predict the stock. Financial equities lead in several windows, as shown
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372261-9b0fff8c-be71-47ca-8928-55005d683598.png">
</p>
### High betweenness centrality stocks: 
We looked at stocks with high betweeness Centrality in the network at different windows to find important stocks that will be good price forecasters due to their network location. Financial stocks still lead most times.
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372377-c8d0e597-8336-4a18-a0d6-1f67de93080f.png">
</p>
### Communities throughout time: 
We countedcommunities over time. The market is dynamic,forming new stock communities in each window that may die or survive.
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372387-f870c376-9bf3-497c-9d9e-52c8dbb160f9.png">
</p>
### Jaccard similarity: 
We calculated the Jaccard similarity coefficient of the communities found with the SIC code of these SP500 stocks in each time window with the stock list categorised by industry code. We classed a community as that SIC code if its Jaccard coefficient is greater than 0.25 with the group of stocks classified by the SIC code. Finance, real estate, utilities, energy, telecommunications, and industrial finance are well correlated and trade in groups over different periods, while Information Technology, Materials, Consumer Staples, Consumer Discretionary, and Health Care don’t.
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372393-a1acc273-823c-4eb3-b254-008553f4d71b.png">
</p>

## Network Evolution Visualisations:
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372403-f640f7bf-c632-4c80-b088-dcf47de72b98.png">
</p>
<p align="center">Stock Network (as on 29th August 2022)</p>
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372418-96353ac2-1530-41da-b0db-45985ca7abb9.png">
</p>
<p align="center">Stock Network (with weighted edge size)</p>
<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/29313860/235372455-71685cef-5dee-4b40-8e3d-723c86313be9.png">
</p>
<p align="center">Stock Network (as on 16th March 2020, beginning of COVID-19)</p>

