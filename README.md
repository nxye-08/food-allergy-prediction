# Predicting Food Allergy in Children Who Have No Family History of Allergies

## Summary
Food allergies affect roughly eight percent of children in the United States, causing life threatening reactions. Family history is commonly used to flag children at risk, yet many children develop food allergies despite having no family history. We used a machine learning approach to test how well food allergies can be predicted in these children, and what factors limit that prediction. We hypothesized that demographic and socioeconomic variables collected in national health surveys would predict food allergies in this subgroup. In the 2021 National Health Interview Survey, children were linked to parents through household identifiers, and we identified 5,425 children with no parental allergy history, with 7% of them developing allergies. Our hypothesis was refuted. Models trained on all 159 available demographic variables reached a maximum cross validated area under the curve (AUC) of 0.602. In the 2005 to 2006 National Health and Nutrition Examination Survey, models using routine blood count data reached an AUC of 0.718 for elevated immunoglobulin E, with eosinophil level the strongest predictor across four independent methods. In 294,905 pediatric records, eczema before age two was associated with the development of food allergies in the future (odds ratio 3.88, 95% CI 3.73 to 4.05). Our results suggest that the variables carrying predictive signal are largely absent from public health surveys and indicate which early life clinical measures these surveys would need to collect.

## Key Findings

| Finding  | Result |
| ------------- | ------------- |
| Food allergy rate in children with no family history (NHIS 2021)  | 7.0% |
| Best model using every demographic variable available, 159 in total (NHIS)  | AUC 0.602 |
| Model using a routine blood count (NHANES 2005 to 2006)  | AUC 0.718  |
| Strongest single predictor, agreed on by four separate methods  | Eosinophil percentage  |
| Eczema before age two and later food allergy (CHOP, 294,905 children)  | Odds ratio 3.88, 95% CI 3.73 to 4.05  |

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
