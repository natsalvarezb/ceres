# docker4ceres
We developed a wrapper for a modified implementation of CERES (Collection of Elemental Routines for Echelle Spectra, [Brahm et al 2017](https://ui.adsabs.harvard.edu/#abs/2017PASP..129c4002B/abstract)) using a DockerFile. This allows professional astronomers and students to reduce the spectra taken using FIDEOS (FIber Dual Echelle Optical Spectrograph, [Tala et al., 2014](https://ui.adsabs.harvard.edu/abs/2014SPIE.9147E..89T/abstract)). This is made possible thanks to the TUCAN-1 (Telescopio Universidad Católica - Universidad de Antioquia 1-metro) agreement.

This repository hosts the DockerFiles and instructions required to run CERES on a Docker container. The modified CERES version required for this Dockerization is found in the [ceresUdeA](https://github.com/TUCAN1/ceresUdeA) repository.


# Authors:
 
-  Dr. Germán Chaparro-Molano ([saint-germain](https://github.com/saint-germain)), Computational Physics and Astrophysics Group (FACom) Institute of Physics, University of Antioquia Medellin, Colombia.\
-  Natalia Alvarez-Baena ([nataliaalvarezb](https://github.com/nataliaalvarezb)), Institute of Physics, University of Antioquia Medellin, Colombia.\
-  Dr. Ricardo Carrera ([carrerajimenez](https://github.com/carrerajimenez)), INAF-Osservatorio Astronomico di Padova, vicolo dell'Osservatorio 5, 35122 Padova, Italy.


# About the code

This new version aims to fix the portability issues of installing locally the pipeline allowing students and researchers to use it without harming their computers. This version also allows to reduce spectra that is not linked to a source available in [SIMBAD](https://simbad.unistra.fr/simbad/) as is the case for sky spectra.

# Requirements

This version was tested for macOS with M1 chip and for Ubuntu

# Usage

1. Download the /ceres/ folder with the files ceres.DockerFile.ubuntu, ceres.DockerFile.mac and requirements.txt
2. Delete the .mac or .ubuntu from the DockerFile depending on your OS.
3. Open a terminal and once you are in the /ceres/ folder type

```
sudo docker build -t ceres -f ceres.Dockerfile .
```
  Make sure you include the final dot.

4. Verify that the DockerFile was installed using

```
sudo docker image list
```

5. Run the DockerFile typing

```
sudo docker run -p 8888:8888 ceres
```

6. Type this URL in your browser

```
http://127.0.0.1:8888/
```
7. Open a terminal in JupyterLab and type

```
/bin/bash
cd ceres
```
8. Install CERES with (takes about 15-30 min)

```
python install.py
```
9. Run the pipeline following the instructions on the README of the [original](https://github.com/rabrahm/ceres) CERES version or the [modified](https://github.com/TUCAN1/ceresUdeA) version.

# Installation notes:

- [Installing Docker on Ubuntu](https://www.simplilearn.com/tutorials/docker-tutorial/how-to-install-docker-on-ubuntu)
- To use your own fits files: Make a /fits/ folder within the /ceres/ folder and upload your .fits files here using the JupyterLab environment.
- To use the same container again:
```
sudo docker start (insert your container ID here)
```
- In case you want to start over with the installation, eliminate the container and image with:
```
sudo docker rm $(sudo docker ps -q -a)
sudo docker image rm $(sudo docker image list | grep ceres | awk '{print $3}')
```
- If theres and installation error and the container doesn't finish building:
```
sudo docker image rm $(sudo docker image list | grep none | awk '{print $3}')
```





