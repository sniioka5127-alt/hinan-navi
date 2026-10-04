# Hazard Architecture

## Purpose

Hazard information is integrated as context for evacuation and preparedness.

## Architectural principles

- keep hazard families separable
- load only the hazard data needed for the current context where practical
- keep initial state conservative
- avoid silently treating missing hazard data as “safe”
- preserve provenance for generated hazard packs

## Hazard families

The project architecture has been designed to accommodate multiple official hazard families, including examples such as:

- flood
- inland flooding
- landslide
- tsunami
- storm surge
- volcanic hazards

Availability varies by dataset and release.

## Rendering

Hazard rendering is a visualization aid.

A rendered polygon is not, by itself, a guarantee of current conditions or personal safety.

Official warnings and actual local conditions take precedence.
