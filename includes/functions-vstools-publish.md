1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **publikowania**. Wybierz pozycję **Utwórz nowe**, a następnie kliknij pozycję **Opublikuj**. 

    ![Publikowanie utworzonej aplikacji funkcji](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Jeśli jeszcze nie zostało to jeszcze programu Visual Studio tooyour konto platformy Azure, kliknij przycisk **Dodaj konto...** .  

3. W hello **Tworzenie usługi App Service** okno dialogowe, użyj hello **hostingu** ustawienia jako hello określony w poniższej tabeli: 

    ![Lokalne środowisko uruchomieniowe platformy Azure](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Ustawienie      | Sugerowana wartość  | Opis                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nazwa aplikacji** | Nazwa unikatowa w skali globalnej | Unikatowa nazwa identyfikująca nową aplikację funkcji. |
    | **Subskrypcja** | Wybierz subskrypcję | Witaj toouse subskrypcji platformy Azure. |
    | **[Grupa zasobów](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  Nazwa zasobu hello grupy w których toocreate funkcji aplikacji. |
    | **[Plan usługi App Service](../articles/azure-functions/functions-scale.md)** | Plan Zużycie | Upewnij się, że hello toochoose **zużycie** w obszarze **rozmiar** podczas tworzenia nowego planu.  |
    | **[Konto magazynu](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Nazwa unikatowa w skali globalnej | Użyj istniejącego konta magazynu lub utwórz nowe konto.   |

4. Kliknij przycisk **Utwórz** toocreate aplikacji funkcji na platformie Azure przy użyciu tych ustawień. Po zakończeniu inicjowania obsługi hello Zanotuj hello **adres URL witryny** wartość, która jest adresem hello aplikacji funkcji na platformie Azure. 

    ![Lokalne środowisko uruchomieniowe platformy Azure](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
