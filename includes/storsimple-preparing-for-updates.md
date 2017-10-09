<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Przygotowania do aktualizacji
Konieczne będzie hello tooperform przed skanowania i zastosować aktualizację hello wykonaj następujące kroki:

1. Utwórz migawkę chmury hello danych urządzenia.
2. Upewnij się, że kontroler stałe adresy IP są rutowalne i mogą łączyć się toohello Internet. Stałe adresy IP będą używany tooservice aktualizacje tooyour urządzenia. Można to sprawdzić, uruchamiając następujące polecenia cmdlet na każdym kontrolerze z interfejsu programu Windows PowerShell hello urządzenia hello hello:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Przykładowe dane wyjściowe dla połączenia testowego, gdy stałe adresy IP można łączyć toohello Internet**

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

Po tych czynności sprawdzające wstępnych została ukończona pomyślnie, można kontynuować tooscan i zainstaluj aktualizacje hello.

