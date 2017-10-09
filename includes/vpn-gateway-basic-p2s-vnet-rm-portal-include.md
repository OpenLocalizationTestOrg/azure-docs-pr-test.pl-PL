toocreate sieci wirtualnej w modelu wdrażania usługi Resource Manager hello przy użyciu hello portalu Azure, wykonaj poniższe kroki hello. zrzuty ekranu Hello podano jako przykłady. Należy się, że wartości hello tooreplace własnymi. Aby uzyskać więcej informacji na temat pracy z sieciami wirtualnymi, zobacz hello [omówienie sieci wirtualnych](../articles/virtual-network/virtual-networks-overview.md).

1. W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij pozycję **+**. W hello **marketplace hello wyszukiwania** wpisz "Sieci wirtualnej". Zlokalizuj **sieci wirtualnej** hello zwrócił listy i kliknij przycisk tooopen hello **sieci wirtualnej** strony.

  ![Znajdowanie strony zasobów sieci wirtualnej](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Znajdowanie strony zasobów sieci wirtualnej")
3. Dolnej hello hello strony sieci wirtualnej, z hello **wybierz model wdrożenia** wybierz **Menedżera zasobów**, a następnie kliknij przycisk **Utwórz**.

  ![Wybieranie pozycji Menedżer zasobów](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Wybieranie pozycji Menedżer zasobów")
4. Na powitania **Utwórz sieć wirtualną** skonfiguruj hello ustawienia sieci wirtualnej. Po wypełnieniu pól hello hello czerwony wykrzyknik staje się zielony znacznik wyboru gdy znaki hello wprowadzona w polu hello są prawidłowe. Niektóre wartości mogą być wypełnione automatycznie. Jeśli tak, Zastąp wartości hello własne. Witaj **Utwórz sieć wirtualną** strona wygląda podobnie toohello poniższy przykład:

  ![Weryfikacja pola](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "Weryfikacja pola")
5. **Nazwa**: Wprowadź nazwę hello sieci wirtualnej.
6. **Przestrzeń adresowa**: Wprowadź hello przestrzeni adresowej. Jeśli masz wiele tooadd spacje adres, należy dodać pierwszą przestrzeń adresową. Dodatkowe przestrzenie adresowe można dodać później, po utworzeniu hello sieci wirtualnej.
7. **Nazwa podsieci**: Dodaj hello nazwy i podsieci zakres adresów podsieci. Później dodać dodatkowe podsieci po utworzeniu hello sieci wirtualnej.
8. **Subskrypcja**: Sprawdź, że hello wymienionych subskrypcji jest hello właściwy. Subskrypcje można zmienić za pomocą listy rozwijanej hello.
9. **Grupa zasobów**: Wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę nowej grupy zasobów. W przypadku tworzenia nowej grupy, grupa zasobów hello nazwy zgodnie z tooyour planowane wartości konfiguracji. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
10. **Lokalizacja**: Wybierz lokalizację hello sieci wirtualnej. Lokalizacja Hello Określa, gdzie znajdują się zasoby hello wdrożenie toothis sieci wirtualnej.
11. Wybierz **toodashboard numeru Pin** jeśli mają toobe toofind może łatwo na pulpicie nawigacyjnym hello sieci wirtualnej, a następnie kliknij przycisk **Utwórz**.

 ![Numer PIN toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "toodashboard numeru pin")
12. Po kliknięciu przycisku **Utwórz**, zobaczysz kafelka na pulpicie nawigacyjnym, który będzie odzwierciedlać postęp hello Twojej sieci wirtualnej. Trwa tworzenie Hello kafelka zmienia hello sieci wirtualnej.

  ![Kafelek tworzenia sieci wirtualnej](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Kafelek tworzenia sieci wirtualnej")