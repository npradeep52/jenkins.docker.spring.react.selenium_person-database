# Sping React Project Template


## How to Run The Application
<img src = "./springreact-projecttemplate.gif">


### Running Web Server
* Open the project from `IntelliJ` using the `pom.xml` located at the root directory of this project.
* Run the `MainApplication.java` to begin the Web Server.
* If your application cannot run because something is occupying a port, use this command with the respective port number specified:
    * **OSX and Linux**
        * ``kill -kill `lsof -t -i tcp:8080` ``
    * **Windows**
        * _For use in command line_:
            * `for /f "tokens=5" %a in ('netstat -aon ^| find ":8080" ^| find "LISTENING"') do taskkill /f /pid %a`
        * _For use in bat-file_:
            * `for /f "tokens=5" %%a in ('netstat -aon ^| find ":8080" ^| find "LISTENING"') do taskkill /f /pid %%a`

#### Testing Web Server via Browser
* From a browser, navigate to `http://localhost:8080/h2-console/` and log into the database.

#### Testing Web Server via Postman
* Launch the [Postman](https://curriculeon.github.io/Curriculeon/lectures/java/web/postman/installation/content.html) app and enter the URI `http://localhost:8080/` and hit Send.
