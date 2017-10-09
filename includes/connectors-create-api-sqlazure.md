### <a name="prerequisites"></a>Wymagania wstępne
* Konto platformy Azure; można utworzyć [bezpłatne konto](https://azure.microsoft.com/free)
* [Bazy danych SQL Azure](../articles/sql-database/sql-database-get-started.md) informacje o połączeniu, łącznie z hello nazwy serwera, nazwy bazy danych oraz nazwy użytkownika i hasła. Te informacje zostaną zawarte w hello parametry połączenia bazy danych SQL:
  
    Serwer = tcp:*yoursqlservername*. database.windows.net,1433;Initial katalogu =*yourqldbname*; Utrzymuj informacje o zabezpieczeniach = False; Nazwa użytkownika = {your_username}; Hasło = {your_password}; MultipleActiveResultSets = False; Szyfrowanie = True; TrustServerCertificate = False; Limit czasu połączenia = 30;
  
    Przeczytaj więcej na temat [baz danych SQL Azure](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Podczas tworzenia bazy danych SQL Azure, można też utworzyć hello przykładowe bazy danych dołączone SQL. 
> 
> 

Przed rozpoczęciem korzystania z bazy danych SQL Azure w aplikacji logiki, podłącz tooyour bazy danych SQL. Można to zrobić łatwo w aplikacjach logiki na powitania portalu Azure.  

Połącz tooyour, którą baza danych SQL Azure przy użyciu hello następujące kroki:  

1. Tworzenie aplikacji logiki. W Projektancie aplikacji logiki hello dodać wyzwalacz, a następnie dodaj akcję. Wybierz **Pokaż Microsoft zarządzanych interfejsów API** w hello listy rozwijanej, a następnie wprowadź "sql" hello pola wyszukiwania. Wybierz jedną z akcji hello:  
   
    ![Krok tworzenia połączenia SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Jeśli nie utworzono jeszcze żadnych tooSQL połączenia bazy danych, zostanie wyświetlony monit o szczegóły połączenia hello:  
   
    ![Krok tworzenia połączenia SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Wprowadź szczegóły bazy danych SQL hello. Właściwości oznaczone gwiazdką są wymagane.
   
   | Właściwość | Szczegóły |
   | --- | --- |
   | Łączenie za pośrednictwem bramy |Pozostaw zaznaczenie opcji. Ta jest używana podczas łączenia tooan lokalnego programu SQL Server. |
   | Nazwa połączenia * |Wprowadź dowolną nazwę połączenia. |
   | Nazwa serwera SQL * |Wprowadź nazwę serwera hello; czyli przypominać *servername.database.windows.net*. Hello nazwa serwera jest wyświetlane na hello właściwości bazy danych SQL w hello portalu Azure, a także w parametrach połączenia hello. |
   | Nazwa bazy danych SQL * |Wprowadź nazwę hello należy nadać bazy danych SQL. Jest to wymienione w hello właściwości bazy danych SQL w parametrach połączenia hello: Initial Catalog =*yoursqldbname*. |
   | Nazwa użytkownika * |Wprowadź nazwę użytkownika hello, utworzonej podczas tworzenia hello bazy danych SQL. Jest to wymienione w hello właściwości bazy danych SQL w hello portalu Azure. |
   | Hasło * |Wprowadź hasło hello, utworzonej podczas tworzenia hello bazy danych SQL. |
   
    Te poświadczenia są używane tooauthorize Twojego tooconnect aplikacji logiki i uzyskać dostęp do danych SQL. Po wykonaniu tych czynności szczegóły połączenia wyglądać podobnie toohello następujące:  
   
    ![Krok tworzenia połączenia SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Wybierz pozycję **Utwórz**. 
5. Utworzono połączenie hello powiadomienia. Teraz kontynuować hello innych czynności w aplikacji logiki: 
   
    ![Krok tworzenia połączenia SQL Azure](./media/connectors-create-api-sqlazure/table.png)

