1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

1. Kliknij pozycję **Obliczanie** > **Aplikacja funkcji** i wybierz swoją **subskrypcję**. Następnie należy użyć ustawienia aplikacji hello funkcja określoną w tabeli hello.

    ![Tworzenie aplikacji funkcji w hello portalu Azure](./media/functions-create-function-app-portal/function-app-create-flow.png)

    | Ustawienie      | Sugerowana wartość  | Opis                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nazwa aplikacji** | Nazwa unikatowa w skali globalnej | Nazwa identyfikująca nową aplikację funkcji. | 
    | **[Grupa zasobów](../articles/azure-resource-manager/resource-group-overview.md)** |  myResourceGroup | Określ nazwę dla hello nową grupę zasobów, w których toocreate aplikacji funkcji. | 
    | **[Plan hostingu](../articles/azure-functions/functions-scale.md)** |   Plan Zużycie | Plan hostingu, który definiuje sposób przydzielania zasobów tooyour funkcji aplikacji. W domyślnej hello **zaplanować użycie**, zasoby są dodawane dynamicznie, co jest wymagane przez funkcji. Płacisz tylko za hello uruchomienia funkcji.   |
    | **Lokalizacja** | Europa Zachodnia | Wybierz lokalizację w swojej okolicy lub w pobliżu innych usług, do których Twoje funkcje będą uzyskiwać dostęp. |
    | **[Konto magazynu](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** |  Nazwa unikatowa w skali globalnej |  Nazwa hello nowe konto magazynu używane przez aplikację funkcji. Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery. Możesz także użyć istniejącego konta. |

1. Kliknij przycisk **Utwórz** tooprovision i wdrażanie hello nowej funkcji aplikacji.
