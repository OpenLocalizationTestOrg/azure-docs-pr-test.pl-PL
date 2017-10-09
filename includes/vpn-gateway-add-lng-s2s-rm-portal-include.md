1. W portalu hello z **wszystkie zasoby**, kliknij przycisk **+ Dodaj**. 
2. W hello **wszystko** bloku pole wyszukiwania, wpisz **bramy sieci lokalnej**, następnie kliknij przycisk toosearch. Spowoduje to zwrócenie listy. Kliknij przycisk **bramy sieci lokalnej** tooopen hello bloku, a następnie kliknij przycisk **Utwórz** tooopen hello **Utwórz bramę sieci lokalnej** bloku.

  ![utwórz bramę sieci lokalnej](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. Na powitania **bloku bramy sieci lokalnej Utwórz**, określ hello wartości dla bramy sieci lokalnej.

  - **Nazwa:** określ nazwę obiektu bramy sieci lokalnej.
  - **Adres IP:** to hello publiczny adres IP urządzenia sieci VPN hello interesujące Azure tooconnect do. Określ prawidłowy publiczny adres IP. adres IP Hello nie może być za translatorem adresów Sieciowych, ma toobe osiągalny przez platformę Azure. Jeśli nie masz teraz hello adresu IP, można użyć wartości hello w hello zrzut ekranu, ale będzie konieczne ponownie toogo i zastąp adres IP — symbol zastępczy hello publiczny adres IP urządzenia sieci VPN. W przeciwnym razie Azure nie będą mogli tooconnect.
  - **Przestrzeń adresowa** odwołuje się toohello zakresów adresów dla sieci hello, która reprezentuje tej sieci lokalnej. Można dodać wiele zakresów przestrzeni adresów. Upewnij się, że hello określone w tym miejscu nie pokrywały z zakresami innych sieci, które mają tooconnect do. Azure będzie przekierowywać zakres adresów hello, że wprowadzono adres IP urządzenia sieci VPN lokalnymi toohello. *W tym miejscu użyć własne wartości, nie hello wartości widoczne w hello zrzut ekranu*.
  - **Subskrypcja:** Sprawdź, że hello poprawne subskrypcji jest wyświetlany.
  - **Grupa zasobów:** hello wybierz grupę zasobów, które mają toouse. Możesz utworzyć nową grupę zasobów lub wybrać już utworzoną.
  - **Lokalizacja:** wybierz hello tego obiektu zostanie utworzony w lokalizacji. Możesz tooselect hello sieci wirtualnej znajduje się w tej samej lokalizacji, ale nie jest wymagane toodo tak.

4. Po wybraniu wartości powitania kliknij **Utwórz** u dołu hello bramy sieci lokalnej hello hello bloku toocreate.
