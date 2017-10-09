---
title: "Stan nieprawidłowego działania aaaTroubleshooting w usłudze Azure Traffic Manager"
description: "Jak tootroubleshoot profilów usługi Traffic Manager, gdy będzie wyświetlana jako znacznie mniej wydajna stanu."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="5d124-103">Rozwiązywanie problemów ze stanem obniżonej wydajności w usłudze Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5d124-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="5d124-104">W tym artykule opisano, jak tootroubleshoot profilu Menedżera ruchu Azure wyświetlana obniżeniem stanu.</span><span class="sxs-lookup"><span data-stu-id="5d124-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="5d124-105">W tym scenariuszu należy wziąć pod uwagę skonfigurowano profil Menedżera ruchu, wskazując toosome cloudapp.net hostowanych usług.</span><span class="sxs-lookup"><span data-stu-id="5d124-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="5d124-106">Jeśli wyświetlany hello kondycji z Menedżera ruchu **obniżony** stan, a następnie hello stan jeden lub więcej punktów końcowych może być **obniżony**:</span><span class="sxs-lookup"><span data-stu-id="5d124-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![Stan punktu końcowego obniżeniem](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="5d124-108">Jeśli wyświetlany hello kondycji z Menedżera ruchu **nieaktywne** stan, a następnie oba punkty końcowe mogą być **wyłączone**:</span><span class="sxs-lookup"><span data-stu-id="5d124-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Stan nieaktywny Menedżera ruchu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="5d124-110">Sondy opis Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="5d124-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="5d124-111">Menedżer ruchu uwzględnia toobe punktu końcowego kopii ONLINE tylko wtedy, gdy sondowania hello odbiera odpowiedź 200 protokołu HTTP z hello sondowania ścieżki.</span><span class="sxs-lookup"><span data-stu-id="5d124-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="5d124-112">Druga odpowiedź – 200 jest błąd.</span><span class="sxs-lookup"><span data-stu-id="5d124-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="5d124-113">Przekierowanie 30 x nie powiedzie się, nawet jeśli hello przekierowanie zwraca adres URL 200.</span><span class="sxs-lookup"><span data-stu-id="5d124-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="5d124-114">Dla sondy HTTPs błędów certyfikatów są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="5d124-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="5d124-115">Hello rzeczywistej zawartości hello sondowania ścieżki nie ma znaczenia, pod warunkiem, zwracany jest 200.</span><span class="sxs-lookup"><span data-stu-id="5d124-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="5d124-116">Sondowanie adresu URL toosome statycznej zawartości typu "/ favicon.ico" to technika wspólnej.</span><span class="sxs-lookup"><span data-stu-id="5d124-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="5d124-117">Zawartość dynamiczna, podobnie jak strony ASP hello, może nie zawsze zwrócić 200, nawet wtedy, gdy aplikacja hello jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="5d124-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="5d124-118">Najlepszym rozwiązaniem jest tooset hello sondowania toosomething ścieżki, która ma za mało toodetermine logikę, która hello lokacji jest w górę lub w dół.</span><span class="sxs-lookup"><span data-stu-id="5d124-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="5d124-119">W hello poprzedni przykład, ustawiając hello too"/favicon.ico ścieżki", tylko testowania tego w3wp.exe odpowiada.</span><span class="sxs-lookup"><span data-stu-id="5d124-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="5d124-120">To sondowanie może nie wskazywać aplikacji sieci web jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="5d124-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="5d124-121">Lepszym rozwiązaniem byłoby tooset tooa ścieżki coś takie jak "/ Probe.aspx" mający logiki toodetermine hello kondycji hello witryny.</span><span class="sxs-lookup"><span data-stu-id="5d124-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="5d124-122">Na przykład można użyć wykorzystania tooCPU liczników wydajności lub miary hello liczby żądań zakończonych niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="5d124-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="5d124-123">Lub może próbować tooaccess zasobów bazy danych lub toomake stanu sesji się, że działa hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5d124-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="5d124-124">Jeśli wszystkie punkty końcowe w profilu są ograniczone, Traffic Manager traktuje wszystkie punkty końcowe w dobrej kondycji i tras ruchu tooall punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="5d124-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="5d124-125">Takie zachowanie gwarantuje, że problemy z hello mechanizmu sondowania spowoduje zakończenie przestoju usługi.</span><span class="sxs-lookup"><span data-stu-id="5d124-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5d124-126">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="5d124-126">Troubleshooting</span></span>

<span data-ttu-id="5d124-127">tootroubleshoot błąd sondowania należy narzędzie, które zawiera kod stanu HTTP hello zwrotu z adresem URL badania hello.</span><span class="sxs-lookup"><span data-stu-id="5d124-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="5d124-128">Istnieje wiele dostępnych narzędzi przedstawiające hello raw odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d124-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="5d124-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="5d124-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="5d124-130">Narzędzie curl</span><span class="sxs-lookup"><span data-stu-id="5d124-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="5d124-131">wget</span><span class="sxs-lookup"><span data-stu-id="5d124-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="5d124-132">Ponadto można użyć karty sieciowej hello hello F12 narzędzia do debugowania w odpowiedzi HTTP hello tooview programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="5d124-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="5d124-133">W tym przykładzie chcemy toosee hello odpowiedzi z naszych adresem URL badania: http://watestsdp2008r2.cloudapp.net:80/sondowania.</span><span class="sxs-lookup"><span data-stu-id="5d124-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="5d124-134">Poniższy przykład PowerShell Hello przedstawiono hello problem.</span><span class="sxs-lookup"><span data-stu-id="5d124-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="5d124-135">Przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="5d124-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="5d124-136">Zwróć uwagę, że Odebraliśmy odpowiedź przekierowania.</span><span class="sxs-lookup"><span data-stu-id="5d124-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="5d124-137">Jak wspomniano wcześniej, StatusCode żadnych innych niż 200 oznaczają niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="5d124-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="5d124-138">Zmiany menedżera ruchu hello tooOffline stan punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5d124-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="5d124-139">tooresolve hello problem, może być zwracany tooensure konfiguracji witryny sieci Web hello wyboru, która hello prawidłowego StatusCode ze ścieżki sondowania hello.</span><span class="sxs-lookup"><span data-stu-id="5d124-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="5d124-140">Skonfiguruj ponownie hello Traffic Manager sondowania toopoint tooa ścieżki, która zwraca 200.</span><span class="sxs-lookup"><span data-stu-id="5d124-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="5d124-141">Jeśli Twoje sondowania używa hello protokołu HTTPS, może być konieczne certyfikatu toodisable sprawdzanie błędów protokołu SSL/TLS tooavoid podczas testu.</span><span class="sxs-lookup"><span data-stu-id="5d124-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="5d124-142">Witaj następujące instrukcje programu PowerShell wyłączyć sprawdzanie poprawności certyfikatu dla bieżącej sesji programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="5d124-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="5d124-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d124-143">Next Steps</span></span>

[<span data-ttu-id="5d124-144">O metodach routingu ruchu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="5d124-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="5d124-145">Co to jest Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="5d124-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="5d124-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="5d124-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="5d124-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="5d124-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="5d124-148">Operacje w usłudze Traffic Manager (dokumentacja interfejsu API REST)</span><span class="sxs-lookup"><span data-stu-id="5d124-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="5d124-149">[Polecenia cmdlet systemu Azure Traffic Manager][1]</span><span class="sxs-lookup"><span data-stu-id="5d124-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
