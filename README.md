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

### 알고리즘으로 만화같은 느낌이 잘 표현되는 이미지
원본이미지(좌) 필터링한 이미지(우)
![민트자켓](https://github.com/shfnqkdlfjtm/Unity_Flappy_Balloon_Game/assets/144716487/0f532d59-eebd-40ea-9735-178337d9bd23)
![보라색 상의](https://github.com/shfnqkdlfjtm/Unity_Flappy_Balloon_Game/assets/144716487/b93c7fb6-d854-4164-b110-1db39b8796ca)
![총](https://github.com/shfnqkdlfjtm/Unity_Flappy_Balloon_Game/assets/144716487/d6249108-5ab3-4ce7-816a-4a5f89774012)

만화같은 느낌이 잘 표현되는 이미지들의 특징을 살펴보면 인문과 배경의 명암 대비가 크게 강조되어 뚜렷하게 나타나는 것을 알 수 있다.

### 알고리즘으로 만화같은 느낌이 잘 표현되지 않는 이미지
![파묘 무덤](https://github.com/shfnqkdlfjtm/Unity_Flappy_Balloon_Game/assets/144716487/0a96f985-56d5-45b7-ba36-f22c9e4a52b8)

위의 이미지의 특징을 살펴보면 사진에서 인물의 비중이 작아 이목구비가 뭉개졌다. 또한 배경 사이에도 명암과 채도 차이가 존재하지만, 그 차이가 크지 않아서 blur와 edge가 명확하게 구분되지 않았다.

## 알고리즘의 한계
단순한 사진은 잘 표현되지만 자연 풍경과 같은 미묘한 차이의 색색이 섞인 이미지는 잘 표현되지 않는다.




