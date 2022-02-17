## Optical Astronomy Research

**An investigation into photometric emissions of low-mass stellar objects via observational data from the WIYN 0.9m optical telescope in Kitt Peak, AZ.**

My research group at the Five College Astronomy Department took photometric images in several wavelengths to provide us with data to study light curves produced by varying flux in very low-mass objects. I analyzed the morphology of such curves and compared objects of different masses, ages, and disk types to deepen our understanding of how stellar and substellar objects in their earliest stages change over time.

This project was in collaboration with my research group in Astro341 at Amherst College, this specific concept being explored with my research partner Savio Olivera; I will only be presenting code and writing samples that are my own.

Tools: Jupyter/Python (pandas, numpy, matplotlib, photutils, astropy, scipy), Excel, Astrometry, SAOImageDS9

Primary skills: data cleaning, data pipeline creation, data visualization, data analysis, data management

### Scientific Overview for a Non-Scientific Audience
If you have no experience in astronomy, here's the basics of what you need to know about the science of this project.

Stars and substellar objects (star-like objects that are too low in mass to be considered stars) form when gravity pulls debris together. These objects are very active when forming, as debris falling onto the objects causes 
Clouds of gas and dust collapse under the gravitational pull of a newly formed stellar object; debris collects and begins to orbit the object as it falls to the surface. Instead of falling directly onto the star, this collected matter flattens and forms a disk around the object in order to preserve angular momentum; this is an accretion disk, and many young objects host them until they dissipate within 3Myrs of formation.

Ha wavelength is an indicator of stellar activity: chomospheric activity, flares, etc. changes in Ha flux directly indicate changes in activity. We can measure this by the flux or brightness of objects over time.

In order to make sure an object is only increasing its flux in Ha and not simply becoming brighter in all wavelengths, we need another nearby wavelength to compare: Ha off.

When we take images of space, we must process the raw data prior to analysis. We also superimpose the processed images on top of each other to create a deeper image of our region, allowing us to see deeper into space and view fainter objects more accurately; hundreds of images will result in only a few data points, at least for our investigation into flux changes.


### The Data
The data taken utilized the WIYN 0.9m telescope on Kitt Peak National Observatory with the Half-Degree Imager (HDI), and spans 8 nights from January 19-26, 2020; only 6 nights of data were used due to weather conditions. The regions of space I have analyzed are the Taurus V410 field and the Praesepe cluster; the former, a young star forming region of 1-3Myr, and the latter, a cluster of about 600-800Myr old.


These data were taken in the Hα wavelength (665nm) and Hα continuum narrowband (666nm), and calibration data (bias frames) were taken for each night; every image also contains overscan data, bias adjustment for every single image.

Over 300 raw files total; after reduction over 1300 files total. The final data set is reduced to 12 data points.

increased activity should be displayed as an increase in H-alpha, with no significant change in H-alpha “off”. This comparison rules out any random changes in the flux due to reasons other than accretion or activity, as H-alpha is the only one of the two bands that will display significant change in flux for these reasons.

Data is also taken from Visier using the coordinates of the objects of interest (found via Astrometry) in the images taken. 

### Data Reduction
Images taken from telescopes need to be processed prior to analysis in order to calibrate and clean up intrinsic noise in the CCD.

Standard data reduction procedure in optical wavelengths involves a process of bias subtraction, dark current subtraction, flatfielding. Alignment of images

sorting files: hard-coded sorting methods were used, as this is the simplest method to organize the data
<details>
  <summary>View Filesorter Function</summary>

```
  def filesorter(filename, foldername, fitskeyword_to_check, keyword):
    '''
    This function takes input file and places it in a folder given if it is the correct type of fits file.
    '''
    # this checks if there is a file of that name already, if so then it moves onto the next step, otherwise
    # tells you it does not exist.
    if os.path.exists(filename):
        pass
    else:
        print(filename + " does not exist or has already been moved.")
        return
    
    header = fits.getheader(filename)
    fits_type = header[keyword]
    
    # this checks that there is a folder of that name, and makes it if there is not
    if os.path.exists(foldername):
        pass
    else:
        print("Making new directory: " + foldername)
        os.mkdir(foldername)
    
    # this checks that the file is the correct type of fits file and moves it to the folder if it is
    if fits_type == fitskeyword_to_check:
        destination = foldername + '/'
        print("Moving " + filename + " to: ./" + destination + filename)
        os.rename(filename, destination + filename)  
    return
  ```
  
  </details>
  
<details>
  <summary>View Code</summary>
  
``` 
  #define bias correction & subtraction function
  def bias_correction(filelist, path_to_bias):
    """
    This function takes in a list of images and a master bias image and calculates the corrections to the bias using the 
    overscan of each image. It then bias subtracts each image with this new, corrected master bias and saves the images
    with the prefix b_.
    """
    n = len(filelist)
    for ii in range(n):
        #getting data from images
        im_data = fits.getdata(filelist[ii])
    
        new_header = fits.getheader(filelist[ii])
        
        bias_data = fits.getdata(path_to_bias)
        
        #isolating the overscan from the images
        overscan = im_data[4100:4140,4100:4140]
        
        #take median of overscan region and master bias
        osmed = np.median(overscan)
        
        MBmed = np.median(bias_data)
        
        #make new master bias by normalizing the old one and scaling it by the overscan median
        MBnew = bias_data/MBmed
        
        MBnew = MBnew*osmed
        
        #subtract new bias from image
        subtract_data = im_data - MBnew
        
        #delete overscan now that we are done with it
        new_image = subtract_data[0:4096,0:4096]
        
        #save as new fits file
        fits.writeto('b_' + filelist[ii],new_image, new_header, overwrite = True )
    print('Files bias subtracted and saved with prefix b_')
    return
  
```
  
</details>

### Analysis


### Results
I successfully extracted relative flux data for 12 objects in Taurus and 24 in Praesepe (fig.1 below).

Mass
lower mass = more variable activity, more sporatic and has higher range; this is anticipated due to the nature of lower mass objects

Age
younger objects = more active; older objects are finished accreting and stablized, their primary activity will be flares

Disks
more complete disk = more debris around object = more accretion and thus more activity

### Figures
<img src="images/dataspread.png" width=400>


For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
