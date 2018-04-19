# label_detection_example
How to use label_detection and affine_invariant_features

## Dependencies (and tested versions)
* ROS (kinetic)
* affine_invariant_features
  * Scale-, rotation-, affine-invariant image feature
  * https://github.com/yoshito-n-students/affine_invariant_features
* label_detection
  * Flat object detection based on affine_invariant_features
  * https://github.com/yoshito-n-students/label_detection
  
## Quick start
1. Clone required repogitories and build
   ```
   cd <your_catkin_workspace>/src
   git clone git@github.com:yoshito-n-students/affine_invariant_features.git
   git clone git@github.com:yoshito-n-students/label_detection.git
   git clone git@github.com:yoshito-n-students/label_detection_example.git
   cd <your_catkin_workspace>
   catkin_make
   source devel/setup.bash
   ```
1. Run an example
   ```
   roslaunch label_detection_example offline_label_detection.launch
   ```
   * this will show a scene image with 5 labels (a logo of Tohoku University, etc) detected
   
## How to detect your own targets
1. Create target descriptions
   ```
   rosrun affine_invariant_features generate_target_file <your_target_image> <output_description_file>
   ...
   ```
1. Create a parameter file of feature extraction
   ```
   rosrun affine_invariant_features generate_parameter_file <feature_type> <output_parameter_file>
   ```
1. Extract features from target images
   ```
   rosrun affine_invariant_features extract_features <parameter_file> <target_file> <output_result_file>
   ...
   ```
1. Modify offline_label_detection.launch
   * args: your scene image that may contain targets
   * reference_directory: a directory where your target result files locate
   * parameter_file: your feature parameter file
1. Run
   ```
   roslaunch label_detection_example offline_label_detection.launch
   ```
   * if not detected, try smaller match_ratio
   * for less CPU usage, try positive match_stripes less than the number of CPUs
   * for online detection, try label_detection_node in the label_detection package. [launch/online_label_detection.launch](launch/online_label_detection.launch) may be helpful.
