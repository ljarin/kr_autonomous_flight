


Install dependencies:

$ sudo apt install  python3-catkin-tools python3-rosdep python3-rosinstall python3-vcstool ros-noetic-tf2-sensor-msgs ros-noetic-twist-mux \
   ros-noetic-vision-msgs python3-yaml python3-pycryptodome python3-gnupg libsuitesparse-dev libv4l-dev libceres-dev \
   ros-noetic-random-numbers ros-noetic-mavros-msgs libsdl-dev libsdl-image1.2-dev

$ sudo apt-get update -y

$ sudo apt-get install libpcl-dev -y

$ sudo apt-get install -y libeigen3-dev libtbb-dev libgtest-dev

Clone Repo: (Make sure you have ssh key setup)

git clone git@github.com:ljarin/kr_autonomous_flight.git

git checkout dev_not_fixed_dt

vcs import < external_all.yaml

vcs import < motion_primitives/deps_ssh.repos # (or deps_https.ssh)

rosdep install --from-paths src --ignore-src -r -y

sudo apt install libspdlog-dev

sudo apt-get install ros-noetic-ompl

sudo apt install python3-pcl

pip3 install pandas tqdm

give path to the json file in tracker_params_mp.yaml : dispersion/graph_file: FILL IN PATH

To change planner, change `tracker_params_mp.yaml`, to run planner quickly without running quad simulation(to get control effort and tracking error), set `use_tracker_client` to false

You need three terminals to run the code:
- Terminal 1:

```
roslaunch map_plan_launch run_in_sim.launch 
```


- Terminal 2:


```
rosrun rqt_mav_manager rqt_mav_manager

```

click "motors on" and "take off" (if not running use_tracker_client, you can skip this step and directly run the evaluation script in terminal 3)



- Terminal 3: 

```
rosrun action_planner evaluate_traj_exp.py
```


To change map back to image one, see `run_in_sim.launch `


For experiment, directly run `run_in_exp.launch `, you also need to change the quadrotor name to match motion capture topic
