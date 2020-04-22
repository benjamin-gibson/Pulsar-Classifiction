# Pulsar Classification

## Data - allpulsars.txt
This text file contains data on a bunch of parameters, only some of which are used in the code to do the classification.  Put this file in the same directory as classificationsample.py and the code will run on this data.

The data has been queried from the ATNF (Australian Telescope National Facility) Pulsar Catalogue: https://www.atnf.csiro.au/research/pulsar/psrcat/ .  The catalogue contains data on derived and measured parameters for ~2800 pulsars.

Paper: Manchester, R. N., Hobbs, G. B., Teoh, A. & Hobbs, M., Astron. J., 129, 1993-2006 (2005) (astro-ph/0412641)

## Code - classificationsample.py
This code uses the data from allpulsars.txt to classify pulsars.  It uses columns 2,3,4,5,8,10,15,19,20,22, which are data on the pulsars Galactic Latitude, Galactic Longitude, Rotation Frequency, Rotation Frequency Time Derivative, Dispersion Measure, Rotation Measure, Classification, Energy Loss Rate, Energy Flux (at the Sun), and Magnetic Field Strength at the light cylinder.  All of the above except Galactic Latitude and Longitude and Classification will be used to classify the unclassified pulsars.  The first step is to mask out pulsars who are missing data for these parameters, except for Classification, as many pulsars were not classified.  85 of the remaining pulsars have been classified as 'HE' (Spin-powered pulsar with pulsed emission from radio to infrared or higher frequencies) in the catalogue.  Next is to create a training subset of pulsars by randomly selecting around 200 pulsars from the ~1000 remaining unclassified pulsars.  This training set, which includes the classified pulsars, is used to train a model for classification using 4 different classification methods.

The 4 methods used are K-Nearest-Neighbor, Decision Trees, Random Forest, and Gradient Boosting.  Each classification method utilizes a Sci-Kit Learn function that automates the classifier.  K-Nearest-Neighbor classification uses distance between points in your parameter space to generate a decision boundary where new data points that are within that boundary are classified as such.  Decision Tree classification generates a set of binary decisions that split up the data into classification.  Random Forest classification uses bootstrapping to generate several decision trees, then averages the results.  Gradient Boosting classification runs the same decision tree on the data several times and weights the data based on correct classification in an attempt to bring out weak trends in the data that can be used to classify.

This code generates several classifications of pulsars using each of these methods, varying important parameters in the Sci-Kit function to see how the classification is affected.  In addition, histograms of the distribution of each data set are generated, where nonclassified objects are green, newly classified objects are red, and the training objects are blue.  In the end, around 100 new pulsars are classified as HE, with the Energy Loss Rate, Energy Flux, and Magnetic Field Strength being the most important parameters used to classify objects. 