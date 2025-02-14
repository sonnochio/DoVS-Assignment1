# Notes

for image display, it is (row, colomn)

## Q
f(3,10) = 28
f(max) = 255
f(min) = 21


## Q1 Test yourself
imshow(f(:,241:482)) 

imadjust(f, [0 1],):
first set is the lower and higher bounds
second set is lower bound map to, higher bound map to

**0 (black) and 1 (white).**

Specifies the contrast limits in the input grayscale image that you want to map to values in the output image. Values must be in the range [0 1.0]. The value low_in must be less than the value high_in.

0.5: The lower bound—pixel values at or below 0.5 will be mapped to the new minimum (0).
0.75: The upper bound—pixel values at or above 0.75 will be mapped to the new maximum (1).


J = imadjust(I,[low_in high_in],[low_out high_out]) maps intensity values in I to new values in J such that values between low_in and high_in linearly map to values between low_out and high_out.


## Q: Discuss the results with your classmates and record your observations in your logbook.
It makes the middle intensity of the image a lot lighter.

## equalised graph
The equalized histogram (third graph) is built by counting how many pixels now belong to each new intensity level.

# Task 4 - Noise reduction with lowpass filter
``` Test yourself: Explore various kernel size and sigma value for these two filters. Comment on the trade-off between the choice of these parameters and the effect on the image.```
w_box = fspecial('average', [2 2])
with this, a reduced kernel reduced the smoothing effect. they both smoothed the image.


# Task 5 - Median Filtering
the smoothing didn't make the original image more pixelated. there's greater difference between pixels.


# Task 6 - Sharpening the image with Laplacian, Sobel and Unsharp filters
unsharp didn't work.

Laplacian detects rapid chanegs in intensity
Sobel is edge detection
Unsharp is a mask, by adding it on it makes it sharper


# Task 7 - Test yourself Challenges
Improve the contrast of a lake and tree image store in file lake&tree.png use any technique you have learned in this lab. Compare your results with others in the class.
- 
imfilter(f, w_2, 0); 0 here is just edges are regarded as 0

```
clear all
close all
f = imread('assets/lake&tree.png');

imshow(f)
figure          % open a new figure window
imhist(f);      % calculate and plot the histogram



g=imadjust(f,[45/255 135/255]);
montage({f, g})     % display list of images side-by-side
figure
imhist(g);
```


Use the Sobel filter in combination with any other techniques, find the edge of the circles in the image file circles.tif. You are encouraged to discuss and work with your classmates and compare results.

```
clear all
close all

f = imread('assets/circles.tif');

imshow(f)
figure          % open a new figure window

f_1=fspecial('unsharp');

w_gauss = fspecial('Gaussian', [3 3], 0.2);

g=imfilter(f, f_1,0);

g_gauss = imfilter(f,w_gauss,0);

h=g-g_gauss+f;

montage({f,g,h});
```

office.jpg is a colour photograph taken of an office with badd exposure. Use whatever means at your disposal to improve the lighting and colour of this photo.

```
clear all
close all

f = imread('assets/office.jpg');

imshow(f)

% g2 = imadjust(f, [ ], [ ], 0.5);
% g3 = imadjust(f, [ ], [ ], 0.8);
% g4 = imadjust(f, [ ], [ ], 0.9);
% g5 = imadjust(f, [ ], [ ], 2);

g2=f*1.5;

% montage({f,g2,g3,g4,g5})

montage({f,g2})
```