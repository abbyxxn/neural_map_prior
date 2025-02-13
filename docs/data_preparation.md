# Dataset Preparation

## Download and prepare the nuScenes dataset

Download nuScenes V1.0 full dataset data [HERE](https://www.nuscenes.org/download), including the map extensions(V1.3).
Data
creation should be under the GPU environment.
Prepare nuscenes data by running

```bash
#python tools/create_data.py nuscenes --root-path ./data/nuscenes --out-dir ./data/nuscenes --extra-tag nuscenes
python tools/data_converter/nuscenes_converter.py --data-root your/dataset/nuScenes/
```

You can either use our provided
files [nuScences_map_trainval_infos_train.pkl](https://drive.google.com/file/d/18P8LZcEVxGYAvMQpEROrF0pnpu62ffvD/view?usp=sharing)
and [nuScences_map_trainval_infos_val.pkl](https://drive.google.com/file/d/1H6HfnNqmKBFvNIivApcsRUCgPtxgIq7A/view?usp=sharing).
Copy the infos file into `$neural_map_prior/data/nuscenes/`.

In addition, you will need to
download [train_city_infos.pkl](https://drive.google.com/file/d/1WZ9fzVIiq9V-B8_l3EtF19Q9aLg6hmPG/view?usp=sharing) and
[val_city_infos.pkl](https://drive.google.com/file/d/1J3-BQzbaKJaHsEMZTTVDq5JvO5HHG41M/view?usp=sharing) or you can
generate them using the code provided [here](project/neural_map_prior/data_utils/nusc_city_infos.py). These files
contain information about each sample's city, which is crucial for determining which sample belongs to which map tile.

## nuScenes Dataset Structure

It is recommended to symlink the dataset root to `$neural_map_prior/data/nuscenes`, `$neural_map_prior` means this
repo's root directories. If your folder structure is different from the following, you may need to change the
corresponding paths in config files.

```bash
mkdir data && cd data
ln -s /path/to/your/dataset/nuScenes nuscenes
mkdir nuscenes_infos
```

```
neural_map_prior
├── mmdet3d
├── tools
├── projects
│   ├── nmp
│   ├── configs
├── ckpts
├── data
│   ├── nuscenes
│   │   ├── maps <-- used
│   │   ├── samples <-- key frames
│   │   ├── sweeps  <-- frames without annotation
│   │   ├── v1.0-mini <-- metadata and annotations
│   │   ├── v1.0-test <-- metadata
|   |   ├── v1.0-trainval <-- metadata and annotations
│   │   ├── nuScences_map_trainval_infos_train.pkl <-- train annotations
│   │   ├── nuScences_map_trainval_infos_val.pkl <-- val annotations
│   ├── nuscenes_infos
│   │   ├── train_city_infos.pkl
│   │   ├── val_city_infos.pkl
```

