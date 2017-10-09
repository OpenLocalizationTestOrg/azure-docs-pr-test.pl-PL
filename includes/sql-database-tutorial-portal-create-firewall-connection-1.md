## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Utwórz pustą bazę danych SQL przy użyciu hello portalu Azure

Baza danych Azure SQL jest tworzona ze zdefiniowanym zestawem [zasobów obliczeniowych i przechowywania](../articles/sql-database/sql-database-service-tiers.md). Witaj baza danych została utworzona w ramach [grupy zasobów platformy Azure](../articles/azure-resource-manager/resource-group-overview.md) i [serwera logicznego bazy danych SQL Azure](../articles/sql-database/sql-database-features.md). 

Wykonaj te kroki toocreate pustej bazy danych SQL. 

1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.

2. Wybierz **baz danych** z hello **nowy** i wybrać opcję **bazy danych SQL** z hello **baz danych** strony. 

   ![Tworzenie bazy danych puste](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Wypełnianie hello bazy danych SQL formularza z hello następujących informacji, jak pokazano na powitania poprzedzających obrazu:   

   | Ustawienie | Sugerowana wartość | Opis |
   | --------| --------------- | ----------- | 
   | **Nazwa bazy danych** | mySampleDatabase | Prawidłowe nazwy baz danych opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych). | 
   | **Subskrypcja** | Twoja subskrypcja  | Aby uzyskać szczegółowe informacje o subskrypcjach, zobacz [Subskrypcje](https://account.windowsazure.com/Subscriptions). |
   | **Grupa zasobów** | myResourceGroup | Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). |
   | **Wybierz źródło** | Pusta baza danych | Określa, czy można utworzyć pustej bazy danych. |
   ||||

4. Kliknij przycisk **serwera** toocreate i skonfiguruj nowy serwer dla nowej bazy danych. Wypełnianie hello **nowy formularz serwera** z hello następujących informacji: 

   | Ustawienie | Sugerowana wartość | Opis |
   | --------| --------------- | ----------- | 
   | **Nazwa serwera** | Wszelkie globalnie unikatowej nazwy. | Prawidłowe nazwy serwera opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa). | 
   | **Identyfikator logowania administratora serwera** | Wszelkie prawidłową nazwę. | Prawidłowe nazwy identyfikatorów logowania opisano w artykule [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych).|
   | **Hasło** | Wszystkie prawidłowe hasło. | Hasło musi mieć co najmniej ośmiu znaków i musi zawierać znaki z trzech z następujących kategorii hello: wielkich liter, małych liter, cyfr i znaków innych niż alfanumeryczne. |
   | **Lokalizacja** | Żadnej prawidłowej lokalizacji. | Aby uzyskać informacje na temat regionów, zobacz temat [Regiony systemu Azure](https://azure.microsoft.com/regions/). |
   ||||

   ![tworzenie serwera bazy danych](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Kliknij pozycję **Wybierz**.

6. Kliknij przycisk **warstwa cenowa** toospecify hello warstwę i poziom wydajności usługi dla nowej bazy danych. W tym samouczku, wybierz **20 jednostek Dtu** i **250** GB miejsca do magazynowania.

   ![tworzenie bazy danych s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Kliknij przycisk **Zastosuj**.  

8. Wybierz **sortowania** dla hello pustej bazy danych (w tym samouczku, wartość domyślna używana hello). Aby uzyskać więcej informacji na temat sortowań zobacz [sortowania](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Kliknij przycisk **Utwórz** tooprovision hello w bazie danych. Inicjowanie obsługi administracyjnej ma o toocomplete minutę i pół. 

10. Na pasku narzędzi hello, kliknij przycisk **powiadomienia** procesu wdrażania hello toomonitor.

   ![powiadomienie](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Utworzyć regułę zapory poziomu serwera przy użyciu hello portalu Azure

Witaj usługi baza danych SQL tworzy zapory na poziomie serwera hello. Początkowo hello Zapora uniemożliwia zewnętrznych narzędzi i aplikacji łączących toohello serwera lub bazy danych tooany na powitania serwera. Połączenia są dozwolone po utworzeniu reguły zapory tooopen określonych adresów IP. Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](../articles/sql-database/sql-database-firewall-configure.md) adresów IP klienta i tooenable łączność zewnętrzną przez zaporę bazy danych SQL hello tylko adresu IP. 


> [!NOTE]
> Baza danych SQL Azure komunikuje się za pośrednictwem portu 1433. Możesz połączyć tooSQL bazy danych tylko wtedy, gdy Zapora hello sieci zezwala na ruch wychodzący przez port 1433.


1. Po zakończeniu wdrażania hello, kliknij przycisk **baz danych SQL** z menu po lewej stronie powitania, a następnie kliknij przycisk **mySampleDatabase** na powitania **baz danych SQL** strony. Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji. Skopiuj tę w pełni kwalifikowaną nazwę serwera do użycia w przyszłości.

   > [!IMPORTANT]
   > Należy to pełna nazwa tooconnect tooyour serwera i jego baz danych w kolejnych Szybki Start.
   > 

   ![nazwa serwera](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello. Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server. 

   ![reguła zapory serwera](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Kliknij przycisk **Dodaj adres IP klienta** na powitania narzędzi tooadd IP bieżący adres tooa nowej reguły zapory. Reguła zapory może otworzyć port 1433 dla pojedynczego adresu IP lub zakresu adresów IP.

4. Kliknij pozycję **Zapisz**. Dla bieżącego adresu IP otwierania portu 1433 na serwerze logicznym hello tworzona jest reguła zapory poziomu serwera.

   ![ustawianie reguły zapory serwera](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Kliknij przycisk **OK** , a następnie zamknij hello **ustawienia zapory** strony.

Teraz można podłączyć toohello serwera bazy danych SQL Azure i jej baz danych za pomocą narzędzi takich jak SQL Server Management Studio (SSMS). połączenie Hello jest z tego adresu IP i używa konta administratora serwera na powitania utworzone wcześniej.


> [!IMPORTANT]
> Domyślnie dostęp za pośrednictwem zapory bazy danych SQL hello jest włączona dla wszystkich usług platformy Azure. Kliknij przycisk **OFF** na toodisable tej strony dla wszystkich usług platformy Azure.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Pobierz wartości parametrów połączeń przy użyciu hello portalu Azure

Pobierz hello pełni kwalifikowaną nazwę serwera dla serwera bazy danych SQL Azure w hello portalu Azure. Możesz użyć hello pełną nazwę tooconnect tooyour serwera przy użyciu programu SQL Server Management Studio.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

2. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 

3. W hello **Essentials** okienka w hello strony portalu systemu Azure dla bazy danych, Znajdź, a następnie skopiuj hello **nazwy serwera**.

   ![informacje o połączeniu](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
