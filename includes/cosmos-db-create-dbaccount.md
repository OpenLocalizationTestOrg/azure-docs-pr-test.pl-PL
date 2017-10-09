1. W nowym oknie, zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W okienku po lewej stronie powitania kliknij **nowy**, kliknij przycisk **baz danych**, a następnie w obszarze **bazy danych Azure rozwiązania Cosmos**, kliknij przycisk **Utwórz**.
   
   ![Hello Azure portalu okienku baz danych](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-1.png)

3. Na powitania **nowe konto** bloku będzie określić konfigurację hello, który ma obowiązywać dla tego konta bazy danych Azure rozwiązania Cosmos. 

    Usługa Azure Cosmos DB umożliwia wybranie jednego z czterech modeli programowania: Gremlin (graf), MongoDB, SQL (DocumentDB) oraz Tabela (klucz-wartość). Każdy z tych modeli wymaga obecnie osobnego konta.
    
    W tym artykule szybki start, firma Microsoft program względem hello interfejsu API usługi DocumentDB, więc należy wybrać **SQL (DocumentDB)** w trakcie wypełniania hello formularza. Jeśli masz dane grafu dla aplikacji mediów społecznościowych, dane typu klucz/wartość (tabela) lub dane zmigrowane z aplikacji MongoDB, weź pod uwagę, że usługa Azure Cosmos DB może zapewnić globalnie rozproszoną platformę usługi bazy danych o wysokiej dostępności dla wszystkich Twoich aplikacji o znaczeniu krytycznym.

    Wypełnij pola hello na powitania **nowe konto** bloku, korzystając z informacji hello w hello następującego zrzutu ekranu jako przewodnik - wartości może różnić się od wartości hello hello zrzucie ekranu.
 
    ![Witaj nowego bloku konta usługi dla bazy danych Azure rozwiązania Cosmos](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-2.png)

    Ustawienie|Sugerowana wartość|Opis
    ---|---|---
    ID|*Unikatowa wartość*|Unikatowa nazwa do identyfikacji tego konta usługi Azure Cosmos DB. Ponieważ *documents.azure.com* jest dołączany toohello identyfikator Podaj toocreate identyfikator URI, użyj a unikatowy, ale do zidentyfikowania identyfikatora. Identyfikator Hello może zawierać tylko małe litery, cyfry i znaki łącznika (-) hello, i może zawierać 3 znaków too50.
    Interfejs API|SQL (DocumentDB)|Firma Microsoft program względem hello [interfejsu API usługi DocumentDB](../articles/documentdb/documentdb-introduction.md) dalszej części tego artykułu.|
    Subskrypcja|*Twoja subskrypcja*|Witaj subskrypcji platformy Azure mają toouse dla tego konta bazy danych Azure rozwiązania Cosmos. 
    Grupa zasobów|*Witaj samą wartość jak identyfikator*|Witaj Nowa nazwa grupy zasobów dla Twojego konta. Dla uproszczenia hello takie same nazwy można użyć jako identyfikatora 
    Lokalizacja|*Witaj region najbliższy tooyour użytkowników*|Witaj lokalizację geograficzną, w których toohost konta bazy danych Azure rozwiązania Cosmos. Wybierz lokalizację hello najbliższego toogive użytkowników tooyour ich hello najszybszy dostęp do danych toohello.
4. Kliknij przycisk **Utwórz** toocreate hello konta.
5. Na górnym pasku narzędzi powitania kliknij hello **powiadomienia** ikona ![ikonę powiadomienia hello](./media/cosmos-db-create-dbaccount/notification-icon.png) procesu wdrażania hello toomonitor.

    ![Hello Azure portalu okienko powiadomień](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-nosql-notification.png)

6.  Gdy okno powiadomienia hello wskazuje okna powiadomień zakończyło się pomyślnie, zamknij hello wdrożenia hello i hello Otwórz nowe konto z hello **wszystkie zasoby** Kafelek na powitania pulpitu nawigacyjnego. 

    ![Witaj konta usługi DocumentDB na kafelku wszystkie zasoby powitalne](./media/cosmos-db-create-dbaccount/all-resources.png)
 
