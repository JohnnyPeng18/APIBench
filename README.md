# APIBench
APIBench is the benchmark for evaluating the performance of API recommendation approaches released in paper "*[Revisiting, Benchmarking and Exploring APIRecommendation: How Far Are We?](https://www.yunpeng.site/files/apirec.pdf)*".

## Download the Benchmark

As GitHub does not hold large datasets, you can download the benchmark dataset at [Zenodo]().

## Benchmark Details

Currently APIBench contains two sub-dataset for evaluating the performance of query-based and code-based API recommendation approaches, namely APIBench-Q and APIBench-C. Each sub-dataset has a Java version and a Python version.

### Task Definition

Here we give the definitions of query-based and code-based API recommendation:

**Query-based API recommendation:**  Approaches for query-based API recommendation aim at providing related APIs to developers given a query which describes programming requirements in natural language. The approaches can inform developers which API to use for a programming task.

**Code-based API recommendation:** Approaches for code-based API recommendation aim at predicting the next API given the code surrounding the point of prediction. They can directly improve the efficiency of coding.

### APIBench-Q

APIBench-Q is located in the folder `APIBench/APIBench_Q`. There are a `Python` folder and a `Java` folder in it for the Python and Java version of APIBench-Q.

Currently there are two `json` files in each version:

`Original{Java,Python}Queries.json`: It contains the original queries, corrsponding APIs and API classes, along with the source the query collected from (Stack Overflow or Tutorial Websites).

`Reformulated{Java,Python}Queries.json` : It contains all the elements in `Original{Java,Python}Queries.json`. Besides, it contains the reformulated queries derive from the original queries. The reformulated queries are wrapped by `@`.

Currently we apply the following query reformulation techniques to process the original queries:

| Technique                 | Source                                                       |
| ------------------------- | ------------------------------------------------------------ |
| RACK                      | https://github.com/masud-technope/RACK-Replication-Package   |
| NLP2API                   | https://github.com/masud-technope/NLP2API-Replication-Package |
| SEQUER                    | https://github.com/kbcao/sequer                              |
| Google Prediction Service | http://suggestqueries.google.com/complete/search?            |
| NLPAUG                    | https://github.com/makcedward/nlpaug                         |

**Number of queries in APIBench-Q:**

|            | Original | Expanded | Modified |
| ---------- | -------- | -------- | -------- |
| **Python** | 4,309    | 173,517  | 224,068  |
| **Java**   | 6,563    | 400,126  | 341,276  |

### APIBench-C

APIBench-C is located in the folder `APIBench/APIBench_C`. There are a `Python` folder and a `Java` folder in it for the Python and Java version of APIBench-C.

Currently there are two `zip` files and a `json` file in each version:

`{Java,Python}_MetaData.zip`: It contains the metadata `json` files for code in each domain. The `long`, `normal `and `short` kewords indicate the function with extremely long, moderate and extremely short lengths.

`{Java, Python}_Code.zip`: It contains the source code of repositories we mined from GitHub at April, 2021. Only `.py` and `.java` files are reserved.

`{Java, Python}RepoInfo.json`: It contains the information of Github repositories we collected, including the lines of code, code ratio, domain, files, forks, stars, addresses, etc.

**The structure of metadata:**

```python
"$filename$": {
		"$classname$" or "@Global@": {
      "$funcname$":{
        "@FuncLoc@":[
          $startlineno$,
          $endlineno$
        ],
        "$APIname$":[
          [
            $lineno$,
            $columnno$,
            "pure" or "attr",  #whether called from a class
            "Front", "Mdiddle" or "Back" #location of recommendation point
          ],
          ...
          ,
          "Standard", "User-defined", "Popular", or "Unknown" #category of APIs
        ]
      }
    }
}
```



**Statistics of APIBench-C:**

![image](https://github.com/JohnnyPeng18/APIBench/blob/main/imgs/benchc.png)

## Baseline Results

To facilitate further research on API recommendation and reduce the burden of re-implementing different baselines, we release all the evaluation results and outputs of 11 baselines along with 4 IDEs discussed in the paper.

Please go to the `experiment_results`folder for further detailed information.

## Cite Us

If you use our benchmark dataset and related experiment results or code, please cite us:

```
@misc{peng2021revisiting,
      title={Revisiting, Benchmarking and Exploring API Recommendation: How Far Are We?}, 
      author={Yun Peng, Shuqing Li, Wenwei Gu, Yichen Li, Wenxuan Wang, Cuiyun Gao, and Michael Lyu},
      year={2021},
      archivePrefix={arXiv},
      primaryClass={cs.SE}
}
```

