# Qwen2 VL Data Processing Pipeline

Welcome to the **Qwen2 VL Data Processing Pipeline** repository. This pipeline is designed to prepare raw labeled data for training the Qwen2 VL model. It organizes raw PDFs, processes them into normalized images and labels, and prepares inputs and expected outputs for the QWen2-VL.

## Table of Contents

- [Project Structure](#project-structure)
- [Directory Hierarchy](#directory-hierarchy)
- [Directory and Pipeline Explanation](#directory-and-pipeline-explanation)
  - [1. Root Directory (`root/`)](#1-root-directory-root)
  - [2. `qwen2vl/`](#2-qwen2vl)
    - [`10Trail_Revised/`](#10trail_revised)
    - [`normalized_data/`](#normalized_data)
    - [`processed_json_user/`](#processed_json_user)
    - [`processed_json_assistant/`](#processed_json_assistant)
    - [`all_transformed/`](#all_transformed)
    - [`user_instruction.txt`](#user_instructiontxt)
    - [`system_instruction.txt`](#system_instructiontxt)
  - [3. `papers/`](#3-papers)

---

## Project Structure

```plaintext
root/
├── qwen2vl/
│   ├── 10Trail_Revised/
│   │   ├── adfm.201604509/
│   │   │   ├── adfm.2016045090010.jpg
│   │   │   ├── adfm.2016045090010.json
│   │   │   ├── adfm.2016045090011.jpg
│   │   │   ├── adfm.2016045090011.json
│   │   │   └── ... (additional pages)
│   │   ├── adfm.201604510/
│   │   │   ├── adfm.2016045100010.jpg
│   │   │   ├── adfm.2016045100010.json
│   │   │   └── ... (additional pages)
│   │   └── ... (additional PDF folders)
│   ├── normalized_data/
│   │   ├── adfm.201604509/
│   │   │   ├── adfm.2016045090010.jpg
│   │   │   ├── adfm.2016045090010.json
│   │   │   ├── adfm.2016045090011.jpg
│   │   │   ├── adfm.2016045090011.json
│   │   │   └── ... (additional pages with normalized dimensions)
│   │   └── ... (additional PDF folders)
│   ├── processed_json_user/
│   │   ├── adfm.201604509/
│   │   │   ├── adfm.2018077880010_transformed.txt
│   │   │   ├── adfm.2018077880011_transformed.txt
│   │   │   └── ... (additional transformed user inputs)
│   │   └── ... (additional PDF folders)
│   ├── processed_json_assistant/
│   │   ├── adfm.201604509/
│   │   │   ├── adfm.20180522000010_transformed.json
│   │   │   ├── adfm.20180522000011_transformed.json
│   │   │   └── ... (additional transformed assistant outputs)
│   │   └── ... (additional PDF folders)
│   ├── all_transformed/
│   │   ├── adfm.201604509/
│   │   │   ├── adfm.2016045090010.jpg
│   │   │   ├── adfm.2016045090011.jpg
│   │   │   └── ... (all normalized image files)
│   │   ├── adfm.201604510/
│   │   │   ├── adfm.2016045100010.jpg
│   │   │   └── ... (additional normalized image files)
│   │   └── ... (additional PDF folders)
│   ├── user_instruction.txt
│   └── system_instruction.txt
├── papers/
│   ├── adma.202005946.pdf
│   ├── adma.202005947.pdf
│   └── ... (additional raw PDF papers)
└── README.md

```


---

## Directory Hierarchy

### 1. Root Directory (`root/`)
The main directory containing all subdirectories and files related to the data processing pipeline.

### 2. `qwen2vl/`
Primary workspace for preparing and processing data for the Qwen2 VL training pipeline.

#### `10Trail_Revised/`
- **Purpose:** Contains the initial processed data extracted from raw PDF papers.
- **Structure:** Each subfolder (e.g., `adfm.201604509/`) represents a single PDF paper.
  - **JPEG Files (`.jpg`):** Image representations of each page (e.g., `adfm.2016045090010.jpg` for page 10).
  - **JSON Files (`.json`):** Ground truth labels corresponding to each image (e.g., `adfm.2016045090010.json`).

#### `normalized_data/`
- **Purpose:** Stores the normalized versions of images and JSON labels from `10Trail_Revised/`.
- **Normalization Details:** Images have standardized height and width to ensure consistency across the dataset, which is crucial for model training.
- **Structure:** Mirrors the `10Trail_Revised/` folder structure with normalized `.jpg` and `.json` files.

#### `processed_json_user/`
- **Purpose:** Contains transformed user input files for the LLM (Large Language Model).
- **Structure:** Each PDF paper folder contains `.txt` files (e.g., `adfm.2018077880010_transformed.txt`) representing user instructions or inputs for each page.
- **Flexibility:** While you can use a single `user_instruction.txt` for all training inputs, this structure allows for different user inputs per image if needed.

#### `processed_json_assistant/`
- **Purpose:** Holds the expected outputs from the LLM assistant.
- **Structure:** Similar to `processed_json_user/`, each paper folder contains `.json` files (e.g., `adfm.20180522000010_transformed.json`) that represent the assistant's expected responses for each page.

#### `all_transformed/`
- **Purpose:** Contains all normalized image files transformed from PDFs, facilitating easy access and aggregation during training.
- **Structure:** Mirrors the PDF structure with folders per paper and `.jpg` files for each normalized page image.
  - **Example:**
    - `adfm.201604509/`
      - `adfm.2016045090010.jpg`
      - `adfm.2016045090011.jpg`
      - `...` (additional normalized image files)
    - `adfm.201604510/`
      - `adfm.2016045100010.jpg`
      - `...` (additional normalized image files)

#### `user_instruction.txt`
- **Purpose:** A global user input file for the LLM, applicable to all training instances unless overridden by specific files in `processed_json_user/`.

#### `system_instruction.txt`
- **Purpose:** Contains system-level instructions or prompts for the LLM, consistent across all training calls.

### 3. `papers/`
- **Purpose:** Stores all raw PDF papers before any processing.
- **Structure:** Each PDF file is named uniquely (e.g., `adma.202005946.pdf`), corresponding to its processed data folders in `qwen2vl/`.


---

