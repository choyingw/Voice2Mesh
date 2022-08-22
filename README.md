#  <div align="center">Cross-Modal Perceptionist</div>
CVPR 2022 "Cross-Modal Perceptionist: Can Face Geometry be Gleaned from Voices?"

Cho-Ying Wu, Chin-Cheng Hsu, Ulrich Neumann, University of Southern California

[<a href="https://arxiv.org/abs/2203.09824">Paper</a>] [<a href="https://choyingw.github.io/works/Voice2Mesh/index.html">Project page</a>] [<a href="https://drive.google.com/drive/folders/1tT36oDujNXBw5SpwhY3PiBnGIE0FbvCs?usp=sharing">Voxceleb-3D Data</a>]

[TODO]: 
2. Evaluation code
3. Training code

<p align="center">
<img src="demo/overall_purpose.png" style="width:70%;" align="centering">
</p>

We study the cross-modal learning and analyze the correlation between voices and 3D face geometry. Unlike previous methods for studying this correlation between voices and faces and only work on  the 2D domain, we choose 3D representation that can better validate the supportive evidence from the physiology of the correlation between voices and skeletal and articulator structures, which potentially affect facial geometry.

<ins>Comparison of recovered 3D face meshes with the baseline.</ins>

<p align="center">
<img src="demo/supervised_comp.png" style="width:70%;" align="centering">
</p>

<ins>Consistency for the same identity using different utterances.</ins>

<p align="center">
<img src="demo/coherence.png" style="width:70%;" align="centering"> 
</p>
    
##  <div align="center">Demo: Preprocessed fbank</div>

We test on Ubuntu 16.04 LTS, NVIDIA 2080 Ti (only GPU is supported), and use anaconda for installing packages

Install packages

1. `conda create --name CMP python=3.8`
2. Install PyTorch compatible to your computer, we test on PyTorch v1.9 (should be compatible with other 1.0+ versions)
3. install other dependency: opencv-python, scipy, PIL, Cython, pyaudio

    Or use the environment.yml we provide instead: 
    - `conda env create -f environment.yml`
    - `conda activate CMP`

4. Build the rendering toolkit (by c++ and cython) for overlapping 3D meshes on images with configurations

    ```
    cd Sim3DR
    bash build_sim3dr.sh
    cd ..
    ```

Download pretrained models and 3DMM configuration data

5. Download from [<a href="https://drive.google.com/file/d/1tqTSDrVVL3LkOWN-hduELm3YkWJ2ZUqu/view?usp=sharing">here</a>] (~160M) and unzip under the root folder. This will create 'pretrained_models' and 'train.configs' under the root folder. 

Read the preprocessed fbank for inference 

6. `python demo.py` (This will fetch the preprocessed MFCC and use them as network inputs)
7. Results will be generated under `data/results/` (pre-generated references are under `data/results_reference`)

More preprocessed MFCC and 3D mesh (3DMM params) pairs can be downloaded: [<a href="https://drive.google.com/drive/folders/1tT36oDujNXBw5SpwhY3PiBnGIE0FbvCs?usp=sharing">Voxceleb-3D Data</a>].

##  <div align="center">Demo: Use device mic input </div>

1. Do the above 1-5 step. Plus, download the <a href="https://drive.google.com/file/d/1A9NKnlkvmcd8U17EuuI00YfPnPdjSsgM/view?usp=sharing">mean female</a> and <a href="https://drive.google.com/file/d/1UcW2HP5RsqPSRxel0vmE6Vzi4EFUXGSV/view?usp=sharing">mean male</a> mesh.

2. `python demo_mic.py` The demo will take 5 seconds recording from your device and predict the face mesh. 

We perform unsupervised gender classfication based on mean male and female shape and calculate the statistics between the predicted face and mean shape. Also we calculate the distance between the four types of faces (Regular, Slim, Skinny, Wide)and indicate which type the voice is closer to.

3. Results will be generated under data/results

##  <div align="center">Citation</div>
If you find our work useful, please consider to cite us.

    @inproceedings{wu2022cross,
    title={Cross-Modal Perceptionist: Can Face Geometry be Gleaned from Voices?},
    author={Wu, Cho-Ying and Hsu, Chin-Cheng and Neumann, Ulrich},
    booktitle={CVPR},
    year={2022}
    }


This project is developed on [<a href="https://github.com/choyingw/SynergyNet">SynergyNet</a>], [<a href="https://github.com/cleardusk/3DDFA_V2">3DDFA-V2</a>] and [<a href="https://github.com/cmu-mlsp/reconstructing_faces_from_voices">reconstruction-faces-from-voice</a>]
