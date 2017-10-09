Użyj tooadd grupę zasobów tooa tag **zestawu grup azure**. Jeśli grupa zasobów hello nie ma żadnych znaczników, przekazać hello tagu.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Tagi są aktualizowane jako całość. Jeśli chcesz tooadd tag tooa grupę zasobów, w której ma znaczników, przekazuj wszystkie tagi hello. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Tagi nie są dziedziczone przez zasoby w grupie zasobów. Użyj tooadd zasób tooa tag **zestaw zasobów platformy azure**. Przekaż hello numer wersji interfejsu API dla typu zasobu hello dodawanego hello tagu. Wersja interfejsu API hello tooretrieve, należy użyć hello następujące polecenia z hello dostawcy zasobów dla typu hello ustawieniu:

```azurecli
azure provider show -n Microsoft.Storage --json
```

W wynikach hello Wyszukaj żądany typ zasobu hello.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Teraz, podaj tej wersji interfejsu API, nazwa grupy zasobów, nazwę zasobu typu zasobu i wartość tagu jako parametry.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Znaczniki istnieje bezpośrednio na zasobów i grup zasobów. Pobierz toosee hello znaczników, grupy zasobów i jej zasobach z **Pokaż grupy azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Polecenie to zwraca metadane dotyczące grupy zasobów hello, w tym wszelkie tooit znaczniki zastosowane.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

Możesz wyświetlić przy użyciu hello tagi dla określonego zasobu **Pokaż zasobów platformy azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

Użyj tooretrieve wszystkie zasoby hello z wartością tagu:

```azurecli
azure resource list -t Dept=Finance --json
```

Użyj wszystkich grup zasobów hello z wartością tagu tooretrieve:

```azurecli
azure group list -t Dept=Finance
```

Możesz przeglądać znaczników hello w ramach subskrypcji hello następujące polecenie:

```azurecli
azure tag list
```
