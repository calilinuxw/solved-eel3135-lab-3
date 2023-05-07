Download Link: https://assignmentchef.com/product/solved-eel3135-lab-3
<br>
<strong>Images in MATLAB</strong>

For our purpose here, we will divide images into two categories: grayscale (“black-and-white”) and color images:

<ul>

 <li>A greyscale image can be thought of as a two-dimensional discrete-“time” signal with the two “time” dimensions being the vertical and horizontal pixel indices (or simply the pixel <em>location</em>) and the value of the signal being the intensity of the pixel at that pixel location.</li>

 <li>A color image can be thought of as a collection of three “grayscale” images, with each set of three pixels with the same location indicating the intensities of the three primary colors (red, green, and blue) at that location of the image.</li>

</ul>

In MATLAB, a greyscale image can be represented by a matrix. The row (first) and column (second) indices of the matrix respectively give the vertical and horizontal pixel indices while the value of an element in the matrix stores the intensity of the image at that location. On the other hand, a color image can be represented by 3-dimensional array (a collection of three matrices) with the third index ranging from 1 to 3 corresponding to the primary colors of red, green, and blue.

One may use the imagesc function to display grayscale and color images in MATLAB. For a grayscale image, imagesc uses the current <em>color map </em>to display the image. The color map can be set using the colormap function. To display a true grayscale image, we need to set the current color map to grayscale

&gt;&gt; colormap(gray);

Otherwise, imagesc will display the grayscale image using pseudo colors specified by the current color map. You should do

&gt;&gt; help imagesc

&gt;&gt; help colormap

to learn more about the two functions.

<h1>Lab 3 Exercises</h1>

<ul>

 <li>Unless stated otherwise, you must submit your solutions to all the lab exercises in this section.</li>

 <li>Your laboratory solutions should be submitted on Canvas as a single PDF. The simplest way is to put your codes and answers for all the lab exercises in a single MATLAB Publisher script and use %% to separate the codes and answers for different exercises into different sections as described in the information section of Lab 1.</li>

</ul>

<strong>Exercise 3.1:</strong>

The piece of MATLAB code below provides some examples of how to generate, display, and manipulate grayscale images. Copy the code to a MATLAB script and replace each corresponding comment with the appropriate description. This piece of code is designed to show you how to work with images in MATLAB.

<strong>Note: </strong>You may use the MATLAB function help to learn more about the MATLAB functions used in the code. You should also run the code to help you understand how it works and help you write your comments. <strong>You may use and/or modify elements of this MATLAB code to answer questions asked in Lab Exercise 3.2 below.</strong>

% USER DEFINED VARIABLES

<ul>

 <li>= 15; % Width</li>

 <li>= 1:160; % Horiztonal Axis y = 1:80;            % Vertical Axis</li>

</ul>

% ==&gt; Comment about the next line here &lt;== z = round(127*exp(-1/w.^2*((y.’-40).^2+(x-80).^2)));

% ==&gt; Comment about the next line here &lt;== colormap(gray);

% ==&gt; Comment about the next three lines here &lt;==

[xs,ys,zs] = image_system1(z,2,2);

za            = image_system2(zs,-10,35); zb = image_system3(za,-30,35);

% PLOT RESULT WITH SUBPLOT figure(1);

<table width="584">

 <tbody>

  <tr>

   <td width="219">subplot(2,2,1);</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

  <tr>

   <td width="219">imagesc(x, y, z);</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

  <tr>

   <td width="219">axis image; title(’Original’)</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

  <tr>

   <td width="219">subplot(2,2,2);</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

  <tr>

   <td width="219">imagesc(xs, ys, zs);</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

  <tr>

   <td width="219">axis image;</td>

   <td width="365">% ==&gt; Add comment about this command &lt;==</td>

  </tr>

 </tbody>

</table>

title(’After System 1’)

subplot(2,2,3);  % ==&gt; Add comment about this command &lt;== imagesc(xs, ys, za);             % ==&gt; Add comment about this command &lt;== axis image;  % ==&gt; Add comment about this command &lt;== title(’After System 2’) subplot(2,2,4);            % ==&gt; Add comment about this command &lt;== imagesc(xs, ys, zb);            % ==&gt; Add comment about this command &lt;== axis image; % ==&gt; Add comment about this command &lt;== title(’After System 3’)

function [xs, ys, zs] = image_system1(z,Dx,Uy) %IMAGE_SYSTEM1 ===&gt; Describe function here &lt;===

% ==&gt; Comment about the next line here &lt;== zs = zeros(ceil(Uy*size(z,1)),ceil(size(z,2)/Dx));

% ==&gt; Comment about the next two lines here &lt;== ys = 1:ceil(Uy*size(z,1)); xs = 1:ceil(size(z,2)/Dx);

% ==&gt; Comment about the next line here &lt;== zs(1:Uy:end,1:end) = z(1:end,1:Dx:end);

end

function [za] = image_system2(z,Sx,Sy) %IMAGE_SYSTEM2 ===&gt; Describe function here &lt;===

% ====&gt; Comment about the next line here &lt;==== za = zeros(size(z,1), size(z,2));

for nn = 1:size(z,1)

for mm = 1:size(z,2)

% ====&gt; Comment about next line here &lt;==== if nn&gt;Sy &amp;&amp; nn-Sy&lt;size(z,1) &amp;&amp; mm&gt;Sx &amp;&amp; mm-Sx&lt;size(z,2) % ====&gt; Comment about this line here &lt;==== za(nn,mm) = 1/2*z(nn-Sy,mm-Sx);

end

end

end

end

function [zb] = image_system3(za,Sx,Sy) %IMAGE_SYSTEM3 ===&gt; Describe function here &lt;===

% ====&gt; Comment about next two lines here &lt;==== x = 0:1:size(za,2)-1; y = 0:1:size(za,1)-1;

% ====&gt; Comment about next two lines here &lt;====

xs = mod(x-Sx, size(za,2)); ys = mod(y-Sy, size(za,1));

% ====&gt; Comment about next line here &lt;==== zb = za(ys+1,xs+1);

end

<strong>Exercise 3.2:</strong>

This exercise shows you how to use MATLAB to implement three important operations in image processing: (1) sampling (converting a large image to a small image), (2) anti-aliasing (reducing distortions from aliasing), and (3) interpolation (converting a small image to a large image).

<ul>

 <li><em>(Sampling) </em>Write a MATLAB function image sample implementing the following usage example:</li>

</ul>

&gt;&gt; [xs, ys, zs] = image_sample(z, D);

which inputs a grayscale image z and samples every D pixels in both the horizontal and vertical direction. It outputs the sampled image zs and the new axes xs and ys.

<ul>

 <li><em>(Sampling) </em>The file mat stores the MATLAB matrix lighthouse. Use the MAT-</li>

</ul>

LAB command

&gt;&gt; load(’lighthouse.mat’)

to load the matrix lighthouse from the MAT file into MATLAB. The matrix lighthouse represents a grayscale image. Apply image sample to the image lighthouse by sampling every 2 pixels in the horizontal and vertical directions to obtain the sampled image lighthouse sampled. Use subplot to show side-by-side images before and after sampling. Compare the two images and describe how aliasing manifests in sampling the lighthouse image (<u>hint: </u>aliasing distorts your signal). Relate this to your understanding of aliasing from class.

<ul>

 <li><em>(Anti-aliasing) </em>Write a MATLAB function image antialias implementing the following usage example:</li>

</ul>

zaa = image_antialias(z);

which inputs a grayscale z and outputs the anti-aliased image zaa. Design the anti-aliasing function to compute each point of <em>z<sub>aa</sub></em>[<em>x,y</em>] (i.e., the mathematical notation for zaa) according to the two-dimensional difference equation (i.e., a discrete-time system/filter)

<u>Hint: </u>You may use the function image system2 from Lab Exercise 3.1 as a guide.

<ul>

 <li><em>(Anti-aliasing) </em>Use a for-loop to apply the anti-aliasing function image antialias to the high-resolution image lighthouse SIX times to obtain the anti-aliased image lighthouse aax6, and then apply the sampling function image sample on lighthouse aax6 to obtain a new sampled image lighthouse aax6 sampled. Use subplot to show side-by-side the original image lighthouse, the anti-aliased image lighthouse aax6, the sampled image lighthouse sampled</li>

</ul>

in (b), and the anti-aliased-and-then-sampled image lighthouse aax6 sampled. What does the anti-aliasing filter do to the image? How does it reduce aliasing? Why is this useful in real-world applications?

<ul>

 <li><em>(Interpolation) </em>Write a MATLAB function image insertzeros implementing the following usage example:</li>

</ul>

[xz, yz, zz] = image_insertzeros(zaas, U);

which inputs an anti-aliased and sampled (grayscale) image zaas, and outputs the image zz. The output image contains U-1 zero-valued pixels inserted between each pixel from zaas, both horizontally and vertically. The function also outputs the new axes xz and yz. <u>Hint: </u>You may use the function image system1 from Lab Exercise 3.1 as a guide.

<ul>

 <li><em>(Interpolation) </em>Apply image insertzeros to your anti-aliased and sampled image lighthouse aax6 sampled in (d) to obtain the image lighthouse zeros by add one zero (i.e. U=2) zeros between each pixel. Your function image antialias can be used to implement anti-aliasing or interpolation! Therefore, apply image antialias to lighthouse zeros SIX times to do interpolation to obtain the interpolated image lighthouse interpolated. What are the dimensions of lighthouse interpolated? Use subplot to show side-by-side the images lighthouse, lighthouse zeros, and lighthouse interpolated. What does the interpolation filter do to the image? Why is this useful in real-world applications?</li>

</ul>

<strong>Exercise 3.3 (Extra credits: +20 points):</strong>

Extend your functions image sample, image antialias and image insertzeros to handle grayscale as well as color images. Repeat parts (b), (d), and (e) of Lab Exercise 3.2 using the zebra image in the MAT file zebra.mat. You may need to increase the sampling factor <em>D </em>in (b) if you want to see more severe aliasing after sampling. You may also need to change the number of applications of the anti-aliasing and interpolation filter in (d) and (e) to get good interpolation results. If you have the image processing toolbox, you may use the function imread to read in a GIF or JPEG image for testing in place of zebra.