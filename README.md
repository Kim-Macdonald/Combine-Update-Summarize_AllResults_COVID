# Combine-Update-Summarize_AllResults_COVID

## UpdateQCsummaryLineages_v3serv_v2.py

This script will: 
- Combine VoCcaller output for all runs/directories in analysis directory. 
- Update lineage calls & metadata for all samples 
  - using output from another pipeline here: https://github.com/BCCDC-PHL/pangolin-nf which runs pangolin on all samples in the analysis directory and outputs a single file of results, each day.
  - the script finds the newest pangolin file and updates lineages etc for all samples, and then re-calls VoCs, VoIs, Other lineages of Interest, Non-VoCs, QC Fails, etc.  
- Replace pangolin lineages with manually reviewed calls if applicable. 
- Output file of updated results for all samples
- Output file of samples analyzed today (compares prior runs analyzed to those being analyzed currently to produce the differences (newest samples)).

### Usage

If not already done: set up environment with pandas, and any other dependencies (done on sabin already)

    conda create -n pandas pandas


First run the 2 scripts to combine results for a run, and call VoCs/VoIs/Other etc for a run (https://github.com/Kim-Macdonald/mergeQCresults_plusMissing and https://github.com/Kim-Macdonald/VoCcaller):

     Navigate to the directory for that sequencing run:
     cd /path/To/analysisDirectory/<RunID>
     
     Run the 2 scripts on that sequencing run:
     conda activate pandas; python3 /path/To/mergeQCresults_plusMissing_v5b.py; python3 /Path/To/addVoCcalls_RunNum_v2.py; conda deactivate
     
     To run the 2 scripts on all sequencing runs:
     cd /path/To/analysisDirectory
     
     

Then run UpdateQCsummaryLineages_v3serv_v2.py: 

    cd /path/To/analysisDirectory
    conda activate pandas; python3 /Path/To/UpdateQCsummaryLineages_v3serv_v2_oldPostAnalysis.py; conda deactivate

### Output

The script will produce 2 output files, and 2 intermediate files you should keep (are used to generate list of samples analyzed today):

- Runs_CombinedQCsummary_PlusNewestLineages_[date].csv (This is the file with results for all samples in the analysis directory (all sequencing runs in that directory)
- Runs_CombinedQCsummary_vs_Prior_v0_[date]_Run#-#.csv (This is a list of the samples analyzed today - can be used in QC dashboards etc to summarize and report on QC metrics etc for the current runs) (generated by a comparison of the 2 files below)
- Runs_CombinedQCsummary_v0.csv 
- Runs_CombinedQCsummary_prior_v0.csv (if you re-run the script, and want it to re-output the file of runs analyzed today (e.g. if you remove low quality samples/libraries, and want the new file to exclude those runs), you may want to copy this file somewhere before-hand, then rename to Runs_CombinedQCsummary_v0.csv. Otherwise it will say there are no new runs today (if you use the Runs_CombinedQCsummary_v0.csv file as-is). Otherwise you can manually make changes to the 2nd file, as needed. 



## RemoveRepeatsFromUpdatedLineages_v1.py




## SummarizePassFailStats_v2.py




