
# Time-Series to Image Conversion

This script processes time-series data from CSV files and generates various visual representations, including time-series plots, Gramian Angular Fields (GAF), Markov Transition Fields (MTF), Recurrence Plots (RP) and Grayscale Replication Image(gs). The generated images are saved in specified directories.

## Features

- **Time-Series Plot**: Generates a line plot of the time-series data.
- **Gramian Angular Field (GAF)**: Converts time-series data into both GADF and GASF images using summation and difference methods.
- **Markov Transition Field (MTF)**: Represents the transition matrix of binned time-series data as an image.
- **Recurrence Plot (RP)**: Visualizes the recurrence of states within a time-series.
- **Gray Scale Image (GS)**: Converts normalized data into a grayscale image by replicating datapoints.

For sparse sensors, only gs and time series line plots are generated, for sensors showing variations MTF, RP, GASF, GADF and time-series line plots are generated.

## Prerequisites

Ensure you have the following Python packages installed:

- `numpy`
- `pandas`
- `matplotlib`
- `Pillow`
- `pyts`

You can install the required packages using `pip`:

\`\`\`bash
pip install numpy pandas matplotlib Pillow pyts
\`\`\`

## Usage

### Command Line Execution

You can run the script from the command line by providing two directory paths as arguments: one for saving the output images and another for locating the input CSV files. The csv directory should contain the preprocessed and synchronized csv files of all sensors.

\`\`\`bash
python process_time_series.py /path/to/output/directory /path/to/csv/directory
\`\`\`

- \`/path/to/output/directory\`: The directory where the generated images will be saved.
- \`/path/to/csv/directory\`: The directory containing the CSV files to be processed.

### Example

\`\`\`bash
python process_time_series.py ./output ./data
\`\`\`

In this example:
- \`./output\` is the directory where the processed images will be saved.
- \`./data\` is the directory containing the CSV files.

## CSV File Format

- The script processes CSV files where the time-series value is stored in the second column of each CSV file(first column reserved for TIMESTAMP).
- The script assumes the CSV files are named in a specific manner corresponding to certain parameters defined in the script.

## Script Overview

- **save_time_series_plot**: Generates and saves a time-series plot.
- **save_image**: Saves various types of generated images based on the directory specified.
- **split_with_overlap**: Splits the time-series data into overlapping segments.
- **read_csv_and_process**: Main function for reading the CSV, processing the data, and generating images.
- **gaf_norm, rp_mtf_norm, gs_norm**: Functions for normalizing data before image generation.
- **process_and_save_images**: Orchestrates the generation and saving of all image types.
- **find_csv_files**: Searches for the specified CSV files within the provided directory.

## Customization

- You can customize the segmentation size, overlap, and normalization bounds by modifying the script where parameters are defined.
- You can also add or remove CSV files to process by editing the \`csv_filenames\` list in the \`main\` function.
- Fine-Tuning for Sensors

The script supports fine-tuning of processing parameters for each sensor. This includes:

- Normalization Bounds: Adjust the lower and upper bounds for normalizing data, which is critical for accurate image generation.
- Number of Bins (n_bins): Define the number of bins used in Markov Transition Fields, which controls the resolution of the MTF images.
- Threshold Values (threshold): Set threshold values for Recurrence Plots to control the sensitivity of state recurrences.

## Error Handling

The script will raise a \`FileNotFoundError\` if any of the specified CSV files are not found in the provided directory.

## Memory Management

The script uses explicit memory management practices to ensure that large datasets are handled efficiently.
