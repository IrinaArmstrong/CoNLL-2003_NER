# CoNLL-2003_NER
Named entity recognition (NER) on CoNLL-2003 dataset (English subset).

---

**The main notebook with BERT models** training and evaluation cycle for this task is: [My_TestTaskNER.ipynb](https://github.com/IrinaArmstrong/CoNLL-2003_NER/blob/main/My_TestTaskNER.ipynb) <br>
**The model with additional CRF head** was running in separate notebook [My_TestTaskNER CRF](https://github.com/IrinaArmstrong/CoNLL-2003_NER/blob/main/My_TestTaskNER CRF.ipynb) due to different libraries & frameworks versions.

#### Used instruments
* pytorch and pytorch-lightning
* transformers (including: datasets)
* allennlp
* tensorboard (for monitoring training process)
* seqeval and conlleval (as metrics)

## Models Results & Comparison
For greater clearness, I will summarize everything in the table below:

| Model  	|  Overall Acc 	|  Overall Precision 	|  Overall Recall 	|   Overall F1 	|   LOC F1 	|   MISK F1 	|   ORG F1 	|   PER F1 	|   Size (Mb.)	| 
|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-: |:-:	|
|  BERT base cased 	|  0.991 	|   0.874	|  0.892 	|   0.881	| 0.881  	|  0.680 	|   0.774	|  0.878 	|  435.594	|
|  BERT base uncased 	|   0.991	|   0.874	|   0.892	|  0.881 	|   0.880	|   0.680	|  0.774 	|   0.878	|  435.594 	|
|  BERT CRF head 	|   0.977	|   0.892	|   0.904	|   0.897	|   0.898	|   0.708	| 0.792  	|   0.895	|  433.270	|

### **Summary**

*   As expected, **the register-sensitive model (BERT cased) is qualitatively outperforms to the register-insensitive (BERT uncased)** one by 0.8 (~1%) percentage points (on overall F1 measure). <br>
Moreover, mostly **suffers precision scores** and recall over all entities increases.  <br>
Also, it is noticeable that the problems are caused by detecting MISK (names of miscellaneous entities) and ORG (organizations) types of named entities, which is explained by the fact that without capitalizing the initial tokens of these entities, they are difficult to identify in the text. <br>

*   The harders named entity type for detection is **MISK (names of miscellaneous entities)** (examples: *German, EU-wide, Spanish, BSE, British and etc.*) 
due to the questionable semantic boundaries of the class (very close to LOC or O).

### Results

<div align=center>

![](Sample.PNG?raw=true)
*Detected Named Entities from notebook*

</div>


### **Future improvements**

*   Use larger models such as **BERT large (cased)** and compare the quality gain (while taking into account the advantages of case-sensitive models.
*   There is **a strong imbalance of classes** and another next stap is to augment training dataset with new samples for NE classes: ``` [`PER`, `ORG`, `LOC`, `MISK`] ```
