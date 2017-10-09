> [!NOTE]
> * Brama sieci VPN Hello publicznego adresu IP ulegnie zmianie po migracji ze starego tooa SKU nowe jednostki SKU.
> * Nie można migrować klasyczny toohello bram sieci VPN nowe jednostki SKU. Klasyczne sieci VPN bramy może stosować tylko hello starszej wersji jednostki SKU (stare).
> 

Nie można zmienić rozmiaru sieci VPN Azure bramy między hello starego jednostki SKU i hello nowe rodziny SKU. Jeśli masz w modelu wdrażania usługi Resource Manager hello bramy sieci VPN, korzystających z hello starszej wersji jednostki SKU hello, można migrować toohello nowe jednostki SKU. toomigrate, możesz usunąć hello istniejącą bramę sieci VPN dla sieci wirtualnej, a następnie utwórz nową.

Przepływ pracy migracji:

1. Usuń wszystkie bramy sieci wirtualnej toohello połączenia.
2. Usuń hello starego bramy sieci VPN.
3. Utwórz nową bramę sieci VPN hello.
4. Zaktualizuj urządzenia sieci VPN między lokalnymi przy hello nowy adres IP bramy VPN (w przypadku połączeń lokacja-lokacja).
5. Zaktualizuj wartość adresu IP bramy powitania dla bram sieci lokalnej do wirtualnymi łączących toothis bramy.
6. W przypadku klientów P2S łączenia sieci wirtualnej toohello przez tę bramę sieci VPN, należy pobrać nowe pakiety konfiguracji sieci VPN klienta.
7. Ponownie utwórz bramę sieci wirtualnej toohello połączeń hello.
