## Upload docker container in azure web app

### 1) Create a azure container registory
### 2) Create a web app in azure and select container 
### 3) login using that conatiner registory name
### 4) Build and push docker images in 
To push a Docker multi-container application to Azure Container Registry, you can follow these steps:

1. **Build your Docker images**: Make sure you have built the Docker images for all the containers in your multi-container application. You can use the `docker build` command to build each image. Make sure to tag the images appropriately.

2. **Tag the images**: Azure Container Registry requires images to have a specific naming format. The format is `<registry-name>.azurecr.io/<image-name>:<tag>`. Replace `<registry-name>` with the name of your Azure Container Registry, `<image-name>` with the name you want to give to your Docker image, and `<tag>` with the version or tag for the image.

   For example, if your registry name is `myregistry` and your image name is `myapp`, you would tag the image as `myregistry.azurecr.io/myapp:1.0`.

3. **Login to Azure Container Registry**: Use the Azure CLI or Azure PowerShell to log in to your Azure account and authenticate with Azure Container Registry. Run the following command in your terminal or command prompt:
   
   ```bash
   az acr login --name <registry-name>
   ```

   Replace `<registry-name>` with the name of your Azure Container Registry.

4. **Push the Docker images**: After logging in, you can push the Docker images to Azure Container Registry using the `docker push` command. Run the following command for each image:

   ```bash
   docker push <registry-name>.azurecr.io/<image-name>:<tag>
   ```

   Replace `<registry-name>`, `<image-name>`, and `<tag>` with the appropriate values for your images.

5. **Verify the images in Azure Container Registry**: To confirm that the images have been successfully pushed to Azure Container Registry, you can check the registry using the Azure portal or the Azure CLI. Run the following command:

   ```bash
   az acr repository list --name <registry-name> --output table
   ```

   Replace `<registry-name>` with the name of your Azure Container Registry.

Once you have completed these steps, your Docker multi-container application will be pushed to Azure Container Registry and available for use in your Azure environment.
