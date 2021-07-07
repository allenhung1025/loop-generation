# loop-generation
Open source of ISMIR-21 submission, “A Benchmarking Initiative for Audio-domain Music Generation using the FreeSound Loop Dataset”
## Quick Start
* Generate loops from looperman pretrained model
``` bash
$ gdown --id 1GQpzWz9ycIm5wzkxLsVr-zN17GWD3_6K -O looperman_checkpoint.pt
$ CUDA_VISIBLE_DEVICES=2 python generate_audio.py \
    --ckpt "looperman_checkpoint.pt" \
    --pics 100 --data_path "./data/looperman" \
    --store_path "./generated_looperman_one_bar"
``` 
* Generate loops from freesound pretrained model
``` bash
$ gdown --id 197DMCOASEMFBVi8GMahHfRwgJ0bhcUND -O freesound_checkpoint.pt 
$ CUDA_VISIBLE_DEVICES=2 python generate_audio.py \
    --ckpt "freesound_checkpoint.pt" \
    --pics 100 --data_path "./data/freesound" \
    --store_path "./generated_freesound_one_bar"
``` 
## Pretrained Checkpoint
* [Looperman pretrained model link](https://drive.google.com/file/d/1GQpzWz9ycIm5wzkxLsVr-zN17GWD3_6K/view?usp=sharing) 
* [Freesound pretrained model link](https://drive.google.com/file/d/197DMCOASEMFBVi8GMahHfRwgJ0bhcUND/view?usp=sharing)

## Preprocess the Loop Dataset
In the `preprocess` directory and modify some settings(e.g. data path) in the codes and run them with the following orders
``` bash
$ python trim_2_seconds.py
$ python extract_mel.py
$ python make_dataset.py
$ python compute_mean_std.py 
```
## Train the Model
``` bash
CUDA_VISIBLE_DEVICES=2 python train_drum.py \
    --size 64 --batch 8 --sample_dir [sample_dir] \
    --checkpoint_dir [checkpoint_dir]\
    [mel-spectrogram dataset from the proprocessing]
```
* checkpoint_dir stores model in the designated directory.
* sample_dir stores mel-spectrogram generated from the model.
* You should give the data directory in the end.

## References
* The code comes heavily from [StyleGAN2 from rosinality][stylegan2] 
* [unagan from ciaua][unagan].

[stylegan2]: https://github.com/rosinality/stylegan2-pytorch
[unagan]: https://github.com/ciaua/unagan