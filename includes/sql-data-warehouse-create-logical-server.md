### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Utwórz nowy serwer logiczny SQL w hello portalu Azure

1. Kliknij pozycję **Nowy**, wyszukaj **serwer logiczny**, a następnie naciśnij klawisz **ENTER**.

    ![wyszukiwanie serwera logicznego](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Wybierz pozycję **SQL Server (serwer logiczny)**. 

    ![wybieranie serwera logicznego](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Kliknij przycisk **Utwórz** tooopen hello nowy blok programu SQL Server (serwer logiczny).

   <kbd>![Otwórz blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![blok serwera logicznego](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. W polu tekstowym Nazwa serwera bloku hello programu SQL Server (serwer logiczny) Podaj prawidłową nazwę dla nowego serwera logicznego hello. Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.
    
    ![nazwa nowego serwera](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Witaj pełni kwalifikowaną nazwę dla nowego serwera będą < your_server_name >. database.windows.net.
    >
    
4. W polu tekstowym powitania serwera admin logowania Podaj nazwę użytkownika logowania uwierzytelniania SQL powitania dla tego serwera. Tę nazwę logowania jest określany jako powitania serwera głównego identyfikatora logowania. Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.
    
    ![identyfikator logowania administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. W hello **hasło** i **Potwierdź hasło** pola tekstowe, podaj hasło dla konta głównego identyfikatora logowania serwera hello. Zielony znacznik wyboru wskazuje, czy podane hasło jest poprawne.
    
    ![Hasło administratora SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Wybierz subskrypcję, w której masz uprawnienia toocreate obiektów.

    ![subskrypcja](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. W polu tekstowym grupy zasobów hello wybierz **Utwórz nowy** , a następnie w polu tekstowym grupy zasobów hello, podaj prawidłową nazwę dla nowej grupy zasobów hello, (umożliwia także istniejącą grupę zasobów, jeśli został już utworzony dla siebie). Zielony znacznik wyboru wskazuje, czy podana nazwa jest poprawna.

    ![nowa grupa zasobów](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. W hello **lokalizacji** pole tekstowe, wybierz danych Centrum lokalizacji odpowiednie tooyour — takie jak "Australia Wschodnia".
    
    ![lokalizacja serwera](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Witaj wyboru **Zezwalaj usługom platformy azure tooaccess serwera** nie można zmienić tego bloku. Można zmienić to ustawienie na powitania serwera zapory bloku. Aby uzyskać więcej informacji, zobacz artykuł [Wprowadzenie do zabezpieczeń](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. Kliknij przycisk **Utwórz**.

    ![przycisk Utwórz](./media/sql-data-warehouse-create-logical-server/create.png)

