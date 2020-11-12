# IR-SMART <br> Information Retrieval - Semantic Answer Type Prediction



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Built With](#built-with)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Dataset](#dataset)
  * [File Structure](#file-structure)
  * [Final Steps](#final-steps)
* [Usage](#usage)
* [Results](#result)
* [Contributors and License](#contributors)
* [Contact](#contact)

---
</br>

<!-- ABOUT THE PROJECT -->
## About The Project

**IR-SMART** contain the generated code for a university project located [here](https://github.com/kbalog/ir-course/tree/master/project).

Given a query formatted in natural language, the code should be able to predict the expected answer type from a set of candidate entitites from collected target ontology. In this project the target ontology used is from the DBpedia 2016 dump.

</br>

### Built With
The project has utilized the following tools and libraries extensively:

* [Jupyter Notebook](https://jupyter.org/install)
* [ElasticSearch](https://elasticsearch-py.readthedocs.io/en/7.10.0/)
* [GenSim](https://pypi.org/project/gensim/)
* [NumPy](https://pypi.org/project/numpy/)
* [Scikit-Learn](https://pypi.org/project/scikit-learn/)

</br>

<!-- GETTING STARTED -->
## Getting Started

To get a local copy up and running follow these simple steps. It is assumed that the user has jupyter notebook available, and it is recommended to use a Conda distribution(Anaconda/Miniconda).

</br>

### Prerequisites
Install the necessary python libraries(if conda is not used):

```
pip install --upgrade elasticsearch gensim numpy scipy scikit-learn
```

Other dependencies might exist, but they have been installed through conda-distribution

</br>

### Dataset
Due to overall size of dataset this has be downloaded separately:
1. [DBpedia long_abstract_en.ttl](http://downloads.dbpedia.org/2016-10/core-i18n/en/long_abstracts_en.ttl.bz2)
2. [DBpedia instance_types_en.ttl](http://downloads.dbpedia.org/2016-10/core-i18n/en/instance_types_en.ttl.bz2)
3. [SeMantic AnsweR Type dataset](https://github.com/smart-task/smart-dataset/tree/master/datasets/DBpedia)
4. [GloVe Wikipedia 2014 + Gigaword 5 pretrained embeddings](http://nlp.stanford.edu/data/glove.6B.zip/)

</br>

### File structure
Once all the files has been downloaded, extract them and place them in such a way that the directory structure is as follows(the files highlighted with `##` are the files you need to download&place yourself):
``` sh
📦IR-SMART
 ┣ 📂datasets
 ┃ ┣ 📂DBpedia
 ┃ ┃ ┣ 📜instance_types_en.ttl ##
 ┃ ┃ ┣ 📜long_abstracts_en.ttl ##
 ┃ ┃ ┣ 📜smarttask_dbpedia_test_questions.json ##
 ┃ ┃ ┗ 📜smarttask_dbpedia_train.json ##
 ┃ ┣ 📂gensim
 ┃ ┃ ┗ 📜...
 ┃ ┗ 📂glove
 ┃   ┣ 📜glove.6B.100d.txt ##
 ┃   ┣ 📜glove.6B.200d.txt ##
 ┃   ┣ 📜glove.6B.300d.txt ##
 ┃   ┗ 📜glove.6B.50d.txt  ##
 ┣ 📂results
 ┃ ┣ 📜advanced.csv
 ┃ ┣ 📜baseline.csv
 ┃ ┗ 📜test_type_predictions.csv
 ┣ 📜.gitignore
 ┣ 📜baseline_variable_test.ipynb
 ┣ 📜evaluation.ipynb
 ┣ 📜indexer.ipynb
 ┣ 📜indexer_compact.ipynb
 ┣ 📜LICENSE
 ┣ 📜README.md
 ┗ 📜trial_and_error.ipynb
```
The necessary code to execute is located in `indexer_compact.ipynb` and `evaluation.ipynb`

The other ipynb-files, contain an alternative larger index(`indexer.ipynb`), tests to see how varying parameter values affected the score(`baseline_variable_test`). `trial_and_error` contain a failed early attempt to make the ES-indexing more effective by first loading all datafiles into memory and then initializing ES-indexing(not recommended to run)

</br>

### Final Steps
* Execute all cells within `indexer_compact.ipynb`, this will generate the ElasticSearch index necessary for all consecutive steps.
  * PS: Ensure that Elasticsearch is running either as a systemd-process(linux), or that the bat-file is running(Windows)
  * PS: You will have to uncomment the functioncall `createTheIndex()`, in cell 5  to generate the index, and `indexData(10000)` mear the bottom of the file.

* Execute all cells within `evaluation.ipynb`, this will perform the evaluation using both the baseline and advanced implementation.
  * PS: Uncomment the `convertGlovetoGensim()` function call in cell 5, this is necessary to allow GenSim to parse the GloVe embedding-file.


</br>

<!-- USAGE EXAMPLES -->
## Usage

</br>

<!-- RESULT EXAMPLES -->
## Result
The achieved accuracy scores has been summarized in the table below:

|      Method      | Accuracy | NDCG@5 | NDCG@10 |
|:----------------:|:--------:|:------:|:-------:|
|  Strict Baseline |          |        |         |
| Lenient Baseline |          |        |         |
|  Strict Advanced |          |        |         |
| Lenient Advanced |          |        |         |

</br>

## Contributors

* [Contributors](https://github.com/BerntA/IR-SMART/graphs/contributors)

</br>

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.

</br>

<!-- CONTACT -->
## Contact
#### Bernt Andreas Eide
* e-mail: ba.eide@stud.uis.no
* GitHub: [@BerntA](https://github.com/BerntA "handle on GitHub")

#### Stian Seglem Bjåland
* e-mail: ss.bjaland@stud.uis.no
* GitHub: [@Chrystallic](https://github.com/Chrystallic "handle on GitHub")

