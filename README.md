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
For doing the PageRank Algorithm the graph has to be made. An inner join is made between the
title_principals and title_basics based on the tconst, which is the common column between the two
datasets, with the aim of choosing only movies that are in both files. The result will be in a variable
named sql_df.
In the next step, a new RDD is created named cast_id_to_movie_list. In this variable the nconst
which is the unique identifier of each actor or actress is the key, and its value is a list of movies in
which the person has played.
For creating this RDD, it is important to reduce the data to just people who are actors or actresses.
Firstly, a map function is run on the sql_df to choose just the columns nconst, tconst, and category.
Then, the method filter is used to choose just the actor or actress. With the help of a groupByKey
and a map function, the cast_id_to_movie_list with the mentioned characteristics is made. It is the
basis for making the nodes.
In the next step, a map function is executed to find the movies that have at least one common actor
or actress. The new RDD is named movie_id_to_movie_id. Each element of movie_id_to_movie_id
is a tuple of movies that share an actor or actress together. Therefore, if the person has played in 8
movies, there are 56 tuples in the related list of that special person. The method flatMap is run on
the movie_id_to_movie_id. Therefore, its elements are just the tuples of movies that have at least
one common actor or actress.
At this step, the initial graph has to be created. With the class “pyspark.sql.types.Row”, it is
possible to create a row object. With the help of Row and doing a map function the vertices of the
graph are made from the nodes variable with the command of v = nodes.map(row).toDF(). The
toDF method provides a very concise way to create a Dataframe. The name of the variable
containing all the vertices is named v.
The edges are also made by implementing the methods movie_id_to_movie_id.toDF([“src”, “dst”])
and the method dropDuplicates method. The name of the variable containing all the edges is named
e. The DataFrame which is related to edges should contain two special columns: “src” (source
vertex ID of edge) and “dst” (destination vertex ID of edge).By having both the vertices and edges, it is tried to make the needed graph named g. The type of the
variables v and e is pyspark.sql.dataframe. GraphFrame is a package which has been developed
with Apache Spark. It can be used to provide DataFrame-Based Graphs. By considering that the
edges and the vertices are ready, it is possible to create the graph with the help of GraphFrames.
The created graph is named g.
The GraphFrames Library has a method which is named PageRank. Then we rank the verticies
based on their importance. By doing that the PageRank which is based on the Historic Approach is
made.
The PageRank which is based on the Probabilistic Approach is implemented by the library
NetworkX. The PageRank algorithm running by NetworkX receives the graph g as its input. The
graphs in NetworkX are directed. If the graph is undirected, it will be changed to a directed Graph.
This matter is done by converting each edge to two edges.
• The damping factor in this algorithm is alpha and it has a value in the range from 0 to 1. It is
possible to choose the maximum number of iterations of the power method in the eigenvalue
solver, it is an optional value and it has to be an integer. This parameter is named max_iter.
• The convergence in the power method can be monitored by an optional parameter named
tol. It is the error Tolerance that analyzes the convergence.
• It is possible to assign a value as a PageRank to each node at the start of the algorithm. The
assignment is done by a dictionary. The name of this parameter is named nstart.
• The algorithm returns a dictionary that has the node names and the PageRank Value.
• The algorithm finishes when the maximum number of iterations is finished or the error
Tolerance of graph_node_number * tol is reached.
• If the algorithm is not able to reach convergence based on the specified value for the
Tolerance in the specified value for the maximum number of iterations, the algorithm
returns PowerIterationFailedConvergence.
• The networkX has PageRank_numpy, PageRank_scipy, networkx.PageRank Algorithms.
Each of the three Algorithms has a different approach to dealing with the task.
Networkx.PageRank_scipy() solves the power method by implementing the SciPy sparse-matrix. It
has two parameters which can be tuned and can control the accuracy, which are tol and maix_iter
At the same time, for the aim of calculating the largest eigenvalue/eigenvector of the Google
matrix, the networkx.PageRank() uses a pure python implementation of the power method. The
networkx.PageRank() has also the two parameters tol and maix_iter.
On the other hand, the networkx.PageRank_numpy() is a a Numpy (full) Matrix implementation to
compute the largest eigenvalue and eigenvector.
## How The Proposed Solution Scales Up With Data Size
The entire process of making the data ready to feed the PageRank algorithm has been done in
resilient distributed datasets (RDD). In some sections of the code, the RDD is converted to SQL
Dataframe to make the process more convenient. According to the Spark documentation, the
computational costs of both approaches are identical. Moreover, the probability matrix and the
power method which is used to calculate the PageRank are implemented by map-reduce jobs.
The only part of the calculation which is not considered as an RDD is the PageRank vector. In a
worst-case scenario, the size of this vector could roughly reach 8 * e9 bytes which is still much less
than available RAM in nowadays clusters.The solution scales up according to dataset size. In order to guarantee that the solution can work
properly for larger datasets. The type “movie” is replaced with the type “short”. The volume of the
“short” type is 43 percent higher than the volume of the “movie” type. The proposed Algorithms
are implemented on the “short” type, and it is shown that the Algorithms work well also for larger
Datasets. By considering Historic and the Probabilistic PageRank methods, the number of common
short movies is 19 out of 20, which is an accuracy of 95 percent. The tables below show the
ranking Table for the Historic and the ProbabilisticAlgorithms. These results are for the maximum
number of iterations of 10

