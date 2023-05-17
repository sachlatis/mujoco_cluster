# mujoco_cluster
How to download mujoco on cluster:
Download the MuJoCo version 2.1 binaries for [Linux](https://mujoco.org/download/mujoco210-linux-x86_64.tar.gz).
Extract the downloaded mujoco210 directory into ~/.mujoco/mujoco210.

0. Create conda environment
```
$ conda create -n mujoco_env python=3.9
$ conda activate mujoco_env
$ pip install mujoco
```
1.
Install libraries with conda (normally you could install them with sudo but not in a cluster)
```
$ conda activate mujoco_env
$ conda install -c conda-forge glew
$ conda install -c conda-forge mesalib
$ conda install -c anaconda mesa-libgl-cos6-x86_64
$ conda install -c menpo glfw3
```
2. When running your code, you will want to tell mujoco which backend to use. This can be done by setting the appropriate environment variables.
```
pip install mujoco
pip install mujoco-py
```
3. Test that your mujoco works
```
$ python3
import mujoco_py
import os
mj_path = mujoco_py.utils.discover_mujoco()
xml_path = os.path.join(mj_path, 'model', 'humanoid.xml')
model = mujoco_py.load_model_from_path(xml_path)
sim = mujoco_py.MjSim(model)

print(sim.data.qpos)
# [0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]

sim.step()
print(sim.data.qpos)
# [-2.09531783e-19  2.72130735e-05  6.14480786e-22 -3.45474715e-06
#   7.42993721e-06 -1.40711141e-04 -3.04253586e-04 -2.07559344e-04
#   8.50646247e-05 -3.45474715e-06  7.42993721e-06 -1.40711141e-04
#  -3.04253586e-04 -2.07559344e-04 -8.50646247e-05  1.11317030e-04
#  -7.03465386e-05 -2.22862221e-05 -1.11317030e-04  7.03465386e-05
#  -2.22862221e-05]
```
