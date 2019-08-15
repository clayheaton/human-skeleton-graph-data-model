# Skeleton-Graph

This repository contains a graph model of the human skeleton, mapping 206 bones of the skeleton to the body regions to which they belong and, where appropriate, to each other with "proximal" and "distal" connections. Where proximal and distal are not appropriate descriptors, nearby or connecting bones are considered "adjacent."

The data was entered by me (Clay Heaton) into [Airtable](https://airtable.com) and exported into [NetworkX](https://networkx.github.io/documentation/stable/index.html) via the Airtable API. The Airtable base was exported into `bones.csv` and `regions.csv`, included here. You can view the original data in Airtable (and clone it into a 'base' of your own) by [visiting this link](https://airtable.com/shr2jsqWd6vE9zdiv).

There are three types of nodes:

- `bone`: These represent the 206 bones in the skeleton. The numbering of the bone nodes begins at `1`.
- `region`: These represent body parts containing the bones, such as `Left Arm` or `Ribcage`. The numbering of the `region` nodes begins at `1001`.
- `super_region`: These represent more abstract regions. For instance, the `super_region` called `Head` is adjacent to the regions `Skull` and `Face`. The `super_region` called `Arm` is adjacent to the regions `Right Arm` and `Left Arm`. Whereas the `region` called `Right Arm` should only have edges connecting to the bones of the right arm, the `super_region` called `Arm` should have edges connecting to all of the bones in both the right and left arms. The numbering of `region` and `super_region` nodes begins at `2001`.

There are several types of edges:

- `bone` is an `edge_type` going from a `region` or `super_region` node to a bone node.
- `region` is an `edge_type` going from a `bone` to a `region` or `super_region`

The purpose of creating this repository was to support the creation of a dynamic bone injury model for working with procedural content generators. 

If you are interested in creating a variant of the graph or fixing errors with the data contained herein, please consider making a pull request. I'm happy to merge in fixes or variations to the graph. Let me know if you use the data - I'm interested to see where it goes.

The data in this repository is not intended to be used for medical purposes and may contain anatomical inaccuracies.

This repository and the data it contains are in the public domain.