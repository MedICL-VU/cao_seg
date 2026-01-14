# Automated CAO segmentation
This repository is for training the Segmentation model. For any questions, please send emails/slacks.

# Authors
* **Maintainer:** Jane (kanyifeechukwu.j.oguine@Vanderbilt.Edu)


  
**TLDR**

put [checkpoint](https://vanderbilt.app.box.com/folder/310974131184) at same level of "test_one_line.py" and "test_one_line_import.py"
```
python test_one_line.py --input_dir <YOUR_INPUT_DIR> ---output_dir <YOUR_OUTPUT_DIR>
```
input directory contains raw frames, 1080x1920, and the same size results are saved in output_dir

This repo is generic and will continue to be updated/organized.

**Quick visualization**
<p align="center">
    <img src="/assets/part_all.gif" width="1000"/> <br />
</p>
(compression issue occurs in top row)

## News
- **2025-03-06:** Integrated Mobileone_S1 in the framework.
- **2025-03-05:** Integrated a modified SAM2 in the framework.
- **2025-01-21:** Automated segmentation framework with generic U-Net is built.

## Workflow for monocular endoscopic segmentation and depth estimation
1. preprocess raw videos
2. use pretrained models to generate pseudo-labels, such as our pretrained model for segmentation and depth maps or pretrained foundation models (sam and depth-anything)
3. clean pseudo-labels
4. train

## Getting ready

**Installation**

```
git clone https://github.com/ALISS-ARPAH/CAO_seg
cd CAO_seg
conda create -n cao_seg python=3.9
conda activate cao_seg
pip install -r requirements.txt
```


**before training**
1. [preprocess](https://github.com/ALISS-ARPAH/CAO_seg/tree/main/src/data/preprocessing) data
2. generate [data split](http://github.com/ALISS-ARPAH/CAO_seg/tree/main/src/data/get_split) for training
3. If you want to use pretrained weights of SAM2, [download](https://dl.fbaipublicfiles.com/segment_anything_2/072824/sam2_hiera_large.pt) and place it under [sam2_checkpoints](https://github.com/ALISS-ARPAH/CAO_seg/src/sam2_checkpoints) folder 


## Get started
**Train**

```
python train.py --name <YOUR_RUNNING_NAME> --json_path <YOUR_SPLIT_PATH>
```


**Test**

``` 
python test.py --test_data_dir <YOUR_DATA_FOLDER> --name <YOUR_RUNNING_NAME>
```

To save the predictions ```--save_results --save_results_dir <YOUR_SAVE_RESULTS_DIR>```


Either put pretrained file in the checkpoints/<--name>/cp/ (I suggest running train.py first for 1-2 minutes and folders will be created automatically)

or use --pretrained_path


**Batch testing**

``` 
python test_batch.py
```

You need to **manually** modify the arguments in this Python file. Currently, it only supports the frames stored in subfolders of a given parent folder. 

```bash
parent_folder/
├── video1/
│   ├── frames/
├── video2/
│   ├── frames/
├── video3/
│   ├── frames/
```

## Get it done

1. Check Python files in the post_analysis folder for generating overlayed videos or images.


## License

The model is licensed under the [Apache 2.0 license](LICENSE)




## Questions

Please send an email to hao.li.1@vanderbilt.edu or Slack me for any questions, and I am always happy to help! :)



## limitations

a lot

