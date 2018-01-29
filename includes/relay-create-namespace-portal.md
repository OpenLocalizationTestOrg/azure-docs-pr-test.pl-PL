1. Zaloguj się w witrynie [Azure Portal][Azure portal].
2. W menu po lewej stronie wybierz pozycję **+ Utwórz zasób**. Następnie wybierz pozycję **Integracja w przedsiębiorstwie** > **Relay**.
3. W obszarze **Tworzenie przestrzeni nazw** wprowadź nazwę przestrzeni nazw. System od razu sprawdza, czy nazwa jest dostępna.
4. W polu **Subskrypcja** wybierz subskrypcję platformy Azure, w której chcesz utworzyć przestrzeń nazw.
5. W polu [Grupa zasobów](../articles/azure-resource-manager/resource-group-portal.md) wybierz istniejącą grupę zasobów, w której znajdzie się przestrzeń nazw, lub utwórz nową.  
6. W polu **Lokalizacja** wybierz kraj lub region, w którym powinna być hostowana przestrzeń nazw.
   
    ![Create namespace][create-namespace]
7. Wybierz pozycję **Utwórz**. System utworzy przestrzeń nazw i włączy ją. Po kilku minutach system aprowizuje zasoby dla Twojego konta.

### <a name="get-management-credentials"></a>Uzyskiwanie poświadczeń zarządzania

1. Wybierz pozycję **Wszystkie zasoby**, a następnie wybierz nowo utworzoną nazwę przestrzeni nazw.
2. W obszarze przestrzeni nazw usługi Relay wybierz pozycję **Zasady dostępu współdzielonego**.  
3. W obszarze **Zasady dostępu współdzielonego** wybierz pozycję **RootManageSharedAccessKey**.
   
    ![connection-info][connection-info]
4. W obszarze **Zasady: RootManageSharedAccessKey** wybierz przycisk **Kopiuj** obok pozycji **Parametry połączenia — klucz podstawowy**. Spowoduje to skopiowanie parametrów połączenia do schowka do późniejszego użycia. Wklej tę wartość do Notatnika lub innej tymczasowej lokalizacji.
   
    ![connection-string][connection-string]

5. Powtórz poprzedni krok w celu skopiowania i wklejenia wartości pozycji **Klucz podstawowy** w lokalizacji tymczasowej do późniejszego użycia.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
