<h1>Develop a Python App to Access Key Vault Using a Service Principal</h1>


<h2>Description</h2>
Azure Active Directory (AD) can play a crucial role in not only user management, but also with application security for Azure-based solutions. When an application is registered in Azure AD and provided a service principal, it can be used to securely access other Azure resources that support Azure AD authentication. In this hands-on lab, we'll use an existing service principal and client secret to demonstrate how a registered application can use Azure AD authentication to access Key Vault.
<br />

<h2>Environments Used </h2>

- <b>Azure</b>
- <b>Windows 11</b>
- <b>Power Shell</b>
  
<h2>Program walk-through:</h2>

<h3>Create a Key Vault</h3>


1. From the top of the Azure portal resource group page, click Create.
2. In the search bar, type key vault.
3. Select Key Vault > Create.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. For the Subscription field, leave it as the pre-selected Azure Active Directory subscription.
2. From the Resource group dropdown menu, select the preexisting resource group that has already been created.
3. In the Key vault name field, enter a name for the key vault.
4. For the Subscription field, leave it as the pre-selected Azure Active Directory subscription.
5. From the Resource group dropdown menu, select the preexisting resource group that has already been created.
6. In the Key vault name field, enter a name for the key vault.
7. From the Region dropdown menu, select West US.
8. For the Pricing tier field, leave the Standard option selected.
9. Change the Days to retain deleted vaults field to 7.
10. At the bottom of the screen, click Next.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Under Access policies, click Create.
2. From the Configure from template dropdown menu, select Key, Secret, & Certificate Management.
3. Click Next.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. Navigate to the lab instructions page, and under Credentials, copy the provided Application Client ID for the Service Principal.
2. Paste the Application Client ID in the search bar.
3. From the context menu, select the service principal associated with the client ID.
4. Click Next > Next.



<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- At the bottom of the screen, click Create > Review + create.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Once the validation is complete and you are notified that it has passed, click Create at the bottom of the screen.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Set Up the Python Application</h3>

1. Open the Cloud Shell in the Azure portal or your own local development environment.

  - Click Bash.
  - Click Show advanced settings.
  - Change the Cloud Shell region to West US.
  - Under Storage account, make sure Create new is selected and enter a unique name.
  - Under File share, make sure that Create new is selected and enter a unique name.
  - Click Create storage.
  - If the storage is created successfully, the Bash shell will open at the bottom of the Azure portal page.

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Clone the Python application that was provided for the lab:
```
git clone https://github.com/linuxacademy/content-develop-a-python-app-to-access-key-vault-using-a-service-principal.git
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Navigate into the folder that has just been downloaded:
```
cd content-develop-a-python-app-to-access-key-vault-using-a-service-principal
```


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- List the files in the folder:
```
ls
```
- Open the Python application code file:
```
code pyappregkeyvault.py
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Here is the Python application in its’ entirety: 

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Install the azure.identity package:
```
pip install azure.identity
```

<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- Install the azure.keyvault.secrets package:
```
pip install azure.keyvault.secrets
```


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Configure the Python Application</h3>

- View your Azure account details to obtain the information necessary for configuration:
```
az account list
```



<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the Python application code, navigate to the “# Information required to authenticate using a Service Principal” section, and paste the tenant ID you copied in the tenant_id variable field.
2. Navigate to the lab instructions page, and under Credentials, copy the provided Application Client ID.
3. In the Python application code, paste the client ID you copied in the client_id variable field.
4. On the lab instructions page, copy the provided Secret.
5. In the Python application code, paste the secret you copied in the client_secret variable field.
6. In the Azure portal, copy the name of the key vault as it appears at the top of the page.
7. In the Python application code, navigate to the # Information for the Key Vault section, and paste the name of your key vault in the keyVaultName variable field.
8. Save the changes you made to the Python application code and close the editor.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

<h3>Run the Python Application and Access Secrets in the Key Vault</h3>

1. In the Bash shell, run the application:
```
python pyappregkeyvault.py
```
2. When prompted, Would you like to retrieve an existing secret? (Y/N):, type n and press Enter.
3. When prompted, Would you like to create a new secret? (Y/N):, type y and press Enter.
4. When prompted to Enter a name for your new secret:, type a name for your secret and press Enter.
5. When prompted to Enter a value for your new secret:, type a value for your secret and press Enter.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

- On the key vault's Secrets page, click Refresh.
- Verify that the secret you just created appears in the list of secrets.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

1. In the Bash shell, run the application again:
```
python pyappregkeyvault.py
```
2. When prompted, Would you like to retrieve an existing secret? (Y/N):, type y and press Enter.
3. When prompted, What is the name of the existing secret:, type the name of the secret you just created and press Enter.
4. Verify that the value that is returned matches the value for the secret that you just entered.
5. When prompted, Would you like to create a new secret? (Y/N):, type n and press Enter.


<br/>
 
<p align="center">
<img src="https://i.imgur.com/jjQxANw.png" height="80%" width="80%" alt="Disk Sanitization Step"/>
</p>

<br />
<br />

