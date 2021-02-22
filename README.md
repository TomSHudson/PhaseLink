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

### Notes on the parameter file (params.json):

 - *t_win* - Length of window (in seconds) to generate synthetic training events within. (float)
 - *n_max_picks* - Number of picks in training set. (int)
 - *n_epochs* - Number of training epochs for training synthetic model. (int)
 - *batch_size* - The size of each batch for training. (int)
 - *n_min_nucl* - The minimum number of phase picks to nucleate as a cluster. (int)
 - *n_min_merge* - Minimum number of picks to merge as an event. (int)
 - *n_min_det* - Minimum number of events required to make a detection. (int)
 - *avg_eve_sep* - The average event separataion time for the training dataset, in seconds. (float)
 - *outfile*: *sjfz_det_linked.nlloc*,
 - *outpkl*: *sjfz_det_linked.pkl*,
 - *device*: *cpu*,
 - *model_file*: *example/phaselink_model/model_to_use.cpu.pt*,
 - *station_file*: *station_list.txt*,
 - *station_map_file*: *station_map.pkl*,
 - *sncl_map_file*: *sncl_map.pkl*,
 - *gpd_file*: *anza_gpd_J1-10_rem.output*,
 - *pr_min*: 0.50,
 - *trig_dur_min*: 0.00,
 - *nlloc_loc_path*: *loc/cahuilla*,
 - *wf_path*: *wf*,
 - *plot_unassociated*: false,
 - *max_t_resid*: 999.0,
 - *plot_seismicity*: true,
 - *lat_min*: 31.0,
 - *training_dset_X*: *shimane_train_X.npy*,
 - *training_dset_Y*: *shimane_train_Y.npy*,
 - *lat_max*: 37.0,
 - *n_train_samp*: 10000,
 - *lon_min*: -121.0,
 - *lon_max*: -115,
 - *fault_file*: */home/zross/src/Qt_flt_v2-0latlonNAD27.MIF*,
 - *n_min_radius*: 8,
 - *trav_time_p*: *tt.pg*,
 - *trav_time_s*: *tt.sg*,
 - *datum*: 0.0,
 - *n_fake*: 0,
 - *max_event_depth*: 25.0,
 - *min_hypo_dist*: 10.0,
 - *max_hypo_dist*: 100.0,
 - *max_pick_error*: 0.50,
 - *n_threads*: 8,
 - *catalog_file_post*: *anza_test.xml*,
 - *back_project*: false,
 - *stop_read_early*: false


Contact Zachary Ross (Caltech) with any questions.
