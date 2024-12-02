## Requirement 

- Create VPC with /16 range

![preview](images_folder/project/image1.jpg)
- Create IGW for VPC
- Create Two Subnets
- Pub and Pvt
- Pub Should have 4k Ip's
- Pvt Should Have 256 Ip's

![preview](images_folder/project/image2.jpg)
![preview](images_folder/project/image3.jpg)
![preview](images_folder/project/image4.jpg)
![preview](images_folder/project/image5.jpg)
![preview](images_folder/project/image6.jpg)
![preview](images_folder/project/image7.jpg)
![preview](images_folder/project/image8.jpg)


- Create 3 servers across diff subnets.
![preview](images_folder/project/image9.jpg)
![preview](images_folder/project/image10.jpg)
![preview](images_folder/project/image11.jpg)
![preview](images_folder/project/image12.jpg)
![preview](images_folder/project/image13.jpg)
![preview](images_folder/project/image14.jpg)
![preview](images_folder/project/image15.jpg)
![preview](images_folder/project/image16.jpg)
![preview](images_folder/project/image17.jpg)

- These servers are used for running application
- Create a DB - using RDS

![preview](images_folder/project/image18.jpg)

![preview](images_folder/project/image19.jpg)

- CODE For the Project - https://github.com/Ai-TechNov/On-Premise-Deployement.git

- Create 3 ec2 instance across Pvt-Subnets
- Deploy Above mentioned python code on the ec2's
- Create and Integrate RDS - DB within the code across all the 3 ec2. 
- As the app is running on PVT, it should be accessible via www !!
- The DB should be purely Pvt, and access should remian strictly to the admin !!

![preview](images_folder/project/image20.jpg)
![preview](images_folder/project/image21.jpg)

- For the Above infra, i want load-balancing to be configured.
- I want  Auto scaling for the 3 ec2's in order to avoid FT.
- These instances should be monitored and notificaitons should be in place !!

- Finally, The routing should happen via, ROUTE-53 using a Custom domain !

- IF any users browses the CDN, it should reach to app, where the app should collect user info and store it to the DB.
But, i want all the infra to be deployed in pvt-resources !!

![preview](images_folder/project/image22.jpg)
![preview](images_folder/project/image23.jpg)
![preview](images_folder/project/image24.jpg)
![preview](images_folder/project/image25.jpg)
![preview](images_folder/project/image26.jpg)
![preview](images_folder/project/image27.png)
![preview](images_folder/project/image28.png)
