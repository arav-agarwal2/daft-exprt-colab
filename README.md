Visit the [real daft-exprt github page](https://github.com/ubisoft/ubisoft-laforge-daft-exprt) for more information.

To make the above work in Colab, you will *probably* need access to Colab's terminal, which will require Colab pro
  [ This is probably removable, but I have no clue on how to do it ]
  
Steps:
- Create a cell that does the following, and run it.
```
!wget -O mini.sh https://repo.anaconda.com/miniconda/Miniconda3-py38_4.8.2-Linux-x86_64.sh
!chmod +x mini.sh
!bash ./mini.sh -b -f -p /usr/local
```
- Run the following steps in the terminal
```
eval "$(conda shell.bash hook)" 
conda create -n daft_exprt python=3.8 -y 
conda activate daft_exprt
conda config --add channels conda-forge
conda install montreal-forced-aligner
pip install -r pip_requirements.txt
pip install pyworld
pip install -e ../.[pytorch] --find-links https://download.pytorch.org/whl/torch_stable.html
make MFA_pretrained
conda install ipykernel
```

That's it! When running scripts, please use:
```
/usr/local/envs/daft_exprt/bin/python
```
instead of python, and the jupyter notebook itself does not "really" work yet.

It's generally recommended to use the GPU only on the actual model training. 

Main Changes:
- Changed REAPER to pyworld, so that GLIBC 2.29 errors are avoided
- Updated MFA install to most recent version, which changes some parameters
- Found a solid method of getting conda with environments 'working' [ Can we just support it? ]
