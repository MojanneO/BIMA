
# Time-Series to Image Conversion

This script processes time-series data from CSV files and generates various visual representations, including time-series plots, Gramian Angular Fields (GAF), Markov Transition Fields (MTF), Recurrence Plots (RP), and Grayscale Replication Images (GS). The generated images are saved in specified directories.

## Features

- **Time-Series Plot**: Generates a line plot of the time-series data.
- **Gramian Angular Field (GAF)**: Converts time-series data into both GADF and GASF images using summation and difference methods.
- **Markov Transition Field (MTF)**: Represents the transition matrix of binned time-series data as an image.
- **Recurrence Plot (RP)**: Visualizes the recurrence of states within a time-series.
- **Grayscale Image (GS)**: Converts normalized data into a grayscale image by replicating data points.

For sparse sensors, only GS and time-series line plots are generated. For sensors showing variations, MTF, RP, GASF, GADF, and time-series line plots are generated.

## Prerequisites

Ensure you have Python installed and the following Python packages:

- `numpy`
- `pandas`
- `matplotlib`
- `Pillow`
- `pyts`

You can install the required packages using pip:

\`\`\`bash
pip install numpy pandas matplotlib Pillow pyts
\`\`\`

## Usage

### Command Line Execution

You can run the code by running the jupyter cell dedicated to the csv to image conversion procedure; you need to provide 2 paths which are describe below:

- base_dir : The directory where the generated images will be saved.
- csv_base_dir: The directory containing the CSV files to be processed.

Before doing so, you can run the first cell to modify the POINT\_MESS function according to our need


### CSV File Format

The script processes CSV files where the time-series value is stored in the second column of each CSV file (the first column is reserved for `TIMESTAMP`). The script assumes the CSV files are named in a specific manner corresponding to certain parameters defined in the script.

## Script Overview

- **save_time_series_plot**: Generates and saves a time-series plot.
- **save_image**: Saves various types of generated images based on the directory specified.
- **split_with_overlap**: Splits the time-series data into overlapping segments.
- **read_csv_and_process**: Main function for reading the CSV, processing the data, and generating images.
- **gaf_norm, rp_mtf_norm, gs_norm**: Functions for normalizing data before image generation.
- **process_and_save_images**: Orchestrates the generation and saving of all image types.
- **find_csv_files**: Searches for the specified CSV files within the provided directory.

## Customization

### Segmentation and Normalization

You can customize the segmentation size, overlap, and normalization bounds by modifying the script where parameters are defined:

- **Segmentation Size**: Controls the size of the time-series chunks processed at a time.
- **Overlap**: Defines the amount of overlap between segments.
- **Normalization Bounds**: Adjust the lower and upper bounds for normalizing data, which is critical for accurate image generation.

### Adding or Removing CSV Files

You can add or remove CSV files to process by editing the `csv_filenames` list in the main function.

### Fine-Tuning for Sensors

The script supports fine-tuning of processing parameters for each sensor, including:

- **Normalization Bounds**: Adjust the bounds for each sensor to ensure accurate image generation.
- **Number of Bins (`n_bins`)**: Define the number of bins used in Markov Transition Fields, which controls the resolution of the MTF images.
- **Threshold Values (`threshold`)**: Set threshold values for Recurrence Plots to control the sensitivity of state recurrences.

## Error Handling

The script will raise a `FileNotFoundError` if any of the specified CSV files are not found in the provided directory.

## Memory Management

The script uses explicit memory management practices to ensure that large datasets are handled efficiently. The garbage collector is manually invoked to free up memory during processing.

## Expected Output

After running the script, you should see a set of directories for each sensors within your specified output directory, and each directory should have the following subdirectories:

- **gs/**: Contains grayscale replication images.
- **ts/**: Contains time-series line plots.
- **gasf/**: Contains Gramian Angular Summation Field images.
- **gadf/**: Contains Gramian Angular Difference Field images.
- **rp/**: Contains Recurrence Plot images.
- **mtf/**: Contains Markov Transition Field images.

Each directory will contain images corresponding to the processed chunks of your time-series data.

## Example Parameters

Here’s a table summarizing the impact of different parameters you might adjust:

| Parameter       | Description                                                             | Impact                                   |
|-----------------|-------------------------------------------------------------------------|------------------------------------------|
| `chunk_size`    | Size of the time-series chunks                                          | Larger chunks capture more data per image|
| `overlap`       | Amount of overlap between consecutive chunks                            | Higher overlap can capture more continuity between segments|
| `n_bins`        | Number of bins for MTF                                                  | Higher bins result in higher resolution images|
| `threshold`     | Sensitivity threshold for RP                                            | Lower threshold captures finer recurrences|

## Links and References

- Learn more about [Gramian Angular Fields (GAF)](https://pyts.readthedocs.io/en/stable/generated/pyts.image.GramianAngularField.html).
- Learn more about [Markov Transition Fields (MTF)](https://pyts.readthedocs.io/en/stable/generated/pyts.image.MarkovTransitionField.html).
- Learn more about [Recurrence Plots (RP)](https://pyts.readthedocs.io/en/stable/generated/pyts.image.RecurrencePlot.html).


