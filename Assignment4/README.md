# CSCI 580 Assignment 4: TSP with Simulated Annealing and a Genetic Algorithm

Geraldo Castro, Fall 2026

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Gcastro02/CSCI580_Geraldo_Castro/blob/main/Assignment_4/TSP_SA_and_GA_Assignment_Skeleton.ipynb)

For this assignment I solved the same 40-city Traveling Salesman Problem in two ways, Simulated Annealing (SA) with 2-opt moves and a Genetic Algorithm (GA) on permutation tours. I compared both of them against a nearest-neighbor baseline. I also added extra logging so I could compare how the two algorithms behave while they run, not just their final answers.

## What's in this folder

| File | What it is |
|---|---|
| `TSP_SA_and_GA_Assignment_Skeleton.ipynb` | The notebook with all the code, plots and outputs |
| `CSCI580_A4_Report_Geraldo_Castro.pdf` | The technical report |
| `README.md` | This file |

## How to run it

1. Click the **Open in Colab** badge above, or upload the notebook to Google Colab or Jupyter.
2. Go to **Runtime > Run all**.
3. The whole thing takes about a minute. The 10-seed comparison at the end of Part 6 is the slowest cell.

The only thing it needs besides the Python standard library is `matplotlib`, which Colab already has.

## What each part of the notebook does

- **Parts 1 to 4:** the provided code for generating cities, measuring tour length, doing 2-opt moves, plotting, and the nearest-neighbor baseline.
- **Part 5A (SA):** I filled in the acceptance rule (always take a better tour, take a worse one with probability `exp(-delta / T)`) and the geometric cooling schedule `T = max(T * alpha, 1e-12)`.
- **Part 5B (GA):** I wrote tournament selection, order crossover (OX), and swap mutation.
- **Part 6:** I made copies of SA and GA that log extra data while they run. They record the ΔE of every accepted and rejected SA move, the GA population average, and how many unique tours are left in the population each generation. The cells after that plot the data, compare SA and GA by number of tour evaluations, and run both algorithms with 10 different seeds. My answers to the four Part 6 questions are in the text cell at the end of that part.

## Results (from my Colab run)

| Method | Best length | Improvement over NN |
|---|---|---|
| Nearest neighbor | 6.0214 | (baseline) |
| Simulated Annealing | 5.0057 | 16.87% |
| Genetic Algorithm | 5.3672 | 10.86% |

Both methods passed the 10% improvement check with the default parameters. SA did better and was a lot more consistent across seeds. The GA lost most of its diversity in the first 30 or so generations and then got stuck. The report goes into the details.

## A note on reproducing the numbers

All the random number generators are seeded, so running the notebook again on Colab should give the same numbers. On a different computer or Python version you might see slightly different values, because tiny floating point differences can change which random moves get accepted. The overall pattern (SA beating GA, GA losing diversity early) should still be the same.
