Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.

[!INCLUDE [resource group intro text](resource-group.md)]

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Ogólnie rzecz biorąc tworzenia zasobu grupy i hello zasobów w regionie, w pobliżu. toosee obsługiwane lokalizacje dla aplikacji sieci Web platformy Azure, uruchom hello `az appservice list-locations` polecenia. 
