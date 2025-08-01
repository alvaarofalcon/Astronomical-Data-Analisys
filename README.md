# Astronomical-Data-Analysis
Portfolio of data analysis applied to astronomical images.

Hello! It's Alvaro. Here is my repository of data analysis applied to astronomical images. The objective is to show how I managed, processed, analysed and visualised the data of images in order to extract significant information to achieve the goal of studying astronomy and astrophysics of the celestial objects of interest.

The astronomical images basically are matrices of raw data that contain noise, instrumental signal and the information that we are seeking. Here, I'll show the workflow of my work on the image analysis: from the cleaning and calibration to the statistical modelling and the visualization of the results. 

### Main libraries

Through these projects I used the following libraries and tools oriented to data analysis and scientific computation:

* **Process and data analysis:** `NumPy`, `Pandas`
* **Data visualization:** `Matplotlib`
* **Analysis of images and astronomical data:** `Astropy`, `CCDProc`, `Photutils`
* **Symbolic compute:** `SymPy`


## Projects

Here I'll detail the procedure carried out in any project:

### 1. The calibration: The "data cleaning" in astronomy
* **File:** `MasterFlat.ipynb`
* **Objective:** This is the fundamental cleaning of the data contained in images. Before the analysis, it's crucial to clean the systematic noise and the 'signature' of the instrument. This process is analog to any other process of the cleaning and pre-processing of the data, and one has to do this with each image taken from a telescope.
* **The process:**
    1.  **Noise reduction (BIAS/Dark):** I combined multiple images of `BIAS` and `dark frames` in order to create a "master dark", that has the thermal and the sensor noise of the entire instrument.
    2.  **Sensitivity correction (Flat-Fielding):** This is the subtraction of the "master dark" from the `flat-field` images. Then, these images are normalized and combined in order to create a "master flat", which corrects the variations of sensitivity pixel to pixel.
    3.  **Result:** Clean and calibrated images, ready to be scientifically analysed.
* **Libraries:** `Astropy`, `CCDProc`, `NumPy`.

### 2. Analysis of aperture photometry of a binary variable
* **File:** `BinaryVariable.ipynb`
* **Objective:** Determine the optimal aperture size in order to measure the flux of a star, minimizing the relative error. This is a classic problem of parameter optimization.
* **Process:**
    1.  **Metrics extraction:** I measured the flux of a star and its associated error for different aperture sizes.
    2.  **Error analysis:** I calculated a performance metric (the inverse of the relative error of the flux) in order to find the point in which the signal is maximal and the noise minimal.
    3.  **Visualization and optimization:** It was plotted the metrics versus the aperture size, identifying visually the optimal radius of aperture.
* **Libraries:** `NumPy`, `Matplotlib`.

### 3. Calculation of the Atmospheric Extinction Coefficient
* **File:** `ExtinctionC.ipynb`
* **Objective:** Quantify how the earth atmosphere attenuates the light coming from the cosmos. This analysis uses a model of linear regression in order to determine a physical parameter from the observational data.
* **Process:**
    1.  **Data extraction from the images:** It was used **SExtractor** (an external tool called from Python) in order to perform automated photometry on a series of images of standard stars taken for different heights with respect to the horizon.
    2.  **Data storage:** The instrumental magnitude, together with the air mass (a measure of the atmosphere thickness) and the catalog magnitudes, were stored in a Pandas `DataFrame`.
    3.  **Linear regression:** A linear model was fitted (`np.polyfit`) between the corrected magnitude and the air mass. The slope of this linear function is the extinction coefficient.
    4.  **Results:** The coefficients for the bands B (0.45 ± 0.03) and V (0.30 ± 0.02) were calculated, with a correlation coefficient (R²) higher than 0.98, showing an excellent fit.
* **Libraries:** `Pandas`, `NumPy`, `Matplotlib`, `Astropy`, `Subprocess`.

### 4. Analysis of a Luminosity Profile of an Elliptical Galaxy
* **File:** `EllipticalGalaxy.ipynb`
* **Objective:** Analyze the distribution of light of the galaxy NGC 4472 to verify if it follows the de Vaucouleurs law, valid for elliptical galaxies.
* **Process:**
    1.  **Processing of images:** I stacked many images in order to amplify the signal/noise relation.
    2.  **Isophotes fit:** I used `photutils` in order to fit a series of concentric ellipses (isophotes) to the galaxy profile, extracting parameters like intensity, ellipticity and angular position.
    3.  **Data transform and modelling:** It was calculated the surface brightness (µ) and it was plotted against the semimajor-axis (r^(1/4)) in order to verify if the linear relation was valid as the de Vaucouleurs law predicts.
    4.  **Calculation of Physical parameters:** From the parameters obtained from the linear regression, I calculated the effective radius and the effective surface brightness.
* **Libraries:** `Photutils`, `Astropy`, `CCDProc`, `NumPy`, `Matplotlib`.

### 5. Creation of a Color-Magnitude diagram.
* **File:** `ColorMagnitude.ipynb`
* **Objective:** Build an H-R diagram (a fundamental graph in Astrophysics) for a cluster of stars, which allows us to identify its principal sequence and its evolutionary stage.
* **Process:**
    1.  **Alignment and combination:** The images taken with two different filters (band B and V) were aligned (with linear transformations carried out by Astroalign) and combined in order to improve the quality.
    2.  **(Data Joining):** The stars were extracted from both final combined images. Then, a "join" of the two catalogues was made, associating each star of the image B with its correspondent at V based on its coordinates.
    3.  **Calibration and Feature Engineering:** The instrumental magnitudes were calibrated using a reference star with a well-known brightness. A color index (B-V) was created.
    4.  **Visualization:** The final result is a dispersion diagram which shows the absolute magnitude against the color index, showing the structure of the cluster.
* **Libraries** `Astroalign`, `CCDProc`, `Pandas`, `Astropy`, `NumPy`, `Matplotlib`.

### 6. Determination of an Asteroid's Orbit
* **File:** `asteroide.ipynb`
* **Objective:** Calculate the trajectory and the orbital parameters of an asteroid from a series of images taken over time (i.e. observing the movement of the asteroid in the sky).
* **Process:**
    1.  **Temporal Series Analysis:** The coordinates (X, Y) of the asteroid and two reference stars were extracted from 41 images, creating a dataset of temporal series of position.
    2.  **Coordinate transformation:** The transformation from pixel coordinates (X, Y) to celestial coordinates was carried out using the equations well known from the astronomy.
    3.  **Motion modeling:** A linear regression was carried out on the celestial coordinates as a function of time in order to determine the asteroid's angular velocity in both directions (µ_α and µ_δ).
    4.  **Resolution of the System of equations:** Using `SymPy`, it was solved a system of non-linear equations based on the orbital mechanics in order to determine the distance and the radial velocity of the asteroid. Finally, parameters like orbital inclination and the longitude of the ascending node were calculated.
* **Libraries:** `SymPy`, `Pandas`, `NumPy`, `Matplotlib`, `Astropy`.
