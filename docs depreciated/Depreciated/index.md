---
title: Circular Future Cities Ontology
---

# CFC Ontology Documentation

This document provides an overview of the **CFC Ontology**—a city‐scale material passport ontology designed to support circular economy principles in the built environment. It describes the ontology’s purpose, namespace prefixes, imports, class and property hierarchies, alignment with existing vocabularies (OntoCityGML, BOT, DIC, CEO, CAMO, etc.), and usage examples. This documentation can be published alongside the ontology at `https://w3id.org/cfc`.

---

## Table of Contents

- [CFC Ontology Documentation](#cfc-ontology-documentation)
  - [Table of Contents](#table-of-contents)
  - [1. Introduction](#1-introduction)
  - [2. Namespace Prefixes](#2-namespace-prefixes)
  - [3. Ontology Imports](#3-ontology-imports)
  - [4. High‐Level Structure](#4-highlevel-structure)
    - [City and Sector](#city-and-sector)
    - [Buildings and Components](#buildings-and-components)
    - [Materials and Material Resources](#materials-and-material-resources)
    - [Lifecycle Events](#lifecycle-events)
    - [Agent Roles](#agent-roles)
    - [Circular Exchange (CEO) Concepts](#circular-exchange-ceo-concepts)
    - [Circular Asset Management (CAMO) Concepts](#circular-asset-management-camo-concepts)
  - [5. Object Properties](#5-object-properties)
  - [6. Data Properties](#6-data-properties)
  - [7. Alignment with OntoCityGML and BOT](#7-alignment-with-ontocitygml-and-bot)
  - [8. Usage Examples](#8-usage-examples)
    - [8.1 Defining a City and Sector](#81-defining-a-city-and-sector)
    - [8.2 Creating a Building with Components](#82-creating-a-building-with-components)
    - [8.3 Recording a Demolition Event and Material Recovery](#83-recording-a-demolition-event-and-material-recovery)
    - [8.4 Issuing Asset Work Orders (CAMO)](#84-issuing-asset-work-orders-camo)
    - [8.5 Geometry Attachments via OMG](#85-geometry-attachments-via-omg)
  - [9. Versioning and Publication](#9-versioning-and-publication)
    - [Publishing Steps](#publishing-steps)

---

## 1. Introduction

The **CFC Ontology** (Circular Future Cities Material Passport Ontology) is an OWL ontology that integrates:

* **City‐scale topology** (using OntoCityGML and BOT)
* **Building, component, and material definitions** (aligning with DIC Building Materials, BPO)
* **Lifecycle events** (construction, renovation, maintenance, design, demolition)
* **Stakeholder and agent roles** (aligning with DIC Agents)
* **Circular economy exchange** (using CEO: Circular Exchange Ontology)
* **Asset management** (using CAMO: Circular Asset Management Ontology)
* **Geometry support** (using OMG: Ontology for Managing Geometry)
* **Property evolution and provenance** (using OPM, PROV)

Its purpose is to model material‐passport data at multiple levels—from city sectors down to individual components—so that queries can traverse from topological zones (city/sector/building) through to material resources and stakeholder actions. By importing and aligning existing ontologies, CFC remains modular, extensible, and interoperable with other Linked‐Data ecosystems.

> **Published Context**: This ontology was published as part of the **Future Cities Laboratory’s Circular Future Cities** project, under the Singapore-ETH Centre collaboration.

---

## 2. Namespace Prefixes

The following prefixes are used throughout the ontology:

```turtle
@prefix owl:    <http://www.w3.org/2002/07/owl#> .
@prefix rdf:    <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:   <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd:    <http://www.w3.org/2001/XMLSchema#> .
@prefix time:   <http://www.w3.org/2006/time#> .
@prefix prov:   <http://www.w3.org/ns/prov#> .
@prefix bot:    <https://w3id.org/bot#> .
@prefix bpo:    <https://w3id.org/bpo#> .
@prefix dica:   <https://w3id.org/digitalconstruction/Agents#> .
@prefix dicp:   <https://w3id.org/digitalconstruction/Processes#> .
@prefix dicl:   <https://w3id.org/digitalconstruction/Lifecycle#> .
@prefix dicbm:  <https://w3id.org/digitalconstruction/BuildingMaterials#> .
@prefix omg:    <http://w3id.org/omg#> .
@prefix opm:    <https://w3c-lbd-cg.github.io/opm#> .
@prefix ceo:    <http://ld-ce.com/vocab/CEO#> .
@prefix camo:   <http://ld-ce.com/vocab/CAMO#> .
@prefix ocg:    <https://raw.githubusercontent.com/TheWorldAvatar/ontology/main/ontology/ontocitygml/ontocitygml.owl#> .
@prefix cfc:    <https://w3id.org/cfc/ontology#> .
```

* **cfc:** The base namespace of this ontology, published at `https://w3id.org/cfc/ontology`.
* **ocg:** OntoCityGML vocabulary for city‐scale 3D modeling.
* **bot:** Building Topology Ontology (core concepts like Building, Site, Storey).
* **bpo:** Building Product Ontology (assemblies, products).
* **dica/dicp/dicl/dicbm:** Digital Construction Information (Agents, Processes, Lifecycle, Materials).
* **omg:** Ontology for Managing Geometry (links spatial geometry to objects).
* **opm:** Ontology for Property Management (tracks property evolution over time).
* **ceo:** Circular Exchange Ontology (Offers, Requests, Transactions).
* **camo:** Circular Asset Management Ontology (Assets, AssetCondition, WorkOrder).

---

## 3. Ontology Imports

CFC imports the following external ontologies to leverage existing semantics:

1. **OntoCityGML**
   URL: `https://raw.githubusercontent.com/TheWorldAvatar/ontology/main/ontology/ontocitygml/ontocitygml.owl`

   * Provides classes such as `ocg:City`, `ocg:CityObject`, `ocg:Building`, `ocg:Site`, `ocg:BuildingPart`, and geometry properties like `ocg:containsCityObject`.

2. **BOT (Building Topology Ontology)**
   URL: `https://w3id.org/bot`

   * Offers classes like `bot:Building`, `bot:Site`, `bot:Storey`, `bot:Space`, `bot:Element`, and properties such as `bot:containsZone`.

3. **BPO (Building Product Ontology)**
   URL: `https://w3id.org/bpo`

   * Defines `bpo:assembly` and other product‐level classes for representing assemblies.

4. **DIC Agents**
   URL: `https://w3id.org/digitalconstruction/Agents`

   * Defines classes `dica:Agent`, `dica:Person`, `dica:Organization`, and roles under `dica:StakeholderRole`.

5. **DIC Materials**
   URL: `https://w3id.org/digitalconstruction/Materials`

   * Defines `dicbm:Material` and related classes for describing building materials and their properties.

6. **DIC Lifecycle**
   URL: `https://w3id.org/digitalconstruction/Lifecycle`

   * Defines `dicl:LifecycleStage` and associated process/activity classes.

7. **OMG (Ontology for Managing Geometry)**
   URL: `http://w3id.org/omg`

   * Defines `omg:Geometry` and `omg:GeometryState`, with properties like `omg:hasGeometry`, `omg:lodLevel`, and geometry serialization (e.g., `omg:asGML`, `omg:asIFC`).

8. **OPM (Ontology for Property Management)**
   URL: `https://w3c-lbd-cg.github.io/opm`

   * Enables tracking how property values evolve over time, linking to provenance and metadata.

9. **CEO (Circular Exchange Ontology)**
   URL: `http://ld-ce.com/vocab/CEO`

   * Defines `ceo:Offer`, `ceo:Request`, `ceo:Transaction`, and properties like `ceo:offeredBy`, `ceo:requestedBy`, `ceo:involvesAgent`.

10. **CAMO (Circular Asset Management Ontology)**
    URL: `http://ld-ce.com/vocab/CAMO`

    * Provides classes `camo:Asset`, `camo:AssetCondition`, `camo:WorkOrder`, and properties such as `camo:responsibleForAsset`, `camo:orders`.

---

## 4. High‐Level Structure

Below is an overview of the major class hierarchies and their intended usage.

### City and Sector

* **cfc\:City**

  * Subclass of `ocg:City` (OntoCityGML).
  * Represents an entire city or municipality.
  * Restriction: `cfc:hasSector` → `cfc:Sector`.

* **cfc\:Sector**

  * Subclass of `ocg:CityObject` (OntoCityGML)
  * Represents a neighborhood, planning district, or administrative subregion within a city.
  * Restriction: `cfc:hasBuilding` → `bot:Building` (each Sector contains zero or more BOT Buildings).

**Notes on Alignment**

* We do **not** subclass `cfc:Sector` under `bot:Zone`, because `bot:Zone` is intended for smaller site contexts. Instead, `cfc:Sector` is directly an `ocg:CityObject`, which allows integration within 3D city models.

### Buildings and Components

* **BOT Imported Classes**

  * `bot:Building`, `bot:Site`, `bot:Storey`, `bot:Space`, `bot:Element`.

* **cfc\:BuildingComponent**

  * Subclass of `bot:Element` and `ocg:CityObject`.
  * Represents any physical building element or assembly within a building (e.g., walls, beams, columns, stairs).

* **Component Subclasses**
  Each of the following is a subclass of `cfc:BuildingComponent`, and also `ocg:CityObject`. Some assemblies also include `bpo:assembly`:

  * **cfc\:Window** (e.g., frame + glazing)
  * **cfc\:Door** (frame + leaf)
  * **cfc\:Roof** (rafters, sheathing, coverings)
  * **cfc\:Beam** (horizontal structural member)
  * **cfc\:Column** (vertical structural member)
  * **cfc\:Wall** (enclosure or partition element)
  * **cfc\:Stair** (treads, risers, supports)
  * **cfc\:Floor** (floor slab or assembly)
  * **cfc\:Foundation** (footings, slab‐on‐grade)
  * **cfc\:KitchenComponent** (cabinetry, countertops, built‐in appliances; `bpo:assembly`)
  * **cfc\:PlumbingComponent** (pipes, fixtures, fittings)
  * **cfc\:ElectricalComponent** (wiring, outlets, panels, fixtures)
  * **cfc\:MechanicalComponent** (pumps, motors, ductwork)
  * **cfc\:HVACComponent** (ductwork, air handlers, chillers)

    * **cfc\:HeatingComponent** (boilers, radiators, heaters)
    * **cfc\:VentilationComponent** (ducts, fans, vents)
  * **cfc\:PlasterComponent** (drywall, plasterboard)
  * **cfc\:CladdingComponent** (siding, panels, curtain walls)
  * **cfc\:WindowCurtainWallComponent** (curtain wall + glazing; `bpo:assembly`)

### Materials and Material Resources

* **cfc\:Material**

  * Subclass of `dicbm:Material`. Models any building material (concrete, steel, wood, etc.).

* **Material Subclasses**

  * **cfc\:StructuralSteel**
  * **cfc\:CopperMaterial**
  * **cfc\:AluminumMaterial**
  * **cfc\:BrassMaterial**
  * **cfc\:StainlessSteelMaterial**
  * **cfc\:TimberMaterial**
  * **cfc\:ConcreteMaterial**
  * **cfc\:BrickMaterial**
  * **cfc\:GlassMaterial**
  * **cfc\:GypsumBoardMaterial**
  * **cfc\:InsulationMaterial**
  * **cfc\:WaterproofingMaterial**
  * **cfc\:FlooringMaterial**
  * **cfc\:PaintMaterial**

* **cfc\:MaterialResource**

  * Subclass of `ceo:Resource` (CEO).
  * Represents a retrievable quantity of a given `cfc:Material` (e.g., “10 tons of reclaimed StructuralSteel”).

### Lifecycle Events

Each event class is a subclass of both `dicp:Activity` and `prov:Activity`. This allows for linking agents, timestamps, and provenance.

* **cfc\:DemolitionEvent**

  * When a building or component is demolished, generating `cfc:MaterialResource`.
* **cfc\:ConstructionEvent**

  * When a building or component is constructed or installed.
* **cfc\:RenovationEvent**

  * When a building or component is upgraded or refurbished without full demolition.
* **cfc\:MaintenanceEvent**

  * When routine upkeep, repairs, or servicing occur.
* **cfc\:DesignEvent**

  * When architectural or engineering design/planning takes place.

### Agent Roles

All roles subclass `dica:StakeholderRole` (from DIC Agents). These can attach to any `dica:Person` or `dica:Organization` via `dica:hasRole`.

* **cfc\:UrbanPlannerRole**
* **cfc\:ArchitectRole**
* **cfc\:EngineerRole**
* **cfc\:ConsultantRole**
* **cfc\:ContractorRole**
* **cfc\:ManufacturerRole**
* **cfc\:EndUserRole**
* **cfc\:DeconstructorRole**
* **cfc\:DemolitionContractorRole**
* **cfc\:ReclaimerRole**
* **cfc\:SalvageContractorRole**

### Circular Exchange (CEO) Concepts

* **cfc\:MaterialOffer**

  * Subclass of `ceo:Offer`. Represents an agent’s offer to provide a material resource.
* **cfc\:MaterialRequest**

  * Subclass of `ceo:Request`. Represents an agent’s demand for a material resource.
* **cfc\:MaterialTransaction**

  * Subclass of `ceo:Transaction`. Represents a completed exchange between offer and request.

Key properties:

* **cfc\:makesOffer** <subPropertyOf ceo:offeredBy>
  Domain: `dica:Agent` → Range: `cfc:MaterialOffer`.
* **cfc\:makesRequest** <subPropertyOf ceo:requestedBy>
  Domain: `dica:Agent` → Range: `cfc:MaterialRequest`.
* **cfc\:participatesInTransaction** <subPropertyOf ceo:involvesAgent>
  Domain: `dica:Agent` → Range: `cfc:MaterialTransaction`.

### Circular Asset Management (CAMO) Concepts

* **cfc\:Asset**

  * Subclass of `camo:Asset`. Tracks any physical asset or component through its lifecycle.
* **cfc\:AssetCondition**

  * Subclass of `camo:AssetCondition`. Represents condition states (e.g., new, in‐use, worn, end‐of‐life).
* **cfc\:WorkOrder**

  * Subclass of `camo:WorkOrder`. Scheduled tasks such as inspection, maintenance, or deconstruction.

Key properties:

* **cfc\:assignedToAsset** <subPropertyOf camo:responsibleForAsset>
  Domain: `dica:Agent` → Range: `cfc:Asset`.
* **cfc\:ordersWork** <subPropertyOf camo:orders>
  Domain: `dica:Agent` → Range: `cfc:WorkOrder`.

---

## 5. Object Properties

Below is a summary of the major object properties defined in CFC:

| Property                           | Domain                  | Range                     | Subproperty of                                 | Comment                                                                             |
| ---------------------------------- | ----------------------- | ------------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------- |
| **cfc\:hasSector**                 | `cfc:City`              | `cfc:Sector`              | `ocg:containsCityObject`                       | Relates a City to a Sector (district within the city).                              |
| **cfc\:hasBuilding**               | `cfc:Sector`            | `bot:Building`            | `ocg:containsCityObject`<br>`bot:containsZone` | Relates a Sector to one or more BOT Buildings.                                      |
| **cfc\:hasMaterial**               | `cfc:BuildingComponent` | `cfc:Material`            | —                                              | Indicates the material constituting a component.                                    |
| **cfc\:hasDemolitionEvent**        | `bot:Building`          | `cfc:DemolitionEvent`     | —                                              | Associates a Building with its Demolition event.                                    |
| **cfc\:generatesResource**         | `cfc:DemolitionEvent`   | `cfc:MaterialResource`    | `prov:generated`                               | Indicates a demolition event that generates a specific material resource for reuse. |
| **cfc\:derivedFromComponent**      | `cfc:MaterialResource`  | `cfc:BuildingComponent`   | `prov:wasDerivedFrom`                          | Links a recovered resource back to its originating component.                       |
| **cfc\:performedBy**               | `dicp:Activity`         | `dica:Agent`              | `prov:wasAssociatedWith`                       | Indicates which Agent performed a lifecycle event.                                  |
| **cfc\:offeredBy**                 | `cfc:MaterialResource`  | `dica:Agent`              | —                                              | The agent offering this resource in the circular exchange context.                  |
| **cfc\:makesOffer**                | `dica:Agent`            | `cfc:MaterialOffer`       | `ceo:offeredBy`                                | Links an Agent to the MaterialOffer they create.                                    |
| **cfc\:makesRequest**              | `dica:Agent`            | `cfc:MaterialRequest`     | `ceo:requestedBy`                              | Links an Agent to the MaterialRequest they create.                                  |
| **cfc\:participatesInTransaction** | `dica:Agent`            | `cfc:MaterialTransaction` | `ceo:involvesAgent`                            | Associates an Agent with a completed MaterialTransaction.                           |
| **cfc\:assignedToAsset**           | `dica:Agent`            | `cfc:Asset`               | `camo:responsibleForAsset`                     | Indicates that an Agent is responsible for a specific Asset.                        |
| **cfc\:ordersWork**                | `dica:Agent`            | `cfc:WorkOrder`           | `camo:orders`                                  | Indicates that an Agent issues a WorkOrder for an Asset.                            |

> **Note:** Some properties (e.g., `cfc:hasBuilding`) are marked as subproperties of both BOT and OntoCityGML containment properties, ensuring proper integration with both spatial and topological models.

---

## 6. Data Properties

| Property                 | Domain                  | Range         | Comment                                                              |
| ------------------------ | ----------------------- | ------------- | -------------------------------------------------------------------- |
| **cfc\:quantity**        | `cfc:MaterialResource`  | `xsd:decimal` | Quantity value (e.g., 10.5) of material available for reuse.         |
| **cfc\:unit**            | `cfc:MaterialResource`  | `xsd:string`  | Unit of measure (e.g., “kg”, “m²”).                                  |
| **cfc\:hasLoadCapacity** | `cfc:BuildingComponent` | `xsd:decimal` | Load-bearing capacity of a component or material (e.g., “350.0” kN). |

---

## 7. Alignment with OntoCityGML and BOT

The CFC ontology aligns BOT and OntoCityGML concepts to ensure consistent spatial/topological modeling:

1. **BOT → OntoCityGML Alignments**

   ```turtle
   bot:Building  rdfs:subClassOf ocg:Building .
   bot:Site      rdfs:subClassOf ocg:Site .
   bot:Storey    rdfs:subClassOf ocg:BuildingPart .
   bot:Space     rdfs:subClassOf ocg:BuildingPart .
   ```

   * Any `bot:Building` is also an OntoCityGML `ocg:Building`. Similarly, `bot:Site` aligns to `ocg:Site`, and `bot:Storey`/`bot:Space` align to `ocg:BuildingPart`.

2. **`cfc:City` and `cfc:Sector`**

   * `cfc:City` is a subclass of `ocg:City`, enabling 3D city modeling and linking to geometry.
   * `cfc:Sector` is a subclass of `ocg:CityObject` (rather than `bot:Zone`), because city‐scale sectors can be arbitrary shapes and are better represented as `CityObject` in a 3D context.

3. **Containment Properties**

   * **`ocg:containsCityObject`** (OntoCityGML)
   * **`bot:containsZone`** (BOT)
   * **`cfc:hasBuilding`** is a subproperty of both, ensuring a CFC Sector can contain Buildings in both topological (BOT) and 3D (OntoCityGML) contexts.

---

## 8. Usage Examples

Below are a few illustrative RDF/Turtle snippets showing how to instantiate CFC concepts and link them:

### 8.1 Defining a City and Sector

```turtle
ex:MetropolisCity
    a           cfc:City ;
    rdfs:label  "Metropolis"@en ;
    cfc:hasSector ex:DowntownSector, ex:UptownSector ;
    ocg:hasGeometry ex:Metropolis_Geometry_LOD0 .

ex:DowntownSector
    a           cfc:Sector ;
    rdfs:label  "Downtown"@en ;
    cfc:hasBuilding ex:CentralTower, ex:OldWarehouse ;
    ocg:hasGeometry ex:Downtown_Geometry_LOD1 .

ex:UptownSector
    a           cfc:Sector ;
    rdfs:label  "Uptown District"@en ;
    cfc:hasBuilding ex:UptownMall, ex:ResidentialBlock ;
    ocg:hasGeometry ex:Uptown_Geometry_LOD1 .
```

* **`ex:MetropolisCity`** is a `cfc:City` that contains two sectors: `ex:DowntownSector` and `ex:UptownSector`.
* Each Sector is also an `ocg:CityObject` with its own geometry.

### 8.2 Creating a Building with Components

```turtle
ex:CentralTower
    a           bot:Building ;
    rdfs:label  "Central Tower"@en ;
    ocg:hasGeometry ex:CentralTower_Footprint_LOD2 ;
    cfc:hasDemolitionEvent ex:CentralTower_DemoEvent ;
    bot:hasStorey ex:CentralTower_Storey1, ex:CentralTower_Storey2 .

ex:CentralTower_Storey1
    a           bot:Storey ;
    rdfs:label  "Storey 1 (Ground Floor)"@en ;
    bot:hasSpace ex:CentralTower_LobbySpace .

ex:CentralTower_LobbySpace
    a           bot:Space ;
    rdfs:label  "Lobby Space"@en .

# Components
ex:CT1_Window_001
    a                   cfc:Window ;
    rdfs:label          "Window #001 on Central Tower Facade"@en ;
    cfc:hasMaterial     cfc:GlassMaterial ;
    omg:hasGeometry     ex:CT1_Window_001_Geom .

ex:CT1_Beam_A1
    a                   cfc:Beam ;
    rdfs:label          "Steel Beam A1 on Storey 1"@en ;
    cfc:hasMaterial     cfc:StructuralSteel ;
    cfc:hasLoadCapacity "500.0"^^xsd:decimal ;
    omg:hasGeometry     ex:CT1_Beam_A1_Geom .
```

* **`ex:CentralTower`** is a `bot:Building` and also an `ocg:Building` by alignment.
* It has two storeys (`bot:Storey`), a demolition event, and several component instances (Windows, Beams).
* Each component references its material and geometry.

### 8.3 Recording a Demolition Event and Material Recovery

```turtle
ex:CentralTower_DemoEvent
    a                   cfc:DemolitionEvent ;
    rdfs:label          "Demolition of Central Tower"@en ;
    time:hasBeginning   "2026-01-15T08:00:00Z"^^xsd:dateTime ;
    cfc:performedBy     ex:DemoCorpInc ;
    cfc:generatesResource ex:SteelBeamA1_Resource, ex:GlassWindow001_Resource .

ex:SteelBeamA1_Resource
    a                   cfc:MaterialResource ;
    rdfs:label          "Reclaimed Steel Beam A1"@en ;
    cfc:derivedFromComponent ex:CT1_Beam_A1 ;
    cfc:quantity        "1.0"^^xsd:decimal ;
    cfc:unit            "unit" ;
    cfc:offeredBy       ex:DemoCorpInc .

ex:GlassWindow001_Resource
    a                   cfc:MaterialResource ;
    rdfs:label          "Reclaimed Glass from Window #001"@en ;
    cfc:derivedFromComponent ex:CT1_Window_001 ;
    cfc:quantity        "2.5"^^xsd:decimal ;   # e.g., 2.5 m² of glass
    cfc:unit            "m²" ;
    cfc:offeredBy       ex:DemoCorpInc .

ex:DemoCorpInc
    a                   dica:Organization ;
    rdfs:label          "DemoCorp Inc."@en ;
    dica:hasRole        cfc:DemolitionContractorRole, cfc:ReclaimerRole ;
    cfc:makesOffer      ex:SteelBeamA1_Resource, ex:GlassWindow001_Resource .
```

* A `cfc:DemolitionEvent` is performed by `ex:DemoCorpInc`, which generates two material resources (a reclaimed steel beam and reclaimed glass).
* Each `cfc:MaterialResource` links back to the original component via `cfc:derivedFromComponent`.
* `ex:DemoCorpInc` (a `dica:Organization` with roles) makes circular economy offers for these reclaimed materials.

### 8.4 Issuing Asset Work Orders (CAMO)

```turtle
ex:BeamAssemblyA
    a                   cfc:Asset ;
    rdfs:label          "Beam Assembly A (Asset)"@en ;
    camo:hasCondition   ex:AssetCondition_InUse ;
    camo:workOrder      ex:BeamAssemblyA_MaintenanceOrder .

ex:AssetCondition_InUse
    a                   cfc:AssetCondition ;
    rdfs:label          "InUseCondition"@en ;
    rdfs:comment        "Asset is currently in active service."@en .

ex:BeamAssemblyA_MaintenanceOrder
    a                   cfc:WorkOrder ;
    rdfs:label          "WorkOrder: Inspect Beam Assembly A"@en ;
    camo:forAsset       ex:BeamAssemblyA ;
    camo:scheduledDate  "2025-09-01T10:00:00Z"^^xsd:dateTime ;
    cfc:ordersWork      ex:AssetManagerJohn .

ex:AssetManagerJohn
    a                   dica:Person ;
    rdfs:label          "Asset Manager John"@en ;
    dica:hasRole        cfc:EndUserRole ;
    cfc:ordersWork      ex:BeamAssemblyA_MaintenanceOrder .
```

* Represents an Asset (`BeamAssemblyA`) tracked in CAMO, with a current condition and an associated `cfc:WorkOrder`.
* `ex:AssetManagerJohn` (a `dica:Person`) orders the maintenance inspection.

### 8.5 Geometry Attachments via OMG

```turtle
# Example of attaching geometry to a Sector and Building
ex:UptownSector_Geometry_LOD1
    a                 omg:Geometry ;
    omg:lodLevel      "1"^^xsd:integer ;
    omg:asGML         "<gml> … Uptown District footprint … </gml>"^^xsd:string .

ex:UptownSector
    a                 cfc:Sector ;
    rdfs:label        "Uptown District"@en ;
    ocg:hasGeometry   ex:UptownSector_Geometry_LOD1 .

ex:CentralTower_Footprint_LOD2
    a                 omg:GeometryState ;
    omg:lodLevel      "2"^^xsd:integer ;
    omg:asIFC         "# IFC file data for Central Tower LOD2"^^xsd:string ;
    prov:generatedAtTime "2024-06-01T00:00:00Z"^^xsd:dateTime .

ex:CentralTower
    a                 bot:Building ;
    rdfs:label        "Central Tower"@en ;
    ocg:hasGeometry   ex:CentralTower_Footprint_LOD2 .
```

* Demonstrates how to attach `omg:Geometry` or `omg:GeometryState` to an OntoCityGML object (Sector, Building) for spatial modeling.

---

## 9. Versioning and Publication

* **Ontology IRI:** `https://w3id.org/cfc/ontology`
* **Turtle File Location:**

  * Browseable at: `[ontology/cfc.owl](https://github.com/DigiConstructLab-TU-Delft/CircularFutureCitiesOntology/blob/main/ontology/cfc.owl)` 
  


---

**Contact and Acknowledgments**

* Developed under the **Circular Future Cities** initiative of the Future Cities Laboratory, a collaboration between ETH Zürich and the Singapore-ETH Centre, with support from the National Research Foundation (NRF).
* Integrates contributions from OntoCityGML, BOT, DIC, CEO, CAMO, OMG, and OPM communities.

For questions, comments, or contributions, please file an issue in the GitHub repository:
`https://github.com/DigiConstructLab-TU-Delft/CircularFutureCitiesOntology/issues`

---

End of documentation.
