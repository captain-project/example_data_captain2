# Example files for CAPTAIN 2.0 (beta)

**Daniele Silvestro - 23.09.2025**

To install CAPTAIN v.2 go to [this repository](https://github.com/captain-project/captain2).  

### Species distribution data
Examples of habitat suitability maps are provided in the `present_habitat_suitability` folder. These are expected to be the results of species distribution models (SDMs) predicting habitat suitability going from 0 (unsuitable) to 1 (suitable). All spatial data are provided as `.tif` files or numpy arrays (`.npy` files) assuming matching resolution and extent across all layers.


Future habitat suitability can be used in the model to incorporate the effects of climate change in the analysis (examples in `future_habitat_suitability`). These maps ideally come from running the SDMs trained with present data with future climate and environmental predictors. Alternatively, they can be estimated from within CAPTAIN based on present habitat suitability and future climate and environmental data.


### Environmental layers
Different environmental layers can be incorporated in the analysis including disturbance (e.g. land use), costs, existing protected areas. The values provided in these layers should be rescaled between 0 and 1. It is assumed that larger values represent higher disturbance, higher costs, or higher level of protection, depending on the layer. 


### Species traits
Species-specific traits can be incorporated in the analysis if they are available or can be approximated. These can include: migration ability, growth rate, sensitivity to anthropogenic disturbance, and a current assessment of species extinction risk. The latter is assumed to include 5 threat level (following the IUCN Red List scheme). 
An example file is provided in the `species_traits.csv` table. 


### Main CAPTAIN parameters
Many parameter settings can be changed in the model including: 

* The conservation target  
* The rules based on which the conservation status of a species can change over time (e.g. increases or decreases linked with population dynamics or range size changes) 
* The reward system that defines what the model is optimized for

The parameters are provided in the file `captain_config.txt`   
**Note:** you need to edit the example config file to provide the full path to the input files:
```
data_dir = full_path/example_data_captain2 
models_dir = full_path/example_data_captain2
```


### Training a model

To train a model you can execute the script `train_model.py` providing the config file with its full path: 

```
python train_model.py full_path/config_train.txt

```

Note the training a full model might require more epochs than the 100 specified in the example `config_train.txt` file. This can be changed in the config file, section `[general]` to, e.g.

```
epochs = 1000
```

A pre-trained example file is included in the [trained_model_example](https://github.com/captain-project/example_data_captain2/tree/main/trained_model_example) folder.

### Predicting conservation priorities with a trained model

After training a model you can run predictions to identify the conservation priority areas.

```
python captain_predict.py full_path/config_predict.txt

```

**Note:** you need to edit the example config file to provide the full path to the input files and provide the trained model file name.

```
data_dir = full_path/example_data_captain2 
models_dir = full_path/example_data_captain2
trained_model_file = test20250525.log

```

An example of the prediction output is included in the [predictions_example](https://github.com/captain-project/example_data_captain2/tree/main/predictions_example) folder. 






















