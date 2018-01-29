Aby utworzyć sieć wirtualną w modelu wdrożenia usługi Resource Manager w witrynie Azure Portal, wykonaj poniższe kroki. Zamieszczone zrzuty ekranu są przykładowe. Przedstawione wartości należy zastąpić własnymi. Aby uzyskać więcej informacji dotyczących pracy z sieciami wirtualnymi, zobacz temat [Omówienie sieci wirtualnych](../articles/virtual-network/virtual-networks-overview.md).

>[!NOTE]
>Jeśli chcesz, aby ta sieć wirtualna nawiązywała połączenie z lokalizacją lokalną (poza tworzeniem konfiguracji P2S), musisz zapewnić koordynację z administratorem sieci lokalnej w celu wyznaczenia zakresu adresów IP, którego będzie można używać w szczególności dla tej sieci wirtualnej. Jeśli po obu stronach połączenia sieci VPN istnieje powielony zakres adresów, ruch nie będzie przekierowywany w oczekiwany sposób. Ponadto jeśli chcesz połączyć tę sieć wirtualną z inną siecią wirtualną, przestrzeń adresowa nie może pokrywać się z inną siecią wirtualną. Dlatego należy odpowiednio zaplanować konfigurację sieci.
>
>

1. W przeglądarce przejdź do witryny [Azure Portal](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij pozycję **+**. W polu **Szukaj w witrynie Marketplace** wpisz „Sieć wirtualna”. Znajdź pozycję **Sieć wirtualna** na liście wyników i kliknij, aby otworzyć stronę **Sieć wirtualna**.

  ![Znajdowanie strony zasobów sieci wirtualnej](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Znajdowanie strony zasobów sieci wirtualnej")
3. Z listy **Wybierz model wdrożenia** w dolnej części strony Sieć wirtualna wybierz pozycję **Menedżer zasobów**, a następnie kliknij przycisk **Utwórz**.

  ![Wybieranie pozycji Menedżer zasobów](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Wybieranie pozycji Menedżer zasobów")
4. Na stronie **Tworzenie sieci wirtualnej** skonfiguruj ustawienia sieci wirtualnej. Po wypełnieniu pól czerwony wykrzyknik zmieni się na zielony znacznik wyboru, jeśli znaki wprowadzone w polu są prawidłowe. Niektóre wartości mogą być wypełnione automatycznie. W takim przypadku należy zastąpić je własnymi wartościami. Strona **Tworzenie sieci wirtualnej** wygląda podobnie do przedstawionej w poniższym przykładzie:

  ![Weryfikacja pola](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/vnetp2s.png "Weryfikacja pola")
5. **Nazwa**: Wprowadź nazwę sieci wirtualnej.
6. **Przestrzeń adresowa**: Wprowadź przestrzeń adresową. Jeśli masz wiele przestrzeni adresowych do dodania, dodaj pierwszą przestrzeń adresową. Możesz dodać dodatkowe przestrzenie adresowe później, po utworzeniu sieci wirtualnej.
7. **Subskrypcja**: Sprawdź, czy wyświetlana jest prawidłowa subskrypcja. Subskrypcje można zmieniać, korzystając z listy rozwijanej.
8. **Grupa zasobów**: Wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę nowej grupy zasobów. Jeśli tworzysz nową grupę, nadaj jej nazwę odpowiadającą wartościom planowanej konfiguracji. Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).
9. **Lokalizacja**: Wybierz lokalizację sieci wirtualnej. Lokalizacja określa miejsce, w którym zostaną umieszczone zasoby wdrażane w tej sieci wirtualnej.
10. **Podsieć**: Dodaj nazwę podsieci i zakres adresów podsieci. Możesz dodać dodatkowe podsieci później, po utworzeniu sieci wirtualnej.
11. Wybierz opcję **Przypnij do pulpitu nawigacyjnego**, jeśli chcesz, aby Twoją sieć wirtualną można było łatwo znaleźć na pulpicie nawigacyjnym, a następnie kliknij przycisk **Utwórz**.

 ![Przypnij do pulpitu nawigacyjnego](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "Przypnij do pulpitu nawigacyjnego")
12. Po kliknięciu przycisku **Utwórz** na pulpicie nawigacyjnym zostanie umieszczony kafelek, który będzie odzwierciedlać postęp Twojej sieci wirtualnej. Wygląd kafelka zmienia się w trakcie tworzenia sieci wirtualnej.

  ![Kafelek tworzenia sieci wirtualnej](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Kafelek tworzenia sieci wirtualnej")