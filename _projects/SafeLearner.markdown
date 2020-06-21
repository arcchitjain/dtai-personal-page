---
layout: page
title: SafeLearner
description: SafeLearner is based on the work, titled as Scalable Rule Learning in Probabilistic Knowledge Bases, by Arcchit Jain, Tal Fredman, Ondrej Kuzelka, Guy Van den Broeck, and Luc De Raedt. The work was accepted and published in the 1st Conference on Automated Knowledge Base Construction (AKBC) 2019 and held at the University of Massachusetts from 20 - 22 May 2019. It's code can be found at <a class="page-link" href="https://github.com/arcchitjain/SafeLearner/tree/AKBC19">https://github.com/arcchitjain/SafeLearner/tree/AKBC19</a>.
img: /assets/img/pattern.png
# redirect: https://github.com/arcchitjain/SafeLearner/tree/AKBC19
---

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/akbc_logo_crop.png" alt="" title="AKBC Logo"/>
    <img class="col two left" src="{{ site.baseurl }}/assets/img/Podium Pic - UMass.jpeg" alt="" title="Presenting SafeLearner at AKBC19"/>
</div>

## Motivation
Knowledge Bases (KBs) are becoming increasingly large, sparse and probabilistic. These KBs are typically used to perform query inferences and rule mining. But their efficacy is only as high as their completeness. Efficiently utilizing incomplete KBs remains a major challenge as the current KB completion techniques either do not take into account the inherent uncertainty associated with each KB tuple or do not scale to large KBs. 

Probabilistic rule learning not only considers the probability of every KB tuple but also tackles the problem of KB completion in an explainable way. For any given probabilistic KB, it learns probabilistic first-order rules from its relations to identify interesting patterns. But, the current probabilistic rule learning techniques perform grounding to do probabilistic inference for evaluation of candidate rules. It does not scale well to large KBs as the time complexity of inference using grounding is exponential over the size of the KB. In this paper, we present SafeLearner - a scalable solution to probabilistic KB completion that performs probabilistic rule learning using lifted probabilistic inference - as faster approach instead of grounding. 


## Impact

We proposed a probabilistic rule learning system, named SafeLearner, that supports lifted inference. It first performs structure learning by mining independent deterministic candidate rules using AMIE+ and later executes joint parameter learning over all the rule probabilities. SafeLearner extends ProbFOIL+ by using lifted probabilistic inference (instead of using grounding). Therefore, it scales better than ProbFOIL+. In comparison with AMIE+, it is able to jointly learn probabilistic rules over a probabilistic KB unlike AMIE+ which only learns independent deterministic rules (with confidences) over a deterministic KB. We experimentally show that SafeLearner scales as good as AMIE+ when learning simple rules. Trying to learn complex rules leads to unsafe queries which are not suitable for lifted inference. But lifted inference helps SafeLearner in outperforming ProbFOIL+ which does not scale to NELL Sports Database without the help of a declarative bias.


## Documentation

This is a documentation on how to install and use the codes of **[SafeLearner](https://github.com/arcchitjain/SafeLearner/tree/AKBC19)**.
It is licensed under [Apache-2.0 license](https://github.com/arcchitjain/SafeLearner/blob/master/LICENSE).


### Dependencies
* Python 3.6
* PostgreSQL (version > 9.1)
* Java


### Installation
#### Use *pipenv*  to install the following required python packages
1. Install *pipenv* first, if not already installed:
```
pip install pipenv
```
2. Clone this repository to your local machine
```
git clone -b AKBC19 --single-branch https://github.com/arcchitjain/SafeLearner.git
```
3. Move to this repository and install all the required packages:
```
pipenv install
```
This should install the following packages in a virtual environment of Python 3.6 for you:
* *ad*
* *nltk*
* *problog*
* *psycopg2*
* *sqlparse*
* *sympy*

4. Now, to activate the virtual environment, run the following:
```
pipenv shell
```
5. Steps to install *Prover9* - Python module for *nltk* <br>
*Prover9* is a non-standard package which gets installed by the following steps:
	1. Download  LADR-2009-11A.tar.gz from [https://www.cs.unm.edu/~mccune/prover9/download/](https://www.cs.unm.edu/~mccune/prover9/download/)
	2. Extract its files and run ‘make all’
	3. Copy all the files created in ‘bin’ folder to any of the following locations:
``` 
    /usr/local/bin/prover9 
    /usr/local/bin/prover9/bin
    /usr/local/bin
    /usr/bin
    /usr/local/prover9
    /usr/local/share/prover9
```

### Input Parameters

**SafeLearner** supports many variations of its main algorithm:

Argument | Description
-------|------
`file` | Input file with location (Required Argument)
`-t` | Target predicate with arity (Eg: -t "coauthor/2")
`-l` | Maximum rule length; Maximum number of total literals in a rule (including head)
`--log` | Logger file with location 
`-v` | Verbosity level of the log (Use -v -v -v for full verbosity)
`-s` | Specify scoring/loss function for SGD (Default: "cross_entropy", Other options: "accuracy", "squared_loss")
`--lr` | Specify earning rate parameter of SGD
`-i` | Specify number of iterations of SGD
`-c` | Cost of misclassification for negative examples (Default: 1.0)
`-q` | Input -q to denote an input file with facts enclosed in double quotes
`--minpca` | Minimum PCA Confidence Threshold for *Amie+*
`--minhc` | Minimum Standard Confidence Threshold for *Amie+*
`-r` | Allow recursive rules to be learned
`-a` | Specify maximum number of *Amie+* to be considered as candidate rules
`-d` | Disable/ignore typing of predicates while pruning *Amie+* rules
`--db_name` | Specify the name of the database to be used	
`--db_user` | Specify the username that can access the database
`--db_pass` | Specify the password to access the database
`--db_localhost` | Specify the localhost to can access the database


### Example

You need to create a PostgreSQL Database first before running **SafeLearner**:
```
psql
CREATE DATABASE test_dbname;
\q
```
This creates an empty database in *psql* server on your machine.  Now, in the following command,  replace 'test_dbuser' with the username of your *psql* server and add password and localhost name if required.
```
python3 safelearner.py Data/Test-Coauthor/illustrative_example.pl --log test.log -v -v -v -i 10000 --lr 0.00001 --minpca 0.00001 --minhc 0.00001 --db_name test_dbname --db_user test_dbuser
```
Running this command will execute **SafeLearner** on a small toy dataset and would ensure that it had got installed correctly.

## Acknowledgements

The authors express their sincere regards to Anton Dries and Sebastijan Dumancic for their invaluable input, and the reviewers for their useful suggestions. This work has received funding from the European Research Council under the European Union's Horizon 2020 research and innovation programme (#694980 SYNTH: Synthesising Inductive Data Models), from the various grants of Research Foundation - Flanders, NSF grants #IIS-1657613, #IIS-1633857, #CCF-1837129, NEC Research, and a gift from Intel.
