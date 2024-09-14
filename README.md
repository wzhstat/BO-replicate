# closed-loop-replicate
# Python Version
python 3.7.7
# Install Requirements
To run the reaction condition selector you need to make sure you have installed anaconda. ```conda_env.yml``` is needed to recreate the environment.
```
conda env create -f conda_env.yml
```

# Hierarchical clustering
In order to obtain the initial reaction substrate, the following steps were adopted:<br>
1. Assembled about 5,400 purchasable aryl halides from the inventory of common chemical suppliers through data mining.<br>
2. Using a hierarchical clustering strategy, the building blocks in these chemical Spaces were grouped according to their common aromatic ring substructures and hanging functions, and 54 of the most representative molecules were selected.<br>
3. Combining these molecules with 54 commercially available aryl n-methyliminodiacetic acid (MIDA) borates defined a subselected matrix range of 2688 representative cross-coupled products. Subsequently, based on Tanimoto's similarity greedy algorithm, this work identifies 11 representative substrate pairs from the range to maximize the mutual dissimilarity of the resulting products.<br>

In order to perform clusterization & selection (with all comercially available bromides stored in `all_aryls.csv`), use the command:<br>
```
python cluster_balanced.py --radius 3 --mark -N 40 --out_core REPRO  all_aryls.csv
```
The file ```REPRO_clusters_r3_marked_selected.csv``` will contain the selection of bromides used in the study.<br>
   

