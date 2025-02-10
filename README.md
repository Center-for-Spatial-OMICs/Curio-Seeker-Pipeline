# Curio-Seeker-Pipeline
Curio-Seeker Pipeline using Nextflow

There is a [Curio Knowledge website](https://knowledgebase.curiobioscience.com/overview/) which requires registration for access.

# Input
- Input: find the whitelist barcodes by TileID
- Reference, Download on their website (which is the reference)
- Conda environment (built same version STAR2.6.1d)
- NextFlow configuration file change 
- ==Step by Step== !!! by tutorial 
- Prepare the samplesheet.csv like in the example folder 


# Install Pipeline 

![Installation Guide](https://github.com/Center-for-Spatial-OMICs/Curio-Seeker-Pipeline/raw/main/Images/1-Installation.png)


![Setup](https://github.com/Center-for-Spatial-OMICs/Curio-Seeker-Pipeline/raw/main/Images/2-Setup.png)


# Run Pipeline 


```
(star_2.6.1d) yliu08@splpdnb01:/mnt/plummergrp/Yutian/Curio_New/dnb1_mouse_sample71$ nextflow run /mnt/plummergrp/Yutian/Application/curioseeker-v3.0.0/main.nf --input /mnt/plummergrp/Yutian/Curio_New/curioseeker/samplesheet.csv --outdir /mnt/plummergrp/Yutian/Curio_New/dnb1_mouse_sample71/results/ -work-dir /mnt/plummergrp/Yutian/Curio_New/dnb1_mouse_sample71/work/ -resume -profile singularity --igenomes_base /mnt/plummergrp/Yutian/Application/
```

### Samplesheet 

![Samplesheet](https://github.com/Center-for-Spatial-OMICs/Curio-Seeker-Pipeline/raw/main/Images/3-SampleSheetExample.png)

[download example](https://github.com/Center-for-Spatial-OMICs/Curio-Seeker-Pipeline/tree/main/Example)

## Notes on input arguments
- ––input: (Required) Full path to the sample sheet. 
- ––outdir: (Required) Full path to the pipeline’s output folder. 
This folder does not need to be pre-created. Pipeline will auto-create.
If ${root_output_dir} was not specified, the pipeline will create folder results in the current directory.
- –work-dir: (Required) Full path to the pipeline’s work folder, hosting cached results, intermediate files, and step-wise logs.
This folder does not need to be pre-created. Pipeline will auto-create.
If ${root_output_dir} was not specified, the pipeline will create folder work in the current directory.
- ––igenomes_base: Full path to the top level of a reference. In the example reference above, it is the full path to the folder containing ‘Mus_musculus’. It should not include ‘Mus_musculus’. (Required for prebuilt references, Optional for custom references)
- –resume: (Optional) Resume an unfinished pipeline run from where it left off. The resumed pipeline will execute on cached results. 
- –profile: (Required) singularity or docker if you are using a single server linux workstation. slurm or sge if you are using an HPC. 
- –config: Full path to the configuration file specific to your HPC platform. Omit if on a single server linux workstation. Follow instructions here to construct the config file. (Required ONLY if you are submitting each step to a partition on your HPC)

# Outputs

After a successful run, output files can be found in $`{root_output_dir}/results/. `



```
Mouse_liver/
├── ${SAMPLE_ID}_anndata.h5ad
├── ${SAMPLE_ID}_barcodes.tsv
├── ${SAMPLE_ID}_cluster_assignment.txt
├── ${SAMPLE_ID}_genes.tsv
├── ${SAMPLE_ID}_MatchedBeadLocation.csv
├── ${SAMPLE_ID}_Metrics.csv
├── ${SAMPLE_ID}_MoleculesPerMatchedBead.mtx
├── ${SAMPLE_ID}_Report_files
│   └── figure-html
│       ├── Cluster_SPATIAL_combined-1.png
│       ├── QC1-1.png
│       ├── QC2-1.png
│       ├── Top_differentially_expressed_genes_per_cluster-1.png
│       └── Top_spatially_variable_features-1.png
├── ${SAMPLE_ID}_Report.html
├── ${SAMPLE_ID}_seurat.rds
├── ${SAMPLE_ID}_variable_features_clusters.txt
└── ${SAMPLE_ID}_variable_features_spatial_moransi.txt
```

More interpretation can be found [Interpreting Seeker Pipeline Output](https://knowledgebase.curiobioscience.com/bioinformatics/seeker-interpreting-output/)

