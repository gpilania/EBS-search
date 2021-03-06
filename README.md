# Online Search Tool for Graphical Patterns in Electronic Band Structures

This repository hosts the code and a test case for the paper [arXiv:1710.11611](https://arxiv.org/abs/1710.11611). Tested with Python 3.6.5.

To see the tool in action, register for free at: [omdb.diracmaterials.org](https://omdb.diracmaterials.org)

## Installation
```
pip install -r requirements.txt
```

## Example
This repository contains a data folder with a VASP calculation. You can add more calculations here, each folder should contain calculations for a single material.

Create an ANN (approximate nearest neighbours) index (see [create_index.py](create_index.py) for all options):
```
python create_index.py --band_index -1 --width 0.4 --dimensions 16 --trees 10
```

Perform the search for a crossing/node:
```
python search.py --band_index -1 --width 0.4 --dimensions 16 --pattern crossing
```

This prints the angular distance and the following plot should appear:

![Search Result Dirac crossing](misc/crossing_search_result.png)

For reference, see the [OMDB material information](https://omdb.diracmaterials.org/material/cod/7155013). Note that the lookup table also contains information about the gap between the two bands. On the OMDB this is used to apply post-processing to the search results (e.g. filtering out gapped matches).

Run the following commands to search the bands (-2,-1) for a parabola (Figure 8 in the paper):
```
python create_index.py --band_index -2 --width 0.4 --dimensions 16 --trees 10
python search.py --band_index -2 --width 0.4 --dimensions 16 --pattern parabola
```
![Search Result Parabola crossing](misc/parabola_search_result.png)

To search for a mexican hat, increase the window size, resolution (dimensions):
```
python create_index.py --band_index -3 --width 0.8 --dimensions 64 --trees 10
python search.py --band_index -3 --width 0.8 --dimensions 64 --pattern mexican --search_k 200
```
![Search Result Mexican hat](misc/mexican_search_result.png)

## Test data
This repo contains a fake data generator [lib/fake.py](lib/fake.py):

![Fake data](misc/fake_data.png)

```
python create_test_index.py --width 0.4 --dimensions 64 --trees 10
```
```
python test_search.py --width 0.4 --results 6 --dimensions 64 --pattern crossing
```
![Test crossings](misc/test_results_crossing.png)
```
python test_search.py --width 0.4 --results 6 --dimensions 64 --pattern parabola
```
![Test parabola](misc/test_results_parabola.png)
```
python test_search.py --width 0.4 --results 1 --dimensions 64 --pattern mexican
```
![Test mexican](misc/test_results_mexican.png)
