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
cd ./clusterization
python cluster_balanced.py --radius 3 --mark -N 40 --out_core REPRO  all_aryls.csv
```
The file ```REPRO_clusters_r3_marked_selected.csv``` will contain the selection of bromides used in the study.<br>

# Closed-loop
After obtaining an initial set of 11 reactants, 7 different conditions were used on each set of reactants, and the initial result data set was ```MADNESS_suzuki_coupling_results.csv```.<br>
In addition to the starting data, we need the following files before we can proceed with the Closed-loop process:<br>
1. A JSON file ```cache.json```, which have to provide a field ``url`` pointing to the spreadsheet, it can also point directly to the csv file name where the data is stored.<br>
2. JAON files ```space_dict.json```, ```current_space_dict.json```, ```current_space.json``` they represent the space of possible reaction conditions the format is as follows:
```
{
	"base":        ["Na2CO3", "K3PO4"], 
	"solvent":     ["Toluene:water", "1,4-dioxane:water", "DMF:water"],
	"ligand":      ["P(tBu)3", "PPh3", "Pcy3", "SPhos", "XPhos", "dba", "dppf"],
	"temperature": [60, 100]
}
```
I have put the corresponding files for Suzuki coupling under the ```Nanotekton-hangman-d5672b1``` folder <br>
Then you can start running ```do_step.py``` - script that a) downloads the speadsheet from shared Google drive(or directly get from the csv file), b) trains the model and makes prediction for the next step and c) uploads next reactions to the shared Google drive.<br>
Note: The ```update_gdirve``` option requires a properly configured ```rclone```.


   

