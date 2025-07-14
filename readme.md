# Weekly Meal Plan Generator

A Python-based GUI application that uses a genetic algorithm (NSGA-II) to generate weekly meal plans optimized for protein intake, calorie targets, and cost.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Dataset](#dataset)
- [Usage](#usage)
  - [1. Set Meal Plan Count](#1-set-meal-plan-count)
  - [2. Set Calorie Target and Run Algorithm](#2-set-calorie-target-and-run-algorithm)
  - [3. Set Item Count, Calorie Target, and Run Algorithm](#3-set-item-count-calorie-target-and-run-algorithm)
- [Configuration](#configuration)
- [Code Structure](#code-structure)
- [Dependencies](#dependencies)
- [License](#license)

## Features

- Interactive GUI using Tkinter
- Load and process food dataset from an S3 bucket
- Customize meal plan size by item count or calorie target
- Multi-objective optimization with NSGA-II:
  - Maximize protein intake
  - Minimize deviation from calorie target
  - Minimize price, fat, sodium, and carbohydrates
- Display formatted meal plan results with daily averages and cost

## Prerequisites

- Python 3.7 or higher
- AWS credentials configured (if you plan to modify or fetch data from S3)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/yourusername/weekly-meal-plan-generator.git
   cd weekly-meal-plan-generator
   ```

2. (Optional) Create and activate a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate  # macOS/Linux
   venv\Scripts\activate     # Windows
   ```

3. Install required packages:


   ```bash
   pip install numpy pandas deap boto3
   ```

## Dataset

The application loads its food dataset from a publicly accessible S3 URL:

```
https://project444.s3.amazonaws.com/ProjectDataset.csv
```

The CSV should include at least the following columns:

- `asin` (string): Unique identifier
- `Name` (string)
- `Calories` (numeric)
- `Protein (g)`
- `Total Fat (g)`
- `Total Carbohydrate (g)`
- `Sodium (mg)`
- `Price ($)`
- `Total Serving` (servings per item)

## Usage

Run the main script to launch the GUI:

```bash
python meal_plan_generator.py
```

Upon launching, follow these steps:

### 1. Set Meal Plan Count

1. Click **Set mealplan count**.
2. Enter the number of distinct meal plans to generate (e.g., 3).

### 2. Set Calorie Target and Run Algorithm

1. Click **Set calorie target and run algorithm**.
2. Input your desired daily calorie intake (e.g., 2000).
3. The algorithm computes an optimal set based on the calorie target and default item count.
4. Results appear in a new window with meal plan details.

### 3. Set Item Count, Calorie Target, and Run Algorithm

1. Click **Set item count, calorie target and run algorithm**.
2. Specify the number of items per plan (between 2 and 21).
3. Enter the desired daily calorie intake.
4. The solver runs with customized parameters and displays results.

## Configuration

- ``: Number of items in each candidate solution (default 20).
- ``: User-specified calories per day.
- **Genetic Algorithm Parameters**:
  - Population size: 100
  - Generations: 2000
  - Crossover probability (`cxpb`): 0.5
  - Mutation probability (`mutpb`): 0.2

These values can be adjusted directly in the source code.

## Code Structure

- ``: Main application script
- **GUI components**: Tkinter windows and dialogs
- **Data loading**: Pandas reads CSV from S3
- **Genetic Algorithm**: DEAP library with NSGA-II
- **Evaluation**: Custom fitness function accounting for protein, calories, macro- and micro-nutrients, and cost

## Dependencies


```
numpy
pandas
deap
boto3
```

`tkinter` is included in the Python standard library.


