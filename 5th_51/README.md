# 5th Practice - Manangine Data in Docker 

To manage Data and File in Docker Image & Container, there are **"some ways"** to manage 

* **Volume** (Managed by Docker)
  * Anonymous_Volume
  * Named_Volume
* **Bind_Mounts** (Managed by Developer)
  * Read-Only Bind_Mounts 
  * Combine with Anonymous_Volume 
    * To manage Local file or folder not to override inside of Docker Container 
* **.dockerigore**
  
* **ARGuments & ENVironment_Variables**  
  * Build-Time ARGuments
  * Run-Time ENVironment_Variables

</br>
</br> 

* Code or CLI in Dockerfile or CLI 
  
        # # need to concern about cross-device error
        # it makes files that inside of Container move to Outside of Container 

        ~~
        VOLUME [ "/app/feedback" ]
        ~~

        # Anonymous Volumes 
        # edit in Dockerfile
        # only specify path inside of Container, not path outside of Container
        # removed when container is removed 
        # => because docker recreated volume when restart Container

        docker volume ls 
        # list all active Volumes

        docker volume rm "VOL_NAME'
        docker volume prune 
        # prune : remove all unused volumes 
        # delete Volumes 
        # can't remove when volumes is currently in use
        # => need to stop volumes first

        docker volume inspect "VOL_NAME"
        # see information about specific volume
        # Mountpoint 
        # => binding to Virtual Mahchine (when docker run by VM) Path
        # => not a Local path.
        #####################################################################

        docker run ~~ -v feedback:/app/feedback ~~
        # Named Volumes 
        # not edit in Dockerfile, but on CMD when we execute Docker Container

        # -v feedback:/app/feedback 
        # => feedback: specify name of volumes 
        # => /app/feedback : specify path inside of Docker Container to save
        # not removed when container is removed 
        #####################################################################

        docker run ~~ -v feedback:/app/feedback 
                    -v "Local absolute Path:Mounting Path inside Container:ro"  
                    -v /app/node_modules ~~
        # Bind Mounts
        # not edit in Dockerfile
        # but on CMD Line when we execute Docker Container

        # => Local Path that have all codes and content
        # absolute path of project folder

        # need to set Docker can access to Local folder 
        # => Prefereces of Docker - Resources - statement parent folder
        # check about Settings of Docker Toolbox to share folders

        # ~v /app/node_modules
        # create more specific sub-volumes 
        # Fixing about Bind-Mount's existing more specific folder
        # locking that folder not to override

        # Read-Only volumes
        # append ":ro" end of creating Bind Mounts CLI

        # Bind Mounts : not managed by Docker 
        # => not list in "docker volume ls"
        #####################################################################

        ~~
        ENV PORT 80 
        ~~
        EXPOSE $PORT
        ~~

        # Ensure Environment Variable in Dockerfile 
        # available in entire application environment 

        # can use variable name in application after registerd ENV
        # ${ENV_NAME} => need $ to tell Docker ENV_name 

        # ENV => not fixed value, only default value 
        # => can configure while Docker Container run 
        # => docker run ~~ --env PORT=199 -e PORT1=200 ~~ 

        # can make .env file => list all env want to set
        # => docker run ~~ --env-file ./.env ~~ 
        #####################################################################

        ~~
        ARG DEFAULT_PORT=80
        ~~
        ENV PORT $DEFAULT_PORT
        ~~

        # cannot use in code or file, only use in Dockerfile
        # => In Dockerfile ARG can't use in CMD instruction

        # can make dynamic argument setting dynamic Environment Variable
        # can make different image based on same Dockerfile by differ args 
        # => docker build ~ --build-arg DEFAULT_PORT=80 ~ 
        #####################################################################
