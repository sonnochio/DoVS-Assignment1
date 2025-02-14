# How can I rotate a grayscale image by a specified angle (theta) using reverse mapping?
```
function [Out] = Rotate(In, Theta)
    % Get the size of the image
    [rows, cols] = size(In);

    % Calculate the center of the image
    centerX = cols / 2;
    centerY = rows / 2;
    
    % Precompute the rotation matrix (inverse transformation)
    T = [cos(Theta), sin(Theta); -sin(Theta), cos(Theta)];
    
    % Create an output matrix initialized to zeros (black)
    Out = zeros(rows, cols);
    
    % Loop over each pixel in the output image
    for i = 1:rows
        for j = 1:cols
            % Calculate the destination pixel in the original image using reverse mapping
            coords = T * ([j - centerX; i - centerY]);
            newX = round(coords(1) + centerX);
            newY = round(coords(2) + centerY);
            
            % Check if the coordinates are within the bounds of the original image
            if newX > 0 && newX <= cols && newY > 0 && newY <= rows
                Out(i, j) = In(newY, newX);
            end
        end
    end
end

```

# How do I shear a grayscale image in both the X and Y direction and center it?
```
function [Out] = Shear(In, Xshear, Yshear)
    % Get the size of the image
    [rows, cols] = size(In);
    
    % Calculate the center of the image
    centerX = cols / 2;
    centerY = rows / 2;
    
    % Precompute the shearing matrices
    shearMatrixX = [1, Xshear; 0, 1];
    shearMatrixY = [1, 0; Yshear, 1];
    
    % Combine the shearing transformations
    shearMatrix = shearMatrixX * shearMatrixY;
    
    % Create an output matrix initialized to zeros (black)
    Out = zeros(rows, cols);
    
    % Loop over each pixel in the output image
    for i = 1:rows
        for j = 1:cols
            % Apply the reverse mapping for shearing transformation
            coords = shearMatrix * ([j - centerX; i - centerY]);
            newX = round(coords(1) + centerX);
            newY = round(coords(2) + centerY);
            
            % Check if the coordinates are within the bounds of the original image
            if newX > 0 && newX <= cols && newY > 0 && newY <= rows
                Out(i, j) = In(newY, newX);
            end
        end
    end
end
```
