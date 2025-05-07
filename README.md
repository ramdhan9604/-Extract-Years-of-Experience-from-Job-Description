
# Experience Extractor for Job Descriptions

This project extracts the total years of experience required from job descriptions using multiple models and techniques. It compares the results from each model and provides recommendations on the most effective approach.



## Features

- Extracts total experience requirements from job descriptions using 6 different models
- Processes Excel files containing job descriptions
- Uses parallel processing for efficient handling of large datasets
- Compares results from all models and provides a recommended value
- Exports results to Excel with detailed analysis

## Requirements

- Python 3.8 or higher
- Required libraries:
  - pandas
  - numpy
  - torch
  - transformers
  - spacy
  - tqdm
  - openpyxl

## Installation

1. Clone this repository or download the code:
```bash
git clone https://github.com/ramdhan9604/-Extract-Years-of-Experience-from-Job-Description.git
```

2. Create and activate a virtual environment (optional but recommended):
```bash
python -m venv venv
# On Windows
venv\Scripts\activate
# On macOS/Linux
source venv/bin/activate
```

3. Install the required libraries:
```bash
pip install pandas numpy torch transformers spacy tqdm openpyxl
```

4. Download the SpaCy English language model:
```bash
python -m spacy download en_core_web_sm
```

## Usage

1. Prepare your input Excel file with job descriptions. The file should contain at least one column with job description text.

2. Run the script:
```bash
python experience_extractor.py
```

3. Follow the prompts:
   - Enter the path to your Excel file containing job descriptions
   - Confirm or change the column name containing job descriptions (default: `JD_Text`)
   - Specify the output file path for results

Example:
```
$ python experience_extractor.py
Experience Extractor for Job Descriptions
=======================================
Enter the path to the Excel file containing job descriptions: job_descriptions.xlsx

Available columns:
- ID
- JD_Text
- Company
- Position

Enter the name of the column containing job descriptions [default: JD_Text]: 

Processing job descriptions...
[Progress bar...]

Processing completed in 45.32 seconds

Enter the path to save the results Excel file [default: experience_extraction_results.xlsx]: 
Results saved to experience_extraction_results.xlsx
```

## Models Overview

The project implements six different approaches to extract experience requirements:

1. **Rule-based Regex Pattern Matching**: Uses regular expressions to find explicit mentions of experience requirements (e.g., "5+ years", "3-5 years").

2. **SpaCy NER with Custom Rules**: Identifies sentences containing experience-related terms using SpaCy NLP and applies pattern matching to those sentences.

3. **Zero-shot Classification**: Uses pre-trained transformer models to classify job descriptions into predefined experience categories without specific training.

4. **Transformer-based Sequence Classification**: Simulates a fine-tuned model approach by identifying relevant experience sentences.

5. **Named Entity Recognition with Custom Rules**: Focuses on job titles and seniority levels to estimate required experience.

6. **Hybrid Text Classification**: Combines multiple strategies including regex, NER, education requirements, and skill proficiency as proxies for experience levels.

## Output Format

The tool produces an Excel file with the following additional columns:

- **Regex**: Experience extracted using regex patterns
- **SpaCy**: Experience extracted using SpaCy NER
- **Zero-Shot**: Experience extracted using zero-shot classification
- **Transformer**: Experience extracted using transformer-based classification
- **Custom NER**: Experience extracted using custom NER rules
- **Hybrid**: Experience extracted using hybrid text classification
- **Model_Agreement**: Standard deviation between model results (lower means higher agreement)
- **Recommended_Value**: The final recommended experience value

## Performance Analysis

The script includes a built-in analysis of model performance:

- **Success Rate**: Percentage of job descriptions where each model successfully extracted a value
- **Model Agreement**: How closely different models agree on the extracted values
- **Recommended Model**: Based on performance metrics

Performance metrics are printed at the end of processing and are also included in the output Excel file.

## Troubleshooting

Common issues and solutions:

1. **Missing dependencies**:
   - Ensure all required libraries are installed with the correct versions
   - For GPU support, make sure your CUDA version is compatible with PyTorch

2. **Memory errors**:
   - For large files, try increasing system memory or processing in batches
   - Reduce the number of workers in the ThreadPoolExecutor

3. **Slow processing**:
   - Try enabling GPU acceleration if available
   - Disable heavier models like Zero-Shot classification for faster processing

4. **Model-specific issues**:
   - If a particular model is performing poorly, check its specific parameters and thresholds
   - For transformer models, ensure you have internet connectivity for downloading pre-trained models

## Customization

You can customize the tool for your specific needs:

1. **Adding domain-specific patterns**:
   - Modify the regex patterns in `extract_experience_regex()` function
   - Add industry-specific job titles and their experience mappings

2. **Adjusting seniority mappings**:
   - Update the `seniority_mapping` dictionary in the code
   - Customize the years associated with different levels based on your industry

3. **Modifying the processing pipeline**:
   - Change the `process_all_jds()` function to include or exclude specific models
   - Adjust the weighting in the `get_recommended_value()` function

4. **Fine-tuning the models**:
   - For best results, consider fine-tuning the transformer model with labeled data specific to your domain
   - Adjust thresholds and confidence scores based on your dataset characteristics

