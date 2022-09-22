# LWM2M server setup tutorial #

In this tutorial we will setup and test a lwm2m server and client on raspberry pi. Reference from professor Paul Schragger  https://github.com/pschragger/IOT_Tutorials_for_VU/tree/main/RPI_DEVICE_MANAGEMENT_INSTALL_tutorial

## Prerequistes #
### Information about my laptop
My laptop is a MacBook air M1 2020 version.
The router I am using is a GL.iNet model: GL-MT300N-V2.
The Raspberry Pi I am using is Model 4-B 8gb.
##To follow this tutorial you will need: 
A laptop with ssh installed, raspberry Pi dietPi accessible via ssh on wifi or ethernet, leshan server repository (https://www.eclipse.org/leshan/) at [ Leshan Github ]

## Steps ##

### Logon to Raspbery PI ###
1. using
```
ssh dietpi@(IPADDR_OF_PI)
```
2. use the password you setup in the pi configuration
3. This is a screenshot showing the desired pi terminal.
<img width="840" alt="1 firstchangetodietPiinsteadofroot" src="https://user-images.githubusercontent.com/97559266/191800198-a71941a8-3708-4c71-8fa1-fa35ce680601.png">

### Install development environment on RPI

1. Install git
   - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    
    - search for git from the software store (Git version was 17 when I was doing this experiment)   <img width="909" alt="2 searchforgit" src="https://user-images.githubusercontent.com/97559266/191800747-2bcf24a2-271d-4d85-a9ca-7c3b7a4f0e97.png">

    - press spacebar to select ( asterick [*] should show)<img width="921" alt="3 usespacetoselectthesoftwareyouwanttoinstall" src="https://user-images.githubusercontent.com/97559266/191801651-bcd5d964-61ea-4adf-99c0-353979521877.png">
    - tab to ok and press enter <img width="904" alt="4 starttheinstallationofGit" src="https://user-images.githubusercontent.com/97559266/191801782-3db9490e-2221-4aa8-8c75-e29f1bd73537.png">
- press enter and it should show that the Git is installed successfully <img width="889" alt="5 Gitsuccessfullyinstalled" src="https://user-images.githubusercontent.com/97559266/191801976-e4df9969-a448-4a72-a8cf-6ff4bd73ed4f.png">
    - check that is installed by using the command on the pi
    ```
    git --version
    ```
2. Install java jdk

  - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for Java JDK ( should be package 8 )<img width="917" alt="6 searchforjavainthesoftwaremanager" src="https://user-images.githubusercontent.com/97559266/191803790-7b8ed113-7eef-411d-94bc-4288840cfa6e.png">

    - press spacebar to select ( asterick [*] should show)<img width="873" alt="7 choosejavajdk8" src="https://user-images.githubusercontent.com/97559266/191804065-20832fa9-be25-4e1d-8176-5ed5b3db1a21.png">

    - tab to ok and press enter <img width="870" alt="8 installthejava8jdk" src="https://user-images.githubusercontent.com/97559266/191804130-bc48f807-eee0-4ef9-b584-51a4761941cb.png">
    - it should take less then 10 minutes to install the openJDK jre and jdk depending on network traffic
    - press enter and it should show that the java is successfully installed <img width="912" alt="9 javajdkinstalled" src="https://user-images.githubusercontent.com/97559266/191802600-ff585305-bb94-4cfa-948d-4ba9a239f5e0.png">
    - check that is installed by using the command on the pi
    ```
    java --version
    ```
3. Install maven on the rapberry pi
   1. In the dietpi directory create a download directory by typing following command
   ```
   mkdir download
   ```
   2. change directory into the download directory
   ```
   cd download
   ```
   3. download the latest maven tarball using wget, the following is an example - be sure to check the latest version on [apache maven](https://maven.apache.org/download.cgi)
   ```
   wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
   ```
   Here is a screen shot showing maven is downloaded <img width="910" alt="10 downloadmaven" src="https://user-images.githubusercontent.com/97559266/191813302-74866471-bdab-4d57-9cef-ab3dde3b2299.png">

   
   4. unpack the tarball using the following command <img width="889" alt="11 unzipmaven" src="https://user-images.githubusercontent.com/97559266/191811757-8f8e5001-3574-4571-8048-2223ae01b231.png">

   ```
   tar xzvf apache-maven-3.8.6-bin.tar.gz
   ```
   5. Add the bin directory of the created directory apache-maven-3.8.6 to the PATH environment variable
   6. Confirm installation using<img width="892" alt="12 verifiedthatmavenisworking" src="https://user-images.githubusercontent.com/97559266/191811827-91867089-5109-420d-8618-b4d24d84da7f.png">

   ```
   mvn -v
   ```
   7. Setup the environment variables to add maven to the paths taken from [maven install instructions](https://maven.apache.org/install.html)
      - add the bin directory to the path
      ```
      echo 'PATH="${PATH}:~/download/apache-maven-3.8.6/bin"' >>  ~/.bashrc
      ```
   8.  test maven installation using
   ```
   bash
   mvn -v
   ```
   results should look like
 
   Apache Maven 3.8.6 (84538c9988a25aec085021c365c560670ad80f63)
Maven home: /home/dietpi/download/apache-maven-3.8.6
Java version: 17.0.3, vendor: Debian, runtime: /usr/lib/jvm/java-17-openjdk-arm64
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.15.32-v8+", arch: "aarch64", family: "unix"
   
   9. create a JAVA_HOME environment variable pointing the install jdk

      - add the JAVA_HOME to the .bashrc (check your java directory matches the path provided below change as required )
      ```
      sudo echo 'JAVA_HOME="/usr/lib/jvm/java-17-openjdk-arm64"' >> ~/.bashrc
      ```
      - check that the install was complete with
      ```
      bash
      echo $JAVA_HOME
      ```
      result should look like
      ```
      /usr/lib/jvm/java-17-openjdk-arm64
      ```

4. Install nodejs environment

  - On command line in dietpi start dietpi-software
    ```
    sudo dietpi-software
    ```
    - search for NodeJS <img width="904" alt="13 installnodejsenvironment" src="https://user-images.githubusercontent.com/97559266/191812340-a3166c40-f05a-4068-be31-60433b5cce47.png">


    - press spacebar to select ( asterick [*] should show)<img width="914" alt="14 installnodejs" src="https://user-images.githubusercontent.com/97559266/191812370-14bd7605-37fb-48d2-9270-bb3a6d1cc195.png">
    - tab to ok and press enter 
    - it should take less then 10 minutes to install the openJDK jre and jdk depending on network traffic
    - press enter and it should show that the NodeJs is successfully installed <img width="1024" alt="15 nodejsinstallationcompleted" src="https://user-images.githubusercontent.com/97559266/191812439-66aa6a32-7902-494f-804b-6ad36968432c.png">
5. Install leshan git and build  - instructions form [leshan git](https://github.com/eclipse/leshan)
   - clone the leshan repo using
   ```
   cd
   mkdir projects
   cd projects
   git clone https://github.com/eclipse/leshan.git
   ```
   cloning the directory should be less than a minute
   - build leshan
     ```
     cd ~/projects/leshan
     mvn clean install
     ```
   - The build may take 20 minutes or longer
<img width="993" alt="16 createprojectdirectoryandclonetheleshanrepo" src="https://user-images.githubusercontent.com/97559266/191812504-5cb90330-cdc2-4301-a72d-59e961953886.png">
   - verify the server build successfully
<img width="1025" alt="17 buildtheserversuccessful" src="https://user-images.githubusercontent.com/97559266/191812723-ce62ed0a-2014-47da-affd-a04f9f7083e7.png">


### Test the leshan server
1. Start the server using
  ```
  cd ~/projects/leshan
  java -jar leshan-server-demo/target/leshan-server-demo-*-SNAPSHOT-jar-with-dependencies.jar &
  ```
  -  Connect on Leshan demo UI: http://RPI_IPADDR:8080

   My Raspberry PI is using 192.168.8.150 ( from the router admin client page)
   therefore I will use
   ```
   http://192.168.8.150:8080
   ```
   this will bring up te leshan register client page. It should be empty for now
   
   <img width="1431" alt="18 emptypagewiththeserver" src="https://user-images.githubusercontent.com/97559266/191812811-13acb8c0-7bed-47bc-b1e0-13802753835e.png">



  - run the leshan client to add it to the page
  ```
  java -jar leshan-client-demo/target/leshan-client-demo-*-SNAPSHOT-jar-with-dependencies.jar
  ```
  <img width="1034" alt="19 registerleshanclient" src="https://user-images.githubusercontent.com/97559266/191812863-18390df6-b6e3-41a0-9900-d5479fbec173.png">

  

  The result should show the registration of your DietPI host as a Temperature client endipoint
  This end point should continue to register every minute.
  <img width="1440" alt="20 leshanservershowingdietpi" src="https://user-images.githubusercontent.com/97559266/191812889-02c2f663-94ee-41a5-b4b9-d06bb40b03f2.png">

  using ctrl-c to stop the client

  ### check the server page in the leshan server page to see the active url info and public keys and server cert info

###  Continue to the ESP32 lwm2m client build ###
