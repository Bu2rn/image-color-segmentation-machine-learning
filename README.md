# image-color-segmentation-machine-learning
 % Load the image
im = imread('arabidopsis_image.jpg');

% Convert the image to the HSV color space
im_hsv = rgb2hsv(im);

% Extract the hue, saturation, and value channels
hue = im_hsv(:,:,1);
saturation = im_hsv(:,:,2);
value = im_hsv(:,:,3);

% Define the color thresholds for each plant part
leaf_hue_min = 0.2; leaf_hue_max = 0.5;
stem_hue_min = 0.5; stem_hue_max = 0.8;
flower_hue_min = 0.8; flower_hue_max = 1.0;

% Segment the image based on the color thresholds
leaf_mask = (hue >= leaf_hue_min) & (hue <= leaf_hue_max) & (saturation > 0.2);
stem_mask = (hue >= stem_hue_min) & (hue <= stem_hue_max) & (saturation > 0.2);
flower_mask = (hue >= flower_hue_min) & (hue <= flower_hue_max) & (saturation > 0.2);

% Create color-coded images of each plant part
leaf_image = zeros(size(im));
leaf_image(:,:,1) = im(:,:,1) .* uint8(leaf_mask);
leaf_image(:,:,2) = im(:,:,2) .* uint8(leaf_mask);
leaf_image(:,:,3) = im(:,:,3) .* uint8(leaf_mask);

stem_image = zeros(size(im));
stem_image(:,:,1) = im(:,:,1) .* uint8(stem_mask);
stem_image(:,:,2) = im(:,:,2) .* uint8(stem_mask);
stem_image(:,:,3) = im(:,:,3) .* uint8(stem_mask);

flower_image = zeros(size(im));
flower_image(:,:,1) = im(:,:,1) .* uint8(flower_mask);
flower_image(:,:,2) = im(:,:,2) .* uint8(flower_mask);
flower_image(:,:,3) = im(:,:,3) .* uint8(flower_mask);

% Display the color-coded images
figure;
subplot(2,2,1); imshow(im); title('Original Image');
subplot(2,2,2); imshow(leaf_image); title('Leaves');
subplot(2,2,3); imshow(stem_image); title('Stems');
subplot(2,2,4); imshow(flower_image); title('Flowers');
