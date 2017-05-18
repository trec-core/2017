# TREC 2017 Core Track

### Mailing list

* https://groups.google.com/d/forum/trec-core

### TIMETABLE
+ Collection available to participants: February, 2017 [Done]
+ Topics available to participants: ~~April 30, 2017~~ Beginning of May [Done]
+ The evaluation measure will be decided: ~~May 7, 2017~~ Beginning of May
+ Phase 1 runs due from participants: June 18, 2017
+ Phase 2 runs due from participants: July 31, 2017
+ TREC 2017 notebook paper deadline: mid-October
+ TREC 2017 conference: November 14 - 17, 2017

### INTRODUCTION
The primary goals of the proposed core track are three-fold: (a) to bring together the community in a common track that could lead to a diverse set of participating runs, (b) to build one or more new test collections using more recently created documents, and (c) to establish a (new) test collection construction methodology that avoids the pitfalls of depth-k pooling.

As a side goal the track intends to:
1. study the shortcomings of test collections constructed in the past
2. experiment with new ideas for constructing test collections
3. expand existing test collections in a number of dimensions:
   * new participant tasks (ad-hoc/interactive)
   * new relevance judgments (binary/multilevel)
   * new pooling methods
   * new assessment resources (NIST / Crowdsourcing)
   * new retrieval systems contributing documents (Manual/Neural/Strong baselines)

### TRACK TASK
The participants task will be ad-hoc search. Automatic and manual runs are encouraged. The organizers of the track will provide participants with a task (title/description/narrative of TREC topics) and allow participating sites to run the experiment as they wish as long as they contribute a ranked list of documents as an output.

### DATA AND RESOURCES

**Collection**: NYTimes corpus (https://catalog.ldc.upenn.edu/ldc2008t19) – Cost: $300

**Topics**: The topics provided are the TREC Robust Track topics. Most of the topics have have remained the same but some have been revised to reflect the time past (e.g. some descriptions and narratives were turned into historical topics, while others were brought up todate).

There are two sets of topics:
1. Topics to be judged by [NIST](https://trec-core.github.io/2017/core_nist.txt)
2. Topics to be judged by [crowd workers](https://trec-core.github.io/2017/core_crowd.txt)

**Relevance Assessments**:
1. NIST assessors (~50 queries)
2. Crowdsourcing (~200 queries)

### SUBMISSION GUIDELINES

**Phase 1.** By *June 18, 2017*, a site may submit up to 3 submissions of 10,000 top-ranked results. NIST will make a good-faith effort to judge the top-k documents in the site-specified preferred n runs. The values of k and n will be determined by NIST on or around June 19th based on the total number of runs submitted and the overlap in the retrieved documents. Runs will be ranked in order of preference by the site at the time of submission. Every site will be guaranteed that at least one run will be judged to depth k.
 
**Phase 2a**. By *July 31, 2017*, a site may submit up to 7 additional submissions of 10,000 top-ranked results. Note that these additional runs may be submitted at any point, though if they are submitted after June 18th they will not be included in the initial judging.
 
**Phase 2b**. Sometime after the final set is submitted, all submitted runs (from both phases) will be ranked by a combination of precision at k (high quality runs) and the number of unique relevant documents in the top k (unusual runs), computed using both NIST judgments and possibly crowdsourced judgments. (The actual formula needs to be discussed.) NIST will judge the best-scoring m runs to a depth k’ deeper than k, with the values of m and k’ will be determined by NIST based on the total number of submitted and high-scoring runs and the overlap in the retrieved documents. There will be no guarantee that any particular run will be judged in this phase. In particular, there will be no guarantee that every site will have a run with deeper judgments.
 
Note that the scoring of runs in Phase 2 is based upon judgments from Phase 1. That means that runs that were not selected for judging in Phase 1 (either because they were not in the preferred n runs from a site in Phase 1 or because they were submitted in Phase 2) are less likely to be selected for deeper judgment. This challenge is inherent in the approach being taken.

---

System data structures (such as dictionaries, indices, thesauri, etc. whether constructed by hand or automatically) can be built using existing documents, topics, and relevance judgments, but these structures may not be modified in response to the new test topics.  For example, you can't add topic words that are not in your dictionary, nor may the system data structures be based in any way on the results of retrieving documents for the test topics and having a human look at the retrieved documents. A corollary of this rule is that your system may not be tuned to the TREC 2017 topics.

There are many possible methods for converting the supplied topic into queries that your system can execute. TREC defines two broad categories of methods, "automatic" and "manual", based on whether manual intervention is used. Automatic construction is when there is no human involvement of any sort in the query construction process; manual construction is everything else. Note that this is a very broad definition of manual construction, including both runs in which the queries are constructed manually and then run without looking at the results, and runs in which the results are used to alter the queries using some manual operation.

The result of a run is generally a ranking of the top 10,000 documents retrieved for each topic.  You may submit fewer than 1000 documents for a topic, but the ranked retrieval evaluation measures used in TREC evaluate to 10,000 and count empty ranks as irrelevant (so your score cannot be hurt by returning 10,000 documents). Similarly, systems that do not rank documents perform poorly as evaluated by these measures. Note that trec_eval evaluates a run based strictly on scores, not on the ranks you assign in your submission. If you want the precise ranking you submit to be evaluated, the scores must reflect it.

The format to use when submitting ranked results is as follows, using a space as the delimiter between columns.  The width of the columns in the format is not important, but it is important to include all columns and have some amount of white space between the columns.

       30 Q0 ZF08-175-870  0 4238 prise1
       30 Q0 ZF08-306-044  1 4223 prise1
       30 Q0 ZF09-477-757  2 4207 prise1
       30 Q0 ZF08-312-422  3 4194 prise1
       30 Q0 ZF08-013-262  4 4189 prise1
       etc.

where:
  + the first column is the topic number.
  + the second column is the query number within that topic.  This is currently unused and should always be Q0.
  + the third column is the official document number of the retrieved document and is the number found in the "docno" field of the document.
  + the fourth column is the rank the document is retrieved,
  + the fifth column shows the score (integer or floating point) that generated the ranking.  This score must be in descending (non-increasing) order and is important to include so that we can handle tied scores (for a given run) in a uniform fashion (trec_eval sorts documents by these scores, not your ranks).
  + the sixth column is called the "run tag" and should be an unique identifier for your group AND for the method used. That is, each run should have a different tag that identifies the group and the method that produced the run. 

NIST will release a routine that checks for common errors in the result files including duplicate document numbers for the same topic nvalid document numbers, wrong format, and duplicate tags across runs. This routine will be made available to participants to check their runs for errors prior to submitting them.  Submitting runs is an automatic process done through a web form, and runs that contain errors cannot be processed.

### ASSESSMENT AND EVALUATION

**Assessment**: The pooling method is TBD.

**Evaluation**: Participating runs will be evaluated in terms of (a) their ability to rank relevant documents at the top of the returned list, and (b) their ability to contribute unique relevant documents to the pool. A exact evaluation measure/method is TBD.

### Coordinators

* Evangelos Kanoulas (e.kanoulas@uva.nl), University of Amsterdam
* James Allan (allan@cs.umass.edu), University of Massachusetts
* Donna Harman (donna.harman@nist.gov), NIST 
