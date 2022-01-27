# CALSAGOS

CALSAGOS (Clustering ALgorithmS Applied to Galaxies in Overdense Systems) is a python package developed to select cluster members and to search, find and identify substructures and galaxy groups in  and around galaxy clusters using the redshift and position in the sky of the galaxies. CALSAGOS can determine the cluster members in two ways. One by using ISOMER (Identifier of SpectrOscopic MembERs) which is a function developed to select the spectroscopic cluster members defining cluster members as those galaxies with a peculiar velocity lower than the escape velocity of the cluster. On the other hand, CALSAGOS can select the cluster members by using CLUMBERI (CLUster MemBER Identifier) which is a function developed to selectthe cluster members using a 3D-Gaussian Mixture Modules (GMM). Bothfunctions remove the field interlopers by using a 3-sigma clipping algorithm.

In order to search, find and identify substructures and groups in and around a galaxy cluster CALSAGOS uses LAGASU (LAbeller of GAlaxies within SUbstructures) which is a function that allows to assign the galaxies in a cluster to different substructures and groups in and around the galaxy cluster. LAGASU is based on clustering algorithms (GMM and DBSCAN) which search areas with high density to define a substructure or groups

## Install

```
pip install calsagos
```

## Example Usage

```py
from calsagos import lagasu
from calsagos import utils
from calsagos import clumberi


#-- select cluster members
cluster_members = clumberi.clumberi(id_galaxy, ra_galaxy, dec_galaxy, redshift_galaxy, cluster_initial_redshift, ra_cluster, dec_cluster, range_cuts)

# -- defining output parameters from clumberi
id_member = cluster_members[0]
ra_member = cluster_members[1]
dec_member = cluster_members[2]
redshift_member = cluster_members[3]

#-- estimating the galaxy separation of galaxies in the cluster sample to be used as input in lagasu
knn_distance = utils.calc_knn_galaxy_distance(ra_member, dec_member, n_galaxies)

#-- determining the distance to the k-nearest neighbor of each galaxy in the cluster
knn_galaxy_distance = knn_distance[0]

typical_separation = utils.best_eps_dbscan(id_member, knn_galaxy_distance)

#-- Assign galaxies to each substructures
label_candidates = lagasu.lagasu(id_member, ra_member, dec_member, redshift_member, range_cuts, typical_separation, n_galaxies)

#-- defining output parameters from lagasu
id_candidates = label_candidates[0]
ra_candidates = label_candidates[1]
dec_candidates = label_candidates[2]
redshift_candidates = label_candidates[3]
label_zcut = label_candidates[4]
label_final = label_candidates[5]    

# all done

```

Which makes:

A catalogue with cluster members and substructure identification

![alt tag](https://drive.google.com/file/d/1cRYxVQoFIg-sg756C1_pNOi7TfNLQzzT/view?usp=sharing) # CAMBIAR 

## API

Full CALSAGOS documentation can be viewed online in [html](http://www.baryons.org/ezgal/manual/) and [pdf](http://www.baryons.org/ezgal/manual.pdf) formats. # CAMBIAR

If your scientific publication is based on either version of CALSAGOS, then please cite Olave-Rojas et al. 2022

## Testing

```
python test.py
```

## Contributors

[Daniela Olave-Rojas](https://github.com/dolaver/) and Pierlugi Cerulo

## Acknowledgements

We gratefully acknowledge the collaborators of this project for giving us permission to use the data to test this package and for providing us important observations about the work. We especially thank Claudia Mendes de Oliveira and Pablo Araya-Araya for give us access to the mock catalogues from the Southern Photometric Local Universe Survey (S- PLUS; Mendes de Oliveira et al. 2019) and to David Olave-Rojas for help us to develop this package. We are also grateful to Ricardo Demarco, Yara Jaffé and Diego Pallero for their input on this project. Finally, we want to thank everyone who has tested CALSAGOS extensively and provided us with invaluable feedback.


## License

MIT 