# Sentinel 2 Atmospheric correction 
### Feng Yin
### Department of Geography, UCL
### ucfafyi@ucl.ac.uk

This atmospheric correction method uses MODIS MCD43 BRDF product to get a coarse resolution simulation of earth surface. A model based on MODIS PSF is built to deal with the scale differences between MODIS and Sentinel 2. We uses the ECMWF CAMS prediction as a prior for the atmospheric states, coupling with 6S model to solve for the atmospheric parameters. We do not have a proper cloud mask at the moment and no topography correction as well. Homogeneouse surface is used without considering the BRDF effects.

## Data needed:
* MCD43 (`multiply_atmospheric_corection/MCD43`): 16 days before and 16 days after the Sentinel 2 sensing date
* ECMWF CAMS Near Real Time prediction (`multiply_atmospheric_corection/cams`): a time step of 3 hours with the start time of 00:00:00 over the date
* global dem (`multiply_atmospheric_corection/eles`): Global DEM VRT file built from ASTGTM2 DEM, and a bash script under eles/ can be used to generate with the individual files.
* emus (`multiply_atmospheric_corection/emus`): emulators for the 6S and wv restrival, can be found at: http://www2.geog.ucl.ac.uk/~ucfafyi/emus/

## Usage:
* A typical usage is:
`python Sentinel_atmo_cor.py -f /directory/where/you/store/s2/data/29/S/QB/2017/9/4/0/ [-m MCD43_dir -e emus_dir -d global_DEM -c Cams_dir]`

* Arguments inside [ ] means optional.

## Output:
The outputs are the corrected TOA images saved as `B0*_sur.tif` for each band. TOA_RGB.tif and BOA_RGB.tif are generated for a fast visual check of correction results. They all under `/directory/where/you/store/s2/data/29/S/QB/2017/9/4/0/` as the example usage.
