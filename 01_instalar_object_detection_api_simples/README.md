<h3>TensorFlow – Instalação Object Detection API no Ubuntu 18.04.5</h3>

<h4>Referências</h4>

<ul>
<li>https://medium.com/@karol_majek/10-simple-steps-to-tensorflow-object-detection-api-aa2e9b96dc94</li>
<li>https://medium.com/@teyou21/setup-tensorflow-for-object-detection-on-ubuntu-16-04-e2485b52e32a</li>
<li>https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2.md</li>
</ul>

<b>Seguir procedimento para instalação da biblioteca TensorFlow 2.0</b>

<p>Abrir terminal</p>

```
cd ~
sudo apt install -y git
git clone https://github.com/tensorflow/tensorflow
cd tensorflow
git clone https://github.com/tensorflow/models
```

```
sudo apt-get install protobuf-compiler python-pil python-lxml python-tk
pip3 install Cython
pip3 install contextlib2
pip3 install jupyter
pip3 install matplotlib
pip3 install  pandas
```

<h4>Instalar COCO API</h4>
<p>Substituir o caminho <b>/home/edee/</b> conforme está no seu computador. </p>

```
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
make
cp -r pycocotools /home/edee/tensorflow/models/research
```

<h4>Instalar protoc</h4>

<p>Substituir o caminho <b>/home/edee/</b> conforme está no seu computador. </p>

```
cd /home/edee/tensorflow/models/research
protoc object_detection/protos/*.proto --python_out=.

```

<h4>Instalar detecção de objetos</h4>

<p>Substituir o caminho <b>/home/edee/</b> conforme está no seu computador. </p>

```
nano ~/.bashrc

#TensorFlow - Adicionar na ultima linha
export PYTHONPATH=$PYTHONPATH:/home/edee/tensorflow/models/research/:/home/edee/tensorflow/models/research/slim

source ~/.bashrc
```
