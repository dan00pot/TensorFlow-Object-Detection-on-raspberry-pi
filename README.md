# Tensorflow-object-detection-on-raspberry-pi

1. cai he dieu hanh raspbian cho raspberry ( google)

+ tai file 

+ flash den the nho (tot nhat nen dung the >16GB class 10)

+ them file rong SSH de bat che do SSH cho raspbery 

2. thiet lap vnc de control desktop cho raspbery
+ cai dat thu vien vnc

      sudo apt-get update 
      sudo apt-get install realvnc-vnc-server

+ config raspberry de bat VNC

	    sudo raspi-config       ->   Interfacing Options > VNC and select Yes.
  
3. cai tensorflow vao raspberry pi
+ update raspberry	
	
      sudo apt-get update
	    sudo apt-get dist-upgrade
  
+ tao thu muc chua tensorflow

	    mkdir tf
	    cd tf

+ tai xuong tensorflow va cai dat

      wget https://github.com/lhelontra/tensorflow-on-arm/releases/download/v1.8.0/tensorflow-1.8.0-cp35-none-linux_armv7l.whl
      sudo pip3 install /home/pi/tf/tensorflow-1.8.0-cp35-none-linux_armv7l.whl

+ them thu vien

      sudo apt-get install libatlas-base-dev
      
***lxml chứa các mô-đun C cần được biên dịch để cài đặt đúng. Tuy nhiên, việc biên dịch các mô-đun C đó cũng dựa trên việc bạn đã cài đặt một số "thư viện phát triển". Các thư viện phát triển này là các thư viện C, không phải Python và vì vậy các pip sẽ không thể tự động tải chúng từ internet và cài đặt chúng cho bạn.
Do đó, bạn sẽ cần phải tự cài đặt các thư viện phát triển này, rất có thể là sử dụng trình quản lý gói của bạn. Trong một hệ thống Debian (như Ubuntu), đây là ...

	    sudo apt-get install libxml2-dev libxslt-dev
  
Điều này sẽ cài đặt các thư viện phát triển libxml2 và libxslt vào hệ thống cục bộ của bạn. Nếu bạn thử lại để cài đặt lxml, bước biên dịch mô-đun C sẽ hoạt động vì bây giờ các thư viện phát triển này đã có trên hệ thống của bạn.***

    	sudo pip3 install pillow lxml jupyter matplotlib cython
      sudo apt-get install python-tk
      
+ install opencv

    	sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
	    sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
	    sudo apt-get install libxvidcore-dev libx264-dev
      sudo apt-get install qt4-dev-tools
	    pip3 install opencv-python
      
+bien dich va cai dat protobuf
      
      sudo apt-get install autoconf automake libtool curl
      wget https://github.com/google/protobuf/releases/download/v3.6.1/protobuf-all-3.6.1.tar.gz
      tar -zxvf protobuf-all-3.6.1.tar.gz
      cd protobuf-3.6.1
      ./configure (dinh cau hinh)
      make (xay dung goi)
      make check  (xay dung cai dat goi khong can thiet lam ???)
      sudo make install
      cd python
      export LD_LIBRARY_PATH=../src/.libs  (xuat duong dan  thu vien)
      python3 setup.py build --cpp_implementation 
      python3 setup.py test --cpp_implementation
      sudo python3 setup.py install --cpp_implementation
      export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=cpp (duong dan protobuf)
      export PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION_VERSION=3
      sudo ldconfig
      
+ cuoi cung thi reboot lai raspberry

+ thiet lap cau truc tensorflow va bien pythonpath

	    mkdir tensorflow1
	    cd tensorflow1
	    git clone --recurse-submodules https://github.com/tensorflow/models.git
	    sudo nano ~/.bashrc (sua file bash de link duong dan tensorflow)

export PYTHONPATH=$PYTHONPATH:/home/pi/tensorflow1/models/research:/home/pi/tensorflow1/models/research/slim (them vao o dong cuoi cua file bash)
 
	    cd /home/pi/tensorflow1/models/research (di chuyen den research cua file model)
	    protoc object_detection/protos/*.proto --python_out=. (chuyen cacs proto name thanh 	name_pb2.py) 
	    cd /home/pi/tensorflow1/models/research/object_detection (di chuyen de thu muc 	mau cua model)
      wget http://download.tensorflow.org/models/object_detection/ssdlite_mobilenet_v2_coco_2018_05_09.tar.gz
     	tar -xzvf ssdlite_mobilenet_v2_coco_2018_05_09.tar.gz
      
+ bat camera trong rasp-config 
 
      wget https://raw.githubusercontent.com/EdjeElectronics/TensorFlow-Object-Detection-on-the-RaspberryPi/master/Object_detection_picamera.py (mau code cho picamera)
      python3 Object_detection_picamera.py 
      python3 Object_detection_picamera.py --usbcam
 
luu y code nhung vi tri quan trong <3

	
