PROJECT 9

CONTINOUS INTEGRATION PIPELINE FOR TOOLING WEBSITE

INSTALL AND CONFIGURE JENKINS SERVER

STEP 1

* I spinned up an AWS EC2 Server on ubuntu and named it 'jenkins'
* I installed Jenkins and made sure it was up and running.
<img width="1440" alt="Screenshot 2023-02-02 at 11 51 09 AM" src="https://user-images.githubusercontent.com/115854902/220903464-bf9a6984-bda0-4f6c-84a7-2e027f93238a.png">
<img width="1440" alt="Screenshot 2023-02-02 at 11 53 11 AM" src="https://user-images.githubusercontent.com/115854902/220903518-fe7e9ddd-7047-45bd-80d3-8ef6c656cae7.png">
<img width="1440" alt="Screenshot 2023-02-02 at 11 54 08 AM" src="https://user-images.githubusercontent.com/115854902/220903568-d68e510d-ec97-40bc-8214-e28c09623ff5.png">

I also went ahead to open TCP Port 8080 in the security group for Jenkins server.
<img width="1440" alt="Screenshot 2023-02-02 at 11 56 04 AM" src="https://user-images.githubusercontent.com/115854902/220904216-a210880c-7345-4583-8dab-e7a494bec900.png">
I accessed my jenkins server on my browser to perform the initial jenkins set up.
<img width="1440" alt="Screenshot 2023-02-02 at 12 03 31 PM" src="https://user-images.githubusercontent.com/115854902/220904544-d9a5984e-008b-4a73-aded-53d19a6a3e58.png">
<img width="1440" alt="Screenshot 2023-02-02 at 12 26 14 PM" src="https://user-images.githubusercontent.com/115854902/220904578-d5526316-4dc9-42b9-afbc-b1478b0d55b8.png">
<img width="1440" alt="Screenshot 2023-02-02 at 12 27 36 PM" src="https://user-images.githubusercontent.com/115854902/220904613-5313ed49-78d4-41cf-9902-e019ef03f273.png">
<img width="1440" alt="Screenshot 2023-02-02 at 12 33 17 PM" src="https://user-images.githubusercontent.com/115854902/220905101-99ce5759-4aad-4a60-950f-295e506a4774.png">
<img width="1440" alt="Screenshot 2023-02-02 at 12 34 56 PM" src="https://user-images.githubusercontent.com/115854902/220905336-bdb90871-a08c-467d-80eb-3f9ba8305d96.png">
<img width="1440" alt="Screenshot 2023-02-02 at 12 45 13 PM" src="https://user-images.githubusercontent.com/115854902/220905424-ebe76f4c-0098-434b-b73a-401be4719c27.png">

STEP 2

CONFIGURE JENKINS TO RETRIEVE SOURCE CODES FROM GITHUB USING WEBHOOKS.

* The first step i carried out was to enable webhooks in my Github repository settings.
* I added a webhook and input my Jenkins IP Address on the payroll url and content type was application/json.
<img width="1440" alt="Screenshot 2023-02-09 at 11 41 42 AM" src="https://user-images.githubusercontent.com/115854902/220906737-980859f6-e6b1-42b2-b1e3-afceaac4a98a.png">
* The next step was to create a freestyle project in my Jenkins web console.
* During configuration of my Jenkins freestyle project, I chose git repository and put in Tooling Github Repository URL and credentials so that Jenkins can access files in the repository for build actions.
* I saved the configuration and ran the build which was successful.
<img width="1440" alt="Screenshot 2023-02-09 at 1 11 16 PM" src="https://user-images.githubusercontent.com/115854902/220910795-f2ba4c5f-3101-498c-baaa-69e89e40f7cc.png">
![Uploading Screenshot 2023-02-09 at 1.12.33 PM.png…]()
<img width="1440" alt="Screenshot 2023-02-09 at 1 14 34 PM" src="https://user-images.githubusercontent.com/115854902/220911034-3f0378a7-f053-454f-a6f0-27169d2118c8.png">
<img width="1440" alt="Screenshot 2023-02-09 at 1 19 32 PM" src="https://user-images.githubusercontent.com/115854902/220911165-dd8f0c8d-8563-4f82-a600-683027233ca7.png">
<img width="1440" alt="Screenshot 2023-02-09 at 1 19 39 PM" src="https://user-images.githubusercontent.com/115854902/220911231-5263ce61-31b9-4232-8870-9faa49154490.png">

* I added more configuration to my project.
* I configured triggering the Project/Job from Github Webhook a nd "Post - build Actions" to arvchive all the files.
* I made some changes in my Read.md file on the Github Webhook and it automatically pushed a new build on my Jenkins Server.
<img width="1440" alt="Screenshot 2023-02-09 at 1 24 45 PM" src="https://user-images.githubusercontent.com/115854902/220914349-64eac69e-123c-4c20-b3b9-bab3e834b235.png">
<img width="1440" alt="Screenshot 2023-02-09 at 2 05 55 PM" src="https://user-images.githubusercontent.com/115854902/220914958-24fe46ac-63ac-4ba1-9475-89f4c625d075.png">

CONFIGURE JENKINS TO COPY FILES TO NFS SERVER VIA SSH 

STEP 3

* I installed "Publish Over SSH" PLUGIN.
* Then went ahead to configure my project to copy artifacts over to NFS SERVER.
* I saved the configuration, then opened my project configuration page and added another "Post build action".

<img width="1440" alt="Screenshot 2023-02-10 at 8 15 05 PM" src="https://user-images.githubusercontent.com/115854902/220917730-6f92a52b-9ccb-4637-b5c6-1b358d514723.png">
<img width="1440" alt="Screenshot 2023-02-10 at 11 44 58 AM" src="https://user-images.githubusercontent.com/115854902/220918739-681cf4be-3e10-4f1f-bd34-a20cdf906376.png">

<img width="1440" alt="Screenshot 2023-02-16 at 2 00 31 PM" src="https://user-images.githubusercontent.com/115854902/220922174-6f66cae2-1c57-48a9-9d16-be21442e6a03.png">
* I also configured it to send all files produced by the build into my previously defined remote directory. I saved the configuration and went ahead to change/edit my read.md file in my Github tooling repository which trigger a new build in my Console output of my project.
* I also comnected via ssh to my NFS Server to check read.me file to ensure that the files in /mnt/apps have been updated and i saw the changes i previously made in my Github .

<img width="1440" alt="Screenshot 2023-02-16 at 3 40 48 PM" src="https://user-images.githubusercontent.com/115854902/220924678-cd07c02a-ab89-443a-92bd-ac357140c42d.png">

<img width="1440" alt="Screenshot 2023-02-16 at 3 41 54 PM" src="https://user-images.githubusercontent.com/115854902/220924704-d75ea52a-25b2-4124-8f47-33bd2cffcbef.png">

<img width="1440" alt="Screenshot 2023-02-16 at 3 45 18 PM" src="https://user-images.githubusercontent.com/115854902/220924731-9a075fdf-9dbf-429d-8fbf-6ca52d753cd8.png">













