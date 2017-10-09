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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Rozwiązywanie problemów ze stanem obniżonej wydajności w usłudze Azure Traffic Manager

W tym artykule opisano, jak tootroubleshoot profilu Menedżera ruchu Azure wyświetlana obniżeniem stanu. W tym scenariuszu należy wziąć pod uwagę skonfigurowano profil Menedżera ruchu, wskazując toosome cloudapp.net hostowanych usług. Jeśli wyświetlany hello kondycji z Menedżera ruchu **obniżony** stan, a następnie hello stan jeden lub więcej punktów końcowych może być **obniżony**:

![Stan punktu końcowego obniżeniem](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Jeśli wyświetlany hello kondycji z Menedżera ruchu **nieaktywne** stan, a następnie oba punkty końcowe mogą być **wyłączone**:

![Stan nieaktywny Menedżera ruchu](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Sondy opis Menedżera ruchu

* Menedżer ruchu uwzględnia toobe punktu końcowego kopii ONLINE tylko wtedy, gdy sondowania hello odbiera odpowiedź 200 protokołu HTTP z hello sondowania ścieżki. Druga odpowiedź – 200 jest błąd.
* Przekierowanie 30 x nie powiedzie się, nawet jeśli hello przekierowanie zwraca adres URL 200.
* Dla sondy HTTPs błędów certyfikatów są ignorowane.
* Hello rzeczywistej zawartości hello sondowania ścieżki nie ma znaczenia, pod warunkiem, zwracany jest 200. Sondowanie adresu URL toosome statycznej zawartości typu "/ favicon.ico" to technika wspólnej. Zawartość dynamiczna, podobnie jak strony ASP hello, może nie zawsze zwrócić 200, nawet wtedy, gdy aplikacja hello jest w dobrej kondycji.
* Najlepszym rozwiązaniem jest tooset hello sondowania toosomething ścieżki, która ma za mało toodetermine logikę, która hello lokacji jest w górę lub w dół. W hello poprzedni przykład, ustawiając hello too"/favicon.ico ścieżki", tylko testowania tego w3wp.exe odpowiada. To sondowanie może nie wskazywać aplikacji sieci web jest w dobrej kondycji. Lepszym rozwiązaniem byłoby tooset tooa ścieżki coś takie jak "/ Probe.aspx" mający logiki toodetermine hello kondycji hello witryny. Na przykład można użyć wykorzystania tooCPU liczników wydajności lub miary hello liczby żądań zakończonych niepowodzeniem. Lub może próbować tooaccess zasobów bazy danych lub toomake stanu sesji się, że działa hello aplikacji sieci web.
* Jeśli wszystkie punkty końcowe w profilu są ograniczone, Traffic Manager traktuje wszystkie punkty końcowe w dobrej kondycji i tras ruchu tooall punktów końcowych. Takie zachowanie gwarantuje, że problemy z hello mechanizmu sondowania spowoduje zakończenie przestoju usługi.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

tootroubleshoot błąd sondowania należy narzędzie, które zawiera kod stanu HTTP hello zwrotu z adresem URL badania hello. Istnieje wiele dostępnych narzędzi przedstawiające hello raw odpowiedzi HTTP.

* [Fiddler](http://www.telerik.com/fiddler)
* [Narzędzie curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Ponadto można użyć karty sieciowej hello hello F12 narzędzia do debugowania w odpowiedzi HTTP hello tooview programu Internet Explorer.

W tym przykładzie chcemy toosee hello odpowiedzi z naszych adresem URL badania: http://watestsdp2008r2.cloudapp.net:80/sondowania. Poniższy przykład PowerShell Hello przedstawiono hello problem.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Przykładowe dane wyjściowe:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Zwróć uwagę, że Odebraliśmy odpowiedź przekierowania. Jak wspomniano wcześniej, StatusCode żadnych innych niż 200 oznaczają niepowodzenie. Zmiany menedżera ruchu hello tooOffline stan punktu końcowego. tooresolve hello problem, może być zwracany tooensure konfiguracji witryny sieci Web hello wyboru, która hello prawidłowego StatusCode ze ścieżki sondowania hello. Skonfiguruj ponownie hello Traffic Manager sondowania toopoint tooa ścieżki, która zwraca 200.

Jeśli Twoje sondowania używa hello protokołu HTTPS, może być konieczne certyfikatu toodisable sprawdzanie błędów protokołu SSL/TLS tooavoid podczas testu. Witaj następujące instrukcje programu PowerShell wyłączyć sprawdzanie poprawności certyfikatu dla bieżącej sesji programu PowerShell hello:

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

## <a name="next-steps"></a>Następne kroki

[O metodach routingu ruchu Menedżera ruchu](traffic-manager-routing-methods.md)

[Co to jest Menedżera ruchu](traffic-manager-overview.md)

[Cloud Services](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[Operacje w usłudze Traffic Manager (dokumentacja interfejsu API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Polecenia cmdlet systemu Azure Traffic Manager][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
