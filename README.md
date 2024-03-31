# Hellinger_distances_for_MDF
This jupyter (.ipynb) notebook is written as a tool for automatic detection and quantification of mesostructure (including shear bands) based on the measurement of the Hellinger distances between random and actual misorientation distribution function (MDF) experimentally obtained by EBSD or X-ray microscopy. 

All the theoretical details can be found in the publication Oleg Bushuev, Elijah Borodin, Anna Morozova, Andrey Belyakov, Siying Zhu, Andrey P. Jivkov “Detection of mesostructure in severely deformed copper alloys” (2024).

The analysis performed in the notebook is based on the Python libraries of the Voronoi_PCC_Analyser code written by Dr Oleg Bushuev (University of Manchester, 2022-2023). The typical procedure of data analysis consists of a few steps:

(1) Based on the EBSD data, output two files containing 1) all grain orientations expressed in quaternions or Euler angles, and 2) barycentre coordinates of all grains. 

(2) Using the files with barycentre grain coordinates and grain orientations, create 2D tessellation corresponding (topologically equivalent) to the original EBSD map. Neper software (https://neper.info) provides an excellent tool for a Voronoi-like tessellations using terminal commands*: 

```
neper -T -n <number of grains> -dim 2 -domain "square(size1,size2)" -morphooptiini "coo:file(<grain barycentre coordinates>)" -transform "ori(<grain orientations>,des=euler-roe)" -oridescriptor euler-roe -statface size -statedge size -oricrysym cubic -ori uniform -o <name of the output file>
```

```
neper -V <name of the output file .tess> -imagesize <size_in_pixels_1:
size_in_pixels_2> -print <directory/name of the printed image>
```

See details on the Neper Documentation page https://neper.info/doc/neper_t.html#cmdoption-morphooptiini and https://neper.info/doc/neper_t.html#cmdoption-transform

(*For using them Neper must be first installed in the system. It is pretty straightforward for the Linux-based systems: https://neper.info/doc/introduction.html#installing-neper).

(3) Voronoi_PCC_Analyser code must be installed with all its dependencies and libraries. Again, for Linux based systems it can be done simply using**:

```
pip install PCCanalyser
```

**python3 and pip must be installed first, like: 
```
sudo apt update; sudo apt install python3
```

(4) Jupyter notebooks (.jpynb) can be opened in several ways. The most traditional one is to install Jupyter Lab (https://jupyter.org) or use it online. DataSpell (https://www.jetbrains.com/dataspell/) and Datalore (https://www.jetbrains.com/datalore/features/notebooks/) from Jet Brains with its free academic license (https://www.jetbrains.com/community/education/#students) can be highly recommended. 

All the rest details and descriptions are provided inside the Hellinger_distances_for_MDF.jpynb notebook. 

Please feel free e-mail to Dr Elijah Borodin any queries relating with the code.

Voronoi_PCC_Analyser code distributed under the GNU General Public License v3.0
Neper software distributed under the Apache License v2.0

This code has been created as a part of the EPSRC funded projects EP/V022687/1 “Patterns recognition inside shear bands: tailoring microstructure against localisation” (PRISB) and EP/N026136/1 "Geometric Mechanics of Solids: new analysis of modern engineering materials" (GEMS).

Hint:
For Windows-based system, Linux shell can be easily installed. See for details:
https://learn.microsoft.com/en-us/windows/wsl/install
then add new user&password, and do not forget 'sudo apt-get update'; 'sudo apt-get upgrade' the system and software. 
(!) A key step — Ensuring the WSL feature is turned on for your system:
1. Find 'Windows Features' in the Windows Start menu Search;
2. Turn Windows Features ON or OFF;
3. Validate “Windows Subsystem for Linux” is checked;
4. Enabling the feature may require a restart. 

For Mac OS Neper installation is pretty challenging, while possible. Virtual machines, such as Parallels Desktop (https://www.parallels.com/products/desktop/), can be effectively used for Ubuntu Linux installation. 
