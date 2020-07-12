
https://www.tensorflow.org/install/docker

docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter

To run a TensorFlow program developed on the host machine within a container,
mount the host directory and change the container's working directory (-v hostDir:containerDir -w workDir):

docker run -it --rm -v $PWD:/tmp -w /tmp tensorflow/tensorflow python ./script.py

Permission issues can arise when files created within a container are exposed to the host. It's usually best to edit files on the host system.

Start a Jupyter Notebook server using TensorFlow's nightly build with Python 3 support:

docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter

docker run -it -p 8888:8888 -v $PWD:/tmp -w /tmp tensorflow/tensorflow:nightly-py3-jupyter


docker run -it -p 8888:8888 -v $PWD:/tmp -w /tmp tensorflow/tensorflow:nightly-py3-jupyter --notebook-dir=/Users/andrewgaitskell/Code/images-dp/Docker/TensorJupyter/tmp

docker run --runtime=nvidia -it 
    --name tensorflow -p 8888:8888 
    -v /home/kneazle/data/KITTI:/data_host/KITTI kneazle/tf_od_api:part1

How can I use my local files for the Jupyter notebook running in Docker?
docker jupyter-notebook volume docker-container
share improve this question
edited Jan 5 '19 at 22:48
hhh
40.8k5252 gold badges139139 silver badges239239 bronze badges
asked Nov 2 '18 at 11:18
kneazle
1391111 bronze badges

    I think your close to having it figured out --notebook-dir is the directory your seeing in jupyter, that is /tensorflow/models/research/object_detection, so you need to mount your data in a subdirectory of that directory on the container. Try: -v /home/aev21/data/KITTI:/tensorflow/models/research/object_detection/data_host/KITTI – William D. Irons Nov 2 '18 at 19:09


docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx:latest
  
docker run -it \
--name data1 \
--mount type=bind,source="$(pwd)"/data,target=/notebook \
-p 8888:8888 \
-w /notebook tensorflow/tensorflow:nightly-py3-jupyter \
--notebook-dir=/notebook

docker run -it -p 8888:8888 -v /Users/andrewgaitskell/Code/images-dp/Docker/TensorJupyter/tmp:/tf/ tensorflow/tensorflow:nightly-py3-jupyter
