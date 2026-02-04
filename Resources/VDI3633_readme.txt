VDI 3633 Ontology Design Pattern (ODP)
========================================

Version: 1.1
Last Updated: 2026-02-04

OVERVIEW
--------
This Ontology Design Pattern (ODP) is based on VDI 3633 - "Simulation of systems in materials
handling, logistics and production". The ODP models the core concepts from Section 2 (Terms and
definitions) of the VDI 3633 standard.

The ontology provides a formal representation of simulation-related concepts including systems,
models, simulation experiments, simulation runs, and various data types used throughout the
simulation lifecycle.


MAIN CONCEPTS
-------------

1. System
   - A set of interrelated elements separated from the environment
   - Contains processes
   - Can be modeled by simulation models

2. Model
   - Simplified reproduction of a planned or existing system
   - Contains internal model data
   - Models a specific system
   - Part of a simulation environment

3. Process
   - Full set of interacting operations in a system
   - Processes material, energy or information

4. Structure
   - Relations among the elements of a system

5. Simulation
   - Representation of a system with its dynamic processes
   - Comprises simulation experiments

6. SimulationExperiment
   - Targeted empirical investigation of a model's behaviour
   - Contains multiple simulation runs
   - Part of a broader simulation

7. SimulationRun
   - Reproduction of a system's behaviour with a specific executable model
   - Executed with a simulation environment
   - Uses input data, experiment data
   - Produces simulation result data

8. SimulationEnvironment
   - Combination of a model and simulation tool
   - Provides the simulation capability
   - Executes simulation runs

9. SimulationTool
   - Software program to build and execute simulation models

10. Data (abstract base class)
    - ExperimentData: Starting time, duration, model parameters for each run
    - InputData: User-provided static or stochastic data
    - InternalModelData: Constants and variables from model development
    - SimulationResultData: Data collected during simulation runs


OBJECT PROPERTIES
-----------------

Core Relationships:
- modelsSystem / isModeledBy: Model ↔ System
- hasProcess / isProcessOf: System ↔ Process
- comprisesExperiment / isExperimentOf: Simulation ↔ SimulationExperiment
- hasSimulationRun / isSimulationRunOf: SimulationExperiment ↔ SimulationRun
- isExecutedWith / executes: SimulationRun ↔ SimulationEnvironment
- hasModel / isModelOf: SimulationEnvironment ↔ Model
- usesSimulationTool / isUsedBy: SimulationEnvironment ↔ SimulationTool

Data Relationships:
- hasInputData / isInputDataOf: SimulationRun ↔ InputData
- hasExperimentData / isExperimentDataOf: SimulationRun ↔ ExperimentData
- hasSimulationResultData / isSimulationResultDataOf: SimulationRun ↔ SimulationResultData
- hasInternalModelData / isInternalModelDataOf: Model ↔ InternalModelData


PROPERTY CHARACTERISTICS
------------------------

Functional Properties (1:1 relationships):
- hasModel: Each SimulationEnvironment has exactly one Model
- usesSimulationTool: Each SimulationEnvironment uses exactly one SimulationTool
- modelsSystem: Each Model models exactly one System
- isExecutedWith: Each SimulationRun is executed with exactly one SimulationEnvironment
- isSimulationRunOf: Each SimulationRun belongs to exactly one SimulationExperiment
- isExperimentOf: Each SimulationExperiment belongs to exactly one Simulation

Inverse Functional Properties:
- isModelOf: Each Model is part of exactly one SimulationEnvironment


DISJOINT CLASS AXIOMS
----------------------

The ontology defines four groups of mutually disjoint classes to ensure logical consistency:

1. Data Types (all data types are mutually exclusive):
   - ExperimentData ⊥ InputData ⊥ InternalModelData ⊥ SimulationResultData

2. System Concepts (mutually exclusive):
   - Model ⊥ System ⊥ Process ⊥ Structure

3. Simulation Concepts (mutually exclusive):
   - Simulation ⊥ SimulationExperiment ⊥ SimulationRun ⊥ SimulationEnvironment

4. Top-Level Concepts (all main concepts are mutually exclusive):
   - Data ⊥ Model ⊥ System ⊥ Process ⊥ Simulation ⊥ SimulationExperiment ⊥
     SimulationRun ⊥ SimulationEnvironment ⊥ SimulationTool ⊥ Structure


DESIGN DECISIONS
----------------

1. Inverse Properties: All object properties have explicitly defined inverse properties to enable
   bidirectional navigation and inference.

2. Functional Properties: Properties representing 1:1 relationships are declared as functional to
   enforce cardinality constraints.

3. Disjoint Classes: Multiple levels of disjointness axioms ensure that instances cannot belong
   to conflicting classes, improving reasoning and validation.

4. Language Support: The ontology provides labels and comments in both English and German (where
   applicable) to support international use.


USAGE NOTES
-----------

- This ODP is designed to be extended and specialized for specific simulation domains
- The ontology uses OWL 2 DL for maximum expressiveness while maintaining decidability
- All classes and properties include rdfs:comment annotations with definitions from VDI 3633
- The namespace URI is: http://www.semanticweb.org/reif/ontologies/VDI3633#


VERSION HISTORY
---------------

Version 1.1 (2026-02-04):
- Added inverse object properties for all relationships
- Defined property characteristics (Functional, InverseFunctional)
- Added comprehensive disjoint class axioms at multiple levels
- Enhanced semantic precision for better reasoning support

Version 1.0 (initial):
- Core concepts from VDI 3633 Section 2
- Basic object properties and class hierarchy
- English language documentation


FUTURE WORK
-----------

This ODP is an early draft for the SiS ontology and still needs to be expanded to fully map the
VDI 3633 standard, including:
- Additional simulation types and methodologies
- More detailed process modeling concepts
- Extended data property definitions
- Integration with other manufacturing and logistics standards


REFERENCES
----------

VDI 3633 - Simulation of systems in materials handling, logistics and production
Association of German Engineers (Verein Deutscher Ingenieure)


CONTACT
-------

For questions or contributions, please refer to the main SiS repository documentation.
