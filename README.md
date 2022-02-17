# Imaging Service
## APIs
The following APIs accept either a signle image or multiple images upload
### POST /upload/sync
This API is a sync endpoint that will respond to the client once the full upload processing is done
### POST /upload
This API is an async endpoint that will publish a notification to the client once the full upload processing is done

## Component Diagrams

## Storage Estimations
#### Assumptions
1. Original Image size 10 MB
2. Processed Image size 1 MB
3. Number of images upload / day = 10 M
4. 2 records are persisted into DB for original image and final image
##### Needs
- Object Storage size = (1 MB + 10 MB) * 10 M = 11 TB / day
- Block Storage size for DB = 10 M * 2 = 20 GB / day
