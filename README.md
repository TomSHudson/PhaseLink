# PhaseLink: A deep learning approach to seismic phase association

This code accompanies the paper
```
Ross, Z. E., Yue, Y., Meier, M.‐A., Hauksson, E., & Heaton, T. H. ( 2019). PhaseLink: A deep learning approach to seismic phase association. Journal of Geophysical Research: Solid Earth, 124, 856– 869. https://doi.org/10.1029/2018JB016674 [arXiv:1809.02880]
```
There are four scripts that should be used in the following order:
1) phaselink_dataset.py : Build a training dataset from a station file and 1D travel time table. The travel time tables are in the format that is output by the GrowClust code. A decoupled version of this raytracer is provided in raytracer.tar.gz, which has a python wrapper to the F90 routine.

2) phaselink_train.py : Train a stacked bidirectional GRU model to link phases together. This code takes the training dataset produced in step 1 and trains a deep neural net to link together phase detections.

3) phaselink_eval.py : Associate a set of phase detections to earthquakes. This code runs the PhaseLink algorithm in evaluation mode, by using the trained model to link together phases and clustering the links to detect events. It outputs detections in NonLinLoc phase format to be located.

4) phaselink_plot.py : Plot resulting detections after locating them

More details about these codes and input file formats will be added over time. All of the scripts take a json filename as a command line argument. See the example file params.json.

Contact Zachary Ross (Caltech) with any questions.

### Notes on the parameter file (params.json):

 - *t_win* - Length of window (in seconds) to generate synthetic training events within. (float)
 - *n_max_picks* - Number of picks in training set. (int)
 - *n_epochs* - Number of training epochs for training synthetic model. (int)
 - *batch_size* - The size of each batch for training. (int)
 - *n_min_nucl* - The minimum number of phase picks to nucleate as a cluster. (int)
 - *n_min_merge* - Minimum number of picks to merge as an event. (int)
 - *n_min_det* - Minimum number of events required to make a detection. (int)
 - *avg_eve_sep* - The average event separataion time for the training dataset, in seconds. (float)
 - *outfile* - The path to the output file to save all the associated phases for all events output from **phaselink_eval.py**.  (str)
 - *outpkl* - 
 - *device* - The device to use for the training and processing. Can be a GPU or CPU. For CPU use "cpu". For GPU use "cuda:?" where ? is the number of the GPU device to use. (str)
 - *model_file* - The path to the synthetic trained model to use for phase association. This will be the best model output using **phaselink_train.py**. (str)
 - *station_file* - The path to the station information file, detailing station names and locations for all stations in the network. (str)
 - *station_map_file* - Path of the station map pkl file output by **phaselink_dataset.py** (str)
 - *sncl_map_file* - Path of the sncl map pkl file output by **phaselink_dataset.py** (str)
 - *gpd_file* - Path to the unassociated phases to be associated by PhaseLink in **phaselink_eval.py**. The format of this is a GPD output file (see Ross et al 2018). (str)
 - *pr_min* - The minimum probability associated with a phase in order to make a detection. (float)
 - *trig_dur_min* - 
 - *nlloc_loc_path* - 
 - *wf_path* - 
 - *plot_unassociated* - 
 - *max_t_resid* - 
 - *plot_seismicity* - 
 - *lat_min* - 
 - *training_dset_X* - The path to the X part of the training dataset created using **phaselink_datset.py**. (str)
 - *training_dset_Y* - The path to the Y part of the training dataset created using **phaselink_datset.py**. (str)
 - *lat_max* - 
 - *n_train_samp* - Number of training sample. (int)
 - *lon_min* - 
 - *lon_max* - 
 - *fault_file* - 
 - *n_min_radius* - 
 - *trav_time_p* - The path to the 1D P-wave travel-time table to use in **phaselink_datset.py** and **phaselink_eval.py**. Format of the travel-time table is the same as that output by the code GrowClust. (str)
 - *trav_time_s* - The path to the 1D S-wave travel-time table to use in **phaselink_datset.py** and **phaselink_eval.py**. Format of the travel-time table is the same as that output by the code GrowClust. (str)
 - *datum*: 0.0 - The depth reference for the travel-time table, in km. (str)
 - *n_fake* - Number of random/fake picks to include when training. This is a way of introducing noise into the system. (int)
 - *max_event_depth* - The maximum event depth, in km. (float)
 - *min_hypo_dist* - The minimum hypocentral distance, in km. (float)
 - *max_hypo_dist* - The maximum hypocentral distance, in km. (float)
 - *max_pick_error* - The maximum pick error, in seconds. (float)
 - *n_threads* - Number of threads to use during processing (if using cpu device ?) (int)
 - *catalog_file_post* - 
 - *back_project* - If true, back projects the phase. (bool)
 - *stop_read_early* - 



