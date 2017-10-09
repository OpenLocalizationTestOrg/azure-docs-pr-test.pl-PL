Konfigurowanie lokalnych aplikacji sieci web toohello wdrożenia Git z hello [źródło wdrożenia az aplikacji sieci Web — config lokalnych git](/cli/azure/webapp/deployment/source#config-local-git) polecenia.

Usługa aplikacji obsługuje kilka sposobów toodeploy tooa zawartości aplikacji sieci web, takich jak FTP, Git lokalnego GitHub, Visual Studio Team Services i Bitbucket. W ramach tego przewodnika Szybki start wdrożenie jest przeprowadzane przy użyciu lokalnego narzędzia Git. Oznacza to, że wdrażanie przy użyciu toopush polecenia Git z repozytorium tooa lokalnego repozytorium na platformie Azure. 

Zastąp następujące polecenie, w hello  *\<nazwa_aplikacji >* o nazwie aplikacji sieci web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

dane wyjściowe Hello ma hello następującego formatu:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Witaj `<username>` jest hello [użytkownika wdrażania](#configure-a-deployment-user) utworzony w poprzednim kroku.

Skopiuj hello URI pokazano; użyjesz jej w następnym kroku hello.
