Chart-to-Table with Weak Supervision

An IE643 course project exploring how to automatically extract structured tables from visual charts using deep learning and weak supervision.

Overview

Charts contain valuable numerical information, but extracting that information into structured tables is challenging.

This project investigates a Chart-to-Table approach that converts chart images into structured numerical tables using a pretrained visual encoder and a table decoder.

The main objective is to train a model using question-answer (QA) supervision without requiring gold tables during training.

The project also compares this weakly supervised approach against a fully supervised baseline.

Key Features

- Automatic extraction of structured tables from chart images.
- Weakly supervised learning using question-answer pairs.
- Pretrained visual encoders for chart understanding.
- Transformer-based table decoder.
- Comparison between weakly supervised and fully supervised approaches.
- Evaluation of cell existence and numerical value predictions.
- Interactive chart question-answering interface using Gradio.
- OCR-based extraction of chart labels using Tesseract.

Methodology

The project investigates two training approaches:

1. Weakly Supervised Model (Proposed)

The proposed model learns to reconstruct tables without accessing gold tables during training.

It uses:

- Chart images.
- Question-answer pairs.
- Question operation programs.
- Row-count information derived from sum and mean answer pairs.

The model is selected using validation QA accuracy.

2. Fully Supervised Model (Baseline)

The baseline model uses gold tables during training.

It learns through:

- Cell value prediction loss.
- Cell existence prediction loss.

The model is selected using validation extraction F1.

Important: The fully supervised model acts as an upper-bound baseline because it receives additional gold-table supervision. Gold tables from the test split are used only for evaluation.

Model Architecture

The system consists of two major components:

1. Visual Encoder: Extracts visual representations from chart images.
2. Table Decoder: Predicts structured table values and cell existence.

The project explores the following encoders:

Encoder| Description
Pix2Struct Base| Document-pretrained visual encoder
SigLIP Base| Generic image-text pretrained encoder
Debug Patch| Raw pixel patch encoder without pretraining

The decoder uses a Transformer architecture.

Dataset

The project generates synthetic bar and line charts along with corresponding question-answer pairs.

Split| Number of charts
Training| 2,400
Validation| 300
Testing| 300
Total| 3,000

Each chart has approximately 10 QA pairs.

The generated tables contain:

- Up to 6 rows (categories).
- Up to 3 columns (series).

Gold tables are retained for evaluation.

Evaluation Metrics

The models are evaluated using three primary metrics:

- Entry Existence: Whether a predicted table cell exists.
- Value Prediction: Whether the predicted numerical value is correct within a 5% tolerance.
- Overall Extraction: Whether both the cell existence and its value are correct.

The project also examines different error types:

- Incorrect values.
- Missing entries.
- Spurious entries.

The weak and fully supervised models are evaluated separately to understand the effect of different supervision strategies.

Technology Stack

- Python
- PyTorch
- Hugging Face Transformers
- NumPy
- Pandas
- Matplotlib
- Pillow (PIL)
- Gradio
- Tesseract OCR
- Google Colab

Installation

The notebook installs its dependencies automatically.

For a local environment:

pip install -U transformers accelerate sentencepiece gradio pytesseract
pip install numpy pandas torch matplotlib pillow

Tesseract OCR is optional and used for extracting chart labels.

On Ubuntu or Debian:

sudo apt-get install tesseract-ocr

Running the Project

The project is provided as a Jupyter Notebook.

1. Clone the repository:

git clone https://github.com/Priyanshu-511/chart-2-table-IE-643.git

2. Navigate to the project directory:

cd chart-2-table-IE-643

3. Open the notebook:

jupyter notebook IE643_chart2table_Project.ipynb

Alternatively, open the notebook directly in Google Colab:

"Open in Google Colab" (https://colab.research.google.com/github/Priyanshu-511/chart-2-table-IE-643/blob/main/IE643_chart2table_Project.ipynb)

4. Run the notebook cells sequentially to install dependencies, generate data, train models, evaluate results, and explore the interactive interface.

Configuration

The notebook provides a configurable "Config" dataclass.

Some important parameters include:

Parameter| Default
Training charts| 2,400
Validation charts| 300
Testing charts| 300
Epochs| 40
Batch size| 32
Learning rate| 0.0003
Decoder dimension| 256
Transformer layers| 3
Attention heads| 8
Dropout| 0.1
Value tolerance| 5%

A "QUICK_TEST" option is also available for a smaller CPU smoke test.

Project Structure

chart-2-table-IE-643/
│
├── IE643_chart2table_Project.ipynb
└── README.md

The notebook contains the complete implementation, including data generation, model architecture, training, evaluation, and interactive inference.

Future Improvements

Potential directions for further development:

- Extend support to more chart types.
- Evaluate on real-world chart datasets.
- Improve numerical value extraction.
- Support more complex chart layouts.
- Improve OCR and legend detection.
- Explore stronger visual encoders and decoder architectures.
- Improve generalization to unseen chart styles.

Course Project

Course: IE643
Project: Chart-to-Table with Weak Supervision

Repository: "chart-2-table-IE-643" (https://github.com/Priyanshu-511/chart-2-table-IE-643)

---

This project explores the use of weak supervision to reduce dependence on manually annotated structured tables for chart understanding and information extraction.
