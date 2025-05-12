# TabStructNet
## Table Structure Recognition using Top-Down and Bottom-Up Cues


This code is developed using the code from 
1. https://github.com/matterport/Mask_RCNN
1. https://github.com/shahrukhqasim/TIES-2.0 

```
Download necessary files. For download locations and links please refer to note.txt files in the following folders:
1. https://github.com/sachinraja13/TabStructNet/tree/master/coco_model/coco
2. https://github.com/sachinraja13/TabStructNet/tree/master/trained_model/tab/annotations
3. https://github.com/sachinraja13/TabStructNet/tree/master/trained_model/tab/logs/tab20200821T0923
```

```
To train the model using MS coco weights, execute:
python samples/tabnet/tabnet.py train --dataset=trained_model/tab --model=coco
```

```
To train the model using most recently saved weights, execute:
python samples/tabnet/tabnet.py train --dataset=trained_model/tab --model=last
```

```
To evaluate the model using most recently saved weights, execute:
python samples/tabnet/tabnet.py evaluate --dataset=trained_model/tab --model=last
```

Saved weights provided in the Google Drive link are trained using SciTSR dataset.
UNLV train and test split is added in the repository for easy fine-tuning on UNLV and testing.

```
To generate output XML:
1. Execute the TabStructNet model for evaluation as specified in the repository's README.
2. Copy the 4 result folders generated in the trained_model/tab directory to the results folder inside the rename_output_files folder.
3. Execute rename_maskrcnn_result_files.py
4. Copy the 4 result folders generated inside rename_output_files/rename_results to xml_generating_postprocessor directory.
5. Copy the validation JPEG images inside xml_generating_postprocessor/gt_without_box folder.
6. Execute cell_postprocessor_adj.py 
XMLs are generated in processed_xmls folder.
```

##### Please refer to https://github.com/matterport/Mask_RCNN initially for any issues in running the script.


Please use this to cite our work:
```
@misc{raja_2020,
  title={Table Structure Recognition using Top-Down and Bottom-Up Cues},
  author={Sachin Raja, Ajoy Mondal, C V Jawahar},
  year={2020},
  publisher={Springer Science+Business Media},
  journal={Accepted to ECCV-6007}
}
```

## References:
* Mask R-CNN for object detection and instance segmentation on Keras and TensorFlow; Waleed Abdulla; 2017; https://github.com/matterport/Mask_RCNN

* Schreiber, S., Agne, S., Wolf, I., Dengel, A., Ahmed, S.: DeepDeSRT: Deep learning for detection and structure recognition of tables in document images. In: ICDAR. (2017)

* Qasim, S.R., Mahmood, H., Shafait, F.: Rethinking table parsing using graph neural networks. In: ICDAR. (2019)

* Tensmeyer, C., Morariu, V., Price, B., Cohen, S., Martinezp, T.: Deep splitting and merging for table structure decomposition. In: ICDAR. (2019)

* Shahab, A., Shafait, F., Kieninger, T., Dengel, A.: An open approach towards the  benchmarking of table structure recognition systems. In: DAS. (2010)

* Chi, Z., Huang, H., Xu, H.D., Yu, H., Yin, W., Mao, X.L.: Complicated table structure recognition. arXiv (2019)

* Li, M., Cui, L., Huang, S., Wei, F., Zhou, M., Li, Z.: TableBank: Table benchmark for image-based table detection and recognition. In: ICDAR. (2019)


## 環境版本問題處理
方法一(舊版本環境：tensorflow==1.13.1)：  
用 anaconda 安裝 python 3.6 版本，執行 conda create -n env_old python=3.6，避免和 tensorflow==1.13.1 的相容性問題  
將 requirements.txt 的 opencv 版本改成 opencv-python==4.1.2.30，避免版本問題  
安裝 pycocotools，執行 pip install pycocotools  
最後問題：ERROR: Could not build wheels for pycocotools which use PEP 517 and cannot be installed directly  

方法二(新版本環境)：  
指定 Python 版本為 3.12，因 tensorflow 最新版不支援最新的 Python 版本  
去除 requirements.txt 中所有的版本指定(tensorflow、keras)  
降 numpy 版本到2.0 以下，執行 pip install numpy<2.0，因為和 imgaug 套件不相容  
最後問題：ModuleNotFoundError: No module named 'keras.engine' => 需舊版 tensorflow(2.2)，python 版本(3.6)也需舊版  

方法三(tensorflow==2.11.1)：  
conda create -n env_2.11.1 python=3.9
pip install numpy<2.0
ModuleNotFoundError: No module named 'pycocotools' =>  pip install pycocotools
ModuleNotFoundError: No module named 'mrcnn' =>  pip install mrcnn
AttributeError: module 'keras.engine' has no attribute 'Layer'