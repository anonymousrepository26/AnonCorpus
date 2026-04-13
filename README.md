# AnonCorpus
🔗 Dataset Access

The dataset is publicly available at the following link:

[Access the dataset](https://drive.google.com/drive/folders/1XGMxvmwUh7ekDiUIbVFMO4ZPv-9gPvXi?usp=sharing)

## 📌 Introduction
This version of the [anonymised corpus name] builds on the original release by addressing its main limitations and adding key enhancements to improve usability and research value.
The dataset now includes:
* Annotations from both English and French-speaking raters, offering perspectives across languages and cultures.
* A standardized experimental protocol to support reproducible results.
* A consistent labeling strategy: final labels are derived via median-based rules to create a balanced and standardized ground truth, addressing the inconsistency of ad-hoc labeling in prior work.
* Continuous-scale scores (0-100), enabling both classification and regression, while also preserving the original discrete annotations.
* Organized and cleaned data structure for easier access and analysis.
* Automatic transcriptions of all speech clips using Google ASR.
* Language and paralanguage features extracted using modern tools (e.g., Word2Vec, BERT, eGeMAPS, Wav2Vec2.0, Whisper).
* The full experimental pipeline, including configuration files, data splits, and environment details, is provided to support easy replication and extension.

These refinements aim to enable more consistent and flexible investigations into personality perception from speech.

## 📁 Folder Structure Overview
### 1. Dataset
Contains the core data used across all experiments.
#### a. Audio_clips/: 640 audio clips (10 seconds each, 16-bit, 8 kHz) in WAV format.
#### b.  Experimental_Protocol/: Contains key documentation related to the experimental design and label processing.
* Folds.txt: Describes the 5-fold user-independent split applied across all experiments, ensuring no speaker appears in more than one fold.
* Binarization_Method.txt: Explains how binary labels were derived from rater scores using median thresholding, including both the main (all raters) and experimental (filtered raters) approaches.
#### c. Feature_Extraction/:
* Paralanguage/: eGeMAPSv02 (LLDs and Functionals), Wav2vec2 (Encoder and Transformer outputs), Whisper (Encoder output).
* Language/: Word2Vec and BERT embeddings.
#### d. Transcription_Extraction/: Automatically generated French transcriptions using Google ASR, along with the corresponding scripts and source files.
#### e. Metadata/: Speaker-level information (Speaker ID, Gender, Status), a mapping between the original and new human-readable Clip IDs, and a script for metadata analysis and visualization.
#### f. Environment_Information/: Hardware and software setup to ensure full reproducibility (Python version, libraries, etc.).

### 2. Multilingual_Annotation
Contains all experiments based on the new continuous annotations (0-100 scale) provided by English and French raters.
#### a. Data_Management/:
* Tools and resources for annotation processing and statistical analysis.
  * Data_Annotation/: Contains raw rater scores for each personality trait. The directory includes:
    * English/ and French/: Each folder contains CSV files, where each file corresponds to a specific clip set (64 clips) rated by 10 different raters.
    * participants_and_sets.csv: A CSV file mapping each rater (participant ID) to their assigned set.
  * Label_Extraction/: Labels computed by averaging rater scores per clip, then applying a dataset-level median threshold to generate binary classes.
    * All_Raters_Based/: Labels generated from all raters
    * Filtered_Raters_Based/: Labels generated after filtering the raters based on reliability metrics, as part of an effort to improve consistency and inter-rater agreement.
  * Statistical_Analysis/
    * Data_Distribution/: Trait distributions.
    * Inter_Rater_Reliability/: Rater consistency analysis per set using Pearson and Spearman-Brown correlations.
    * Performance_Comparison/: Model performance comparison using error bars and baseline reference.
    * Performance_Summary/: Aggregated metrics (mean ± std) computed from results across all Experiment_Results directories.
    * Traits_Correlation/: Inter-trait prediction analysis by estimating each personality trait from the remaining four. 
#### b. Cross-Validation/:
* Hyperparameter tuning and final evaluation using a nested 5-fold setup with strict user independence (i.e., no speaker appears in more than one fold).
* Folder structure includes both Classification/ and Regression/ tasks.
#### c. Unimodal/:
* Experiments stored in either the Language/ or Paralanguage/ directories, where each folder contains features from a single modality. Each directory is organized into the following subfolders:
  * Classification/ Predicts trait labels binary.
  * Regression/ Predicts continuous trait scores.
  * Data_Preprocessing/ Prepares and cleans raw inputs into a model-ready format.
#### d. Multimodal/:
* Fusion experiments that combine both Language and Paralanguage modalities. The directory contains two subfolders:
  * Classification/ Predicts binary trait labels using multimodal inputs.
  * Regression/ Predicts continuous trait scores using multimodal inputs.
* Fusion is implemented using mid-level and late-level strategies depending on the setup.

### 3. Original_Annotation
Contains experiments using the original discrete BFI-10 annotations, following the same updated experimental protocol applied in the Multilingual_annotation setup.
* Mirrors the structure of the Multilingual_Annotation setup: Unimodal/, Multimodal/, Cross-Validation/, and Data_Management/, However, there are a few key differences:  
  * No distinction is made between annotation type (i.e., annotations are not split by English or French raters) or label source (i.e., labels are based only on raw scores without rater filtering).
  * Only classification tasks are included; regression is not applicable.
  * The Data_Annotation directory contains two sub folders: 
    * BFI_Item_Answers: 11 file csv format, each showing the answers of one rater to the 640 BFI-10 questionnaires corresponding to the audio clips
    * Personality_Scores: 11 CSV files, each containing final trait scores on a 1-5 Likert scale. Each score represents the computed value of a trait based on two BFI-10 questionnaire items per clip.

### 4. README (This file)
A text file providing all the necessary information to understand and use the benchmarking framework.

## 🔁 Reproducibility Notes
* Audio clips were resampled to 16kHz only for Wav2Vec2 and Whisper extraction, ensuring compatibility with these deep learning models.
* Feature extraction was performed using the following tools and sources:
  * Paralanguage:
    * eGeMAPSv02: Used with the openSMILE toolkit. Extracted two types of acoustic features - LLDs (25-dimensional per frame) and Functionals (88-dimensional per clip), using 25 ms windows and 10 ms overlap.
    * Wav2Vec2.0: Used via HuggingFace Transformers. Provided two representations - Encoder output (512-dimensional per frame) and Transformer output from Layer 24 (1024-dimensional per frame).
    * Whisper: Used with the SpeechBrain implementation. Extracted encoder-only outputs (384-dimensional per frame), excluding the decoder to avoid language bias.
  * Language:
    * Word2Vec: Used via HuggingFace to obtain static word-level embeddings (200-dimensional per token) from a pre-trained French Word2Vec model.
    * BERT: Used via HuggingFace to generate contextual embeddings (300-dimensional per token) based on the BERT base model.
* Environment information is available in the Environment_Information/ folder.
* Config files include the predefined fold assignments and selected hyperparameters for each experiment, ensuring consistent and repeatable evaluation.

## 📞 Contact
For more details, contact
...
____________________________________________________________________________________________________________________________________________________________

## 📜 License
This dataset is released for research purposes only
...

## 📖 Citation
If you use this dataset, please cite:
...
