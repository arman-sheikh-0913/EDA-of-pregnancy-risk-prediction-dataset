# Pregnancy Risk Prediction Dataset from West Lombok, Indonesia

## Overview

This dataset contains clinical data from 5,313 pregnant women collected from public health centers in West Lombok Regency, Indonesia, designed to support research in automated pregnancy risk prediction and maternal health monitoring systems.

## Dataset Statistics

- **Total Records**: 5,313 (cleaned dataset) / 5,324 (original raw dataset)
- **Collection Period**: February 2020 - February 2021
- **Study Type**: Prospective cohort study
- **Geographic Coverage**: West Lombok Regency, Indonesia
- **Population**: Pregnant women aged 18-45 years accessing public healthcare
- **File Format**: CSV with header row

## Class Distribution

| Risk Level | Count | Percentage | Clinical Description |
|------------|-------|------------|---------------------|
| Normal (0) | 3,491 | 65.7% | No identified risk factors |
| Low Risk (1) | 1,464 | 27.6% | Minor risk factors present |
| Moderate Risk (2) | 299 | 5.6% | Multiple or moderate risk factors |
| High Risk (3) | 59 | 1.1% | Severe risk factors requiring specialized care |

**Imbalance Ratios**: 
- Moderate Risk: 0.060 (1:17 ratio vs normal)
- High Risk: 0.011 (1:59 ratio vs normal)

## Feature Description

| Variable | Indonesian Term | Data Type | Range/Values | Clinical Significance |
|----------|----------------|-----------|--------------|----------------------|
| `umur` | Umur | Integer | 18-45 | Maternal age (years) |
| `paritas` | Paritas | Integer | 0-10+ | Number of previous births |
| `jarak_anak` | Jarak Anak | Float | 0-999 | Birth spacing in months (999 = nulliparous) |
| `jarak_anak_cat` | - | Integer | 0-2 | Categorized birth spacing |
| `tb` | Tinggi Badan | Float | 135-180 | Height in centimeters |
| `hb` | Hemoglobin | Float | 7-18 | Hemoglobin level (g/dL) |
| `lila` | LILA | Float | 15-35 | Mid-upper arm circumference (cm) |
| `hbsag` | HBsAg | Integer | 1,2 | Hepatitis B surface antigen (1=positive, 2=negative) |
| `hiv` | HIV | Integer | 1,2 | HIV status (1=positive, 2=negative) |
| `dm` | Diabetes Mellitus | Integer | 1,2 | Diabetes history (1=yes, 2=no) |
| `ht` | Hipertensi | Integer | 1,2 | Hypertension history (1=yes, 2=no) |
| `protein` | Protein Urine | Integer | 1,2 | Proteinuria (1=positive, 2=negative) |
| `diastole` | Diastolik | Integer | 60-120 | Diastolic blood pressure (mmHg) |
| `sistole` | Sistolik | Integer | 90-180 | Systolic blood pressure (mmHg) |
| `perdarahan` | Perdarahan | Integer | 1,2 | Bleeding history (1=yes, 2=no) |
| `penyakit_lain_cat` | Penyakit Lain | Integer | 0-1 | Other diseases (0=none, 1=present) |
| `risiko_cat` | Kategori Risiko | Integer | 0-3 | **Target variable**: Risk category |

## Data Collection

### Clinical Sites
- **Primary Site**: Public Health Centers in West Lombok Regency
- **Healthcare Level**: Primary care facilities serving rural and semi-urban populations
- **Population Demographics**: Predominantly Sasak ethnicity, middle to low-income households
- **Healthcare Context**: Indonesian public healthcare system

### Clinical Assessment Protocol
- Risk categories determined following standardized clinical protocols
- Classifications based on American Academy of Pediatrics (AAP) and American College of Obstetrics and Gynecology (ACOG) guidelines
- Independent evaluation by two experienced neonatologists
- Consensus resolution for any classification discrepancies

### Data Quality Measures
- **Missing value rate**: < 0.1% after preprocessing
- **Outlier handling**: Physiologically implausible values removed
- **Validation**: Clinical review of all high-risk classifications
- **Consistency checks**: Cross-validation of related clinical parameters

## Ethical Approvals

Comprehensive ethical clearances obtained from:
- **Poltekkes Kemenkes Semarang Health Research Ethics Committee**
  - Approval No: 0294/EA/KEPK/2020
  - Date: Ethics clearance obtained prior to data collection
- **Institutional Review**: Conducted in compliance with Indonesian health research guidelines
- **Informed Consent**: Written consent obtained from all participants
- **Privacy Protection**: All personal identifiers removed from dataset

## Data Preprocessing

### Original to Cleaned Dataset Changes
- **Records removed**: 11 (0.2% of original dataset)
- **Exclusion criteria**:
  1. Missing pregnancy risk classifications (n=1)
  2. Missing critical clinical parameters (n=1)
  3. Physiologically implausible values (n≈9)
     - Heights < 135 cm or > 180 cm
     - Hemoglobin > 18 g/dL or < 7 g/dL
     - Ages outside reproductive ranges

### Quality Assurance
- **Clinical validity**: All values within physiologically possible ranges
- **Completeness**: No missing values in critical variables
- **Consistency**: Related clinical parameters cross-validated
- **Standardization**: Categorical variables consistently encoded

## Usage Guidelines

### Machine Learning Applications
- **Primary Use**: Multi-class classification with severe imbalance
- **Recommended Techniques**:
  - Ensemble methods (XGBoost, Random Forest)
  - Cost-sensitive learning approaches
  - SMOTE and other resampling techniques
  - Deep reinforcement learning for minority classes
  
### Evaluation Protocols
- **Cross-validation**: Use stratified k-fold to maintain class distribution
- **Patient-level separation**: Ensure no patient appears in both train/test sets
- **Metrics**: Focus on precision, recall, and F1-score for minority classes
- **Clinical relevance**: Prioritize high recall for high-risk cases

### Benchmark Performance
Published results using this dataset:
- **Ensemble XGBoost-DQN**: 98.19% accuracy, 98.19% F1-score
- **Individual XGBoost**: 91% accuracy
- **Individual DQN**: 93% accuracy
- **Baseline methods**: 80-92% accuracy range

## Files Included

1. **`pregnancy_risk_prediction_cleaned.csv`** - Main cleaned dataset (5,313 records)
2. **`pregnancydatasetbanyumulek.xlsx`** - Original raw dataset (5,324 records)
3. **`pregnancy_readme.md`** - This documentation file
4. **`pregnancy_data_dictionary.md`** - Detailed variable descriptions

## Limitations and Considerations

### Geographic and Demographic Scope
- **Single region**: West Lombok, Indonesia
- **Population specificity**: Sasak ethnicity, rural/semi-urban
- **Healthcare context**: Indonesian public health system
- **Generalizability**: May require validation in other populations

### Clinical Limitations
- **Single time-point**: Cross-sectional risk assessment
- **Missing variables**: Some clinical parameters not available
- **Subjective elements**: Some risk factors based on clinical judgment
- **Follow-up data**: Pregnancy outcomes not included

### Technical Considerations
- **Severe imbalance**: High-risk cases represent only 1.1% of dataset
- **Small minority classes**: Limited examples for rare complications
- **Feature engineering**: May benefit from additional derived variables
- **Temporal aspects**: No longitudinal tracking of risk progression

## Research Applications

### Demonstrated Use Cases
1. **Multi-class imbalanced learning**: Testing ensemble approaches
2. **Medical AI development**: Pregnancy risk stratification systems
3. **Healthcare informatics**: Automated screening tools
4. **Public health research**: Population-level risk assessment

### Future Research Directions
1. **Longitudinal studies**: Tracking risk evolution during pregnancy
2. **Multi-site validation**: Generalizability across different populations
3. **Outcome prediction**: Linking risk categories to actual complications
4. **Real-time systems**: Integration with electronic health records

## Citation

When using this dataset, please cite the associated research:

```bibtex
@article{kurnianingsih2025ensemble,
  title={A novel ensemble XGBoost and deep Q-network for pregnancy risk prediction on multi-class imbalanced datasets},
  author={Kurnianingsih and Nobukawa, Sou and Widyawati, Melyana Nurul and others},
  journal={ICT Express},
  volume={11},
  pages={648--656},
  year={2025},
  publisher={Elsevier}
}
```

## Contact Information

For questions about this dataset or research collaboration:
- **Lead Researcher**: Kurnianingsih (kurnianingsih@polines.ac.id)
- **Institution**: Department of Electrical Engineering, Politeknik Negeri Semarang
- **Address**: H. Soedarto Tembalang, Semarang 50275, Central Java, Indonesia

## License and Usage Terms

This dataset is provided for research purposes under the following terms:
- **Academic use**: Freely available for research and educational purposes
- **Commercial use**: Requires explicit permission from authors
- **Data sharing**: Must include proper attribution and citation
- **Ethical compliance**: Users must adhere to medical data research ethics
- **Privacy protection**: No attempts to re-identify participants permitted

## Version History

- **Version 1.0** (2025): Initial release with cleaned dataset
- **Data collection period**: February 2020 - February 2021
- **Processing date**: 2024
- **Publication date**: 2025

## Acknowledgments

This research was supported by:
- Ministry of Education, Culture, Research and Technology of Indonesia
- Poltekkes Kemenkes Semarang
- Public Health Centers in West Lombok Regency
- Clinical staff and participants who contributed to data collection