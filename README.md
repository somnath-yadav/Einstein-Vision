# Einstein-Vision

*This repository contains code base and instruction to setup a use case for visual identification of product*

## Instructions
- Copy Controllers and Page in sandbox
- Upload .pem file to Files tab
- Set Remote Site Settings (Name: PVS_API, Remote Site URL: https://api.metamind.io)
- Click on Upload Image button and upload a image
- Specify impage title (as uploaded) and enter
- Vision API will be called and Predictions with Probabilities displayed

## Custom Image Classifier
- Get access token from: https://api.metamind.io/token
- Upload image dataset (folder with labels)

curl -X POST -H "Authorization: Bearer b142bd7e300749f98789a4a933bd70551be17608" -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data" -F "data=@/home/som2004/AllerganProducts.zip"  https://api.metamind.io/v1/vision/datasets/upload/sync

-- Response

{"id":1002739,"name":"AllerganProducts","createdAt":"2017-05-09T10:20:45.000+0000","updatedAt":"2017-05-09T10:20:45.000+0000","labelSummary":{"labels":[{"id":17275,"datasetId":1002739,"name":"Refresh","numExamples":28},{"id":17276,"datasetId":1002739,"name":"Botox","numExamples":33}]},"totalExamples":61,"totalLabels":2,"available":true,"statusMsg":"SUCCEEDED","type":"image","object":"dataset"}

- Train

curl -X POST -H "Authorization: Bearer 74e836aa7d994a0a2207ac320f8947790d1be9a8" -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data" -F "name=Allergan Product Model" -F "datasetId=1002739" https://api.metamind.io/v1/vision/train

- Response

{"datasetId":1002739,"datasetVersionId":0,"name":"Allergan Product Model","status":"QUEUED","progress":0,"createdAt":"2017-05-09T10:26:15.000+0000","updatedAt":"2017-05-09T10:26:15.000+0000","learningRate":0.001,"epochs":3,"queuePosition":1,"object":"training","modelId":"LBM2SV3OVWBEAP3LO2U7DZQ2SM","trainParams":null,"trainStats":null,"modelType":"image"}


- Predict
curl -X POST -H "Authorization: Bearer 6710ebc7d1c65e017049d5b6aa3793bdca1a81e6" -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data" -F "sampleContent=@/home/som2004/download1.jpg" -F "modelId=LBM2SV3OVWBEAP3LO2U7DZQ2SM" https://api.metamind.io/v1/vision/predict
