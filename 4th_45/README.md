# 4th Practice - Docker Volumes

For created data in Docker Container, it will be removed when Container is removed 

When need to save data whenever Container is removed or not, **need to make Volumes**

* **Volumes** 
  * Folders that mounted on Local, mounted in inside of Containers
  * can use data created inside Docker Container
  * managed by Docker => Docker sets Volumes paths anonymously
* **Annoymous Volumes**
  * Edit in Dockerfile 
  * only specify path inside of Docker Container want to save, not Ouside of Conatiner
  * when Container removed and restart, Annoymous Volumes also removed and recreated
* **Named Volumes**
  * Edit in CMD Line when start Docker Container
  * Having Different to Annoymous Volumes, Named volumes created by Docker 
  * when Container restart, give Volumes parameter same, we can use same volume
  
</br>
 
        # need to concern about cross-device error
        # it makes files that inside of Container move to Outside of Container 

        ...
        VOLUME [ "/app/feedback" ]
        ...

        # Anonymous Volumes 
        # edit in Dockerfile

        # only specify path inside of Container, not path outside of Container
        # removed when container removed because docker recreated volume anonymously

        docker volume ls
        # check Volumes

        docker volume rm "VOL_NAME'
        docker volume prune** 
        # delete Volumes 

        docker run ~~ -v feedback:/app/feedback ~~
        # Named Volumes 
        # not edit in Dockerfile, but on CMD Line when we execute Docker Container

        # -v feedback:/app/feedback
            => feedback: specify name of volumes 
            => /app/feedback : specify path inside of Docker Container to save
        # not removed when container is removed 
