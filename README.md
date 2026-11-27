# EstateLens

EstateLens explores how well property listings can predict house prices in India. The project includes a [browser-based estimator](index.html), a [Google Colab research notebook](PROJECT_MILESTONE_SML.ipynb), and the [compressed housing dataset](kagal-house_prices.csv.zip).

## Try the website

Download the repository using **Code → Download ZIP**, extract it, and open `index.html` in a browser. Choose one of six cities and adjust the area, bedroom and bathroom counts, property age, floor, parking, or transit access. The total estimate and effective price per square foot update as you type.

The standalone website uses illustrative city rates and property adjustments. It runs offline. The model evaluation below applies only to the Python notebook.

## How the research works

1. **Prepare the listings.** Convert prices expressed in lakh or crore to rupees, extract bedroom counts from listing titles, and parse carpet area, super area, bathrooms, and balconies. Combine those five numerical inputs with location, furnishing, transaction type, facing, and ownership.
2. **Explore the data.** Inspect the price distribution, plot carpet area against price, and use a correlation heatmap to examine relationships among numerical features.
3. **Train the models.** The final experiment keeps positive prices between the 1st and 99th percentiles, leaving 175,484 listings. It uses an 80/20 train–test split with random seed 42, scales numerical inputs, encodes categories, and trains three regressors on log-transformed prices.
4. **Evaluate predictions in rupees.** The notebook reverses the log transformation, compares test errors, plots actual against predicted prices, and ranks the leading features. Bathroom count, carpet area, and super area had the highest feature importance in the winning model.

## Results

The notebook records the following scores on the held-out portion of the filtered dataset. Error amounts are in lakh rupees. Lower errors and higher R² indicate better performance on this split.

| Model | Mean absolute error | Root mean squared error | R² |
| --- | ---: | ---: | ---: |
| Linear Regression | 39.71 | 155.91 | −1.309 |
| Decision Tree | 11.26 | 30.62 | 0.911 |
| Random Forest | 10.41 | 27.92 | 0.926 |

The Random Forest had the lowest average absolute error. Its ₹10.41 lakh figure describes the average across test listings. Individual errors can be larger, and the evaluation excludes the extreme ends of the price distribution.

## Run the notebook

1. Open [the notebook in Google Colab](https://colab.research.google.com/github/namandudeja052-cmd/EstateLens/blob/main/PROJECT_MILESTONE_SML.ipynb).
2. Download and extract `kagal-house_prices.csv.zip`. Keep the extracted filename `kagal-house_prices.csv`, which the notebook uses when reloading the data.
3. Choose **Runtime → Run all**. When the first upload cell prompts you, select the extracted CSV.
4. The final cell saves the winning preprocessing and regression pipeline as `house_price_best_model.pkl`. Download it from Colab’s Files panel to keep a copy. When using this pipeline separately, apply `numpy.expm1` to its predictions to recover prices in rupees.

## Project team

Musky Kumar, Naman Dudeja, and Aditya Verma developed this project for **CSET-211 — Statistical Machine Learning**.
