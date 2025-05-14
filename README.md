# Synthetic-Dose-Generator
Software tool for generating synthetic dose distributions that could be used as a training data for automated planning

User Guide: Synthetic Dose Generator for RapidPlan Training
________________________________________
Disclaimer
This software is intended for research and educational purposes only. It is the user's responsibility to verify all results and ensure clinical validity before any clinical use. The developer assumes no responsibility for any clinical outcomes or liabilities arising from the use of this software.
________________________________________
Introduction
Treatment planning is a cornerstone of the radiotherapy workflow and plays a vital role in patient care and clinical outcomes. Traditionally performed by dosimetrists or physicists, manual treatment planning introduces variability due to differing levels of experience, techniques, and judgment. This variability can affect treatment quality and consistency.
To address these challenges, the integration of machine learning into treatment planning has gained significant attention. Automated planning tools, such as Knowledge-Based Planning (KBP) systems like RapidPlan (RP) in the Eclipse Treatment Planning System (TPS), offer the promise of standardization and improved quality. RP uses historical clinical data to generate optimization objectives, streamlining the planning process and reducing inter-planner variability.
However, RP’s effectiveness heavily depends on the quality of training data. Several studies have shown that manually curated RP models often require further tuning or adjustments to achieve acceptable plan quality, particularly for complex treatments. Therefore, high-quality training data is essential for the robustness of these models.
To improve the predictive power of RP, this software tool—Synthetic Dose Generator—was developed. It allows users to generate synthetic, high-quality dose distributions based on anatomical geometry, which can be used to train or enhance RP models. The goal is to produce more consistent and optimal radiotherapy treatment plans.
________________________________________
Methods
The Synthetic Dose Generator was developed in MATLAB to simulate dose distributions using CT data, structure sets, and reference plans. Its key components include:
	Target Dose Simulation: Simulates 95%–105% of prescribed dose within the target volume.
	Fall-Off Modeling: Outside the target, dose is calculated using a double exponential decay:
〖Dose〗_(i ) (%)=〖73.2×exp〗^(-0.0572×d_i )+28.7×〖exp〗^(-0.0117×d_i )                                         (1)
where d_i is the distance from the target boundary.
	OAR Sparing: Incorporates spatial awareness to reduce dose near organs at risk (OARs).
This synthetic dose is then embedded into DICOM-compatible RT Dose and RT Plan files for integration with clinical TPS environments.
________________________________________
Procedure
Prerequisites:
Ensure that your input folder contains the following DICOM files:
	CT images
	RT Structures
	RT Plan
	RT Dose
Steps:
	Load DICOM Folder: Start the application and load the folder containing the DICOM files.
	Structure Reading: The tool will read all available contours from the RT Structure file.
	Target & OAR Selection: Select the PTV(s), CTV(s), and OAR(s). Hold ‘CTRL’ to select multiple contours.
	Enter Prescription Dose: Specify the dose (in Gy) for each selected PTV.
	View Dose Distribution: Visualize the generated synthetic dose distribution.
	Generate New DICOM Files:
	RT Plan: Saved as a file with the suffix _SynPlan
	RT Dose: Saved as a file with the prefix SynDose_...
	Replace Original Dose: Delete the original DICOM RT Dose file.
	TPS Import: Import the updated folder (CT, Structures, new Plan, and new Dose) into Eclipse TPS.
________________________________________
Benefits
	Reduces reliance on manual dose planning
	Enables training of RP models with synthetic, consistent data
	Facilitates generation of high-quality plans even with limited training datasets
________________________________________
Conclusion
The Synthetic Dose Generator is a novel tool designed to standardize and improve the quality of training data for KBP systems like RapidPlan. By using mathematically controlled dose distributions and reducing manual planning variability, this tool empowers clinicians and researchers to develop more robust, effective treatment plans.
________________________________________
For more information or updates, visit: https://horizonnb.ca/facilities/saint-john-regional-hospital/

