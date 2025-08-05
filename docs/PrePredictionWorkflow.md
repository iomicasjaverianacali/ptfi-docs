# Mass trace detection

## Purpose
- Extract mass traces by gathering peaks with similar m/z values that move along retention time.

## Methodology

### Initial Peak Selection
**Sorting**:

  - Peaks from an MSExperiment are sorted by intensity.
  - Stored as a list of potential chromatographic apex positions.

**Noise Filtering**:

  - Only peaks above a user-defined noise threshold are analyzed.
  - Peaks considered as apices must be **n times** above the minimal threshold.
  - Reduces noise and saves computational resources.

### Trace Extension
**Process**:

  - Mass traces are extended in both increasing and decreasing retention time directions.
  - Centroid m/z is calculated on-the-fly as an intensity-weighted mean of peaks.

**Termination**:

  - Frequency of gathered peaks drops below `min_sample_rate`.
  - Number of missed scans exceeds the threshold `trace_termination_outliers`.

### Final Filtering

Only mass traces that meet the following criteria are retained:

  - Satisfy minimal and maximal length requirements.
  - Fulfill the minimal sample rate criterion.

## Outputs
- A refined set of mass traces that meet the defined quality filters.

# Elution peak detection

 > "Mass traces may consist of several consecutively (partly overlapping) eluting peaks, e.g., stemming from (almost) isobaric compounds that are separated by retention time. Especially in metabolomics, isomeric compounds with exactly the same mass but different retentional behaviour may still be contained in the same mass trace" [^2].

## Purpose
- Extract chromatographic peaks from a mass trace.

## Methodology
### Preprocessing
- Applies smoothing to the mass trace's intensities.
- Uses Savitzky-Golay smoothing:
  - Second-order polynomial.
  - Frame length defined by `chrom_fwhm` (full width at half maximum).

### Peak Detection
- Detects local minima and maxima on smoothed intensities.
- Assumes one peak maximum within a fixed peak width (`chrom_fwhm`).

### Filtering
- Optional filtering of mass traces by:
  - Length in seconds ("fixed" filter).
  - Quantile-based criteria.

## Outputs
- A vector of chromatographic peaks for each mass trace (split mass traces).

## Usage
- Call the **`detectPeaks`** function to extract peaks.
- Optionally, use the **`filterByPeakWidth`** function for additional filtering.

# Feature Detection

## Purpose

- Assemble mass traces into composite features belonging to the same isotope pattern.
- Ensure compatibility in:
  - Retention times (RTs).
  - Mass-to-charge ratios (m/z).
  - Isotope abundances.

## Methodology
### Input

- Uses mass traces detected by **MassTraceDetection**.
- Chromatographic peaks are split by **ElutionPeakDetection**.

### Feature Hypothesis Formulation

**Hypothesis Generation**:

  - Feature hypotheses are exhaustively formulated based on mass traces within a local RT and m/z region.

**Scoring**:
  
  - Hypotheses are scored by their similarity to real metabolite isotope patterns.
  - Scores are derived from:
    - Independent models for RT shifts and m/z differences between isotopic mass traces.
  - Isotopic abundances are evaluated using an SVM model to distinguish between correct and false patterns.

### Output

**Composite Features**:

Mass traces that match feature hypotheses are assembled into composite features.

**Singletons**:

Mass traces that could not be assembled and represent low-intensity metabolites with only a monoisotopic mass trace, remain in the **FeatureMap** as singletons with an undefined charge state (0).

[^1]: [C++ API for pyOpenMS: Mass Trace Detection](https://openms.de/current_doxygen/html/classOpenMS_1_1MassTraceDetection.html)
[^2]: [C++ API for pyOpenMS: Elution Peak Detection](https://openms.de/current_doxygen/html/classOpenMS_1_1ElutionPeakDetection.html)
[^3]: [C++ API for pyOpenMS: Feature Detection](https://openms.de/current_doxygen/html/classOpenMS_1_1FeatureFindingMetabo.html)