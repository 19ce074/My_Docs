## Create a senario to show case the practical of Azure Load Balancer

<br />
<br />

### 1)Create a Vnet with the following configuration

| Step     | Screenshot      | 
| ------------- | ------------- |
| 1)   | ![image](https://github.com/19ce074/My_Docs/assets/125547030/43207f44-f4e1-46bd-9368-a7784cb7bb6e)  |  
| 2)   | ![image](https://github.com/19ce074/My_Docs/assets/125547030/dad729d0-b95d-4c85-98e9-f0fc2485c178)  |  
| 3)   | ![image](https://github.com/19ce074/My_Docs/assets/125547030/37975405-c033-42b3-9b8e-2bf3569f95b1)  |

<br />

### 2) Create 2 virtual machines and install apache2 in vm1 and nginx in vm2

| Step     | Screenshot      | 
| ------------- | ------------- |
| 1) | ![image](https://github.com/19ce074/My_Docs/assets/125547030/d9fad230-a370-4665-97ba-e6fe0836177a) ![image](https://github.com/19ce074/My_Docs/assets/125547030/a93527f9-d432-4317-b933-f2190c5b71f3)|
| 2) | ![image](https://github.com/19ce074/My_Docs/assets/125547030/3c59b250-889a-4cac-937c-6539f75d4980) |
| 3) | In advace tab add the script to install webserver into vm <br /> ![image](https://github.com/19ce074/My_Docs/assets/125547030/50d3ac8d-4486-476d-8d2d-dc65324d92ad) |
| 4) | ![image](https://github.com/19ce074/My_Docs/assets/125547030/661c4302-ad25-4e31-9c54-fc3d87ca24f4) |

<br />

Create another vm in the same subnet and install nginx in that.
<br />
![image](https://github.com/19ce074/My_Docs/assets/125547030/f518c1dd-4f47-411b-ae2c-220afc3055e6)

<br />

### 3) Create azure load balancer

| Step     | Screenshot      | 
| ------------- | ------------- |
