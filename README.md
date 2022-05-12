# IUVS_Anomalous_Aurora

All relevant code is in the IUVS_Anomalous_Aurora git repository, and the rest of the data/analysis/results are in the following google drive: https://drive.google.com/drive/folders/1KXxwFY1oK4Xd2802XjIJzWcclw-MNA6T?usp=sharing. This document provides details on how to use the materials, but if there are any remaining questions, please feel free to contact me:
### Contact Info:
Adrienne Pickerill \
Work email: Adrienne.pickerill@lasp.colorado.edu \
Personal email: adriennepi@outlook.com \
Phone number: 425-681-5100 \

## Research Overview
### Motivation
The motivation for this project came from auroral observations that didn’t fit the spectral qualities expected from known auroral emissions on Mars. I refer to these observations as ‘anomalous emissions’. They are most similar in spectra to discrete aurora, in that their main features are Cameron bands and UVD, and they occur on the nightside. However, the IUVS team has found the Cameron band to UVD intensity ratio to be ~7 for discrete aurora, whereas anomalous emissions have a much higher ratio. 
### Data Collection
To form my data set, I looked through quicklooks_v6.5 and picked out potential anomalous emissions based on a lack of UVD in the detector images or spectra. I downloaded the L1C files for these orbits, and ran them through Ben Johnston’s python tool (see his git repository for more info on his code). The tool allowed me to pick specific pixels and sum the spectra of a hand selected set, reducing contamination from cosmic rays, solar continuum, etc. After running ~200 scans through the tool, I reduced my data set to 84 scans. \
Generally, the code works in the following way:
- User gets l1c file for orbit of interest from the maven vm in the folder \maven_iuvs\keep_it_here\nightglow_l1c_feb_2021\orbit#####\mvn_iuv_l1c_periapse-orbit#####* and places it in the folder called l1c_files
- User opens jupyter notebook called LimbSpectralTool_AuroralAnalysisNotebook_MultipleFiles_v20
- Run all cells through cell 6
- Cell 4 loads files for a range of orbits given by the user; change this range to include your orbit
- Cell 6 plots the pixels for the orbit/scan; change these inputs to match your desired orbit/scan 
- NOTE: The scan is in computer numbering, not human numbering. Therefore, if you want to see scan 1 from a quicklook, input 0 for the scan.
- A window pops up with the pixels of the scan colored by UVD intensity and Cameron band intensity, as well as two spectra
- Double click the pixel you want to see the spectrum for – it should pop up in the upper spectrum
- If you like the pixel, continue double clicking to see more. If you don’t want to keep the pixel (i.e if it’s too noisy, etc), press d before clicking the next pixel
- When you are done selecting pixels, press e before selecting your final pixel. This will add all of your clicked pixel spectra together into one spectrum, shown in the lower spectral plot
- Press n to save a numpy file of the selected pixel data. This will be important for plotting the scans in other ways later

For more details, see Ben Johnston's git repository. Likely, anomalous data collection is largely complete. Because of that, and for simplicity, I won't go into too much more detail on using the code to collect data. If more data collection needs to be done, please feel free to contact me for more info on using the code.

## Repository Code
There are 4 python notebooks attached in the git repository. The code is also in the google drive - I would recommend running it based on the folder organization in the drive, because much of the code calls spreadsheets/files from specific places. 
1. LimbSpectralTool_AuroralAnalysisNotebook_load_v21_npy_files_06Feb22022_with_MSO.ipynb \
This code was developed after we ran into some issues with our coordinate systems. In order to view solar zenith angle, latitude, and longitude at the same time for each emission, we converted to MSO coordinates. The v17 and v20 numpy files were converted to MSO numpy files, and run through this tool to get the updated attributes for each emission. This notebook also contains several plotting capabilities that I developed, including comparisons of the anomalous spectra summed together to a discrete emission and to a template, an azimuth angle histogram, a global nightside plot, and a postage stamp plot of all the anomalous emissions together. If any emissions are added, make sure to put the data into master_set.csv to get them to show up in these plots.
2. LimbSpectralTool_AuroralAnalysisNotebook_MultipleFiles_V20.ipynb \
This is the main code that the above bulleted list outlines. Use this code to investigate the individual pixels of any specific orbit/scan.
3. best_orbit_stats.ipynb \
This code contains a lot of the analysis I did with my final data set. The anomalous data is pulled from the master_set spreadsheet, and is compared to data from the total excluded data set (excluded_and_short_updated.csv) and to the discrete emissions contained in iuvs_statistical_detections_short_v7.1.csv. It creates histograms for solar zenith angle, CO/CO2p ratio, latitude, altitude, local time, normalized latitude, normalized solar zenith angle, and season. It also has a plot of the anomalous emissions against the magnetic field map of Mars. Ideally, you should just be able to add any new data to the appropriate spreadsheet, and the plots should work as expected. 
4. falloff_plots.ipynb \
This code is a short analysis I did on CO/CO2p ratio change with altitude. It uses a standard exponential pressure decay equation, which depends on the individual scale heights of CO and CO2 above the homopause. Scale heights, homopause level, and starting pressure values are inputs - feel free to change them to model different scenarios. There is also a mixing ratio plot to demonstrate how the mixing ratio changes with the pressure of each molecule.

## Google Drive Documents
The rest of the code folder on the google drive contains npy files, l1c files, templates, magnetic field maps, etc, that you will hopefully not need to edit/use. These are here so that the code can run smoothly. 

The analysis folder contains a lot of figures - feel free to look through them if you're interested, but the latest versions are in figures/thesis_figs. The limb_tool_figs folder also contains many scans that were run through the coding tool, in case you want to check to see if one you're interested in has already been plotted. Finally, my thesis and thesis slides are in this folder, which will contain a good overview of all the trending, data, and possible explanations.

qls_and_spreadsheets contains all the quicklook files and excel data spreadsheets I've used. The spreadsheets are also in a folder in the code folder so that they can be called by the best_orbit_stats code. 

### Future Work
Aside from further investigation into the current possible explanations, other recent suggestions include:
- Look into anticorrelation to magnetic field, i.e maybe energies of impacting electrons from field acceleration are high enough that it will most often excite both cameron bands and UVD
-  Could be particles coming from dayside to nightside, which would also be found at high altitudes and close to the terminator
-  Plot the altitude and co2 density together since the density at different altitudes varies throughout the year
-  More energy modeling
