<span data-ttu-id="b4c1b-101">Skonfiguruj lokalne wdrożenie Git do aplikacji internetowej za pomocą polecenia [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git).</span><span class="sxs-lookup"><span data-stu-id="b4c1b-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="b4c1b-102">Usługa App Service obsługuje różne metody wdrażania zawartości w aplikacjach internetowych, np. protokół FTP, lokalne narzędzie Git oraz usługi GitHub, Visual Studio Team Services i Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="b4c1b-103">W ramach tego przewodnika Szybki start wdrożenie jest przeprowadzane przy użyciu lokalnego narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="b4c1b-104">Oznacza to, że używa się polecenia Git do wypchnięcia z lokalnego repozytorium do repozytorium na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="b4c1b-105">W poniższym poleceniu zastąp ciąg *\<nazwa_aplikacji>* nazwą swojej aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="b4c1b-106">Dane wyjściowe mają następujący format:</span><span class="sxs-lookup"><span data-stu-id="b4c1b-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="b4c1b-107">Zmienna `<username>` oznacza [użytkownika wdrożenia](#configure-a-deployment-user) utworzonego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="b4c1b-108">Skopiuj pokazany identyfikator URI; zostanie on użyty w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="b4c1b-108">Copy the URI shown; you'll use it in the next step.</span></span>
