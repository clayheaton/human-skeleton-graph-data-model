# Skeleton-Graph

2021-10-06 Update: The original files were moved into the `old` subdirectory. While the CSV should be correct, the `directed_node_link_graph.json` file appeared to export from NetworkX with some errors. I recently recalculated and exported this into `skeleton.json`, but have yet to have time to test it properly. As a hobby project, please do not use this for scientific or medical purposes and be aware that the data and/or code may contain mistakes. I was sitting in my in-laws living room, trying to pay attention to a webinar while assembling the data.

Any updates, bug reports, improvements, etc. are welcome! Feel free to contact me here or @clayheaton on Twitter with any questions. 

🎃


Nodes in `skeleton.json` should all be in this format:

```
{
    "key": "kHand_MetacarpalBone04Right",
    "id_number": 115,
    "bone_name": "Metacarpal 4",
    "side": "right",
    "position": "",
    "readable_name": "Right Metacarpal 4 Bone",
    "alternate_name": ""
}
```

Edges should all be in this format:

```
{
    "edge_type": "adjacent_to",
    "source": "kRegion_ArmLeft",
    "dest": "kRegion_Hand"
}
```

The `Transform.ipynb` file is a recent re-attempt to properly export the data to JSON.

The edge types are converted from the original values using this lookup:

```
edge_keys = {
    'proximal_bones':   'distal_to',
    'adjacent_bones':   'adjacent_to',
    'distal_bones':     'proximal_to',
    'body_regions':     'part_of',
    'adjacent_regions': 'adjacent_to',
    'human_skeleton':   'includes'
}
```

If you make something with the data, let me know! I'd love to see it.

Here are some things I would like to do with this data if I get time:

- Average size & weight of each bone
- General shape of each bone (if that's a thing) for visualization purposes
- Joint types
- Some type of model for pulling bones in the same region together in a sensible manner (this skull/face, for example)

LICENSE: This repository and the data it contains are in the public domain.

----

Everything below here is old information:

This repository contains a graph model of the human skeleton, mapping 206 bones of the skeleton to the body regions to which they belong and, where appropriate, to each other with "proximal" and "distal" connections. Where proximal and distal are not appropriate descriptors, nearby or connecting bones are considered "adjacent."

The data was entered by me (Clay Heaton) into [Airtable](https://airtable.com) and exported into [NetworkX](https://networkx.github.io/documentation/stable/index.html) via the Airtable API. The Airtable base was exported into `airtable_bones.csv` and `airtable_regions.csv`, included here. You can view the original data in Airtable (and clone it into a 'base' of your own) by [visiting this link](https://airtable.com/shr2jsqWd6vE9zdiv). 

The file `directed_node_link_graph.json` contains a JSON representation of the graph in the format [used by this D3 example, by Mike Bostock](https://observablehq.com/@d3/force-directed-graph). The NetworkX documentation for importing and exporting this JSON format can be found [on this page](https://networkx.github.io/documentation/stable/reference/readwrite/json_graph.html).

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