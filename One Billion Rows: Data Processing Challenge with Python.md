# One Billion Rows: Data Processing Challenge with Python


## Introduction

The goal of this project is to demonstrate how to efficiently process a massive data file containing 1 billion rows (~14GB), specifically to calculate statistics (including aggregation and sorting, which are heavy operations) using Python.

This challenge was inspired by the One Billion Row Challenge, originally proposed for Java.

The data file consists of temperature measurements from various weather stations. Each record follows the format `<string: station name>;<double: measurement>`, with the temperature presented to one decimal place.

Here are ten sample lines from the file:

```
Hamburg;12.0
Bulawayo;8.9
Palembang;38.8
St. Johns;15.2
Cracow;12.6
Bridgetown;26.9
Istanbul;6.2
Roseau;34.4
Conakry;31.2
Istanbul;23.0
```

The challenge is to develop a Python program capable of reading this file and calculating the minimum, average (rounded to one decimal place), and maximum temperature for each station, displaying the results in a table sorted by station name.

Example table:

| Station        | Min Temperature | Mean Temperature | Max Temperature |
|----------------|-----------------|------------------|-----------------|
| Abha           | -31.1           | 18.0             | 66.5            |
| Abidjan        | -25.9           | 26.0             | 74.6            |
| Abéché         | -19.8           | 29.4             | 79.9            |
| Accra          | -24.8           | 26.4             | 76.3            |
| Addis Ababa    | -31.8           | 16.0             | 63.9            |
| ...            | ...             | ...              | ...             |

## Dependencies

To run the scripts in this project, you will need the following libraries:

- **Polars**: `0.20.3`
- **DuckDB**: `0.10.0`
- **Dask[complete]**: `^2024.2.0`

## Results

Tests were conducted on a laptop equipped with an Apple M1 processor and 8GB of RAM. The implementations used pure Python, Pandas, Dask, Polars, and DuckDB. The runtime results for processing the 1 billion row file are presented below:

| Implementation     | Time        |
|--------------------|-------------|
| Bash + awk         | 25 minutes  |
| Python             | 20 minutes  |
| Python + Pandas    | 263 sec     |
| Python + Dask      | 155.62 sec  |
| Python + Polars    | 33.86 sec   |
| Python + DuckDB    | 14.98 sec   |

## Conclusion

This challenge clearly highlighted the effectiveness of various Python libraries in handling large volumes of data. Traditional methods like Bash (25 minutes), pure Python (20 minutes), and even Pandas (5 minutes) required a series of tactics to implement batch processing, while libraries like Dask, Polars, and DuckDB proved to be exceptionally efficient, requiring fewer lines of code due to their inherent ability to distribute data in "streaming batches" more effectively. DuckDB excelled, achieving the shortest runtime thanks to its execution and data processing strategy.

These results emphasize the importance of selecting the right tool for large-scale data analysis, demonstrating that Python, with the right libraries, is a powerful choice for tackling big data challenges.

**DuckDB also wins with 1 million rows, making it truly the best.**

## How to Run

To run this project and reproduce the results:

1. Clone this repository.
2. Set the Python version using `pyenv local 3.12.1`.
3. Run the following commands:
    ```bash
    poetry env use 3.12.1
    poetry install --no-root
    poetry lock --no-update
    ```
4. Execute the command `python src/create_measurements.py` to generate the test file.
   - Be patient and go make a coffee; it will take about 10 minutes to generate the file.
5. Ensure you have installed the specified versions of Dask, Polars, and DuckDB.
6. Run the scripts:
    ```bash
    python src/using_python.py
    python src/using_pandas.py
    python src/using_dask.py
    python src/using_polars.py
    python src/using_duckdb.py
    ```
   You can run these through a terminal or a Python-supported development environment.

This project highlights the versatility of the Python ecosystem for data processing tasks, offering valuable insights into tool selection for large-scale analysis.

## Bonus

To run the Bash script described, follow these steps:

1. Make sure you have a Unix-like environment, such as Linux or macOS, that supports Bash scripts natively.
2. Ensure the tools used in the script (`wc`, `head`, `pv`, `awk`, and `sort`) are installed on your system.
   - Most of these tools come pre-installed on Unix-like systems, but `pv` (Pipe Viewer) may need to be installed manually.

### Installing Pipe Viewer (pv)

If you don't have `pv` installed, you can easily install it using your system's package manager. For example:

- On Ubuntu/Debian:
    ```bash
    sudo apt-get update
    sudo apt-get install pv
    ```
- On macOS (using Homebrew):
    ```bash
    brew install pv
    ```

### Preparing the Script

1. Give execution permission to the script file. Open a terminal and run:
    ```bash
    chmod +x process_measurements.sh
    ```
2. Run the script. Open a terminal and run:
    ```bash
    ./src/using_bash_and_awk.sh 1000
    ```
   In this example, only the first 1000 lines will be processed.

When running the script, you will see the progress bar (if `pv` is installed correctly) and eventually, the expected output in the terminal or an output file.
