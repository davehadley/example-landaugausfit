# example-landaugausfit
An example ROOT script that fits a Landau+Gaussian function to a ROOT histogram.

This package provides a pyroot implementation of the ROOT example: [$ROOTSYS/tutorials/fit/langaus.C](https://root.cern.ch/root/html/tutorials/fit/langaus.C.html)

The fitter is implemented by the class `LanGausFit` in the file `langaus.py`. The most basic usage is:
```python
import ROOT
from langaus import LanGausFit
# create a histogram
histogram = ROOT.TH1D("hist", "hist", 100, 0.0, 10.)
histogram.FillRandom("gaus", 1000)
# fit the histogram
fit = LanGausFit()
func = fit.fit(histogram)
# The fitter return a ROOT TF1 (a 1D function).
func.Print()
```

The actual fit function is implemented inside `langaus.C`. If you want to copy this code into another package then you should remember to copy both files. 

You can test the fitter by running the script from the command line. 
```
python langaus.py -o testplot.eps
```

It will generate a Landau+Gaussian distribution, fit the distribution and save the plot to the provided file name.
For more information see the help message:
```
python langaus.py -h
```


```
    usage: Test script for LanGaus fit. [-h] [--mpv MPV] [--sigma SIGMA]
                                    [--width WIDTH] [--nevents NEVENTS]
                                    [--xlow XLOW] [--xhigh XHIGH] [-o OUTPUT]

optional arguments:
  -h, --help            show this help message and exit
  --mpv MPV             Generate data with this Landau MPV
  --sigma SIGMA         Generate data with this Gaussian sigma
  --width WIDTH         Generate data with this Landau width.
  --nevents NEVENTS     Generate this many events.
  --xlow XLOW           Plot min x value
  --xhigh XHIGH         Plot max x value
  -o OUTPUT, --output OUTPUT
                        Output plot file name.
```
