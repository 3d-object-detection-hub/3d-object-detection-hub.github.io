---
layout: default
title: Datasets
permalink: /datasets/
---

# Datasets

A quick summary of the major 3D-object-detection datasets used as benchmarks in autonomous-driving research. Each dataset was collected by equipping a vehicle with multiple cameras and LiDAR sensors, driving through varied environments, and then manually annotating every 3D frame.

<table class="datasets">
  <thead>
    <tr>
      <th>Dataset</th>
      <th>Year</th>
      <th># Cameras</th>
      <th># LiDARs</th>
      <th># Scenes</th>
      <th># Classes</th>
      <th>Locations</th>
      <th>Night</th>
      <th>Rain</th>
      <th>Annotated 3D BBoxes</th>
      <th>Annotated Frames</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        KITTI  
        <a href="https://www.cvlibs.net/publications/Geiger2013IJRR.pdf" target="_blank">
          [Geiger et al. 2013]
        </a>
      </td>
      <td>2012</td>
      <td>2</td><td>1</td>
      <td>22</td><td>3</td><td>Germany</td><td>No</td><td>No</td>
      <td>80 000</td><td>15 000</td>
    </tr>
    <tr>
      <td>
        ApolloScape  
        <a href="https://arxiv.org/abs/1803.06184" target="_blank">
          [Wang et al. 2019]
        </a>
      </td>
      <td>2018</td>
      <td>2</td><td>2</td>
      <td>73</td><td>27</td><td>China</td><td>Yes</td><td>No</td>
      <td>70 000</td><td>80 000</td>
    </tr>
    <tr>
      <td>
        nuScenes  
        <a href="https://arxiv.org/abs/1903.11027" target="_blank">
          [Caesar et al. 2020]
        </a>
      </td>
      <td>2019</td>
      <td>6</td><td>1</td>
      <td>1 000</td><td>23</td><td>USA / Singapore</td><td>Yes</td><td>Yes</td>
      <td>1.4 M</td><td>40 000</td>
    </tr>
    <tr>
      <td>
        Argoverse  
        <a href="https://arxiv.org/abs/1911.02620" target="_blank">
          [Chang et al. 2019]
        </a>
      </td>
      <td>2019</td>
      <td>9</td><td>2</td>
      <td>113</td><td>15</td><td>USA</td><td>Yes</td><td>Yes</td>
      <td>993 000</td><td>22 000</td>
    </tr>
    <tr>
      <td>
        Waymo Open  
        <a href="https://arxiv.org/abs/1912.04838" target="_blank">
          [Sun et al. 2019]
        </a>
      </td>
      <td>2019</td>
      <td>5</td><td>5</td>
      <td>1 150</td><td>4</td><td>USA</td><td>Yes</td><td>Yes</td>
      <td>12 000 000</td><td>230 000</td>
    </tr>
    <tr>
      <td>
        Lyft Level 5  
        <a href="https://arxiv.org/abs/2006.14480" target="_blank">
          [Houston et al. 2021]
        </a>
      </td>
      <td>2019</td>
      <td>7</td><td>3</td>
      <td>366</td><td>9</td><td>USA</td><td>No</td><td>No</td>
      <td>1.3 M</td><td>46 000</td>
    </tr>
    <tr>
      <td>
        H3D  
        <a href="https://arxiv.org/abs/1903.01568" target="_blank">
          [Patil et al. 2019]
        </a>
      </td>
      <td>2019</td>
      <td>3</td><td>1</td>
      <td>160</td><td>8</td><td>USA</td><td>No</td><td>No</td>
      <td>1.1 M</td><td>27 000</td>
    </tr>
  </tbody>
</table>

---

## Parameter Descriptions

- **Dataset**: Name of the benchmark and original publication citation.  
- **Year**: Release year of the dataset.  
- **# Cameras**: Number of synchronized RGB cameras.  
- **# LiDARs**: Number of LiDAR sensors.  
- **# Scenes**: Distinct driving sequences or collection drives.  
- **# Classes**: Number of object categories annotated (e.g., cars, pedestrians).  
- **Locations**: Geographic areas where data was recorded.  
- **Night**: Indicates if night-time data is included.  
- **Rain**: Indicates if driving in rainy conditions is present.  
- **Annotated 3D BBoxes**: Total count of 3D bounding boxes labeled.  
- **Annotated Frames**: Number of keyframes with full 3D annotations.  
