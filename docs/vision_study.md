# Vision task typology for manufacturing inspection

## 1. Context

Quick study & comparison on cv approaches for this project

## 2. Compared approaches
4 main (and often complementary) approches :
- Image classification
- Object detection
- Semantic / instance segmentation
- Anomaly detection

## 3. Comparison matrix

| Criterion | Classification | Object detection | Segmentation | Anomaly detection |
|---|---|---|---|---|
| Output | label(s) | set of bounding boxes & class labels associated | set of image segments with associated labels (pixel-wise) | a score (anomaly prediction), eventually a mask (set of anomaly pixels) and heatmap (scores of anomaly per pixel) |
| Required labels | on dataset | on various data objects, with labels | on each pixel, but for training on each segment | baseline of normal objects, anomaly labels useful for detection |
| Annotation cost | low : each item in dataset need to be labeled | medium : annotation of objects with associated class, and annotation of object within data | high : higher precision on data labeling & boundary identification | low : just a set of standard and non anomaly objects |
| Can localize defect? | no : label is attributed to the whole data | yes | yes, precisely (pixel wise) | yes, precisely with a "confidence" score |
| Works with few defects? | yes, but does not give information on the number of defects, only if 1+ are present. | yes at inteference, but needs enough defect examples for training | yes: out of segments pixels can be interpreted as defects | yes |
| Handles unknown defects? | no | no | no | yes |
| Interpretability | low : does not explicit where the defect is or why it's labeled as a defect | middle : can detect and indicate where is a known defect | high : indicates known defects precisely, and can also identify areas of unknown segments (ie defects for shapes that are already known) | high, but can be influenced by noise, imprecise, or difficult to interpret |
| Industrial fit | low : easy to implement, yields pass/fail results | middle : works on known defects, but limited on unknown defects, textural defects...| good : can be used to reliably detect defects, handle multiples typology of pieces at the same time, and can indicate area of unknowns. | good, if normal training data is representative and threshold calibration is done properly |
| Main limitations | medium : easy to implement and useful for pass/fail, but limited for operator review and root cause analysis | only works on already seen data | processing power is bigger, data prep is more costly, as is inference | main limitation is about getting representative data for training, threshold can be hard to calibrate |

## 4. Scenario analysis

4 scenarios : 
#A : Business wants to know if an object is conform or not
In this case, a simple classification will work : pass/fail results, with low inference costs and low prep cost. It's best value for money, if labeled conform/non conform examples are available, of course.

#B : Business wants to know where a defect is located, eg a shard
In this case, business wants to know where the defect is, but there's a question that needs to be asked : why? If it's for further engineering analysis, a simple bounding box will be enough. If data is needed for further analysis via computer vision, segmentation would be useful.
Once again, it's a matter of costs against benefits.

#C : Business has a lot of standard images, but does not have defect data
Perfect use case for anomaly detection via deviation from a normal baseline.

#D : Business has lots of data, several known defects and labeled data
Here, we need to refine the objective. Here, segmentation would work, useful for further analysis, defect evolution over time (that could answer industrial tests on materials : can a defect be influenced by materials in the object?) etc.
For simpler analysis purposes, bounding boxes would be enough (eg for reports on how many defects on a batch etc.)

## 5. Preliminary architectural choice
