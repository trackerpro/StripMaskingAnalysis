# Strip Masking Analysis 

This repository was developed in order to fine tune and design the single-strip masking analysis implemented in the SiStrip commissioning workflow as ```PedsFullNoise``` task.

## CMSSW Setup:

```sh
cmsrel CMSSW_12_1_0 ;
cd CMSSW_12_1_0/src ;
cmsenv;		      
git-cms-init; 
git-cms-addpkg DataFormats/SiStripCommon/;
git-cms-addpkg DPGAnalysis/SiStripTools/;
git-cms-addpkg CommonTools/TrackerMap;
git cms-addpkg DQM/SiStripCommissioningAnalysis;
git cms-addpkg DQM/SiStripCommissioningClients;
git cms-addpkg DQM/SiStripCommissioningDbClients;
git cms-addpkg DQM/SiStripCommissioningSources;	 
git cms-addpkg DQM/SiStripCommissioningSummary;
git clone git@github.com:trackerpro/StripMaskingAnalysis.git TrackerDAQAnalysis/StripMaskingAnalysis
scramv1 b -j 4;
```

## Producing the source DQM files for the Pedestal runs

```sh
cd TrackerDAQAnalysis/StripMaskingAnalysis/test;
cmsRun pedestalDQMfromDat_cfg.py partition=<partition> inputPath=<input path for the dat files> doFEDErr=<make map of bad channels> runNumber=<Run number to pick files in the /opt/cmssw directory>
cmsRun pedestalSourcefromDQM_cfg.py inputFiles=<input files> inputPath=<input path for DQM files>
```

## Run the analysis

Using the codes located in ```macros``` directory. In particular:

* ```fullPedestalAnalysis.C```: runnning the classsification analysis for bad strips on the DQM file with per-APV histogram storing in tree format the result of test-statistics for every strip
* ```plotPedestalAnalysis.C```: plot result for good and bad strips as example i.e. noise distributions, values of the various test-statistics etc based on defined criterion
* ```plotTestStatistics.C```: plot the value/distribution of the main test statistics
