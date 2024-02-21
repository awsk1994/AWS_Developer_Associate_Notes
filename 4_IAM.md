# IAM

## Users & Groups

* IAM = Identity and Access Management (Global Service)
* **Root account** created by default, shouldn't be used or shared
* **Users** are people within your organization, and can be grouped.
* **Groups** can only contain users; not other groups
* Users do not have to belong to a group, and user can belong to multiple groups

<img src="./img/4_IAM/1.png"/>

## Permissions
* **Users or Groups** can be assigned JSON documents called **policies**
* These policies define the **permissions** of the user
* In AWS, you apply the **least priviledge principal**; don't give more permissions that a user needs


<img src="./img/4_IAM/2.png"/>

## Hands On

* IAM -> Users 
    * Notice how the region for IAM is 'global'

<img src="./img/4_IAM/3.png"/>

* Click "Create User"
    * Why need to create user?
        * Because right now, you are using Root User; which is not best practice
        

<img src="./img/4_IAM/4.png"/>

* Click "Next"

<img src="./img/4_IAM/6.png"/>

* Click "Create group"
* Select Administrator Access

<img src="./img/4_IAM/7.png"/>


<img src="./img/4_IAM/8.png"/>
<img src="./img/4_IAM/9.png"/>
<img src="./img/4_IAM/10.png"/>


* IAM -> Dashboard -> AWS Account -> Sign-in URL for IAM users in this account -> Open this in incognito
    * Set alias for convenience
    * Reason for this: so we have 2 screens to work with

<img src="./img/4_IAM/11.png"/>

<img src="./img/4_IAM/12.png"/>

## IAM Policies

