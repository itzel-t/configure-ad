<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" height="40%" width="70%"alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory (On-Premises) Within Azure</h1>
In this tutorial, we'll walk you through implementing AD on-premises within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10

<h2>High-Level Deployment and Configuration Steps</h2>

- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Set up Remote Desktop for non-administrative users on Client-1

<h2>Deployment and Configuration Steps</h2>
<br />
<br />
<h3 align="center">Create Resources in Azure</h3>
<br />
<p>
  Create a Virtual Network and name it "Active-Directory-Vnet" and name the Resource Group "Active-Directory-Lab":
</p>
<br />  
<p>
  <img width="822" height="701" alt="Screen Shot 2025-10-13 at 1 22 04 PM" src="https://github.com/user-attachments/assets/f29e79f1-28cc-46c1-955f-d7a171ac489f" />
</p>
<p>
  Create a Virtual Machine (Windows 2022) and name it "DC-1". Place it in the resource group "Active-Directory-Lab" and in networking, place it in "Active-Directory-Vnet". 
</p> 
<p>
  Username: Labuser
</p> 
<p>
  Password: Networking10
</p>
<br />  
<p>
  <img width="829" height="701" alt="Screen Shot 2025-10-13 at 1 22 39 PM" src="https://github.com/user-attachments/assets/85baa35b-a8a0-4a0c-af0d-d25fd6214874" />
</p>
<h3 align="center"> ↓ </h3>
<p>
<img width="1095" height="657" alt="Screen Shot 2025-10-13 at 1 24 06 PM" src="https://github.com/user-attachments/assets/f6d95193-fef7-4075-9850-f40cdfa4aca5" />
</p>
<h3 align="center"> ↓ </h3>
<p>
<img width="1084" height="580" alt="Screen Shot 2025-10-13 at 1 24 10 PM" src="https://github.com/user-attachments/assets/d853748d-07e1-49dd-871c-ec8335434fd6" />
</p>
<h3 align="center"> ↓ </h3>
<p>
<img width="919" height="662" alt="Screen Shot 2025-10-13 at 1 27 06 PM" src="https://github.com/user-attachments/assets/a61f32bf-4b1d-4da9-81b9-e343de6bd887" />
</p> 
<br />  
<p>
  Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in the previous step:
</p>
<p>
  Username: Labuser
</p> 
<p>
  Password: Networking10
</p>
<br />  
<p>
<img width="1069" height="631" alt="Screen Shot 2025-10-13 at 1 31 54 PM" src="https://github.com/user-attachments/assets/f382cab8-f336-46cc-86e7-b1e91982cb39" />
</p>
<h3 align="center"> ↓ </h3>
<p>
<img width="973" height="513" alt="Screen Shot 2025-10-13 at 1 31 59 PM" src="https://github.com/user-attachments/assets/3bfe6a86-fe93-4064-8119-b47356f20b2e" />
</p>
<h3 align="center"> ↓ </h3>
<p>
<img width="977" height="513" alt="Screen Shot 2025-10-13 at 1 32 16 PM" src="https://github.com/user-attachments/assets/7a64e558-1b3a-441b-8b10-4388ae53ec0f" />
</p>
<br />
<br />
 <h3 align="center"> Set the Domain Controller’s NIC Private IP address to be static </h3>
<p>
  Click on DC-1 → Networking → Network Setting ↓
</p>
<p>
  <img width="822" height="657" alt="Screen Shot 2025-10-13 at 1 43 18 PM" src="https://github.com/user-attachments/assets/52aba705-2ae4-433e-b3a2-a641175ae55e" />
</p>
<p>
  Click on Network Interface / IP configuration ↓
</p>
<br />  
<p>
  <img width="826" height="550" alt="Screen Shot 2025-10-13 at 1 43 26 PM" src="https://github.com/user-attachments/assets/3ae0bc46-5c68-4415-b3f3-8dfa758932bb" />
</p>
<br />  
<p>
  Click on "ipconfig1" ↓
</p> 
<p>
 <img width="810" height="647" alt="Screen Shot 2025-10-13 at 1 44 35 PM" src="https://github.com/user-attachments/assets/9a5cc83c-5b14-458b-bd32-b3c1793ff25a" />
</p>
<br />  
<p>
  Change the private IP address setting from Dynamic to Static and save ↓
</p>
<p>
  <img width="825" height="659" alt="Screen Shot 2025-10-13 at 1 44 51 PM" src="https://github.com/user-attachments/assets/f92b73b2-0524-4a7c-b253-f31d4d49e60b" />
</p>
<br />
<br />
<h3 align="center">Connect to DC-1 </h3>
<br />
<p>
  Open windows and log in to DC-1 by using the public IP Address. In this lab, it would be helpful to name them to distinguish between the two VMs. ↓
</p>
<br />  
<p>
  <img width="824" height="686" alt="Screen Shot 2025-10-13 at 1 46 15 PM" src="https://github.com/user-attachments/assets/523210c7-ff1c-4273-95ef-b63bc2d56877" />
</p>
<h3 align="center"> ↓ </h3>
<p>
  <img width="1157" height="693" alt="Screen Shot 2025-10-13 at 1 46 59 PM" src="https://github.com/user-attachments/assets/626592b0-649f-4197-b2f3-6f58407b38c4" />
</p>  
<h3 align="center"> ↓ </h3>
<p>
  <img width="1166" height="709" alt="Screen Shot 2025-10-13 at 1 48 35 PM" src="https://github.com/user-attachments/assets/8b41e460-3f38-452e-8536-4f06d572f058" />
</p>  
<br />
<br />
<h3 align="center">Turnning off Firewall in DC-1</h3>
<p>
  Right-click start → run
</p>
<br />  
<p>
  <img width="829" height="752" alt="Screen Shot 2025-10-13 at 1 50 16 PM" src="https://github.com/user-attachments/assets/5ad1a26e-2d7e-4200-ae93-60c034666cfd" />
</p>  
<p>
  Type in wf.msc ↓
</p>  
<p>
  <img width="826" height="761" alt="Screen Shot 2025-10-13 at 1 50 28 PM" src="https://github.com/user-attachments/assets/cb82f063-0b62-4eab-9f55-0631994d832a" />
</p>
<br />
<p>
  Click on Windows Defender Firewall and turn off the firewall in Domain Profile, Private Profile, Public Profile, and IPsec Settings ↓
</p> 
<br />  
<p>
  <img width="1429" height="691" alt="Screen Shot 2025-10-13 at 1 51 44 PM" src="https://github.com/user-attachments/assets/d9a00a87-7266-4836-92d5-508bcd10d1f8" />
</p>  
<br />
<br />
<h3 align="center">Changing Client-1 DNS Server</h3>
<p>
  We are changing Client-1's DNS to connect to DC-1's Private IP address. Go back to Azure and find the DC-1 Private IP address and copy it. ↓
</p> 
<br />  
<p>
  <img width="818" height="693" alt="Screen Shot 2025-10-13 at 1 55 24 PM" src="https://github.com/user-attachments/assets/00f6d805-e999-443b-8109-3ccb41759ce6" />
</p>  
<br />  
<p>
  Go back to the home and click on Client-1. Networking → Network Setting → Network Interface / IP Configuration ↓
</p> 
<br />  
<p>
 <img width="828" height="594" alt="Screen Shot 2025-10-13 at 1 55 54 PM" src="https://github.com/user-attachments/assets/6b1fd111-8811-413b-98dc-323cc0dc4edb" />
</p>  
<p>
  Setting → DNS Server → Custom → Save ↓
</p>
<p>
  <img width="827" height="697" alt="Screen Shot 2025-10-13 at 1 56 28 PM" src="https://github.com/user-attachments/assets/00f53f0f-0381-4727-b1c6-2ab0672c6457" />
</p>
<h3 align="center"> Go back to VM and restart Client-1 ↓ </h3> 
<p>
  <img width="823" height="690" alt="Screen Shot 2025-10-13 at 1 57 41 PM" src="https://github.com/user-attachments/assets/f1b486ff-a092-4f3f-935e-a870fad9aae1" />
</p>  
<h3 align="center"> ↓ </h3>
<p>
  <img width="825" height="591" alt="Screen Shot 2025-10-13 at 1 57 45 PM" src="https://github.com/user-attachments/assets/07f73544-c82e-44cb-9159-3bc2c0881c7c" />
</p>  
<h3 align="center"> Checking Client-1 connectivity with DC-1 </h3>
<br />
<p>
  First, start by logging in to Client-1 and click no to everything in the privacy settings ↓
</p>
<p>
  <img width="1138" height="712" alt="Screen Shot 2025-10-13 at 2 01 23 PM" src="https://github.com/user-attachments/assets/deeaa6a4-9cdf-4d03-9f7c-713cda21f62a" />
</p>  
<h3 align="center"> ↓ </h3>
<p>
  <img width="1166" height="718" alt="Screen Shot 2025-10-13 at 2 01 40 PM" src="https://github.com/user-attachments/assets/0c0ac334-2db1-46b9-977b-84e05dd6ae4e" />
</p>  
<h3 align="center"> ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-13 at 2 03 04 PM" src="https://github.com/user-attachments/assets/c1bd897b-edda-4a0c-a9df-97ef0c7c8629" />
</p>  
<p>
  Search for Windows PowerShell ↓
</p>
<p>
  <img width="957" height="595" alt="Screen Shot 2025-10-13 at 2 04 25 PM" src="https://github.com/user-attachments/assets/2ac32e42-35ce-431a-9949-79982ab8fd7a" />
</p>
<p>
  In our Lab DC-1's Private IP address is 10.0.0.4, so that is what we will use to ping the DC-1 Server ↓
</p>
<p>
  <img width="959" height="595" alt="Screen Shot 2025-10-13 at 2 05 49 PM" src="https://github.com/user-attachments/assets/bc3e665f-0edd-4be1-8cd6-d2e4c6b3073e" />
</p>  
<h3 align="center">   ↑ Success Connection! ↑ </h3>
<br />  
   <h3 align="center"> Now going back to our DC-1 to install Roles and Features ↓ </h3>
<p>
  <img width="831" height="784" alt="Screen Shot 2025-10-13 at 2 12 19 PM" src="https://github.com/user-attachments/assets/ed7d224c-15ab-4433-92ba-af8bf8561a00" />
</p>
<p>
   Next → Add Features → Yes to restart → and once it has completed installing, you can close it. ↓
</p>
<p>
  <img width="1123" height="788" alt="Screen Shot 2025-10-13 at 2 12 34 PM" src="https://github.com/user-attachments/assets/b91795eb-77cc-48d8-ad95-ef3b55d8895b" />
</p>
<h3 align="center"> ↓ </h3>
<p>
  <img width="1132" height="793" alt="Screen Shot 2025-10-13 at 2 12 49 PM" src="https://github.com/user-attachments/assets/6d99c7a9-f53e-4fe3-bbcc-4be5088ee790" />
</p>
<h3 align="center"> ↓ </h3>
<p>
  <img width="1128" height="794" alt="Screen Shot 2025-10-13 at 2 13 22 PM" src="https://github.com/user-attachments/assets/6051ed24-de32-4db9-bf06-f75e75811c6a" />
</p>
<h3 align="center"> ↓ </h3>
<p>
  <img width="965" height="781" alt="Screen Shot 2025-10-13 at 2 13 25 PM" src="https://github.com/user-attachments/assets/0ff62aa9-ba32-43b3-8cc6-dbd32bd68973" />
</p>
<h3 align="center"> ↓ </h3>
<p>
  <img width="1127" height="788" alt="Screen Shot 2025-10-13 at 2 18 52 PM" src="https://github.com/user-attachments/assets/422f574d-240f-4229-8f35-b6e2bf5178fc" />
</p>
<br />
<p>
  Then we will promote the server as the Domain Controller ↓
</p>
<p>
  <img width="1128" height="790" alt="Screen Shot 2025-10-13 at 2 19 41 PM" src="https://github.com/user-attachments/assets/5d22e374-f518-4bf2-b0b1-4bca5887da45" />
</p> 
<h3 align="center">Installing Active Directory Domain Services</h3>
<br />
<p>
  Root Domain Name → "mydomain.com" ↓
</p>
<p>
  <img width="1127" height="790" alt="Screen Shot 2025-10-13 at 2 19 55 PM" src="https://github.com/user-attachments/assets/aa75c0ae-b9cd-4637-945c-f0fe05766e02" />
</p>
<h3 align="center">  Password → "Password1" ↓ </h3>
<p>
  <img width="1128" height="789" alt="Screen Shot 2025-10-13 at 2 20 12 PM" src="https://github.com/user-attachments/assets/f423e73d-2ca1-4016-88dc-587b769d8ba4" />
</p> 
<h3 align="center">  ↓ </h3>
<p>
  <img width="1126" height="790" alt="Screen Shot 2025-10-13 at 2 21 25 PM" src="https://github.com/user-attachments/assets/6b6bfe76-c055-4a16-ba88-8b4a5f577e48" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1132" height="681" alt="Screen Shot 2025-10-13 at 2 21 30 PM" src="https://github.com/user-attachments/assets/db778c3f-1c23-48cf-8f17-b68b567b546c" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1129" height="793" alt="Screen Shot 2025-10-13 at 2 21 39 PM" src="https://github.com/user-attachments/assets/869bf62f-e96c-474c-9955-46dd9a51db6b" />
</p> 
<h3 align="center">  ↓ </h3>
<p>
  <img width="1127" height="789" alt="Screen Shot 2025-10-13 at 2 22 17 PM" src="https://github.com/user-attachments/assets/74d2b59e-ab20-4c4a-86c1-9b95a2f41a79" />
</p>  
<br />
<br />
<p>
  Once installation is done, it will automatically restart the PC ↓
</p>
<p>
  <img width="1127" height="791" alt="Screen Shot 2025-10-13 at 2 24 18 PM" src="https://github.com/user-attachments/assets/c4f1b808-fa6a-4dab-836b-3cb97fb9e24b" />
</p>
<p>
 When you log back in, you can now use the domain we just created. Remember, it is important to use "\" when separating the domain and the username ↓
</p>
<p>
  <img width="442" height="233" alt="Screen Shot 2025-10-14 at 12 57 11 PM" src="https://github.com/user-attachments/assets/e7afb9ee-8630-4c99-a3b5-3737b7871ded" />
</p>
<br />
<br />
<h3 align="center">Active Directory Users and Computers ↓ </h3>
<p>
  <img width="955" height="594" alt="Screen Shot 2025-10-14 at 1 01 13 PM" src="https://github.com/user-attachments/assets/46e55081-02e1-4d29-ae63-a1c142c06dbe" />
</p> 
<p>  
  Right-click "mydomain.com" → New → Organizational Unit → _EMPLOYEES ↓
</p>
<p>
  <img width="955" height="592" alt="Screen Shot 2025-10-14 at 1 02 24 PM" src="https://github.com/user-attachments/assets/a4312043-8b72-484f-a9ad-0a43129bc60a" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="829" height="789" alt="Screen Shot 2025-10-14 at 1 03 28 PM" src="https://github.com/user-attachments/assets/fde50499-a78c-42d1-8d38-990d30055634" />
</p>
<br />
<p>
  Right-click "mydomain.com" → New → Organizational Unit → _ADMINS ↓
</p>
<p>
   <img width="828" height="795" alt="Screen Shot 2025-10-14 at 1 03 53 PM" src="https://github.com/user-attachments/assets/cadbd1d5-e965-4916-a4e1-5afdd3ba2f9c" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="824" height="787" alt="Screen Shot 2025-10-14 at 1 04 18 PM" src="https://github.com/user-attachments/assets/0ac5210a-c3be-42a4-a63f-387e7e4cbc96" />
</p>
<p>
  Then you'll refresh "mydomain.com" so it can be organized alphabetically. After this, we will right-click _ADMINS to create a new user. We will name her Jane Doe and have her user log in be "jane_admin" and have her password be "Password1".  ↓
</p>
<p>
  <img width="827" height="788" alt="Screen Shot 2025-10-14 at 1 04 50 PM" src="https://github.com/user-attachments/assets/c758197c-0fd1-4151-9cc0-93ba46f69f1b" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="828" height="786" alt="Screen Shot 2025-10-14 at 1 05 36 PM" src="https://github.com/user-attachments/assets/5d90bf7d-4aa7-485c-8148-db80ffae48d1" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="828" height="791" alt="Screen Shot 2025-10-14 at 1 07 13 PM" src="https://github.com/user-attachments/assets/8aa1bbd6-d623-43ed-ab6f-40c9e299f596" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="829" height="795" alt="Screen Shot 2025-10-14 at 1 08 15 PM" src="https://github.com/user-attachments/assets/8de6b8ab-011b-44d2-8049-e5f04c6d4126" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="825" height="786" alt="Screen Shot 2025-10-14 at 1 08 34 PM" src="https://github.com/user-attachments/assets/f4e85f1f-e995-4bb5-8ef2-24555686c838" />
</p>  
<br />
<br />
<p>
 Now, to make Jane Doe an admin, we're going to right-click Jane Doe and click on properties. Then, we will add her to the Members of and enter the object names as "domain admins". ↓
</p>
<p>
  <img width="828" height="787" alt="Screen Shot 2025-10-14 at 1 09 06 PM" src="https://github.com/user-attachments/assets/8bea623f-d26e-4505-b4b0-7c9ccf3baf2c" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="832" height="791" alt="Screen Shot 2025-10-14 at 1 09 28 PM" src="https://github.com/user-attachments/assets/83f4e956-2ce6-42f4-9209-7bac3b7f67d0" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="825" height="794" alt="Screen Shot 2025-10-14 at 1 09 47 PM" src="https://github.com/user-attachments/assets/e1c63d54-f96c-4ee5-998a-2e427a1bd3e7" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="830" height="685" alt="Screen Shot 2025-10-14 at 1 09 53 PM" src="https://github.com/user-attachments/assets/91a21ed0-c2d3-4ca7-a680-3aa16e3a1664" />
</p>
<br />
<br />
<h3 align="center">Log in as Jane Doe in Client-1 ↓ </h3>
<br />
<p>
 <img width="439" height="234" alt="Screen Shot 2025-10-14 at 1 47 47 PM" src="https://github.com/user-attachments/assets/aed9fc5f-4e25-46f0-8233-7ff817e74f89" />
</p>
<p>
System → Rename this PC (advanced) → Change Domain → input "mydomain.com" in Domain change → Confirm domain change ↓
</p>
<p>
  <img width="824" height="600" alt="Screen Shot 2025-10-14 at 1 14 46 PM" src="https://github.com/user-attachments/assets/322c2308-9609-4c6f-bf9e-89def2117b7e" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 16 38 PM" src="https://github.com/user-attachments/assets/3eb173e5-2794-429f-8562-6a22d4ad7170" />
</p>
<h3 align="center">  ↓ </h3>
<p>
<img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 16 56 PM" src="https://github.com/user-attachments/assets/f38235ab-e209-40b1-aa7a-d806ab8bda84" />
</p>
<h3 align="center">  ↓ </h3>
<p>
 <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 17 20 PM" src="https://github.com/user-attachments/assets/fe04021c-16d5-477f-8a67-aa3780b653d4" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 19 05 PM" src="https://github.com/user-attachments/assets/55c42331-39ee-4778-8db7-7af6a618de48" />
</p>
<p>
  Agree to the domain change and restart the PC ↓
</p>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 19 42 PM" src="https://github.com/user-attachments/assets/7cc3f036-3aa1-4f4f-9b62-252089c2d0d9" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 19 45 PM" src="https://github.com/user-attachments/assets/2075cccb-7894-4ec6-8d5a-8b91b293b16e" />
</p>
<br />
<br />
<h3 align="center">Log in as Jane Doe in DC-1  ↓ </h3>
<p>
   <img width="444" height="237" alt="Screen Shot 2025-10-14 at 1 11 44 PM" src="https://github.com/user-attachments/assets/a37490c6-c7b2-4a82-a22c-1899755e5f15" />
</p>
<p>
 Go to Active Directory Users and Computers to create a new folder called "_CLIENTS" and move Client-1 from the Computers folder to _CLIENTS. ↓ 
</p> 
<p>  
  <img width="818" height="793" alt="Screen Shot 2025-10-14 at 1 25 05 PM" src="https://github.com/user-attachments/assets/39faf9b4-5c58-4073-a7f3-67418502cbc9" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="828" height="786" alt="Screen Shot 2025-10-14 at 1 25 23 PM" src="https://github.com/user-attachments/assets/92236b19-8deb-422d-87c8-ae93694964a0" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="826" height="790" alt="Screen Shot 2025-10-14 at 1 25 37 PM" src="https://github.com/user-attachments/assets/884d6139-a501-4b7d-a201-d8629835dfaf" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img src="https://i.imgur.com/6QOGzs6.png" height="75%" width="100%" alt="observe create users script"/>
</p>
<br />
<br />
<h3 align="center"> Now Jane Doe will log back into Client-1 → System → Remote Desktop → "Select users that can remotely access this PC" → Add users → add domain users  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 49 46 PM" src="https://github.com/user-attachments/assets/a41a5991-b5b7-4302-97af-4a6139974c5e" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 54 04 PM" src="https://github.com/user-attachments/assets/76f34567-565d-437d-b01d-4964bfe32d94" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 54 23 PM" src="https://github.com/user-attachments/assets/27857781-f90f-4ceb-9868-8f97ec6b76b4" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 54 56 PM" src="https://github.com/user-attachments/assets/a34796cc-b521-4e4a-ba5c-b47ef1cf371e" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1434" height="704" alt="Screen Shot 2025-10-14 at 1 55 02 PM" src="https://github.com/user-attachments/assets/d2cf50f2-6485-4a65-9d33-861ac9f02997" />
</p>
<br />
<br />
<h3 align="center"> Jane will log back into DC-1 and open PowerShell ISE as an administrator ↓ </h3>
<p>
  <img width="828" height="602" alt="Screen Shot 2025-10-14 at 1 23 59 PM" src="https://github.com/user-attachments/assets/de081fe6-c577-40d9-a35f-1bf06c727be7" />
</p>  
<p>
  We are going to save this file in the Desktop as "create-users" ↓
</p> 
<br />
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 1 59 52 PM" src="https://github.com/user-attachments/assets/8523227d-1b1f-4898-bf07-c9ae0a1c6971" />
</p> 
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 00 50 PM" src="https://github.com/user-attachments/assets/c41fea5b-77f7-4dfc-9122-ae146ace7028" />
</p>  
<p>
Please create a new file, and paste this script to create users (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1), and then we are going to let it run ↓
</p>  
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 00 40 PM" src="https://github.com/user-attachments/assets/71679700-6b21-4201-a2bb-dd69c9875520" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 02 12 PM" src="https://github.com/user-attachments/assets/769ed905-4391-4a73-895d-7a549a8e53f2" />
</p>
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="708" alt="Screen Shot 2025-10-14 at 2 02 18 PM" src="https://github.com/user-attachments/assets/3f5c91c8-660d-4f00-98b6-5f9cd09b04ae" />
</p>  
<p>
  If nothing went wrong, then you will see random users being created. You will also be able to see the new users in _EMPLOYEES.  ↓ 
</p>  
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 02 44 PM" src="https://github.com/user-attachments/assets/02c9c035-5ca1-4cf0-a436-27bf1da8cc3b" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 04 11 PM" src="https://github.com/user-attachments/assets/b03949eb-2633-4553-a33d-6b910a66a269" />
</p>  
<br />
<br />
<h3 align="center">  Now chose a random user in _EMPLOYEES and add them in Members of  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 05 13 PM" src="https://github.com/user-attachments/assets/dbdf6571-b4d0-418b-8776-d63c80f578e2" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1440" height="900" alt="Screen Shot 2025-10-14 at 2 06 50 PM" src="https://github.com/user-attachments/assets/c9ca7883-6400-4935-b611-90c7da2464d6" />
</p>  
<p>
  By adding them as a member of you will now be able to log in to Client-1 using their domain and bring us to the end of this lab. ↓
</p> 
<p>
  <img width="444" height="228" alt="Screen Shot 2025-10-14 at 2 05 45 PM" src="https://github.com/user-attachments/assets/20facf2c-9f51-4697-bc49-23554a838068" />
</p>  
<h3 align="center">  ↓ </h3>
<p>
  <img width="1433" height="701" alt="Screen Shot 2025-10-14 at 2 06 01 PM" src="https://github.com/user-attachments/assets/39546ae0-b349-471d-8c6e-323ee15ace1e" />
</p>  
<p>
 In this tutorial, I showed you how to view traffic between virtual machines and learn a little bit about network security protocols. You now have a better understanding of how network traffic flows and how to monitor it effectively. This knowledge is essential for identifying potential security vulnerabilities and ensuring that your systems are protected against unauthorized access or data breaches. ( ദ്ദി ˙ᗜ˙ )
</p>
<p>
  Please take a moment to clean up the Azure environment after we're finished so you don't have to pay for unnecessary charges in the future. ( ˶°ㅁ°) !!
</p>
