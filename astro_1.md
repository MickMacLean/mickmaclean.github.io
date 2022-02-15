## Optical Astronomy Research

**An investigation into photometric emissions of low-mass stellar objects via observational data from the WIYN 0.9m optical telescope in Kitt Peak, AZ.**

My research group at the Five College Astronomy Department took photometric images in the Hα wavelength (665nm), and Hα continuum narrowband (666nm), to provide us with data to study light curves produced by varying flux in the Hα band. I analyzed the morphology of such curves and comparing objects of different masses, ages, and disk types to deepen our understanding of how stellar and substellar objects in their earliest stages change over time.

This project was in collaboration with my research group in Astro341 at Amherst College, this specific concept being explored with my research partner Savio Olivera; I will only be presenting code and writing samples that are my own.

Tools: Jupyter/Python (pandas, numpy, matplotlib, photutils, astropy, scipy), Excel, Astrometry, SAOImageDS9

Primary skills: data cleaning, data pipeline creation, data visualization, data analysis, data management

### The Data

### Data Reduction

Images taken from telescopes need to be processed prior to analysis in order to calibrate and clean up intrinsic noise in the CCD.

sorting files: hard-coded sorting methods were used, as this is the simplest method to organize the data
<details>
  <summary>View Code</summary>
  
``` 
  
```

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

### Visualizations & Analysis

### Results



For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
