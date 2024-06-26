# Low_Light_Image_enhancement
PSNR : 27.6

Low-light image enhancement is a crucial subfield of computer vision focused on improving image clarity captured in dim lighting. Conventional techniques often demand reference images or manual adjustments, which are not always practical. The Zero-DCE (Zero-Reference Deep Curve Estimation) framework offers a groundbreaking solution by enhancing low-light images without needing reference images or extensive preprocessing. This framework's main advantage is its ability to function without paired low-light and normal-light images, making it highly versatile. Additionally, Zero-DCE is lightweight, making it ideal for devices with limited computational power, such as smartphones. It achieves fine-tuned enhancement by estimating pixel-wise and high-order tonal curves from the input image. By iteratively refining these curves, Zero-DCE effectively manages various lighting conditions within a single frame.

Unlike traditional methods, Zero-DCE does not require paired input/output image data for training. Instead, it uses non-reference loss functions that evaluate the enhancement quality of the images.

These functions are designed to be differentiable and can assess the quality of the enhanced image without needing reference images. They effectively guide the network's learning process, ensuring the output images are optimally enhanced.

Exposure Loss

This function ensures the enhanced image has appropriate overall brightness. It calculates the loss based on deviations of the mean brightness of non-overlapping patches from a target value E. Initially, the RGB channels are averaged to get the overall brightness of each pixel. The loss is then computed by applying average pooling over patches and comparing their brightness to E.

Illumination Smoothness Loss

This function promotes smooth and gradual changes in brightness across the image, avoiding abrupt transitions. It calculates the differences in brightness between neighboring pixels vertically (∇y) and horizontally (∇x), then averages these differences over all pixels and images in the batch

Color Constancy Loss

The goal of this loss function is to maintain a balanced color representation in the enhanced image. It computes the loss based on the mean color values of the red, green, and blue channels, penalizing deviations from ideal color balance. The function calculates the squared differences between the mean values of each pair of channels (p and q), and then returns the square root of the sum of these differences.

Spatial Consistency Loss

This loss function focuses on maintaining the spatial coherence of feature maps across consecutive training epochs. It ensures that the average intensity values of local regions in the enhanced image (denoted as Y) are consistent with those in the input image (denoted as I). By preserving the relative differences between neighboring regions, this loss function helps enhance the image without losing spatial consistency.
