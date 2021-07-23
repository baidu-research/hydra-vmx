# OpenVINO

## Overview
OpenVINO™ toolkit is a comprehensive toolkit for quickly developing applications and solutions that solve a variety of tasks including emulation of human vision, automatic speech recognition, natural language processing, recommendation systems, and many others. Based on latest generations of artificial neural networks, including Convolutional Neural Networks (CNNs), recurrent and attention-based networks, the toolkit extends computer vision and non-vision workloads across different hardware including EdgeBoard-VMX, maximizing performance.

OpenVINO can be installed on Linux, Windows, MacOS, RaspberryPI and so on, we will use Linux as the example here.


## Installation
Take either of the following to install the OpenVINO:
- [Install Intel® Distribution of OpenVINO™ toolkit for Linux](https://docs.openvinotoolkit.org/latest/openvino_docs_install_guides_installing_openvino_linux.html)
- [Version 2021.4](https://docs.openvinotoolkit.org/2021.4/openvino_docs_install_guides_installing_openvino_linux.html)

Unpack:
```
tar -xvzf l_openvino_toolkit_p_<version>.tgz
cd l_openvino_toolkit_p_<version>
```

Install
```
sudo ./install_GUI.sh		// GUI
sudo ./install.sh   		// Command Line
```

Please strictly follow to finish the installation procedure (package 2021.4 is provided as reference).
- Introduction
- Requirements
- Overview
- Install OpenVINO™ Toolkit Core Components
- Install External Software Dependencies
- Set the Environment Variables
- Configure the Model Optimizer


## Setup

Add current Linux user to the users group:
```
sudo usermod -a -G users "$(whoami)"
```

Instal the USB rules:
```
sudo cp /opt/intel/openvino_2021/inference_engine/external/97-myriad-usbboot.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger
sudo ldconfig
```


## Scripts Sample

Image Classification:
```
cd ${INTEL_OPENVINO_DIR}/deployment_tools/demo
eog car.png

./demo_squeezenet_download_convert_run.sh -d MYRIAD

	Top 10 results:
	Image /home/user/dldt/inference-engine/samples/sample_data/car.png
	classid probability label
	------- ----------- -----
	817     0.8363345   sports car, sport car
	511     0.0946488   convertible
	479     0.0419131   car wheel
	751     0.0091071   racer, race car, racing car
	436     0.0068161   beach wagon, station wagon, wagon, estate car, beach waggon, station waggon, waggon
	656     0.0037564   minivan
	586     0.0025741   half track
	717     0.0016069   pickup, pickup truck
	864     0.0012027   tow truck, tow car, wrecker
	581     0.0005882   grille, radiator grille
	total inference time: 2.6642941
	Average running time of one iteration: 2.6642941 ms
	Throughput: 375.3339402 FPS
	[ INFO ] Execution successful
```

Inference Pipeline:
```
./demo_security_barrier_camera.sh -d MYRIAD
```
<img src="vmx-openvino-inference.jpg" height="30%" width="30%">

Benchmark:
```
./demo_benchmark_app.sh -d MYRIAD
```


## Code Application
- [Use the Model Downloader to download suitable models](https://docs.openvinotoolkit.org/latest/openvino_docs_get_started_get_started_linux.html#download-models)
- [Convert the models with the Model Optimizer](https://docs.openvinotoolkit.org/latest/openvino_docs_get_started_get_started_linux.html#convert-models-to-intermediate-representation)
- [Download media files to run inference on](https://docs.openvinotoolkit.org/latest/openvino_docs_get_started_get_started_linux.html#download-media)
- [Run inference on the Image Classification Code Sample and see the results](https://docs.openvinotoolkit.org/latest/openvino_docs_get_started_get_started_linux.html#run-image-classification)
- [Run inference on the Security Barrier Camera Demo application and see the results](https://docs.openvinotoolkit.org/latest/openvino_docs_get_started_get_started_linux.html#run-security-barrier)

Building:
```
cd $INTEL_OPENVINO_DIR/inference_engine_samples/cpp
# to compile C samples, go here also: cd <INSTALL_DIR>/inference_engine/samples/c
build_samples.sh
cd $INTEL_OPENVINO_DIR/deployment_tools/open_model_zoo/demos
build_demos.sh
```

Executables:
```
~/inference_engine_samples_build/intel64/Release
~/inference_engine_cpp_samples_build/intel64/Release
~/inference_engine_demos_build/intel64/Release
```

Command Template:
```
<path_to_app> -i <path_to_media> -m <path_to_model> -d MYRIAD
./object_detection_demo_ssd_async -i ~/Videos/catshow.mp4 -m ~/ir/fp32/mobilenet-ssd.xml -d MYRIAD
```

Entire Command Example:
```
object_detection + head pose
./object_detection_demo_ssd_async -i ~/Videos/catshow.mp4 -m ~/ir/fp32/mobilenet-ssd.xml -d CPU -m_hp headpose.xml -d_hp MYRIAD

object_detection + head pose + age-gender
./object_detection_demo_ssd_async -i ~/Videos/catshow.mp4 -m ~/r/fp32/mobilenet-ssd.xml -d CPU -m_hp headpose.xml -d_hp MYRIAD -m_ag age-gender.xml -d_ag MYRIAD
```


## Others
- [Install From Images](https://docs.openvinotoolkit.org/2021.4/openvino_docs_install_guides_installing_openvino_images.html)
- [Security](https://docs.openvinotoolkit.org/2021.4/openvino_docs_security_guide_introduction.html)

