# Fresh-Fish-Classifier

## Problem Statement
Singapore's fresh fish market is worth USD 850 million this is expected to grow at a CAGR of 2.5% to $960 million in 2028. Only 4.4% of these fresh fish are sold online. 75% of the offline sales are through our big markets such as local wet markets, Sheng Siong, NTUC, Prime, and Giant. 

The online sales are made up of live auctions and digital shops. A Straits Time article about one of our pioneer fresh fish digital shops, Tankfully Fresh is quoted saying "We called it Tankfully Fresh because it's the feeling we want our customers to have when they open their package".

This goes to show the importance of the freshness of the fish. In the same article the founder also mentions, that the younger generation these days do not like to visit the earthier environments such as our wet markets, and even if they do, they don't exactly know how to evaluate a fish and haggle prices based on the true quality of the fish. Instead, they may end up paying more for sub-standard products. A search into the Google reviews of all the offline and online stalls also reveals many instances of customers having bad experiences from receiving or buying fish that are not fresh and paying expensive prices.
  
  So how do we:
  1. **Improve consumer confidence in online deliveries to ensure that the customer receives fresh fish**.
  2.  **Empower customers with the necessary bargaining power by helping them determine the freshness of the fish**.
  3. **Help online and offline businesses gain a competitive advantage by assuring the customer that their fish is fresh**

  ### Solution:
  The envisaged solution is a model that can tell how long a fish has been out from the sea by scanning it with a camera.

  ### Use cases:
  1. The model could be an app that consumers can download on their mobile devices to scan the fish in the markets or when they receive them from deliveries. 
  2. The model could also be deployed at live stream auctions and brick-and-mortar stalls using display-like devices to improve customer confidence.

  ### Success Factors:
  The success factor for the solution is that it should **work in a real-world environment** with a **mean average precision** of at least **85%**.

## Data - Collection:
To collect reliable data and simulate actual market conditions. 3 fish were bought from the market and stored in a styrofoam box from days 0 -7. The melted ice in the styrofoam box was drained and topped up with fresh ice daily. The fish was photographed near the eye region from 8 different angles. A total of 300 images were captured throughout the 7 days.

## Exploratory Data Analysis 

**Observations from images**:

Generally, on day 0 the fish eyes are mostly back with a golden perimeter. From days 1-2, the fish eyes become, foggy and white but still translucent. On day 4 the fish eyes turn dry and less translucent. Usually after day 4, the   fish eyes will then tend to become pinkish and red.

However, during the experiment, the fish were observed to deteriorate at different rates. One of the fish eyes became foggy on day 0 itself, while the other 2 remained bright and black, whereas another fish was observed to deteriorate very slowly. On day 2 its eyes were still mostly black and a little foggy while the eyes of the other 2 were mostly white.

**Observations from colour channels**: 

To examine the colour channels, the annotated images were cropped and stored in folders according to their class.  The pixel values for the red, blue, and green channels and greyscale images were normalised for each image and aggregated for each class (Day 0 -7). This data was then plotted using a box pot to examine if there were any patterns in pixel values as the fish deteriorated

Day 0 was observed to usually have a low magnitude across all colour channels, and day 4 had the highest magnitude. Based on the grey scale box plot, and cropped images, the fish eyes were mostly black on day 0 and white on day 4. Since white is a combination of red, green, and blue, at maximum pixel values, and black is represented by near zero pixel value, this could be the reason why day 4 had the highest magnitude across all three colour channels, and day 0 had the lowest.

## Data Processing & Training

The origin data was then further augmented using albumentations. Only flip and rotational transformations were applied so as not to alter the image resolutions, dimensions, or colours. The original and augmented data were then labeled using roboflow and trained using Yolov8s.

## Results
Below are the results from the validation:

- *F1 Score*: **0.99** at 0.669 confidence 
- *MAP*: **0.995**: @0.5 IOU

A Steamlit app was built to put the model to the test. The model was able to detect and classify the seabass in 2 separate videos. These videos were taken at prime and sheng siong.

## Conclusion & Recommendations for Future Work:

The success factors were met. Below are some recommendations for future work to bring more value in the food retail space for both the customers and businesses.

- The model could be upscaled to a larger variety of fish
- Explore using alternate imaging devices, such as hyperspectral imaging to make the model more robust, or expand the use cases to fruits and vegetables

## Files:

The [split_annoted_images](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/EDA/Split_Annotated_images.ipynb) file segregates the annotated data to train, test, and split.

The [crop_images](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/EDA/crop_images.ipynb) file crops the fish eyes from the images and stores the cropped photos in folders based on their class.

The [eda_main](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/EDA/EDA_Main.ipynb) file is where the eda is executed.

The [augmentation](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/Training/Augmentation.ipynb), file augments the images using Albumentaions.

The [yolov8_training](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/Training/yolov8_Training.ipynb) is the file where the training was executed.

The [model outputs](https://github.com/thanaraj90/Fresh-Fish-Classifier/tree/main/model%20outputs) folder contains the results obtained from the training and includes the models weights.

The [app.py](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/streamlit/app.py) excutes the streamlit application that was build with the model. Note that the videos have been removed from the videos directory due to storage limitations. Upload a videos folder with videos and set the path to these videos in [settings.py](https://github.com/thanaraj90/Fresh-Fish-Classifier/blob/main/streamlit/settings.py) to use the application.
