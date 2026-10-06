# Technical Overview

## ECHO Forest Scatter v0.1

ECHO Forest Scatter is a procedural environment-art system developed in Blender 5.2.2 LTS. It separates the workflow into two complementary layers: procedural asset generation through **TreeBase** and terrain-scale placement through **ECHO Forest Scatter**.

## 1. TreeBase

TreeBase is the procedural vegetation foundation of the project and predates the forest-scatter layer.

The workflow begins with an artist-authored Bézier trunk. Geometry Nodes then builds the supporting procedural structure around that authored primary form. The system was developed modularly so that branch generation could be reused across successive hierarchy levels instead of constructing each order as an unrelated graph.

The implemented system includes procedural branch hierarchies, forks, roots and foliage. Foliage remains instanced, allowing the generated vegetation to retain procedural editability without unnecessarily realizing large numbers of leaf meshes.

TreeBase established the source assets used by the later forest-scattering workflow.

## 2. Forest source collection

ECHO Forest Scatter receives a Blender Collection as its asset source. Individual points are assigned deterministic source variants, allowing multiple tree forms and additional environment assets to participate in the same placement workflow.

The presentation scene intentionally includes both TreeBase-derived vegetation and a rock source. This demonstrates that the collection-driven scatter is not restricted to a single tree mesh or asset category.

The selected variant is retained as procedural metadata through the `echo_tree_variant` point attribute.

## 3. Distribution and art direction

Candidate placement is generated across the terrain and controlled through a compact modifier interface.

Artist-facing controls currently cover:

- Seed
- Tree Collection
- Density
- Density Mask
- Minimum Spacing
- Ground Embed
- Terrain Alignment
- Max Slope
- Scale Variation
- Use Boundary
- Boundary Object

Density can be art-directed using the named attribute `ECHO_Forest_Density`, enabling painted spatial control instead of relying exclusively on uniform procedural distribution.

Slope filtering constrains placement according to the terrain surface, while terrain alignment allows assets to respond to the underlying normal. Ground Embed provides a small placement offset for visual integration with the terrain.

## 4. Optional boundary

An optional boundary object can restrict the region in which forest placement is allowed. The boundary remains an editable scene control and can be disabled when unrestricted terrain distribution is more appropriate for the desired composition.

This control is particularly useful as an art-direction layer rather than as a requirement of the scatter algorithm.

## 5. Variation

Variation is deterministic from the exposed Seed. The system combines source-asset selection with random orientation and uniform scale variation to reduce visible repetition while preserving reproducibility.

## 6. Instancing and editability

The final forest is produced through instancing. The scatter system does not require realizing every tree or forest asset into unique mesh geometry, preserving a lighter and more editable procedural workflow.

Source assets can therefore remain independently editable while the environment is regenerated from the Geometry Nodes modifier.

## 7. Current scope

Version 0.1 focuses on the production-ready core of the procedural workflow: TreeBase asset generation, collection-driven scattering, density art direction, terrain response, variation and optional boundaries.

Exact variable-radius pairwise collision resolution is intentionally not presented as a feature of this version. A separate spatial-solver architecture is being considered for future development so that advanced placement constraints do not compromise the reliability or clarity of the Geometry Nodes scatter layer.

## Presentation documentation

Additional images will document:

- the final environment;
- the TreeBase Geometry Nodes system;
- the ECHO Forest Scatter node graph;
- painted density control;
- boundary control;
- the artist-facing modifier interface.
