# How to run the `predict_CASMI_2022_modular.py` script?

# CASMI files

The CASMI files should have the following folder structure:

pos
    -A_M1_posPFP
        -A_M1_posPFP_01.mzml
        -A_M1_posPFP_02.mzml
    -A_M2_posPFP
        -A_M2_posPFP_01.mzml
        -A_M2_posPFP_02.mzml
    .
    .
    .
neg
    -A_M7_negPFP
        -A_M7_negPFP_03.mzml
        -A_M7_negPFP_04.mzml
    .
    .
    .

## [OPTION 1] Using default parameters

python predict_CASMI_2022_modular.py \
    --chromatograms_dir path/to/dir/with/mzml/files \
    --model_dir /path/to/models/dir \
    --model_name originaldata_datadriven_tokenizer \
    --output_dir /path/to/output/dir
    --protcol CASMI

## [OPTION 2] Overriding specific parameters via command line

python predict_CASMI_2022_modular.py \
    --chromatograms_dir path/to/dir/with/mzml/files \
    --model_dir /path/to/models \
    --model_name originaldata_datadriven_tokenizer \
    --output_dir /path/to/output/dir \
    --mass_trace_mass_error_ppm 15.0 \
    --mass_trace_chrom_peak_snr 4.0 \
    --feature_detection_local_rt_range 3.0
    --protcol CASMI

## [OPTION 3] Providing a JSON file with the desired parameters

python predict_CASMI_2022_modular.py \
    --chromatograms_dir path/to/dir/with/mzml/files \
    --model_dir /path/to/models/ \
    --model_name originaldata_datadriven_tokenizer \
    --output_dir /path/to/output/dir \
    --params_file params.json \
    --protcol CASMI

## [OPTION 4] Combining JSON file and command-line overrides

python predict_CASMI_2022_modular.py \
    --chromatograms_dir path/to/dir/with/mzml/files \
    --model_dir /path/to/models/dir \
    --model_name originaldata_datadriven_tokenizer \
    --output_dir /path/to/output/dir \
    --params_file params.json \
    --mass_trace_mass_error_ppm 15.0
    --protcol CASMI

If both a file and command line parameters are used, and the user specifies the same parameter in the command line and in the file, the value given by the command line will override the value in the file.

## Example of `params.json` file

{
    "mass_trace_mass_error_ppm": 10.0,
    "mass_trace_noise_threshold_int": 0.12e04,
    "mass_trace_chrom_peak_snr": 3.0,
    "mass_trace_min_sample_rate": 0.5,
    "mass_trace_min_length": 5.0,
    "mass_trace_max_length": -1.0,
    "mass_trace_quant_method": "area",
    "elution_peak_width_filtering": "auto",
    "elution_peak_chrom_fwhm": 2.0,
    "elution_peak_chrom_peak_snr": 3.0,
    "elution_peak_min_fwhm": 1.0,
    "elution_peak_max_fwhm": 60.0,
    "elution_peak_masstrace_snr_filtering": "false",
    "feature_detection_remove_single_traces": "false",
    "feature_detection_local_rt_range": 2.0,
    "feature_detection_local_mz_range": 10.0,
    "feature_detection_charge_lower_bound": 1,
    "feature_detection_charge_upper_bound": 3,
    "feature_detection_chrom_fwhm": 2.0,
    "feature_detection_report_summed_ints": "false",
    "feature_detection_enable_RT_filtering": "true",
    "feature_detection_isotope_filtering_model": "metabolites (5% RMS)",
    "feature_detection_mz_scoring_13C": "false",
    "feature_detection_use_smoothed_intensities": "true",
    "feature_detection_report_convex_hulls": "true",
    "feature_detection_report_chromatograms": "false",
    "feature_detection_mz_scoring_by_elements": "false",
    'make_ms2_mz_tolerance': 0.01, 
    'make_ms2_rt_tolerance': 5.0, 
    'max_peak_filter_pptg':0.2,
    'merger_spectra_mz_binning_width':5.0,
    'merger_spectra_mz_binning_width_unit':"ppm",
    'merger_spectra_sort_blocks':"RT_ascending",
    'merger_spectra_mz_tolerance':1.0e-04,
    'merger_spectra_mass_tolerance':0.0,
    'merger_spectra_rt_tolerance':15.0,
    'filter_type':"window_mower",
    'window_mower_windowsize':50.0,
    'window_mower_peakcount':2, 
    'window_mower_movetype':'slide',
    'threshold_mower_threshold':0.05,
    'nlargest_n':200, 
    'filename_feature_map':"feature_map",
    'filename_ms2s_mzml':"ms2s",
    'filename_consensus_map':"consensus_map",
}

## Command Line Arguments Description

Below is a description of each argument that can be used with the `predict_CASMI_2022_modular.py` script:

### Required Arguments

- `--chromatograms`: Path to the directory containing the mzML files structured as described above.
- `--model_dir`: Path to the directory containing the prediction models.
- `--model_name`: Name of the model to use for predictions (e.g., "originaldata_datadriven_tokenizer.pth") WITH THE EXTENSION.
- `--output_dir`: Path to the directory where output files will be saved.
- `--protcol`: Protocol to use for prediction, e.g., "CASMI".

### Mass Trace Parameters

- `--mass_trace_mass_error_ppm`: Mass error tolerance in parts per million (default: 10.0).
- `--mass_trace_noise_threshold_int`: Intensity threshold for noise filtering (default: 1200).
- `--mass_trace_chrom_peak_snr`: Signal-to-noise ratio for chromatographic peak detection (default: 3.0).
- `--mass_trace_min_sample_rate`: Minimum required sampling rate (default: 0.5).
- `--mass_trace_min_length`: Minimum length of mass traces (default: 5.0).
- `--mass_trace_max_length`: Maximum length of mass traces. -1.0 for no maximum (default: -1.0).
- `--mass_trace_quant_method`: Method for quantification ("area" or alternative methods).

### Elution Peak Parameters

- `--elution_peak_width_filtering`: Setting for peak width filtering (default: "auto").
- `--elution_peak_chrom_fwhm`: Full width at half maximum for chromatographic peaks (default: 2.0).
- `--elution_peak_chrom_peak_snr`: Signal-to-noise ratio for elution peak detection (default: 3.0).
- `--elution_peak_min_fwhm`: Minimum full width at half maximum (default: 1.0).
- `--elution_peak_max_fwhm`: Maximum full width at half maximum (default: 60.0).
- `--elution_peak_masstrace_snr_filtering`: Enable/disable SNR filtering for mass traces (default: "false").

### Feature Detection Parameters

- `--feature_detection_remove_single_traces`: Whether to remove features with single traces (default: "false").
- `--feature_detection_local_rt_range`: Local retention time range for feature detection (default: 2.0).
- `--feature_detection_local_mz_range`: Local m/z range for feature detection (default: 10.0).
- `--feature_detection_charge_lower_bound`: Lower bound for charge state detection (default: 1).
- `--feature_detection_charge_upper_bound`: Upper bound for charge state detection (default: 3).
- `--feature_detection_chrom_fwhm`: Chromatographic FWHM for feature detection (default: 2.0).
- `--feature_detection_report_summed_ints`: Whether to report summed intensities (default: "false").
- `--feature_detection_enable_RT_filtering`: Enable/disable RT filtering (default: "true").
- `--feature_detection_isotope_filtering_model`: Model for isotope filtering (default: "metabolites (5% RMS)").
- `--feature_detection_mz_scoring_13C`: Enable/disable 13C m/z scoring (default: "false").
- `--feature_detection_use_smoothed_intensities`: Use smoothed intensities (default: "true").
- `--feature_detection_report_convex_hulls`: Report convex hulls (default: "true").
- `--feature_detection_report_chromatograms`: Report chromatograms (default: "false").
- `--feature_detection_mz_scoring_by_elements`: Enable/disable m/z scoring by elements (default: "false"). 
- `--filename_feature_map`: Name of the feautureXML files with the Feature map info. Do not add the extension. (default: feature_map).
- `--filename_consensus_map`: Name of the consensusXML files with the Consensus map info. Do not add the extension. (default: consensus_map).

### MS2-Features Mapping Parameters
- `--make_ms2_mz_tolerance`: m/z tolerance for MS2 features mapping (default: 0.01).
- `--make_ms2_rt_tolerance`: RT tolerance for MS2 features mapping (default: 5.0).
- `--filename_ms2s_mzml`: Name of the mzML files with the MS2 spectra. Do not add the extension. (default: ms2s).
- `--max_peak_filter_pptg`: Maximum peak filter for pptg (default: 0.2).
- `--merger_spectra_mz_binning_width`: m/z binning width for merging spectra (default: 5.0).
- `--merger_spectra_mz_binning_width_unit`: Unit for m/z binning width (default: "ppm").
- `--merger_spectra_sort_blocks`: Sorting method for blocks (default: "RT_ascending").
- `--merger_spectra_mz_tolerance`: m/z tolerance for merging spectra (default: 1.0e-04).
- `--merger_spectra_mass_tolerance`: Mass tolerance for merging spectra (default: 0.0).
- `--merger_spectra_rt_tolerance`: RT tolerance for merging spectra (default: 15.0).
- `--filter_type`: Type of filter to apply (default: "window_mower").
- `--window_mower_windowsize`: Window size for the window mower filter if `--filter_type:"window_mower"` (default: 50.0).
- `--window_mower_peakcount`: Number of peaks to keep in the window mower filter if `--filter_type:"window_mower"` (default: 2).
- `--window_mower_movetype`: Movement type for the window mower filter if `--filter_type:"window_mower"` (default: "slide").
- `--threshold_mower_threshold`: Threshold for the threshold mower filter if `--filter_type:"threshold_mower"` (default: 0.05).
- `--nlargest_n`: Number of largest peaks to keep if `--filter_type:"nlargest"` (default: 200).


### Other Arguments

- `--params_file`: Path to a JSON file containing parameter settings (as shown in the example above).