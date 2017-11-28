<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="55287-101">Przygotowania do aktualizacji</span><span class="sxs-lookup"><span data-stu-id="55287-101">Preparing for updates</span></span>
<span data-ttu-id="55287-102">Konieczne będzie przed skanowania i zastosować aktualizację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55287-102">You will need to perform the following steps before you scan and apply the update:</span></span>

1. <span data-ttu-id="55287-103">Utwórz migawkę chmury danych urządzenia.</span><span class="sxs-lookup"><span data-stu-id="55287-103">Take a cloud snapshot of the device data.</span></span>
2. <span data-ttu-id="55287-104">Upewnij się, że kontroler stałe adresy IP są rutowalne i można połączyć się z Internetem.</span><span class="sxs-lookup"><span data-stu-id="55287-104">Ensure that your controller fixed IPs are routable and can connect to the Internet.</span></span> <span data-ttu-id="55287-105">Te stałe adresy IP będzie używany do obsługi aktualizacji na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="55287-105">These fixed IPs will be used to service updates to your device.</span></span> <span data-ttu-id="55287-106">Można to sprawdzić, uruchamiając następujące polecenie cmdlet na każdym kontrolerze z interfejsu programu Windows PowerShell urządzenia:</span><span class="sxs-lookup"><span data-stu-id="55287-106">You can test this by running the following cmdlet on each controller from the Windows PowerShell interface of the device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="55287-107">**Przykładowe dane wyjściowe dla połączenia testowego, gdy stałe adresy IP można połączyć się z Internetem**</span><span class="sxs-lookup"><span data-stu-id="55287-107">**Sample output for Test-Connection when fixed IPs can connect to the Internet**</span></span>

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

<span data-ttu-id="55287-108">Po ręcznej kontrole wstępne została ukończona pomyślnie, można przejść do skanowania i zainstalować aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="55287-108">After you have successfully completed these manual pre-checks, you can proceed to scan and install the updates.</span></span>

