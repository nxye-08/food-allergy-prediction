# Predicting Food Allergy in Children Who Have No Family History of Allergies

## Key Findings

## Datasets
Everything here is public, and the notebook pulls it in automatically.

* NHIS 2021. A national survey where children can be matched to their parents
through a household ID. This is what makes the no family history analysis
possible.
* NHANES 2005 to 2006. The one survey cycle that measured total IgE in blood,
which is why the biological model is built on it.
* CHOP. A large set of pediatric records released publicly on Zenodo, used to
check the eczema result on a much bigger sample.

## How to Reproduce
1. Open notebook/food_allergy_analysis.ipynb in Google Colab, or run it locally
using the packages in requirements.txt.
2. Run the cells top to bottom.
3. The data downloads on its own, so there is nothing to fetch by hand. Figures
save to the working folder as the notebook runs.

## Methods

* Models: logistic regression, random forest, and gradient boosting.
* Feature selection using all three standard families: mutual information (filter),
recursive feature elimination (wrapper), and LASSO with tree importance
(embedded). I also ran mRMR as a second opinion.
* Scoring: five fold cross validation, using AUC as the main measure.

## Limitations

* I did not apply the survey sampling weights, so these numbers describe the
samples I built rather than the country as a whole
* The biological model rests on one NHANES cycle. Total IgE only exists in the 2005
to 2006 data, so there is nothing to pool it with
* The NHANES part looks at children in general, not specifically children without a
family history, because that survey does not ask children about family history
* Eosinophils go up because an allergic reaction is already happening. They mark an
allergy that exists, so they cannot screen a healthy baby before anything starts
* The core biology here is settled science. I measured and framed it in a new way,
but I did not discover it
