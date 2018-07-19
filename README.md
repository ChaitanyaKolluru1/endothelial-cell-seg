# Endothelial Cell Segmentation

Software allows for segmenting cells in the endothelial layer of cornea using deep learning techniques (currently U-Net). 

## Getting Started

Graphical Processing Units (GPU) cards are required for quick neural network training and testing. This code is designed to work well with the GPU nodes (systems) at Case Western Reserve University's High Performance Cluster (HPC). Please create an account for yourself on the cluster under Dr. Wilson's account. Send an email to hpc-support@case.edu for the same and cc Dr. Wilson. All instructions regarding using the cluster are at: https://sites.google.com/a/case.edu/hpc-upgraded-cluster/home. Sign up for their interactive seminars during the semester: https://canvas.case.edu/courses/3014. This step is required if you want to train and test the neural networks and modify the code. If you just want to look at the code for now, you don't have to do this.

### Accessing the HPC and getting things ready

Files on the HPC can be accessed using WinSCP software. This software allows one to copy files to/from the cluster and edit existing files on the cluster. Every user gets a folder on the HPC to work in (something like /home/<CaseID>/). Next, to run commands, you can use MobaXTerm or similar software to connect to the HPC (rider.case.edu), with an SSH connection. Enter your Case credentials to start a session. After you have an SSH connection, there are two ways to run your software:

- Interactive mode: You request the resource you need (CPU/GPU, RAM, cores, time etc.), get the resource, and then run a file.
- Job (batch) mode: You submit a job script that contains commands, and the script will be run when the resources you request (CPU/GPUs) are available. You don't have to wait if the resources you need aren't readily available in this case.

I'll demonstrate the interactive mode now. First, we request a GPU node (essentially just a PC which has some graphic cards on it):
```
srun --x11 -p gpu -C gpup100 -N 1 -c 12 --gres=gpu:2 --mem=186g --time=72:00:00 --pty /bin/bash
```
This requests a NVIDIA P100 GPU with 1 CPU (N), 12 cores (-c), 2 P100 cards (gpu:2), 186 GB of RAM (mem) for 72 hours (time). It opens a command line interface (/bin/bash) to such a system. IMPORTANT: You have to free resources back when you are done. To do this, type exit before closing your session.

There are two ways to run deep learning software:
1. Use the readily available tensorflow module in the HPC. For that, we run the following:
```
export OMP_NUM_THREADS=1
module swap intel gcc
module load tensorflow
```
You now have access to a GPU system with tensorflow and keras libraries loaded. If you want to see the versions:
```
python
import tensorflow as tf
tf.__version__
import keras as K
K.__version__
```
Currently, Tensorflow 1.4.0 and Keras 2.1.3 are installed. Modules are maintained by the HPC staff, and might not contain all the python libraries that we might need. Request for adding new libraries to the module can be done by writing to hpc-support@case.edu.

2. Use a singularity image that we (our lab) can control. New python libraries can be installed on this image which can be executed on the cluster.
```
module load gcc cuda singularity
singularity shell --nv /home/cxk340/singularity_image/keras_tf.img
```

Both these methods will give you a shell that can run python with the deep learning libraries (keras, tensorflow) available. We can now run our software.

### Folder organization



## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
