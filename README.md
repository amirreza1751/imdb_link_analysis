# imdb_link_analysis

<h3> Link to kaggle notebook</h3>
<a href="https://www.kaggle.com/code/amirrezadashtigenave/imdblinkanalysis"> kaggle notebook </a>

</br>

<h3> Link to Google Colaboratory version</h3>
<a href="https://colab.research.google.com/drive/1ip6gYP6kJNodu32MHUTHA-965b2QIFKw?usp=sharing"> Google Colab </a>


## Table of contents
* [Introduction](#Introduction)
* [Technologies](#technologies)
* [Repository_Contents](#Repository_Contents)
* [Methodology](#Methodology)

## Introduction:
* In this task Algorithm for massive datasets are used to rank the the Imdb moives. 
* It is a big Dataset, and three diffenet PageRank Algorithms are used to rank the most important movies,the results of the three algorithms are compared. 
## Dataset Description
* IMDb is a famous name in the movie Industry. On its website, it is possible to retrieve a wide range
of information about movies. In this analysis, we use the IMDb dataset, which has been realized
based on IMDb’s non-commercial licensing. The Dataset has been published on the Kaggle
website. The dataset is in the category of large datasets. It contains sub-datasets which are
title.akas.tsv.gz, title.basics.tsv.gz, title.principals.tsv.gz, and title.ratings.tsv.gz. The raw data has
been stored in the format of tab-separated value (TSV) files, which is a text format. In TSV files,
data is stored in a table structure. Each record of the table is stored as one line in the text file. The
purpose of the task is to create a ranking system between movies. For doing this activity it is needed
to create a graph whose nodes are movies, and nodes are connected by edges if between two nodes
there is at least one common actor or actress. It is possible to create the graph by using the data
which is stored in two sub_datasets which are title.basics.tsv, and title.principals.tsv. The dataset
title.basics.tsv is read and its separator is a tab. It has the following columns:
• Tconst which is an alphanumeric unique identifier of the title
• TitleType which is the type of the title such as movie, short, tvseries, tvepisode, video and
etc.
• PrimaryTitle which is the more popular title / the title used by the filmmakers on
promotional materials at the point of release
• OriginalTitle – original title in the original language
• StartYear (YYYY) – represents the release year of a title
• RuntimeMinutes – primary runtime of the title, in minutes
• Genres (string array) – includes up to three genres associated with the title
The title.basics dataset has 9202163 rows. The data is read during the execution of the code from
the Kaggle API. The data is also updated weekly.More than 75.4 percent of the data is composed of TV Episodes. The second rank is for short
movies with 9.6 percent, and the third rank is for movies with 6.7 percent. The other types such as
videos, tv movies are about 8 percent of the whole dataset.
## Dataset Preprocessing
* In order to implement the algorithm, firstly, it is needed to make the nodes of the graph. The first map function is implemented, and each record of the file title_basics is reduced to just two columns which are tconst and titleType. The created variable is named nodes, and the output is filtered by selecting titleType= movie. The total number of rows that are related to movies is 620463. In the second map function, the RDD node is limited to just the Tconst columns.
## The Considered Algorithms and Their Implementations
The PageRank algorithm is a general concept, and there are different approaches to implementing it,
and these different approaches can produce different results.
One large category of PageRank algorithms is based on probability. In other words, the result of the
probability-based algorithm is a probability distribution, and a probability is assigned to each node.
There is also another variant of PageRank Algorithm generating float numbers that can be higher
than 1 such as 38.28. It is important to mention that the first PageRank Algorithm which was
proposed by Larry Page and Sergey Brin was based on this approach. Therefore, it is called the
Historic Approach in this paper.
It is important to consider that two parameters can influence the finishing of the PageRank
Algorithms. These two parameters are the number of iterations and the number of Tolerances.
In this paper, three different PageRank Algorithms are implemented, and their results are
compared.
## Experiment Description

