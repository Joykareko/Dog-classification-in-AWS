# Image Classification using AWS SageMaker

Use AWS Sagemaker to train a pretrained model that can perform image classification by using the Sagemaker profiling, debugger, hyperparameter tuning and other good ML engineering practices. This can be done on either the provided dog breed classication data set or one of your choice.

## Project Set Up and Installation
Enter AWS through the gateway in the course and open SageMaker Studio. 
Download the starter files.
Download/Make the dataset available. 

## Dataset
The provided dataset is the dogbreed classification dataset which can be found in the classroom.
The project is designed to be dataset independent so if there is a dataset that is more interesting or relevant to your work, you are welcome to use it to complete the project.

### Access
Upload the data to an S3 bucket through the AWS Gateway so that SageMaker has access to the data. 
-Done

### Different .py files used.
I created 3 .py files.
 I used hpo.py-I used this for debugger and profiler creation through use of smdebug module. This file is genrally similar to the train_model.py file but with additional variables for my test and train functions to include hooks for debugging and profile creation.
I also created a train_model.py. This contained the functions for training and testing and model creation. I used Resnet50 as my pretrained model of choice.
Initial endpoint invocation generated an error, so I used a custom model_endpoint.py script file to call the endpoint and use the file to generate a prediction on a test image.

## Hyperparameter Tuning
What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search

I used Resnet50 as my pretrained model of choice.
For the hyperparameter ranges, I specified the learning rate range and the batch sizes.

Remember that your README should:
- Include a screenshot of completed training jobs
![completed training jobs.png](CD0387-deep-learning-topics-within-computer-vision-nlp-project-starter/Successful training jobs.png)
- Logs metrics during the training process
Done within the scripts
- Tune at least two hyperparameters
I tuned Learning rate and batch size.
- Retrieve the best best hyperparameters from all your training jobs
The best hyperparameters for the best training job were:
batch size-32, learning rate-0.007559624430866038
## Debugging and Profiling
**TODO**: Give an overview of how you performed model debugging and profiling in Sagemaker
I downloaded smdebug in sagemaker, then set up the dependencies in script mode.
In my notebook, I set up the rules, profiler configurations and debugger configurations.
I set up my estimator and fit it to my dog images data.
### Results
**TODO**: What are the results/insights did you get by profiling/debugging your model?
AT first, the model was overfitting.
I also realized it was running solely on CPU hence the long compute periods so, I changed the model to run on GPU.
Once I changed these the compute time took less than 10 minutes(20 minutes before).
I also checked the GPU utilization as well as the model performance graph.

**TODO** Remember to provide the profiler html/pdf file in your submission.
-Done

## Model Deployment
**TODO**: Give an overview of the deployed model and instructions on how to query the endpoint with a sample input.
Done

```
from PIL import Image
import io
# TODO: Run an prediction on the endpoint
with open("./test.jpg", "rb") as f:
    payload = f.read()
    
type(payload)

response=predictor.predict(payload, initial_args={"ContentType": "image/jpeg"})
response
```

**TODO** Remember to provide a screenshot of the deployed active endpoint in Sagemaker.
Done

![completed endpoint.png](CD0387-deep-learning-topics-within-computer-vision-nlp-project-starter/Deployed endpoint.png)

## Standout Suggestions
**TODO (Optional):** This is where you can provide information about any standout suggestions that you have attempted.
