# Astronomical-Data-Analisys
Portfolio of data analisys applied to astronomical images.

Hello! It's Alvaro. Here is my repository of data analisys applied to astronomical images. The objective is to show how I managed, processed, analysed and visualised the data of images in order to extract significant information to achieve the goal of study the astronomy and the astrophysics of the celestial objects of interest.

The astronomical images basically are matrices of raw data that contain noise, instrumental signal and the information that we are seeken. Here, I'll show the flux of my work on the image's analisys: from the clean and calibration to the statistical modelling and the visualization of the results. 

### Main libraries

Through this projects I used the next libraries and tools oriented to data analisys and scientific computation:

* **Process and data analisys:** `NumPy`, `Pandas`
* **Data visualization:** `Matplotlib`
* **Analisys of images and astronomical data:** `Astropy`, `CCDProc`, `Photutils`
* **Symbolic compute:** `SymPy`


## Projects

Here I'll detail the procedure carried out in any project:

### 1. The calibration: The "data cleaning" in astronomy
* **File:** `MasterFlat.ipynb`
* **Objetcive:** This is the fundamental cleaning of the data contained in images. Before the analisys, its crucial clean the sistematic noise and the 'firm' of the instrument. This process is analog to any other process of the cleaning and pre processing of the data, and one has to do this with each image taked from a telescope.
* **The process:**
    1.  **Noise reduction (BIAS/Dark):** I combined multiple images of `BIAS` y `dark frames` in order to create a "master dark", that has the thermal and the sensor noise of the entire instrument.
    2.  **Sensibility correction (Flat-Fielding):** This is the substraction of the "master dark" from the `flat-field` images. Then, this images are normalized and combined in order to create a "master flat", which correct the variations of sensibility pixel to pixel.
    3.  **Result:** Clean and calibrated images, ready to be scientificly analysed.
* **Libraries:** `Astropy`, `CCDProc`, `NumPy`.

### 2. Analisys of aperture photometry of a binary variable
* **File:** `BinaryVariable.ipynb`
* **Objective:** Determine the optimal aperture size in order to measure the flux of a star, minimizing the relative rror. This is a classic problem of parameters optimization.
* **Process:**
    1.  **Metrics extraction:** I measured the flux of a star and its asociated error for different aperture sizess.
    2.  **Análisis de Error:** I calculated a perfofmance metric (the inverse of the relative error of the flux) in order to found the point in which the signal is maximal and the noise minimal.
    3.  **Visualization and optimization:** It was plotted the metrics versus the aperture siza, identifyng visually the optimal radius of aperture.
* **Libraries:** `NumPy`, `Matplotlib`.

### 3. Calculation of the Atmospheric Exctintion Coefficient
* **File:** `ExtintionC.ipynb`
* **Objective:** Cuantify how the earth atmosphere attenuates the light coming from the cosmos. This analisys uses a model of linear regrssion in order to determine a physical parameter from the observational data.
* **Proceso de Análisis:**
    1.  **Extracción de Datos de Imágenes:** It was used **SExtractor** (an external tool called from Python) in order to perform automatised photometry on a series of images of standar stas taken for different heights with respect to the horizon.
    2.  **Data storage:** The instrumental magnitud, together with de mass air (a measure of the atmosphere thickness) and the catalog magnitudes, were stored in a Pandas `DataFrame`.
    3.  **Linear regression:** A linear model was fitted (`np.polyfit`) between the corrected magnitude and the air mass. The slope of this linear function is the extinction coefficient.
    4.  **Resultados:** The coefficients for the bands B (0.45 ± 0.03) and V (0.30 ± 0.02) were calculated, with a correlation coefficient (R²) superior to 0.98, showing an excellent fit.
* **Libraries:** `Pandas`, `NumPy`, `Matplotlib`, `Astropy`, `Subprocess`.

### 4. Analisys of a Luminosity Profile of an Elliptical Galaxy
* **Archivo:** `EllipticalGalaxy.ipynb`
* **Objective:** Analyze the distribution of light of the galaxy NGC 4472 to verify if it follows the De Vacouleurs law, valid for elliptical galaxies.
* **Process:**
    1.  **Processing of images:** I stacked many images in order to amplify the signal/noise relation.
    2.  **Isophotes fit:** I used `photutils` in order to fit a series of concentric ellipses (isphotes) to the galaxy profile, extracting parameters like intensity, ellipticity and angular position.
    3.  **Data transform and modelling:** It was calculated the superficial brillance (µ) and it was plotted against the semimajor-axis  (r^(1/4)) in order to verify if the linear relation was valid as the De Vaucouleurs law predicts.
    4.  **Calculation of Physical parameters:** From the parameters obtained from the linear regression, I calculated the effective radius and the effective superficial brillance.
* **Libraries:** `Photutils`, `Astropy`, `CCDProc`, `NumPy`, `Matplotlib`.

### 5. Creation of a ColorMagnitude diagram.
* **File:** `ColorMagnitude.ipynb`
* **Objetive:** Build an H-R diagram (a fundamental graph in Astrophysics) for a cluster of stars, which allows identify it's principal sequence and it's evolutive stage.
* **Process:**
    1.  **Alignment and combination:** The images taken with two differents filters (band B and V) were alligned (with linear transformations carried out by Astroaling) and combined in order to improve the quality.
    2.  **(Data Joining):** The stars were extracted from both final combined images. Then, a "join" of the two catalogues was made, asocciating each star of the image B with it correspondent at V based in it's coordinates.
    3.  **Calibration and Feature Engineering:** The instrumental magnitudes were calibrated using a reference star with a well known bright. A color index (B-V) was created.
    4.  **Visualization:** The final result is a dispersion diagram which shows the absolute magnitude against the color index, showing the structure of the cluster.
* **Libraries** `Astroalign`, `CCDProc`, `Pandas`, `Astropy`, `NumPy`, `Matplotlib`.

### 6. Determination of an Asteroid's Orbit
* **File:** `asteroide.ipynb`
* **Objective:** Calculate the trajectorie and the orbital parameters of an asteroid from a series of images taken through the time (i.e. observing the movement of the asteorid in the sky).
* **Process:**
    1.  **Temporal Series Analisys:** The coordinates (X, Y) of the asteroid and two reference stars were extracted from 41 images, creating a dataset of temporal series of position.
    2.  **Coordinates transformation:** The transformation from pixel coordinates (X, Y) to celestial coordinates was carried out using the ecuations well known from the astronomy.
    3.  **Motion modeling:** A linear regression was carried out on the celestial coordinates in function of the time in order to determine the asteroid's angular velocity in both directions (µ_α y µ_δ).
    4.  **Resolution of the System of equations:** Using `SymPy`, it was solved a system of non-linear equations based on the orbital mechanics in order to determine the distance and the radial velocity of the asteroid. Finally, parameters like orbit's inclination and the longitude of the ascending node were calculated.
* **Libraries:** `SymPy`, `Pandas`, `NumPy`, `Matplotlib`, `Astropy`.
