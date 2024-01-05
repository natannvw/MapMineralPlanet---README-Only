# MapMineralPlanet---README-Only
Automated algorithm for global mineral mapping with Spaceborne Hyperspectral Imaging Processing - README Only
This is only the README Demo for my private repo

# Abstract
In my master's research, I addressed an intriguing question in planetary science: how could ancient Mars maintain a climate warm enough to support liquid water? I focused on the sulfur cycle hypothesis, testing the presence and implications of sulfur-bearing minerals on the Martian surface using advanced Hyperspectral Imaging Processing (HSI).

**Key Achievements**:
1. **Data Acquisition and Management**:
Innovated a robust 'search engine' to systematically access and retrieve Mars' hyperspectral satellite imagery from NASA's archives, enabling a comprehensive analysis of the entire planet.
2. **Algorithm Development and Innovation**:
Pioneered the enhancement of hyperspectral imaging algorithms for sensitive and precise mineral detection. My work crucially resolved an algorithmic challenge persisting for over two decades in satellite hyperspectral imaging, significantly enhancing mineral exploration methodologies applicable to Mars and other planetary bodies (like Earth).
3. **Global Mineral Mapping and Analysis**:
Conducted an exhaustive application of the algorithms to map minerals globally across Mars. My approach was particularly focused on identifying spectral features of calcium sulfite, alongside existing and newly observed calcium sulfate minerals. This detailed mineral mapping was instrumental in testing and validating the sulfur cycle hypothesis, offering new perspectives on the planet's past environmental conditions.

*Note: Hyperspectral Imaging Processing (HSI) merges image and signal processing to analyze multidimensional data cubes, enriching our interpretation of planetary surfaces and atmospheres.*

Through this research, I not only contributed to our understanding of Mars but also advanced the field of hyperspectral imaging, demonstrating its potential in planetary science and beyond.

# MapMineralPlanet  

The following project was part of my MSc research in Planetary Science at the Weizmann Institute of Science.  
`MapMineralPlanet` is the first global automated algorithm for mineral exploration with NASA's data acquired by the Mars Reconnaissance Orbiter (MRO) Compact 
Reconnaissance Imaging Spectrometer for Mars (CRISM) instrument.
For more information, see https://pds-geosciences.wustl.edu/missions/mro/crism.htm.

- [MapMineralPlanet](#MapMineralPlanet)
      - [The Problem](#The-Problem)
      - [The Challenge](#The-Challenge)
      - [The Solution](#The-Solution)
      - [Significance and Applications](#Significance-and-Applications)
  - [Dependencies](#Dependencies)
  - [Spectral Library](#SpectralLibrary)
  - [Search and Download TERs or MTRDRs](#Search-and-Download-TERs-or-MTRDRs)
      - [Case - specific scene or scenes](#Case---specific-scene-or-scenes)
      - [Case - global exploration](#Case---global-exploration)
  - [Find the mineral](#Find-the-mineral)
      - [Case - specific scene or scenes](#Case---specific-scene-or-scenes)
      - [Case - global exploration](#Case---global-exploration)
  - [Analyze](#Analyze)
      - [Case - specific scene or scenes](#Case---specific-scene-or-scenes)
      - [Case - global exploration](#Case---global-exploration)
  - [Display](#Display)
  - [Classification](#Classification)


#### *The Problem*
To this day, NASA's scientists analyze each scene (satellite image) manually with **qualitative** assessments with Browse Products[^1]. Then, the spectral analysis was done with the Ratioing method to remove noise and artifacts and enhance the relevant spectral features. This method requires to use of a nearly neutral spectrum chosen **manually**  by the user from the same column of the **unprojected** image (e.g., Targeted Empirical Record (TER)), as the target (the numerator) spectrum was used as the denominator[^2][^3].  
[^2]: Murchie et al. (2007) Compact Reconnaissance Imaging Spectrometer for Mars (CRISM) on Mars Reconnaissance Orbiter (MRO) (https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2006JE002682)
[^3]: Ehlmann et al. (2009) Identification of hydrated silicate minerals on Mars using MRO-CRISM: Geologic context near Nili Fossae and implications for aqueous alteration (https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2009JE003339)

Each scene could take days and weeks to be analyzed by the described above manual methods. Moreover, it is impossible to analyze each pixel in each scene of a size of approximately 500x500, which is ~25,000 pixels (=spectra). Defining some mineral's pixels **required more than 50** connected pixels to be averaged.  

#### *The Challenge*
If one wants to map an entire planet, he should consider that there are thousands of scenes, meaning there are more than a billion spectra to be analyzed. 

#### *The Solution*
My state-of-the-art algorithm analyzes a single scene on its own **within a minute** and **covers the whole of the scene's pixels** with **higher accuracy of down to only a few pixels** to be averaged to define a mineral. So, it is a **quantitative fast acquisition of mineral targets**. And no less important, you can use either map **projected** data (i.e., Map-projected Targeted Reduced Data Record (MTRDR)).  

#### *Significance and Applications*
This algorithm could be used in other space scientific missions, such as ESA's Jupiter Icy Moons Explorer (JUICE).  
This tool can also be applicable in future space mineral exploration, either for asteroid mining or for "in-situ resource utilization", which is the use of resources found on other planets and moons replacing resources that would otherwise be brought from Earth.  
  
![processing](https://user-images.githubusercontent.com/69158504/220324547-db733319-2e2c-41ae-9c8b-e112c45343e8.svg)

## Dependencies
The code has been tested with MATLAB R2021a, R2022a on Windows 10 and Linux.  

**Toolboxes**:  
[Image Processing Toolbox](https://www.mathworks.com/products/image.html)   
[Image Processing Toolbox **Hyperspectral Imaging Library**](https://www.mathworks.com/matlabcentral/fileexchange/76796-image-processing-toolbox-hyperspectral-imaging-library)  
[Statistics and Machine Learning Toolbox](https://www.mathworks.com/products/statistics.html)  
[Signal Processing Toolbox](https://www.mathworks.com/products/signal.html)  
[Deep Learning Toolbox](https://www.mathworks.com/products/deep-learning.html)  
[Parallel Computing Toolbox](https://www.mathworks.com/products/parallel-computing.html)  
[Text Analytics Toolbox](https://www.mathworks.com/products/text-analytics.html)  
[Mapping Toolbox](https://www.mathworks.com/products/mapping.html)  
[MatlabProgressBar](https://github.com/JAAdrian/MatlabProgressBar)  
  

## Spectral Library
First, get a Spectral Library with your desired mineral lab reference as my Spectral Library of Sulfates in '/Spectral Libraries'. This library should be in an ASCII format and wavelength should be in Micrometers (μm) units, as shown in the example: 

```gas
Column 1: Wavelength  
Column 2: Bassanite GDS145  
Column 3: Gypsum LASF41A  
Column 4: Hannebachite BIR1LH058  
Column 5: Alunite F1CC08B  
Column 6: Jarosite LASF21A  
Column 7: Kieserite F1CC15  
Column 8: Magnesium Sulfate 799F366  

  0.909000  0.922418  0.943770  0.589400  0.869423  0.403791  0.855682  0.948961  
  0.909200  0.922402  0.943752  0.589570  0.869412  0.403738  0.855690  0.948869  
  0.909300  0.922393  0.943743  0.589670  0.869407  0.403711  0.855694  0.948822  
  0.909500  0.922376  0.943726  0.589520  0.869396  0.403659  0.855702  0.948730  
  0.909700  0.922359  0.943708  0.589810  0.869385  0.403606  0.855710  0.948637  
  0.909800  0.922350  0.943699  0.590340  0.869379  0.403579  0.855714  0.948591  
  0.910000  0.922333  0.943681  0.590400  0.869368  0.403526  0.855722  0.948498  
  0.910100  0.922322  0.943663  0.590160  0.869376  0.403544  0.855728  0.948511  
  0.910300  0.922295  0.943627  0.590010  0.869392  0.403581  0.855740  0.948538  
  ...  
```

## Search and Download TERs or MTRDRs  
#### Case - specific scene or scenes:
For this example, I choose the FRT00009326 scene
````ruby
product = 'frt00009326_07_if167j_mtr3' 
````

*For multiple scenes, chain products with a cell array

````ruby
MapMineralPlanet.search()
````  
#### Case - global exploration:

For global exploration, you will need to download the full relevant dataset. You should use a cluster or equivalent and use the **batch processing option**[^4].  

You should explicitly define a path (scenes_path = '...') to where to be downloaded and set the 'Products' option to 'All' (default). 
[^4]: https://www.mathworks.com/help/matlab/ref/matlabwindows.html  

Run from the command line (system prompt):
````ruby
matlab -batch "MapMineralPlanet.search_globally()"
````
  
## Find the mineral
#### Case - specific scene or scenes:
````ruby
MapMineralPlanet.detect()
````

#### Case - global exploration:
````ruby
speclib_path = fullfile('Spectral Libraries', 'Sulfates and Sulfite.txt')  % for example
matlab -batch "MapMineralPlanet.detect_globally(mineral = 'bassanite')"
````

**Tips:**  
- You will get 2 .mat files, full and good results in the following format: 'mineral_good|full_results_ddmmyyyy_hhmm.mat'. For example, bassanite_good_results_04082022_1818.mat  
**Use the 'good'.**
- Each scene would take around a minute, and there are ~6600 of them. Do the math how many workers do you need for parallel computing. I used 48 workers, and depending on the target mineral, it took between 14-48 hours.  
- The storage factor between TER and MTR (MTRDR) data is ~2, so consider download size and calculation time.  


## Analyze
For the visualization download scene's **TRU**e color RGB representation or any other type of Browse Products[^1]:

#### Case - specific scene or scenes:
````ruby
MapMineralPlanet.search() 
````
[^1]: Viviano et al. (2014)  Revised CRISM spectral parameters and summary products based on the currently detected mineral diversity on Mars (https://agupubs.onlinelibrary.wiley.com/doi/full/10.1002/2014JE004627)

Now, for the analysis of the good results with detected targets, create an analysis figure:  
````ruby
MapMineralPlanet.review()
````
Or for intercative target spectrum inspection (see more options in the Display section below):
````ruby
MapMineralPlanet.review(interactive = 'on')
````

Or if you wish not more manually:
````matlab
% score_thres = 1.5 raising the threshold for better browsing
````
````ruby
MapMineralPlanet.review(threshold = 1.5);

MapMineralPlanet.review(interactive = 'on');
````
And you can then also input manually the location as row, column.
Tip: use the Data Tip which is available through the axes toolbar to get location from some pixels (note: the 'Index' in the Data Tip in the score map is the pixel's score!):
<!-- ![data_tips](https://user-images.githubusercontent.com/69158504/206673743-5348033f-7ee6-4487-95de-8494fe842bcf.JPG | width=100) -->
<img src="https://user-images.githubusercontent.com/69158504/206673743-5348033f-7ee6-4487-95de-8494fe842bcf.JPG" width="200"/>

````ruby
MapMineralPlanet.trgt_spec(ROW, COLUMN);
````


A PDS Geosciences Node Mars Orbital Data Explorer (ODE) website of the product will be opened together with its figure with the targets to be analyze and reviewed by you:  

https://user-images.githubusercontent.com/69158504/183453409-9f093945-6fe0-4352-8e71-61dd0a620f61.mp4  


**Intercative target spectrum inspection:**

https://user-images.githubusercontent.com/69158504/206129530-af5cc200-b90f-40af-bf34-3b90454498a6.mp4

  
#### Case - global exploration:
````ruby
matlab -batch "MapMineralPlanet.search_globally()"
````

Now, for the analysis of the good results with detected targets, create an analysis figure:  
````ruby
matlab -batch "MapMineralPlanet.review_globally()"
````

## Display
Display the detected targets of the scene with its web page:
````ruby
MapMineralPlanet.disp_scene_fig_web()
````  

![fig](https://user-images.githubusercontent.com/69158504/183451500-a297a82b-d2c6-4d43-bc5a-0230119e18e5.svg)  

## Classification
````ruby
minerals = {'bassanite', ...
            'jarosite',  ...
            'serpentine', ...
            'Nontronite',  ...
            'Montmorillonite',  ...
            'chlorite',  ...
            'analcime',  ...
            'calcite',  ...
            'hematite',  ...
            'gypsum',  ...
            'kaolinite', ...
            'magnesite'};
                        
[maps, fig, libData, original] = MapMineralPlanet.classify(n_endmembers = 3, minerals = minerals);
````
Or if it is the second time you classify with a saved `maps` variable:
````ruby
[~,    fig, libData, original] = MapMineralPlanet.classify(n_endmembers = 3, minerals = minerals, maps = maps);
````

![Classification_1502](https://user-images.githubusercontent.com/69158504/220322685-55d03ba5-82db-42e5-bd5f-a961f7976b69.svg)

Then you can:
````ruby
fig_spec = MapMineralPlanet.spectralPicker(maps, libData = libData, fig = fig, n_refs = 5);
````

![fig_spec_C](https://user-images.githubusercontent.com/69158504/220322896-54eca7b3-7dd5-4f72-9026-62e0601e28cd.svg)
