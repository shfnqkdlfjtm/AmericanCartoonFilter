# AmericanCartoonFilter
Using OpenCV to transform drama images into American Comics-style cartoon images


## 프로그램 및 기능 설명
Transform an image into a cartoon using OpenCV by applying edge detection followed by bilateral filtering and then blending the result with the original image.

    import cv2

    def american_comics_style(image_path):
        # Load image
        img = cv2.imread(image_path)
        
        # Check if image is loaded successfully
        if img is None:
            print("Error: Unable to load image.")
            return None
        
        # Convert image to grayscale
        gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
        
        # Apply median blur to reduce noise
       gray = cv2.medianBlur(gray, 5)
        
        # Detect edges using adaptive thresholding
        edges = cv2.adaptiveThreshold(gray, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 9, 9)
        
        # Create a color version of the image
        color = cv2.bilateralFilter(img, 9, 300, 300)
        
        # Combine edges and color using bitwise_and
        cartoon = cv2.bitwise_and(color, color, mask=edges)
        
        return cartoon
    
    # Path to your input image
    input_image_path = r"C:\Users\samsung\Downloads\jXMyp.jpg"
    
    # Apply American comics style effect
    comics_style_image = american_comics_style(input_image_path)
    
    # Check if comics_style_image is valid before displaying
    if comics_style_image is not None:
        # Display the result
        cv2.imshow("American Comics Style", comics_style_image)
        cv2.waitKey(0)
        cv2.destroyAllWindows()
    else:
        print("Error: Unable to process the image.")


원본이미지(좌) 필터링한 이미지(우)
