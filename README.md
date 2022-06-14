# A Passwrod Vault with a TEE (and chrome extension)
TEE Project of David Berger and Eyal Seckbach

## Overview
Our project has 3 parts:
(1) a chrome extension (**JavaScript, HTML** - independently learned)
(2) a Host /Server application (**C#**)
(3) an Applet that runs in a **TEE** (Trusted Execution Environment) using Intel’s DAL (**java**)

The extension communicates with the Server via a **Websocket**, and the Host communicates with the Applet with **Byte arrays** (Intel’s built-in system). 

The extensions pulls the URL from the browser, and sends to the Host (and to the Applet). The Applet returns a randomly generated password (using **Sha1 algorithm**, based on a **time seed** given by Host). The pairs of URL’s and Password are stored in the Applet’s secure **Flashstorage**. All communication is echoed in the console opened by the a Host (helpful for debugging). 

For **2-point security**, the user must use his computer (“_what you have_”) and enter a master password (“_what you know_”) before accessing any information. 

## How to run our Program (after downloading the Source Code):
(1) Ensure that Intel’s DAL is working, and compile the program into an **".dalp"** file. Increase the flash storage size in the Manifest:
![image](https://user-images.githubusercontent.com/91850832/172611795-ca981c72-9d3f-472c-ab55-574a56447c5a.png)

(2) Set up the Host program, ensure that the applet file path (must be for local computer!) and applet Id are correct
![image](https://user-images.githubusercontent.com/91850832/172613221-b14106a2-af67-431a-86ad-4abf03b36eaa.png)

(3) Run the Server (from the Host application)
![image](https://user-images.githubusercontent.com/91850832/172613513-5f651bc3-110a-4d58-94ed-a304810cb468.png)

(4) Upload the extension’s folder to your google account (**"load unpacked"**)
![image](https://user-images.githubusercontent.com/91850832/172614958-61e22d60-9a5d-403f-a14e-b06fc05de656.png)

(5) Enjoy
![image](https://user-images.githubusercontent.com/91850832/172630405-0717f43d-e0cf-4458-98f8-cb95239d9ff1.png)
![image](https://user-images.githubusercontent.com/91850832/172630716-af28b431-4324-4d95-a9f5-6707fc70cd79.png)
![image](https://user-images.githubusercontent.com/91850832/172663317-8cfb3861-324e-464f-8976-763b6ccadcc9.png)



## (Threat Modeling)
text text text text text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text texttext text text



### Points about the source code:
- [ ] Relevant exceptions in the Host
- [ ] Clear, Universal Emuns
- [ ] Organized API for Applet, and within Applet


### Future ideas:
- [ ] Enabling Multiple users to use the TEE
- [ ] A better random seed (ex physical world generated instead of time...)
- [ ] Allowing User to hide the Console’s Echo






## Motivation of Product:

#### What’s on the market now:
There are many different programs (_software_) which store a User’s passwords (and websites), often storing them in a cloud, theoretically accessible from any location. 

#### Our idea - A Local Password Vault in a TEE:
Instead of storing this sensitive data in a cloud/software, we have a _hardware_ solution - we will store passwords in a **local TEE (Trusted Execution Environment)**. 
A Host app on the computer can communicate with the TEE, and open a WebSocket (with local host) which will communicate with a Google Chrome Extension, allow the User to quickly save pairs of URLs and passwords

#### Strengths of a local Pwd Vault:
 * Hardware is often more secure than software (objectively); less bugs and backdoors, less attack surfaces
 * Implementation, management is much simpler

#### Weaknesses of a local Pwd Vault:
 * Inaccessible if user is not near computer 
 * Not easily portable to another computer (even to switch permanently)
 * If something happens to the Hardware, the information is lost 
 * Not as scalable
 * Must secure communication over the Web socket