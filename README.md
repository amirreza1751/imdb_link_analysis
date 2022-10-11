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
*In this task Algorithm for massive datasets are used to rank the the Imdb moives. 
*It is a big Dataset, and three diffenet PageRank Algorithms are used to rank the most important movies,the results of the three algorithms are compared. 
## Dataset Description
*IMDb is a famous name in the movie Industry. On its website, it is possible to retrieve a wide range
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
## Technologies

