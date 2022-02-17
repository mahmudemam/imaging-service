# Imaging Service
## APIs
The following APIs accept either a signle image or multiple images upload
### POST /upload/sync
This API is a sync endpoint that will respond to the client once the full upload processing is done
### POST /upload
This API is an async endpoint that will publish a notification to the client once the full upload processing is done

## System Arch
![image](https://user-images.githubusercontent.com/11890971/154488850-26a9b4fb-88cb-4e0b-9acd-cafab0103702.png)
### Considerations
1. CDN is added for fastest images read based on user location
2. DB can be NoSQL because for this simple solution there is no relations and NoSQL can be horizontally scaled and add read replica
3. Each microservice is configured to be autoscaled to handle traffic increase
4. A Message queue is added to support long running image process in backgroud to avoid blocking Upload microservice
5. Firebase is used for notification or any other socket connection can be used
6. A load balancer is added to load balance user requests on healthy microservices
7. Non functional requirements for logging and monitoring must be added to know the issues early like ELK, Promotheus/Grafana and Newrelic

## Storage Estimations
#### Assumptions
1. Original Image size 10 MB
2. Processed Image size 1 MB
3. Number of images upload / day = 10 M
4. 2 records are persisted into DB for original image and final image
##### Needs
- Object Storage size = (1 MB + 10 MB) * 10 M = 11 TB / day
- Block Storage size for DB = 10 M * 2 = 20 GB / day
