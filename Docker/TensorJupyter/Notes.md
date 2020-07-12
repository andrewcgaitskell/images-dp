
https://www.tensorflow.org/install/docker

docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter

To run a TensorFlow program developed on the host machine within a container,
mount the host directory and change the container's working directory (-v hostDir:containerDir -w workDir):

docker run -it --rm -v $PWD:/tmp -w /tmp tensorflow/tensorflow python ./script.py

Permission issues can arise when files created within a container are exposed to the host. It's usually best to edit files on the host system.

Start a Jupyter Notebook server using TensorFlow's nightly build with Python 3 support:

docker run -it -p 8888:8888 tensorflow/tensorflow:nightly-py3-jupyter

docker run -it -p 8888:8888 -v $PWD:/tmp -w /tmp tensorflow/tensorflow:nightly-py3-jupyter
