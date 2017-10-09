<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="7c22b-101">Przygotowania do aktualizacji</span><span class="sxs-lookup"><span data-stu-id="7c22b-101">Preparing for updates</span></span>
<span data-ttu-id="7c22b-102">Konieczne będzie hello tooperform przed skanowania i zastosować aktualizację hello wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7c22b-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="7c22b-103">Utwórz migawkę chmury hello danych urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7c22b-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="7c22b-104">Upewnij się, że kontroler stałe adresy IP są rutowalne i mogą łączyć się toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="7c22b-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="7c22b-105">Stałe adresy IP będą używany tooservice aktualizacje tooyour urządzenia.</span><span class="sxs-lookup"><span data-stu-id="7c22b-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="7c22b-106">Można to sprawdzić, uruchamiając następujące polecenia cmdlet na każdym kontrolerze z interfejsu programu Windows PowerShell hello urządzenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="7c22b-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="7c22b-107">**Przykładowe dane wyjściowe dla połączenia testowego, gdy stałe adresy IP można łączyć toohello Internet**</span><span class="sxs-lookup"><span data-stu-id="7c22b-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

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

<span data-ttu-id="7c22b-108">Po tych czynności sprawdzające wstępnych została ukończona pomyślnie, można kontynuować tooscan i zainstaluj aktualizacje hello.</span><span class="sxs-lookup"><span data-stu-id="7c22b-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

