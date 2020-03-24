## Option 2: Clustering Crypto

![Cryptocurrencies coins](Images/cryptocurrencies-coins.jpg)
_[Cryptocurrencies coins by Worldspectrum](https://www.pexels.com/@worldspectrum?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) | [Free License](https://www.pexels.com/photo-license/)_

### Background

You are a Senior Manager at the Advisory Services team on a [Big Four firm](https://en.wikipedia.org/wiki/Big_Four_accounting_firms), one of your most important clients, a prominent investment bank, is interested in offering a new cryptocurrencies investment portfolio for its customers, however, they are lost in the immense universe of cryptocurrencies, they ask you to present a report of what cryptocurrencies are on the trading market and how cryptocurrencies could be grouped towards creating a classification for developing this new investment product.

In this homework assignment, you have the opportunity to put in action your new unsupervised learning and Amazon SageMaker skills to cluster cryptocurrencies and create some plots to present your results.

You are asked to accomplish the following main tasks:

* **[Data Preprocessing](#Data-Preprocessing):** Prepare data for dimension reduction with PCA and clustering using K-Means.

* **[Reducing Data Dimensions Using PCA](#Reducing-Data-Dimensions-Using-PCA):** Reduce data dimension using the `PCA` algorithm from `sklearn`.

* **[Clustering Cryptocurrencies Using K-Means](#Clustering-Cryptocurrencies-Using-K-Means):** Predict clusters using the cryptocurrencies data using the `KMeans` algorithm from `sklearn`.

* **[Visualizing Results](#Visualizing-Results):** Create some plots and data tables to present your results.

* **[Challenge](#Challenge):** Deploy your notebook to Amazon SageMaker.

---

### Files

* [crypto_clustering.ipynb](Starter_Files/crypto_clustering.ipynb)

---

### Instructions

#### Data Preprocessing

In this section, you have to load the information about cryptocurrencies from the provided `CSV` file and perform some data preprocessing tasks. The data was retrieved from  _CryptoCompare_ using this endpoint: `https://min-api.cryptocompare.com/data/all/coinlist`.

Start by loading the data in a Pandas DataFrame named `crypto_df`, and continue with the following data preprocessing tasks.

3. Remove all cryptocurrencies that are not on trading.

4. Remove all cryptocurrencies that have not an algorithm defined.

5. Remove the `IsTrading` column.

6. Remove all cryptocurrencies with at least one null value.

7. Remove all cryptocurrencies without coins mined.

9. Store the names of all cryptocurrencies on a DataFramed named `coins_name`, use the `crypto_df.index` as the index for this new DataFrame.

10. Remove the `CoinName` column.

11. Create dummies variables for all the text features, store the resulting data on a DataFrame named `X`.

12. Use the [`StandardScaler` from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html) to standardize all the data of the `X` DataFrame. Remember, this is important prior to using PCA and K-Means algorithms.

#### Reducing Data Dimensions Using PCA

Use the [`PCA` algorithm from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.PCA.html) to reduce the dimensions of the `X` DataFrame down to three principal components.

Once you have reduced the data dimensions, create a DataFrame named `pcs_df` using as columns names `"PC 1", "PC 2"` and `"PC 3"`;  use the `crypto_df.index` as the index for this new DataFrame.

You should have a DataFrame like the following.

![pcs_df](Images/pcs_df.png)

#### Clustering Cryptocurrencies Using K-Means

In this section, you will use the [`KMeans` algorithm from `sklearn`](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html) to cluster the cryptocurrencies using the PCA data.

Perform the following tasks:

1. Create an Elbow Curve to find the best value for `k`, use the `pcs_df` DataFrame.

2. Once you define the best value for `k`, run the `Kmeans` algorithm to predict the `k` clusters for the cryptocurrencies data. Use the `pcs_df` to run the `KMeans` algorithm.

3. Create a new DataFrame named `clustered_df`, that includes the following columns `"Algorithm", "ProofType", "TotalCoinsMined", "TotalCoinSupply", "PC 1", "PC 2", "PC 3", "CoinName", "Class"`. You should maintain the index of the `crypto_df` DataFrames as is shown bellow.

    ![clustered_df](Images/clustered_df.png)

#### Visualizing Results

In this section, you will create some data visualization to present the final results. Perform the following tasks:

1. Create a 3D-Scatter using Plotly Express to plot the clusters using the `clustered_df` DataFrame. You should include the following parameters on the plot: `hover_name="CoinName"` and `hover_data=["Algorithm"]` to show this additional info on each data point.

2. Use `hvplot.table` to create a data table with all the current tradable cryptocurrencies. The table should have the following columns: `"CoinName", "Algorithm", "ProofType", "TotalCoinSupply", "TotalCoinsMined", "Class"`

3. Create a scatter plot using `hvplot.scatter`, to present the clustered data about cryptocurrencies having `x="TotalCoinsMined"` and `y="TotalCoinSupply"` to contrast the number of available coins versus the total number of mined coins. Use the `hover_cols=["CoinName"]` parameter to include the cryptocurrency name on each data point.
