<span data-ttu-id="0898f-101">Konfigurowanie lokalnych aplikacji sieci web toohello wdrożenia Git z hello [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0898f-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="0898f-102">Usługa aplikacji obsługuje kilka sposobów toodeploy tooa zawartości aplikacji sieci web, takich jak FTP, Git lokalnego GitHub, Visual Studio Team Services i Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="0898f-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="0898f-103">W ramach tego przewodnika Szybki start wdrożenie jest przeprowadzane przy użyciu lokalnego narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="0898f-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="0898f-104">Oznacza to, że wdrażanie przy użyciu toopush polecenia Git z repozytorium tooa lokalnego repozytorium na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0898f-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="0898f-105">Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o nazwie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="0898f-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="0898f-106">dane wyjściowe Hello ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="0898f-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="0898f-107">Witaj `<username>` jest hello [użytkownika wdrażania](#configure-a-deployment-user) utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="0898f-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="0898f-108">Skopiuj hello URI pokazano; użyjesz jej w następnym kroku hello.</span><span class="sxs-lookup"><span data-stu-id="0898f-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
