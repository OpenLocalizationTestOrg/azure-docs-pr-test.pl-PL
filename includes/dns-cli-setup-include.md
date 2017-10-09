## <a name="set-up-azure-cli-for-azure-dns"></a>Konfigurowanie interfejsu wiersza polecenia platformy Azure dla usługi Azure DNS

### <a name="before-you-begin"></a>Przed rozpoczęciem

Sprawdź, czy masz hello poniższych elementach przed rozpoczęciem konfiguracji.

* Subskrypcja platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).
* Zainstaluj najnowszą wersję hello hello Azure CLI, dostępne dla systemu Windows, Linux lub MAC. Więcej informacji znajduje się w temacie [hello instalowanie interfejsu wiersza polecenia Azure](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Zaloguj się tooyour konto platformy Azure

Otwórz okno konsoli i uwierzytelnij się przy użyciu swoich poświadczeń. Aby uzyskać więcej informacji, zobacz [Zaloguj tooAzure z hello wiersza polecenia platformy Azure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Przełącz tryb interfejsu wiersza polecenia

Usługa Azure DNS korzysta z usługi Azure Resource Manager. Upewnij się, że przełącznik polecenia usługi Azure Resource Manager toouse tryb interfejsu wiersza polecenia.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Wybierz subskrypcję hello

Sprawdź subskrypcje hello hello konta.

```azurecli
azure account list
```

Wybierz z toouse Twojej subskrypcji platformy Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów określały lokalizację. Służy to jako hello domyślna lokalizacja dla zasobów w danej grupie zasobów. Jednak ponieważ wszystkie zasoby DNS są globalne, a nie regionalne, wybór hello lokalizacja grupy zasobów nie ma wpływu na usługi Azure DNS.

Ten krok można pominąć, jeśli używasz istniejącej grupy zasobów.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Rejestrowanie dostawcy zasobów

Usługa Azure DNS Hello jest zarządzana przez dostawcę zasobów Microsoft.Network hello. Twoja subskrypcja platformy Azure musi być zarejestrowany toouse tego dostawcy zasobów przed użyciem usługi Azure DNS. Jest to jednorazowa operacja dla każdej subskrypcji.

```azurecli
azure provider register --namespace Microsoft.Network
```

