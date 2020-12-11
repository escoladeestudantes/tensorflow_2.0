<h2>Instalação da biblioteca TensorFlow 2.0 com CUDA 10.0 e cuDNN 7.6.4 no Ubuntu 18.04.5</h2>

<h3>Agradecimentos</h3>

<p><b>Adrian Rosebrock </b> do site PyImageSearch e <b>Manoj Kumar</b> pelo comentário sobre a não instalação do driver caso a placa de vídeo não tenha suporte para tal.</p>

<ul>
<li>https://www.pyimagesearch.com/2019/12/09/how-to-install-tensorflow-2-0-on-ubuntu/</li>
</ul>

<h3>Passo #1 - Instalação das dependências</h3>

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt-get install build-essential cmake unzip pkg-config
$ sudo apt-get install gcc-6 g++-6
$ sudo apt-get install screen
$ sudo apt-get install libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev
$ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
$ sudo apt-get install libopenblas-dev libatlas-base-dev liblapack-dev gfortran
$ sudo apt-get install libhdf5-serial-dev
$ sudo apt-get install python3-dev python3-tk python-imaging-tk
$ sudo apt-get install libgtk-3-dev

```

<h3>Passo #2 - Drivers NVIDIA, CUDA 10.0 e cuDNN 7.6.4</h3>

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
$ sudo apt-get install nvidia-driver-418
$ sudo reboot now
```
<p>Para a minha placa GTX 1660 foi instalado o driver 450.80.02 e é mostrado CUDA 11.0, mas é possível fazer o "downgrade" deste.</p>

```
$ cd ~
$ mkdir installers
$ cd installers/
$ wget https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda_10.0.130_410.48_linux
$ mv cuda_10.0.130_410.48_linux cuda_10.0.130_410.48_linux.run
$ chmod +x cuda_10.0.130_410.48_linux.run
$ sudo ./cuda_10.0.130_410.48_linux.run --override
```
<p>Minhas respostas (Obrigado Manoj Kumar):</p>
<ul>
<li><b>accept</b></li>
<li><b>n</b></li>
<li><b>y</b></li>
<li><b>Pressionar Enter</b></li>
<li><b>y</b></li>
<li><b>y</b></li>
<li><b>Pressionar Enter</b></li>
</ul>
<p>Ocorrerá erro com um trecho da observação sendo algo como:</p>
<ul>
<li><p>To install the driver using this installer, run the following command, replacing  with the name of this run file:
sudo <CudaInstaller>.run -silent -driver </p>
<p>Logfile is /tmp/cuda_install_3969.log</p></li>
</ul>
<h4>Aviso pode ser ignorado e a instalação prosseguida.</h4>

```
$ nano ~/.bashrc
```
<p>Adicionar as linhas no final do arquivo: </p>


```
# NVIDIA CUDA Toolkit
export PATH=/usr/local/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64
```

<p>Salvar o arquivo com <b>Ctrl</b> + <b>x</b> , <b>y</b> , e <b>Enter</b> para voltar ao terminal.</p>

```
$ source ~/.bashrc
$ nvcc -V
```

<p>E aparecerá no terminal:</p>

```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130
```

<p>Acessar o link a seguir, clicar na aba <b>cuDNN v7.6.4 (September 27, 2019), for CUDA 10.0</b> e posteriormente em <b>cuDNN Library for Linux</b>.</p>

<ul>
<li>https://developer.nvidia.com/rdp/cudnn-archive</li>
</ul>

```
$ cd ~/installers
$ tar -zxf cudnn-10.0-linux-x64-v7.6.4.38.tgz
$ cd cuda
$ sudo cp -P lib64/* /usr/local/cuda/lib64/
$ sudo cp -P include/* /usr/local/cuda/include/
$ cd ~
```
<h3>Passo #3 - Instalar pip e ambiente virtual</h3>

```
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python3 get-pip.py
$ pip3 install virtualenv virtualenvwrapper
$ nano ~/.bashrc
```

<p>Adicionar as linhas no final do arquivo: </p>


```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.local/bin/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
export VIRTUALENVWRAPPER_VIRTUALENV=$HOME/.local/bin/virtualenv
source $HOME/.local/bin/virtualenvwrapper.sh
```

<p>Salvar o arquivo com <b>Ctrl</b> + <b>x</b> , <b>y</b> , e <b>Enter</b> para voltar ao terminal.</p>

```
$ source ~/.bashrc
$ mkvirtualenv dl4cv -p python3
```

<p>Ambiente virtual de nome <b>dl4cv</b> foi criado e nele serão instaladas as bibliotecas (incluindo TensorFlow 2.0).</p>

```
$ pip install numpy
$ pip install tensorflow-gpu==2.0.0 #Excluir o termo '-gpu' caso seja feita para CPU
$ pip install opencv-contrib-python
$ pip install scikit-image
$ pip install pillow
$ pip install imutils
$ pip install scikit-learn
$ pip install matplotlib
$ pip install progressbar2
$ pip install beautifulsoup4
$ pip install pandas
```

<h4>Pronto!</h4>

<p>Verificar a instalação:</p>

```
$ workon dl4cv
$ python
>>> import tensorflow as tf
>>> tf.__version__
2.0.0
>>> import tensorflow.keras
>>> import cv2
>>> cv2.__version__
4.1.2
```

<p>Se for possível usar a GPU:</p>

```
$ workon dl4cv
$ python
>>> import tensorflow as tf
>>> tf.test.is_gpu_available()
True
```
