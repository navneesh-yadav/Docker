# Creating Docker Image 

This project is for creating docker image and optimising its size by using Multistage image building for Simple react app.

## Simple docker image creation. 


Here, we will be creating simple docker file to build image ,

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/4fd699dc-a12a-4e56-9bb3-a99a8f28976f)


### `docker build -t myapp`
Using this command will be building image now.
Let see the process of image creation

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/f72b7a34-eb2f-432a-8a19-16973553cc53)


It seems everything fine , let's check if image is creating or not !
### `docker images`
The above command will help to check the image created or exist in our local dir.

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/2fb592dc-7eb7-4350-9d64-c2396b798f03)

Let's analyse the output
This commands has given few details like Repo (IMAGE NAME), TAG , CREATED, SIZE.
Everything looks fine, lets try to run image as container.

### `docker run  <ImageName>`
Here the command will be `docker run myapp`

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/5400037c-83f3-45b4-bb56-290940c5072a)

It seems the container is running , Lets check for the output

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/86665950-9991-4cc1-a79d-dea7d2f801e9)

Everything is fine, but seems the image is of too large size 1.31GB



### Lets try to optimize

As we know the alpine images are less in size, lets try to use it in dockerfile
 
![image](https://github.com/navneesh-yadav/Docker/assets/66907873/3ca1ab9a-14df-42d6-86fa-7fa475a772ab)

Lets build it again trying the above command `docker build -t myapp:opt .` 
Here "opt" is tag to differentiate images.
Have skipped the process and now only checking the image after build using ~docker images ~

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/2128bdde-4ff2-43a9-b5a1-bbf88fdf1291)

The file is now  490MB which was earlier 1.31GB approx the file size reduced by #### 62.6 %.

Can we reduce the file size , yes lets move to try multi stage building.

#Multistage building : 
  1. Will use alpine image to build dependencies
  2. Will copy this dependencies in nginx web service and delete the rest of part.
  
Let's checkout 

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/66b7d1e5-149e-473e-8547-cad6caa0a2b7)

using above dockerfile will create the image again use the same command to bulid image `docker build -t myapp:alpine .`

Now the lets check image size

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/b6d291d3-ba11-4570-909c-d0be4c6f8483)

Now the image size  is 134MB , its reduced to #### 89.73 %.

### Can this be reduced more ?
We have use nginx general image, can we try with alpine image.

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/0032e880-792e-4a0e-a81f-87372cb8e7cc)

Let's build the image using command `docker build -t myapp:nginxalpine`

Lets check the output 

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/75a77990-1415-43b4-b2d8-c920c048da9f)

Wow the image size is now 23.3 MB, wiz reduction of #### 98.18 %

Lets check output by running container `docker run myapp:nginxalpine`
Since we are using nginx the port 80 is by default port.

![image](https://github.com/navneesh-yadav/Docker/assets/66907873/504a82c3-cd99-4a00-a4d6-2b206411dd7e)

It's fine now.

#Conclusion using few steps we have reduced the image size by #### 98 %.

Note: The react app used in this project is created by Navnish the owner of this repo.



