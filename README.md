## Recipe to produce flat trees for B->K(*)LL

The following recipe has been tested on lxplus.

### Prerequisites

* Subscribe to github and set it up for CMSSW, see [here](http://cms-sw.github.io/faq.html#how-do-i-subscribe-to-github).
* Fork the cmg-cmssw repository, see [here](https://github.com/CERN-PH-CMG/cmg-cmssw).
* Fork the new cmgtools-lite repository, see [here](https://github.com/CERN-PH-CMG/cmgtools-lite).
* Then set up your working area, see below.

### Set up CMSSW release area and CMGTools packages

Installation instructions are found [here](https://twiki.cern.ch/twiki/bin/viewauth/CMS/CMGToolsReleasesExperimental#CMGTools_lite_development_releas). 

Documentation and tutorial can be found [here](https://twiki.cern.ch/twiki/bin/view/CMS/CMGToolsMain) and [here](https://twiki.cern.ch/twiki/bin/view/CMS/CMGToolsPythonAnalysis).

### Tweaks to the 'baseline' installation

Edit ```POG_PFID_Loose``` --> ```POG_PFID_Loose2016``` in the line [here](https://github.com/CERN-PH-CMG/cmgtools-lite/blob/94X_dev/H2TauTau/python/proto/analyzers/JetAnalyzer.py#L251)

To obtain correct JECs, run **[this](https://github.com/CERN-PH-CMG/cmgtools-lite/blob/94X_dev/RootTools/data/jec/getJec.py)** cfg using ```cmsRun```. **First**, edit the cfg to use the correct GT (e.g. [this one](https://github.com/ICBPHCMS/BKstLL/blob/master/cfgPython/b0kstee_gen_cfg.py#L108))

### Install and run BKstLL package

```
cd $CMSSW_BASE/src/CMSTools
git clone git@github.com:bainbrid/BKstLL.git
cd BKstLL
scram b
cd cfgPython
heppy test b0kstee_gen_cfg.py -N10
```

Your flat root tree should be found at ```test/BdKstMM/BKstLLGenTreeProducer/tree.root```

It's probably sufficient to run interactively to produce the flat trees.

If that's not quick enough for you, it should be straight forward to configure to run on the batch as follows (untested)

Set ```production=True``` in the cfg file

Then ```heppy_batch.py -o b0kstee_gen_cfg.py -b 'bsub -u hjkagsdjhga -q 8nh < ./batchScript.sh'```

(Note that the ```hjkagsdjhga``` is simply a nonsensical string that stops your inbox getting spammed on job completion.)

