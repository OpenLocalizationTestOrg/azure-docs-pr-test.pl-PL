## <a name="verify-the-output"></a>Sprawdzanie danych wyjściowych
Potok automatycznie tworzy folder wyjściowy w kontenerze obiektów blob adftutorial. Następnie kopiuje plik emp.txt z folderu wejściowego do folderu wyjściowego. 

1. W witrynie Azure Portal na stronie kontenera **adftutorial** kliknij przycisk **Odśwież**, aby wyświetlić folder wyjściowy. 
    
    ![Odświeżanie](media/data-factory-quickstart-verify-output-cleanup/output-refresh.png)
2. Kliknij folder **dane wyjściowe** na liście folderów. 
2. Upewnij się, że plik **emp.txt** jest kopiowany do folderu wyjściowego. 

    ![Odświeżanie](media/data-factory-quickstart-verify-output-cleanup/output-file.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Zasoby, które zostały utworzone w ramach tego przewodnika Szybki start, możesz wyczyścić na dwa sposoby. Możesz usunąć [grupę zasobów platformy Azure](../articles/azure-resource-manager/resource-group-overview.md) zawierającą wszystkie zasoby w tej grupie. Jeśli chcesz zachować inne zasoby bez zmian, usuń tylko fabrykę danych utworzoną w tym samouczku.

Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów łącznie z fabrykami danych w nich zawartymi. Uruchom poniższe polecenie, aby usunąć całą grupę zasobów: 
```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

Jeśli chcesz usunąć tylko fabrykę danych, a nie całą grupę zasobów, uruchom następujące polecenie: 

```powershell
Remove-AzureRmDataFactoryV2 -Name $dataFactoryName -ResourceGroupName $resourceGroupName
```