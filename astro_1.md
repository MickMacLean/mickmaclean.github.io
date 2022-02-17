## Optical Astronomy Research

**An investigation into photometric emissions of low-mass stellar objects via observational data from the WIYN 0.9m optical telescope in Kitt Peak, AZ.**

In collaboration with the Astro341 research group at Amherst College, I was invloved in research in which we took photometric images in several wavelengths to provide us with data to study light curves produced by flux variations in Very Low-Mass Objects (VLMO). I analyzed the morphology of such curves and compared objects of different masses, ages, and disk types to deepen our understanding of how stellar and substellar objects in their earliest stages change over time.

The invesigation of this particular topic was explored with my research partner Savio Olivera; I will only be presenting code and writing samples that are my own.

**Tools:** Jupyter/Python (pandas, numpy, matplotlib, photutils, astropy, scipy), Excel, Astrometry, SAOImageDS9 

**Primary skills:** research, data cleaning, data pipeline development, data visualization, data analysis, data management


### Scientific Overview for a Non-Scientific Audience
If you have no experience in astronomy, here's the basics of what you need to know about the scientific premis of this project.

Clouds of gas and dust collapse under the gravitational pull of a newly formed stellar object; debris collects and begins to orbit the object as it falls to the surface. Instead of falling directly onto the star, this collected matter flattens and forms a disk around the object in order to preserve angular momentum; this is an accretion disk, and many young objects host them until they dissipate around 3Myrs of formation.

Ha wavelength is an indicator of stellar activity: chomospheric activity, flares, etc. changes in Ha flux directly indicate changes in activity. We can measure this by the flux or brightness of objects over time.

In order to make sure an object is only increasing its flux in Ha and not simply becoming brighter in all wavelengths, we need another nearby wavelength to compare: Ha off.

When we take images of space, we must process the raw data prior to analysis. We also superimpose the processed images on top of each other to create a deeper image of our region, allowing us to see deeper into space and view fainter objects more accurately; hundreds of images will result in only a few data points, at least for our investigation into flux changes.


### The Data
The data taken utilized the WIYN 0.9m telescope on Kitt Peak National Observatory with the Half-Degree Imager (HDI), and spans 8 nights from January 19-26, 2020; only 6 nights of data were used due to weather conditions. The regions of space I have analyzed are the Taurus V410 field and the Praesepe cluster, the former, a young star forming region of 1-3Myrs old, and the latter, a cluster of about 600-800Myr old.

These data were taken in the Hα wavelength (665nm) and Hα continuum narrowband (666nm), and calibration data (bias frames) were taken for each night; every image also contains overscan data, which is a bias adjustment tool for every single image. Our observing run for these regions resulted in over 300 raw files total, expanding to over 1300 files after reduction. 

External data is also taken from the VisieR database in order to identify the known traits of these objects, including coordinates, known magnitudes, and disk types. 

<p float="left">
  <img src="images/Praesepe1.png" width=400 />
  <img src="images/Screenshot (64).png" width=398 />
</p>
Fig 1. Final reduced images of Praesepe (left) and Taurus (right) in Hα.

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
  
```
  
</details>

<details> 
   <summary>View Function Module</summary>
 
``` 
  
```

</details>

### Analysis


Photometry function uses coordinates of our target objects, 

<details>
  <summary>View Photometry Function</summary>
  
```  

```

</details>

### Results

#### Final Data Spread
I successfully extracted relative flux data for 14 objects in Taurus and 19 in Praesepe ranging from M1.2 to K6, which is approximately 0.08SM (solar masses) to 0.75SM (Fig.2 Below):
<img src="images/dataspread.png" width=300>

#### Mass (Spectral Type) & Age Affect on Activity
<img src="images/final_comare.png" width=600>
The maximum change in flux over for each night of each object is plotted based on their spectral type. Lower mass objects display higher variable activity on average, having a higher total range of change in flux.

Younger objects, those in Taurus, display more activity than older objects in Praesepe. Objects >3Myrs of age have completed their accretion process and are stablized, thus their primary activity will be flares.
#### Capturing Flare Activity

<p float="left">
  <img src="images/solarflareHa.png" width=485 />
  <img src="images/solarflare.png" width=450 />
</p>

#### Mass (Spectral Type) vs. Disk Type
<img src="images/disk_final.png" width=400>

For objects in Taurus, I plotted objects from least (no disk) to most (full disk) amount of debris surrounding and subsequently falling onto the surface of the object (external data from Visier).
A more complete disk leads to more accretion and thus more activity, as the range of activity is highest for objects likely to be actively accreting. Accretion is a sporadic process, and thus a range of flux changes is expected.


For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
