# Universal Robustness Evaluation Toolkit (for Evasion) - URET

This repository will contain the code for adversarial example generation tools described in:

**A Generic Adversarial Generation Toolkit**

*Kevin Eykholt, Taesung Lee, Doug Schales, Jiyong Jang, Ian Molloy, Masha Zorin*

**Currently, the code is under review for open source release**

## Toolkit Description

Machine learning models are known to be vulnerable to adversarial evasion attacks as illustrated by image classification models. Thoroughly understanding such attacks is critical in order to ensure the safety and robustness of critical AI tasks. However, most adversarial attacks are difficult to deploy against a majority of AI systems because they have focused on image domain with only few constraints. 

URET is a solution that enables users to evaluate their models against adversarial evasion attacks regardless of data representation or model arhitecture. In order to generate adversarial examples for a chosen model and data domain, a user does the following:

1. Select/Define one or more **Data Transformers**.
2. Select one or more **Explorer Configurationss** and define its exploration parameters.
3. Load a pre-trained model and the set of samples to be adversarially transformed.
4. Define any **data constraints** or *data interdependencies**
5. Run URET

To ease evaluation, URET exposes a configuration file interface.

### Data Transformers
A data transformer is an object containing function definitions for how a specific data type can be transformed. The current repository contains pre-defined transformers for some basic data types: numerical, categorical, and string. Data transformers can be combined to support other data representations. For example, tabular data may contain a combination of numerical and categorical data, which URET can support.

For unique data types, URET also exposes a transformation interface so users can define their own data transformers. The generation algorithms are fully compatible with the transformation interface so URET can be extended to support new representations. We include an example by re-coding some binary transformations (https://github.com/endgameinc/gym-malware) as a data transformer.

### Explorer Configurations
In the paper, we characterize our generation process as a graph exploration algorithm. An input is represented as a vertex and our goal is to find a series of edge (representing input transformations) that achieve the adversarial goal. An Explorer is defined by three components: the vertex scoring funtion, the edge ranking algorithm, and the search algorithm.

We define two vertex scoring functions by default:
