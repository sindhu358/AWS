 # Data Engineering
Data flows
Ingestion --> Storage --> Process and Analyze --> Explore and visualize  
**IAM Identity** Types

![image](https://github.com/user-attachments/assets/5289eec4-034a-4616-872f-5ec183808f4b)

**Service account**
Created a service account and then assigned another role thorugh IAM 

Create a cluster and deploy it in APP ENgine


## Cloud storage
Create a bucket with
  1. global unique key(name)
  2. store data(Choose one regions)
      - single
      - dual
      - multiple 
  3.storage class of data(choose one)
    - Autoclass(coldline,archieve class),
    - Default class
      - standard
      - nearline
      - coldline
      - Archieve
  4. COntrol access to objects
  5. how to protect the object data
  6. Data encryption
     - Google-managed encryption key(default)
     - cloud KMS key(create a security for client access- customer managed Encryption key)
        - can also be add a file and create a key through powershell   through some commands((customer supplied Encryption key))

After creating a bucket we can also add a **Lifecycle rule** for automatically deleting over a certain period of time   
we can upload files and ceate file and folders in a bucket
