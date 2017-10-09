toocreate sieci wirtualnej w modelu wdrażania usługi Resource Manager hello przy użyciu hello portalu Azure, wykonaj poniższe kroki hello. Użyj hello [przykładowe wartości](#values) korzystania z tych kroków jako samouczka. Jeśli nie przeprowadzasz te kroki jako samouczek, należy się, że wartości hello tooreplace własnymi. Aby uzyskać więcej informacji na temat pracy z sieciami wirtualnymi, zobacz hello [omówienie sieci wirtualnych](../articles/virtual-network/virtual-networks-overview.md).

1. W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **Nowy**. W hello **marketplace hello wyszukiwania** wpisz "Sieci wirtualnej". Zlokalizuj **sieci wirtualnej** hello zwrócił listy i kliknij przycisk tooopen hello **sieci wirtualnej** bloku.
3. Dolnej hello hello bloku sieci wirtualnej, z hello **wybierz model wdrożenia** wybierz **Menedżera zasobów**, a następnie kliknij przycisk **Utwórz**. Spowoduje to otwarcie bloku Utwórz sieć wirtualną hello.

    ![Tworzenie bloku sieci wirtualnej](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Tworzenie bloku sieci wirtualnej")
4. Na powitania **Utwórz sieć wirtualną** bloku, skonfigurować ustawienia sieci wirtualnej hello. Po wypełnieniu pól hello hello czerwony wykrzyknik staje się zielony znacznik wyboru gdy znaki hello wprowadzona w polu hello są prawidłowe.

  - **Nazwa**: Wprowadź nazwę hello sieci wirtualnej. W tym przykładzie jest używana sieć TestVNet1.
  - **Przestrzeń adresowa**: Wprowadź hello przestrzeni adresowej. Jeśli masz wiele tooadd spacje adres, należy dodać pierwszą przestrzeń adresową. Dodatkowe przestrzenie adresowe można dodać później, po utworzeniu hello sieci wirtualnej. Upewnij się, tej przestrzeni adresowej hello określisz nie zachodzi na powitania przestrzeni adresowej dla lokalizacji lokalnej.
  - **Nazwa podsieci**: Dodaj hello pierwszej nazwy i podsieci zakres adresów podsieci. Możesz dodać dodatkowe podsieci i podsieć bramy hello później, po utworzeniu tej sieci wirtualnej. 
  - **Subskrypcja**: Sprawdź, czy wymienionej subskrypcji hello jest hello właściwy. Subskrypcje można zmienić za pomocą listy rozwijanej hello.
  - **Grupa zasobów**: Wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę nowej grupy zasobów. W przypadku tworzenia nowej grupy, grupa zasobów hello nazwy zgodnie z tooyour planowane wartości konfiguracji. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
  - **Lokalizacja**: Wybierz lokalizację hello sieci wirtualnej. Lokalizacja Hello Określa, gdzie znajdują się zasoby hello wdrożenie toothis sieci wirtualnej.

5. Wybierz **toodashboard numeru Pin** jeśli mają toobe toofind może łatwo na pulpicie nawigacyjnym hello sieci wirtualnej, a następnie kliknij przycisk **Utwórz**. Po kliknięciu przycisku **Utwórz**, zobaczysz kafelka na pulpicie nawigacyjnym, który będzie odzwierciedlać postęp hello Twojej sieci wirtualnej. Trwa tworzenie Hello kafelka zmienia hello sieci wirtualnej.
