# Convolutional Deep Neural Network for Image Classification

## AIM

To Develop a convolutional deep neural network for image classification and to verify the response for new images.

## Problem Statement and Dataset

The goal of this project is to develop a Convolutional Neural Network (CNN) for image classification using the FashionMNIST dataset. The FashionMNIST dataset contains grayscale images of 10 different clothing categories (e.g., T-shirt, trousers, dress, etc.), and the model aims to classify them correctly. The challenge is to achieve high accuracy while ensuring computational efficiency.

## Neural Network Model

![NN MODEL 3](https://github.com/user-attachments/assets/15d7d0b9-9525-4638-8321-9de4f5ff12f3)


## DESIGN STEPS

### STEP 1:
Define the goal of classifying fashion apparel items into 10 categories using a CNN. Ensure high accuracy while maintaining efficiency.

### STEP 2:
Use the FashionMNIST dataset, which contains 60,000 training and 10,000 test images of clothing items. Each image is 28×28 grayscale and labeled with one of 10 classes.

### STEP 3:
Convert images to tensors and normalize pixel values to [0,1]. Use DataLoaders for efficient batch processing during training and testing.

### STEP 4:
Design a CNN with convolutional layers for feature extraction, ReLU activation, pooling layers for downsampling, and fully connected layers for classification

### STEP 5:
Train the CNN using CrossEntropyLoss and Adam optimizer for multiple epochs. Monitor accuracy and loss to ensure proper learning.

### STEP 6:
Test the model on unseen FashionMNIST data, compute performance metrics, and analyze using a confusion matrix.

### STEP 7;
Save the trained model for future use and visualize predictions on sample test images. Optionally, integrate into an application for real-world use.
## PROGRAM

### Name: Tarunika D
### Register Number: 212223040227
```python
class CNNClassifier(nn.Module):
    def __init__(self):
        super(CNNClassifier, self).__init__()
        self.conv1=nn.Conv2d(in_channels=1,out_channels=32,kernel_size=3,padding=1)
        self.conv2=nn.Conv2d(in_channels=32,out_channels=64,kernel_size=3,padding=1)
        self.conv3=nn.Conv2d(in_channels=64,out_channels=128,kernel_size=3,padding=1)
        self.pool=nn.MaxPool2d(kernel_size=2,stride=2)
        self.fc1=nn.Linear(128*3*3,128)
        self.fc2=nn.Linear(128,64)
        self.fc3=nn.Linear(64,10)

    def forward(self, x):
        x=self.pool(torch.relu(self.conv1(x)))
        x=self.pool(torch.relu(self.conv2(x)))
        x=self.pool(torch.relu(self.conv3(x)))
        x=x.view(x.size(0),-1)
        x=torch.relu(self.fc1(x))
        x=torch.relu(self.fc2(x))
        x=self.fc3(x)
        return x

```

```python
model =CNNClassifier()
criterion =nn.CrossEntropyLoss()
optimizer =optim.Adam(model.parameters(),lr=0.001)
```

```python
def train_model(model, train_loader, num_epochs=3):
   for epoch in range(num_epochs):
     model.train()
     running_loss = 0.0

     for images, labels in train_loader:
       optimizer.zero_grad()
       outputs = model(images)
       loss = criterion(outputs, labels)
       loss.backward()
       optimizer.step()
       running_loss += loss.item()
     print('Name: Tarunika D')
     print('Register Number: 212223040227')
     print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {running_loss/len(train_loader):.4f}')

```

## OUTPUT
### Training Loss per Epoch

![Screenshot 2025-03-24 085827](https://github.com/user-attachments/assets/1695a17a-2bb4-437a-ba14-173844f28198)


### Confusion Matrix

![Screenshot 2025-03-24 085852](https://github.com/user-attachments/assets/9ab4f0f1-286d-4f5c-89f7-8e91f49a41dc)


### Classification Report

![Screenshot 2025-03-24 085902](https://github.com/user-attachments/assets/49ada5ce-dd43-4cf8-b099-2572817aa0ae)



### New Sample Data Prediction


![Screenshot 2025-03-24 085908](https://github.com/user-attachments/assets/5d5b6e33-2f80-4fe6-bd44-85f847d0627d)


## RESULT
Thus, We have developed a convolutional deep neural network for image classification to verify the response for new images.
