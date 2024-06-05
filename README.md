# Metal Surface Defect Detection with Transfer Learning and Ensembling

This project implements a metal surface defect detection model using transfer learning and ensembling techniques.

## Project Description

This repository contains the code and resources for a metal surface defect detection model. The model leverages pre-trained deep learning models (transfer learning) and combines their predictions using ensembling to achieve relatively high accuracy in classifying various defect types. For this project i used five pre-trained models including: EfficientNetB5, ResNet50V2, IncpetionV3, MobileNet and VGG19. The imagenet dataset that these models were trained on was normalized in a different way between different models, for example EfficientNetB5 was trained on images where tensor values were between 0 and 255, while for ResNet50V2 these values were between 0 and 1. Because of this, training and validation datasets where scaled appropriately on the fly. To ensemble multiple models that require different preprocessing steps for their inputs i ensured that each model receives its appropriately preprocessed input. This was achieved by creating separate models that apply preprocessing inside their respective sub-networks and then combining their outputs.

## About the Dataset

This dataset (also referred to as he GC10-DET dataset) was taken from kaggle [1]. GC10-DET is a metal surface defect dataset that was collected in a real industry enviroment. It contains ten types of surface defects:
- __punching (Pu)__: In the production line of the strip, the steel strip needs to be punched according to the product specifications; mechanical failure may lead to unwanted punching, resulting in punching defects.
- __weld line (Wl)__: When the strip is changed, it is necessary to weld the two coils of the strip, and the weld line is produced. Strictly speaking, this is not a defect, but it needs to be automatically detected and tracked to be circumvented in subsequent cuts.
- __crescent gap (Cg)__: In the production of steel strip, cutting sometimes results in defects, just like half a circle.
- __water spot (Ws)__: A water spot is produced by drying in production. Under different products and processes, the requirements for this defect are different. However, because the water spots are generally with low contrast, and are similar to other defects such as oil spots, they are usually detected by mistake.
- __oil spot (Os)__: An oil spot is usually caused by the contamination of mechanical lubricant, which will affect the appearance of the product.
- __silk spot (Ss)__: A local or continuous wave-like plaque on a strip surface that may appear on the upper and lower surfaces, and the density is uneven in the whole strip length direction. Generally, the main reason lies in the uneven temperature of the roller and uneven pressure.
- __inclusion (In)__: Inclusion is a typical defect of metal surface defects, usually showing small spots, fish scale shape, strip shape, block irregular distribution in the strip of the upper and lower surface (global or local), and is often accompanied by rough pockmarked surfaces. Some inclusions are loose and easy to fall off and some are pressed into the plate.
- __rolled pit (Rp)__: Rolled pits are periodic bulges or pits on the surface of a steel plate that are punctate, flaky, or strip-like. They are distributed throughout the strip length or section, mainly caused by work roll or tension roll damage.
- __Crease (Cr)__: A crease is a vertical transverse fold, with regular or irregular spacing across the strip, or at the edge of the strip. The main reason is the local yield along the moving direction of the strip in the uncoiling process.
- __waist folding (Wf)__: There are obvious folds in the defect parts, a little more popular, a little like wrinkles, indicating that the local deformation of the defect is too large. The reason is due to low-carbon.

When performing exploratory data analysis i uncovered that the dataset is pretty unbalanced. With the total number of images in the dataset being 2306, number of images in the __silk spot (Ss)__ category containing 650 images and __rolled pit (Rp)__ category containing only 31. Therefore class weighting needs to be implemented.

## Further Developement

Generally this model may be too big to be used in any real world scenarios. To overcome this issue another ensemble configuration can be explored. Also with the introduction of quantization [2], model size could be significantly reduced. Model performance could be further improved with aditional data augmentation strategies as well as collecting more data into a more balanced dataset.

Any feedback or contributions are more then welcome! 😁

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Cool Links and Referrences

[1]  [Defects location for metal surface](https://www.kaggle.com/datasets/zhangyunsheng/defects-class-and-location/data)

[2]  [Quantization for Neural Networks - Lei Mao](https://leimao.github.io/article/Neural-Networks-Quantization/)
