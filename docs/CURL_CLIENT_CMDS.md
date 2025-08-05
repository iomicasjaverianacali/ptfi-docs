# Compute MS2 

## Windows client

curl -X POST http://localhost:5000/compute_ms2 ^
-H "Content-Type: application/json" ^
-d "{\"parameters\": {\"user_name\": \"Julian\", \"project_name\": \"TestProject\", \"ground_truth_ms2_filename\": \"ground_truth\", \"mass_trace_mass_error_ppm\": 10.0, \"mass_trace_noise_threshold_int\": 1000.0, \"mass_trace_chrom_peak_snr\": 3.0, \"mass_trace_min_sample_rate\": 0.5, \"mass_trace_min_length\": 5.0, \"mass_trace_max_length\": -1.0, \"mass_trace_quant_method\": \"area\", \"elution_peak_width_filtering\": \"auto\", \"elution_peak_chrom_fwhm\": 5.0, \"elution_peak_chrom_peak_snr\": 3.0, \"elution_peak_min_fwhm\": 1.0, \"elution_peak_max_fwhm\": 60.0, \"elution_peak_masstrace_snr_filtering\": \"false\", \"feature_detection_remove_single_traces\": \"false\", \"feature_detection_local_rt_range\": 15.0, \"feature_detection_local_mz_range\": 5.0, \"feature_detection_charge_lower_bound\": 1, \"feature_detection_charge_upper_bound\": 3, \"feature_detection_chrom_fwhm\": 5.0, \"feature_detection_report_summed_ints\": \"false\", \"feature_detection_enable_RT_filtering\": \"true\", \"feature_detection_isotope_filtering_model\": \"metabolites (5% RMS)\", \"feature_detection_mz_scoring_13C\": \"false\", \"feature_detection_use_smoothed_intensities\": \"true\", \"feature_detection_report_convex_hulls\": \"true\", \"feature_detection_report_chromatograms\": \"false\", \"feature_detection_mz_scoring_by_elements\": \"false\", \"make_ms2_mz_tolerance\": 0.01, \"make_ms2_rt_tolerance\": 5.0, \"max_peak_filter_pptg\": 0.2, \"merger_spectra_mz_binning_width\": 5.0, \"merger_spectra_mz_binning_width_unit\": \"ppm\", \"merger_spectra_sort_blocks\": \"RT_ascending\", \"merger_spectra_mz_tolerance\": 0.0001, \"merger_spectra_mass_tolerance\": 0.0, \"merger_spectra_rt_tolerance\": 15.0, \"filter_type\": \"window_mower\", \"window_mower_windowsize\": 50.0, \"window_mower_peakcount\": 2, \"window_mower_movetype\": \"slide\", \"threshold_mower_threshold\": 0.05, \"nlargest_n\": 200, \"filename_feature_map\": \"feature_map\", \"filename_ms2s_mzml\": \"ms2s\", \"filename_consensus_map\": \"consensus_map\"}}"

## Linux client

curl -X POST http://localhost:5000/compute_ms2 \
-H "Content-Type: application/json" \
-d '{"parameters": {"user_name": "Julian", "project_name": "TestProject", "ground_truth_ms2_filename": "ground_truth", "mass_trace_mass_error_ppm": 10.0, "mass_trace_noise_threshold_int": 1000.0, "mass_trace_chrom_peak_snr": 3.0, "mass_trace_min_sample_rate": 0.5, "mass_trace_min_length": 5.0, "mass_trace_max_length": -1.0, "mass_trace_quant_method": "area", "elution_peak_width_filtering": "auto", "elution_peak_chrom_fwhm": 5.0, "elution_peak_chrom_peak_snr": 3.0, "elution_peak_min_fwhm": 1.0, "elution_peak_max_fwhm": 60.0, "elution_peak_masstrace_snr_filtering": "false", "feature_detection_remove_single_traces": "false", "feature_detection_local_rt_range": 15.0, "feature_detection_local_mz_range": 5.0, "feature_detection_charge_lower_bound": 1, "feature_detection_charge_upper_bound": 3, "feature_detection_chrom_fwhm": 5.0, "feature_detection_report_summed_ints": "false", "feature_detection_enable
 
# Predict smiles

## Windows client

curl -X POST http://localhost:5000/predict_smiles ^
-H "Content-Type: application/json" ^
-d "{\"parameters\": {\"user_name\": \"Julian\", \"file_name\": \"red_ground_truth\", \"trained_model_name\": \"dd_arch1_lf1_data_1\", \"project_name\": \"QC_ppt_forages_clipped_DELETE\", \"num_pred\": 5, \"predict_approach\": \"beam_search\", \"device\": \"cpu\", \"beam_size\": 3}}"

## Linux client

curl -X POST http://localhost:5000/predict_smiles \
-H "Content-Type: application/json" \
-d '{"parameters": {"user_name": "Julian", "file_name": "red_ground_truth", "trained_model_name": "dd_arch1_lf1_data_1", "project_name": "QC_ppt_forages_clipped_DELETE", "num_pred": 5, "predict_approach": "beam_search", "device": "cpu", "beam_size": 3}}'

 
# Generate predicted SMILES

## Windows client

curl -X POST http://localhost:5000/generate_predicted_ms2 ^
-H "Content-Type: application/json" ^
-d "{\"parameters\": {\"user_name\": \"Julian\", \"project_name\": \"QC_ppt_forages\", \"predicted_ms2_filename\": \"predicted_ms2\", \"ionization\": \"[M+H]+\", \"device\": \"cpu\"}}"

## Linux client

curl -X POST http://localhost:5000/generate_predicted_ms2 \
-H "Content-Type: application/json" \
-d '{"parameters": {"user_name": "Julian", "project_name": "QC_ppt_forages", "predicted_ms2_filename": "predicted_ms2", "ionization": "[M+H]+", "device": "cpu"}}'

# Validate predictions

## Windows client

curl -X POST http://localhost:5000/validate_predictions ^
-H "Content-Type: application/json" ^
-d "{\"parameters\": {\"user_name\": \"Julian\", \"project_name\": \"QC_ppt_forages\", \"predicted_ms2_filename\": \"predicted_ms2\", \"ground_truth_ms2_filename\": \"ground_truth\", \"predicted_smiles_filename\": \"final_predictions\", \"weight_mass_missmatch\": 0.5, \"weight_dreams\": 0.5}}"

## Linux client

curl -X POST http://localhost:5000/validate_predictions \
-H "Content-Type: application/json" \
-d '{"parameters": {"user_name": "Julian", "project_name": "QC_ppt_forages", "predicted_ms2_filename": "predicted_ms2", "ground_truth_ms2_filename": "ground_truth", "predicted_smiles_filename": "final_predictions", "weight_mass_missmatch": 0.5, "weight_dreams": 0.5}}'