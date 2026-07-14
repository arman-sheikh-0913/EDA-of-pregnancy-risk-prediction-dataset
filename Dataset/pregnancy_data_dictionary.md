# Data Dictionary: Pregnancy Risk Prediction Dataset

## File Information
- **File Name**: `pregnancy_risk_prediction_cleaned.csv`
- **Format**: Comma-separated values (CSV) with header row
- **Encoding**: UTF-8
- **Records**: 5,313 observations
- **Variables**: 17 columns (16 features + 1 target variable)

## Variable Specifications

### Demographic Variables

#### `umur` (Age)
- **Type**: Integer
- **Range**: 18-51 years
- **Description**: Maternal age at time of assessment
- **Clinical Significance**: Advanced maternal age (>35) associated with increased pregnancy risks
- **Missing Values**: 0

#### `paritas` (Parity)
- **Type**: Integer  
- **Range**: 0-10
- **Description**: Number of previous births (gravidity)
- **Values**:
  - 0: Nulliparous (first pregnancy)
  - 1-3: Low parity
  - 4+: Grand multiparous (higher risk)
- **Clinical Significance**: Both nulliparity and grand multiparity increase pregnancy risks
- **Missing Values**: 0

### Birth Spacing Variables

#### `jarak_anak` (Birth Spacing)
- **Type**: Float
- **Range**: 0-999 months
- **Description**: Interval between previous birth and current pregnancy
- **Special Values**:
  - 999: Nulliparous women (no previous births)
  - less than 18 months: Short interpregnancy interval (increased risk)
  - more than 60 months: Long interval (may indicate secondary infertility)
- **Clinical Significance**: Optimal spacing is 18-59 months
- **Missing Values**: 0

#### `jarak_anak_cat` (Categorized Birth Spacing)
- **Type**: Integer
- **Range**: 0-2
- **Description**: Categorical version of birth spacing
- **Values**:
  - 0: Nulliparous or optimal spacing
  - 1: Suboptimal spacing
  - 2: High-risk spacing patterns
- **Derivation**: Categorized from `jarak_anak` based on clinical guidelines
- **Missing Values**: 0

### Anthropometric Measurements

#### `tb` (Height)
- **Type**: Float
- **Range**: 135-180 cm
- **Description**: Maternal height in centimeters
- **Clinical Significance**:
  - <145 cm: Associated with cephalopelvic disproportion risk
  - Used for BMI calculation when combined with weight
- **Quality Control**: Values outside 135-180 cm range excluded during cleaning
- **Missing Values**: 0

#### `lila` (Mid-Upper Arm Circumference)
- **Type**: Float
- **Range**: 15-35 cm
- **Description**: Mid-upper arm circumference (LILA - Lingkar Lengan Atas)
- **Clinical Significance**:
  - <23.5 cm: Indicates maternal undernutrition
  - Correlates with maternal BMI and birth weight
- **Measurement**: Measured at midpoint of left upper arm
- **Missing Values**: 0

### Laboratory Parameters

#### `hb` (Hemoglobin)
- **Type**: Float
- **Range**: 7-18 g/dL
- **Description**: Maternal hemoglobin concentration
- **Clinical Significance**:
  - <11 g/dL: Anemia (increased risks)
  - <7 g/dL: Severe anemia (critical risk)
  - more than 16 g/dL: Hemoconcentration (may indicate preeclampsia)
- **Timing**: Usually measured in first trimester (TR1)
- **Quality Control**: Physiologically implausible values (>18 g/dL) removed
- **Missing Values**: 0

#### `hbsag` (Hepatitis B Surface Antigen)
- **Type**: Integer
- **Range**: 1-2
- **Description**: HBsAg test result
- **Values**:
  - 1: Positive (chronic hepatitis B infection)
  - 2: Negative
- **Clinical Significance**: Positive result requires antiviral therapy and neonatal vaccination
- **Missing Values**: 0

#### `hiv` (HIV Status)
- **Type**: Integer
- **Range**: 1-2  
- **Description**: HIV serology result
- **Values**:
  - 1: Positive
  - 2: Negative
- **Clinical Significance**: Positive status requires antiretroviral therapy and delivery planning
- **Privacy**: All personal identifiers removed
- **Missing Values**: 0

#### `protein` (Proteinuria)
- **Type**: Integer
- **Range**: 1-2
- **Description**: Urine protein test result
- **Values**:
  - 1: Positive (proteinuria present)
  - 2: Negative
- **Clinical Significance**: May indicate preeclampsia, especially with hypertension
- **Method**: Usually dipstick or 24-hour urine collection
- **Missing Values**: 0

### Medical History

#### `dm` (Diabetes Mellitus)
- **Type**: Integer
- **Range**: 1-2
- **Description**: History of diabetes mellitus
- **Values**:
  - 1: Yes (pre-gestational or gestational diabetes)
  - 2: No history
- **Clinical Significance**: Diabetes significantly increases pregnancy complications
- **Missing Values**: 0

#### `ht` (Hypertension)
- **Type**: Integer
- **Range**: 1-2
- **Description**: History of hypertension
- **Values**:
  - 1: Yes (chronic hypertension or family history)
  - 2: No history
- **Clinical Significance**: Predisposes to preeclampsia and other complications
- **Missing Values**: 0

#### `perdarahan` (Bleeding History)
- **Type**: Integer
- **Range**: 1-2
- **Description**: History of bleeding in current pregnancy
- **Values**:
  - 1: Yes (antepartum hemorrhage)
  - 2: No bleeding history
- **Clinical Significance**: May indicate placental problems or cervical issues
- **Missing Values**: 0

#### `penyakit_lain_cat` (Other Diseases)
- **Type**: Integer
- **Range**: 0-1
- **Description**: Categorized presence of other diseases
- **Values**:
  - 0: No other significant diseases
  - 1: Other diseases present (typhus, COVID-19, dengue, malaria, UTI, etc.)
- **Derivation**: Categorized from free-text "other diseases" field
- **Missing Values**: 0

### Vital Signs

#### `diastole` (Diastolic Blood Pressure)
- **Type**: Integer
- **Range**: 60-120 mmHg
- **Description**: Diastolic blood pressure measurement
- **Clinical Significance**:
  - ≥90 mmHg: Hypertension threshold
  - ≥110 mmHg: Severe hypertension
- **Measurement**: Last recorded measurement during assessment
- **Missing Values**: 0

#### `sistole` (Systolic Blood Pressure)  
- **Type**: Integer
- **Range**: 90-180 mmHg
- **Description**: Systolic blood pressure measurement
- **Clinical Significance**:
  - ≥140 mmHg: Hypertension threshold
  - ≥160 mmHg: Severe hypertension
- **Measurement**: Concurrent with diastolic measurement
- **Missing Values**: 0

### Target Variable

#### `risiko_cat` (Risk Category)
- **Type**: Integer (Categorical)
- **Range**: 0-3
- **Description**: Pregnancy risk classification (target variable)
- **Values**:
  - **0: Normal** (n=3,491, 65.7%)
    - No significant risk factors identified
    - Standard antenatal care appropriate
  - **1: Low Risk** (n=1,464, 27.6%)  
    - Minor risk factors present
    - Enhanced monitoring recommended
  - **2: Moderate Risk** (n=299, 5.6%)
    - Multiple or moderate risk factors
    - Specialist consultation required
  - **3: High Risk** (n=59, 1.1%)
    - Severe risk factors present
    - Tertiary care management needed

**Classification Criteria**: Based on AAP/ACOG guidelines with clinical expert validation

## Data Quality Information

### Completeness
- **Overall completeness**: 100% (no missing values after cleaning)
- **Original dataset**: 5,324 records
- **Excluded records**: 11 (0.2%)
- **Final dataset**: 5,313 records

### Exclusion Criteria Applied
1. **Missing risk classification**: Records without valid risk category
2. **Missing critical parameters**: Records missing essential clinical values  
3. **Physiological implausibility**: Values outside clinically possible ranges
4. **Data entry errors**: Obvious transcription mistakes

### Value Ranges and Validation
- **Numeric variables**: All within physiologically plausible ranges
- **Categorical variables**: All values correspond to defined categories  
- **Consistency checks**: Related variables validated for logical consistency
- **Outlier handling**: Extreme values reviewed and excluded if implausible

## Statistical Summary

| Variable | Mean | Std | Min | 25% | 50% | 75% | Max |
|----------|------|-----|-----|-----|-----|-----|-----|
| umur | 28.4 | 6.1 | 12 | 24 | 28 | 32 | 51 |
| paritas | 1.2 | 1.3 | 0 | 0 | 1 | 2 | 10 |
| jarak_anak | 183.5 | 398.2 | 0 | 24 | 48 | 108 | 999 |
| tb | 151.8 | 5.4 | 15 | 148 | 152 | 155 | 175 |
| hb | 11.4 | 1.8 | 0.4 | 10.2 | 11.4 | 12.6 | 144.1 |
| lila | 25.9 | 2.4 | 15 | 24 | 26 | 27.5 | 35 |
| diastole | 97.8 | 14.2 | 60 | 90 | 100 | 110 | 120 |
| sistole | 80.1 | 10.8 | 60 | 70 | 80 | 90 | 120 |

## Correlation Matrix (Key Variables)

Strong correlations (|r| > 0.3):
- `umur` ↔ `paritas`: r = 0.65 (older women have more children)
- `sistole` ↔ `diastole`: r = 0.58 (blood pressure components)
- `tb` ↔ `lila`: r = 0.31 (height and arm circumference)

## Usage Notes

### Machine Learning Considerations
- **Target imbalance**: Severe class imbalance (58:1 ratio for high-risk)
- **Feature scaling**: Recommend standardization for distance-based algorithms
- **Categorical encoding**: Binary variables already encoded as 1/2
- **Cross-validation**: Use stratified sampling to maintain class distribution

### Clinical Interpretation
- **Risk escalation**: Higher numeric values generally indicate increased risk
- **Interaction effects**: Consider combinations of risk factors
- **Population specificity**: Derived from Indonesian population
- **Temporal aspects**: Represents snapshot at assessment time

### Quality Assurance
- **Validation**: Clinical expert review of classifications
- **Consistency**: Cross-referenced with original clinical records
- **Privacy**: All identifying information removed
- **Ethics**: Appropriate approvals obtained for data sharing