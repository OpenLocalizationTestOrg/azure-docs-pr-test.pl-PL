1. Zaloguj się na toohello [portalu Azure][Azure portal].
2. W okienku nawigacji po lewej stronie powitania hello portalu kliknij **nowy**, następnie kliknij przycisk **integracji przedsiębiorstwa**, a następnie kliknij przycisk **przekazywania**.
3. W hello **tworzenie przestrzeni nazw** okna dialogowego, wprowadź nazwę przestrzeni nazw. system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.
4. W hello **subskrypcji** pola, wybierz subskrypcję platformy Azure, w których toocreate hello nazw.
5. W hello  **[grupy zasobów](../articles/azure-resource-manager/resource-group-portal.md)**  wybierz istniejącą grupę zasobów, w których hello przestrzeni nazw zostanie na żywo lub Utwórz nową.      
6. W **lokalizacji**, wybierz hello kraj lub region, w którym ma być hostowana przestrzeni nazw.
   
    ![Create namespace][create-namespace]
7. Kliknij przycisk **Utwórz**. teraz Hello system utworzy przestrzeń nazw i włączy ją. Po kilku minutach hello systemu inicjowania obsługi administracyjnej zasobów dla Twojego konta.

### <a name="obtain-hello-management-credentials"></a>Uzyskiwanie poświadczeń zarządzania hello
1. Kliknij hello nowo utworzona nazwa przestrzeni nazw na liście hello przestrzeni nazw.
2. W bloku przestrzeni nazw powitania kliknij **zasady dostępu współużytkowanego**.
3. W hello **zasady dostępu współużytkowanego** bloku, kliknij przycisk **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. W hello **zasad: RootManageSharedAccessKey** bloku, kliknij przycisk Kopiuj hello obok zbyt**połączenia ciąg — podstawowy klucz**, toocopy hello połączenia ciąg tooyour Schowka do późniejszego użycia. Wklej tę wartość do Notatnika lub innej tymczasowej lokalizacji.
   
    ![connection-string][connection-string]

5. Hello powtórzeń poprzedniego kroku, kopiowanie i wklejanie wartość hello **klucza podstawowego** tooa lokalizacji tymczasowej na potrzeby późniejszego użycia.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
