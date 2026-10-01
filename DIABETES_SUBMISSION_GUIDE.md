# Steps to run, publish and submit

## 1. Download and extract
Download Diabetes_Tuning_Ensemble_Project.zip. On Windows, right-click and choose Extract All. Open the diabetes-tuning-ensemble folder. The notebook is Diabetes_Tuning_Ensemble.ipynb and the CSV is data/diabetes.csv.

## 2. Understand the data-source note
The requested Kaggle link returned an access error during preparation:
https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database

The notebook was executed using the supplied public Pima CSV copy from:
https://github.com/npradaschnor/Pima-Indians-Diabetes-Dataset/blob/master/diabetes.csv

Keep both references and the source note in the notebook/README. The original Kaggle bytes could not be checked; the actual source hash is recorded. To reproduce the saved results, use the supplied CSV.

## 3. Run on Kaggle and get your notebook link
1. Sign in at https://www.kaggle.com/.
2. If the original dataset opens for you, choose New Notebook from that page. Otherwise go to Code and choose New Notebook.
3. In the editor, choose File > Import Notebook (or Upload Notebook), then upload Diabetes_Tuning_Ensemble.ipynb.
4. Use the title `Pima Diabetes - Tuning and Ensemble Comparison`.
5. Attach diabetes.csv through Add Input/Add Data. If the original dataset is available, you can attach it. Otherwise use Upload/New Dataset to upload the supplied diabetes.csv, give that data asset a descriptive name and preserve the mirror attribution in its description, then attach it. If the upload option is not in the notebook editor, create the data asset through Kaggle's Datasets > New Dataset flow first, then return to Add Input.
6. Confirm diabetes.csv appears in the Input/Data panel. The notebook searches all subfolders of /kaggle/input/ automatically. No hard-coded dataset-folder edit is needed.
7. Choose Run All. CPU is sufficient; do not enable a GPU. Allow a few minutes for all CV fits.
8. Check that the baseline CV score, both search best-parameter/score outputs, and the four-row results table are visible without errors.
9. Choose Save Version > Save & Run All, or the equivalent option that executes and saves results. Wait for success.
10. Use Share/visibility settings to make the notebook Public if required by your teacher. Review any input-visibility prompt shown by Kaggle when publishing.
11. Open the saved notebook page and copy its actual URL. A typical shape is https://www.kaggle.com/code/YOUR_USERNAME/YOUR_NOTEBOOK_SLUG . Do not submit a placeholder URL.
12. Test the saved notebook link in an incognito window to confirm it can be viewed. Kaggle menu labels may vary slightly.

Kaggle reference: https://www.kaggle.com/docs/notebooks

## 4. Create your GitHub repository link
1. Sign in and open https://github.com/new.
2. Name the repository `diabetes-tuning-ensemble` and add a description such as `Decision Tree tuning with GridSearchCV and RandomizedSearchCV plus a Random Forest ensemble`.
3. Choose Public if required and add a starter README, then create the repository.
4. Choose Add file > Upload files. Upload the CONTENTS of the extracted project folder, including the notebook, README, requirements, guide, data folder and outputs folder. Upload the extracted files rather than only the ZIP.
5. The supplied README replaces the starter README. Commit the upload with a message such as `Add classifier tuning and ensemble assignment`. Complete and merge a pull request if GitHub presents a branch/PR flow.
6. Open the notebook on GitHub to verify the executed results and charts are visible. GitHub displays saved output; it does not execute the notebook.
7. Copy the repository URL, usually shaped like https://github.com/YOUR_USERNAME/diabetes-tuning-ensemble .
8. Add your real Kaggle notebook URL to README.md using the edit/pencil button. You can also add the GitHub URL to the first Markdown cell of the Kaggle notebook and save another version.
9. Test public links in an incognito window. If the teacher requires private sharing, follow their access instructions instead.

GitHub references:
- https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository
- https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

## 5. Optional: run in Google Colab
Open https://colab.research.google.com/, choose Upload notebook and upload the .ipynb. Upload diabetes.csv through the left Files sidebar, then choose Runtime > Run all. The loader checks /content/diabetes.csv. Re-upload the CSV after a runtime reset.

## 6. Submit
- The executed Diabetes_Tuning_Ensemble.ipynb if a file upload is requested.
- Your own published Kaggle notebook URL.
- Your GitHub repository URL.
- The original dataset URL and actual public-copy URL as source attribution.
- The required table is in the notebook and outputs/tuning_ensemble_results.csv.

Your personal publication links are created after publishing under your accounts; they have not been created here. The dataset URL alone does not show your completed work.

## What each stage demonstrates
1. Baseline: establish Decision Tree performance using five-fold CV.
2. GridSearchCV: test all 90 predefined configurations and report the best CV score and parameters.
3. RandomizedSearchCV: test 30 sampled configurations from the same space and report the best CV score and parameters.
4. Random Forest: combine 300 trees and evaluate using the same split/folds.
5. Comparison: display Model | CV Accuracy | Test Accuracy | Best Params, with fixed settings clearly identified for the untuned baseline and ensemble.

Do not manually change scores or repeatedly change settings based on test accuracy. The test set is the final evaluation, not tuning data.
