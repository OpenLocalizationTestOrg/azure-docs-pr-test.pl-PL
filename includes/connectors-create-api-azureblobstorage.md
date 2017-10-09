### <a name="prerequisites"></a>Wymagania wstępne
* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Konta magazynu obiektów Blob Azure](../articles/storage/common/storage-create-storage-account.md) łącznie z nazwą konta magazynu hello i klucza dostępu. Te informacje jest wyświetlany w właściwości hello hello konta magazynu w hello portalu Azure. Przeczytaj więcej na temat [usługi Azure Storage](../articles/storage/common/storage-introduction.md).

Przed rozpoczęciem korzystania z konta magazynu obiektów Blob Azure w aplikacji logiki, podłącz tooyour konta magazynu obiektów Blob Azure. Można to zrobić łatwo w aplikacjach logiki na powitania portalu Azure.  

Połącz tooyour konta magazynu obiektów Blob Azure przy użyciu hello następujące kroki:  

1. Tworzenie aplikacji logiki. W Projektancie aplikacji logiki hello dodać wyzwalacz, a następnie dodaj akcję. Wybierz **Pokaż Microsoft zarządzanych interfejsów API** w hello listy rozwijanej, a następnie wprowadź "blob" w polu wyszukiwania hello. Wybierz jedną z akcji hello:  
   
    ![Połączenia magazynu obiektów Blob platformy Azure — tworzenie krok](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. Jeśli nie utworzono jeszcze żadnych połączeń tooAzure magazyn, zostanie wyświetlony monit o szczegóły połączenia hello:   
   
    ![Połączenia magazynu obiektów Blob platformy Azure — tworzenie krok](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Wprowadź szczegóły konta magazynu hello. Właściwości oznaczone gwiazdką są wymagane.
   
   | Właściwość | Szczegóły |
   | --- | --- |
   | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
   | Nazwa konta magazynu Azure * |Wprowadź nazwę konta magazynu hello. Nazwa konta magazynu Hello jest wyświetlany w właściwości magazynu hello w hello portalu Azure. |
   | Klucz dostępu do konta magazynu Azure * |Wprowadź klucz konta magazynu hello. klawisze dostępu Hello są wyświetlane w właściwości magazynu hello w hello portalu Azure. |
   
    Te poświadczenia są używane tooauthorize Twojego tooconnect aplikacji logiki i uzyskać dostęp do danych. 
4. Wybierz pozycję **Utwórz**.
5. Utworzono połączenie hello powiadomienia. Teraz kontynuować hello innych czynności w aplikacji logiki: 
   
    ![Połączenia magazynu obiektów Blob platformy Azure — tworzenie krok](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

