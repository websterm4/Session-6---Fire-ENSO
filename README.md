Session-6---Fire-ENSO
=====================

#Problem
#Using monthly fire count data from MODIS Terra,develop and test a predictive model,
#for the number of fires per unit area per year driven by Sea Surface Temperature anomaly data.

#Reading the Data

import numpy as np
import glob 
import gdal

filename = 'files/data/MOD14CMH.200011.005.01.hdf'
#take the first hdf file as an example
g = gdal.Open(filename)

subdatasets = g.GetSubDatasets()
for fname, name in subdatasets:
    print name
    print "\t", fname
#subdatasets have been viewed

selected_layers = ["CloudCorrFirePix"]

data = {}

file_template = 'HDF4_SDS:UNKNOWN:"%s":%s'

for i, layer in enumerate(selected_layers):
    this_file = file_template % (filename,layer)
    g = gdal.Open(this_file)
    data[layer] = g.ReadAsArray()
#data now in a numpy array   

year = []
month = []


