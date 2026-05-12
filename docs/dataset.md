# Dataset selection

## Candidate dataset
MVTec AD 2, as per its creator : 
> MVTec AD 2 is a dataset for benchmarking unsupervised anomaly detection methods on challenging use-cases from industrial inspection tasks. It expands existing benchmarks by eight new anomaly detection scenarios with more than 8,000 high-resolution images in total.

## Why MVTec AD 2?
This dataset is free to use for non-commercial purposes (exactly my use case), which is a first good argument. 

I, however, don't select a dataset because it's free, but rather because it serves my purposes : this dataset offers high-quality, industrial grade images with challenging defects to be detected for unsupervised training (which is my use-case). As it is not a dummy dataset, working on this dataset ensures I produce a system that can replicate the pipeline encountered in various industries - an end-to-end PoC that replicates systems used in industries.

As it is also an industry benchmark, it makes sure I work with the relevant kind of data for the industry, and that we speak the same language.

## How to proceed
Considering the training dataset (that is already perfectly organised between training, validation, and tests sets), I see that I have a few options : 
- sheet metal offers a good challenge, with surface defects
- vials offers a *serious false negatives* scenarios, where mistakes could lead to serious issues.
- wallplugs offers multiple items per batch scenarios, with then the requirement to properly identify the defects in a single image
- walnuts offers the same challenge as wallplugs, but with texturing issues
- fruitjelly seems to offer a nice challenge with really different products, with a seemingly strong reflection in order not to overfit.
- fabric offers texturing issues, with patterns.
- can brings the reflection on tracking the same object on multiple sub-images
- rice offers a good reflection on treating a set of individual items as a whole, similar to a texturing issue

## selected category
For this project, I will go with vials.
It offers the benefit of being quite visual for demos to customers, but at the same time complex enough to enable deep-dives in trade-offs between doubts & certainty (false positives, false negatives), system parameters (threshold etc.), costs of anomaly, decision traceability, human-in-the-loop, batch inference...

## limitations
This dataset is high quality, but we are not a in industry setting. Benchmark data are different from production lines, and if we are to use production data, we would then need to consider device setup & parameters, system performance, connection... This would be a project of a another size!
Of course, this project would then integrate into a governance, including business, cybersecurity, IT, ML-OPS etc.
The goal here is rather to demonstrate a system and a capability, than be a OTS product.