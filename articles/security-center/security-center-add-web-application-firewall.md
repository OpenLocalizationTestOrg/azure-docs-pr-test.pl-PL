---
title: "aaaAdd zapory aplikacji sieci web w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** Dodaj sieci web aplikacji zapory ** i ** finalizowanie ochrony aplikacji **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Dodawanie zapory aplikacji sieci web w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure może zaleca dodanie zapory aplikacji sieci web (WAF) z toosecure partnera firmy Microsoft aplikacji sieci web. Ten dokument przeprowadzi Cię przez przykładowy sposób tooapply tego zalecenia.

Wszelkie publicznego połączonej adresu IP (IP poziomie wystąpienia lub IP równoważenia obciążenia) zawierający sieciową grupę zabezpieczeń skojarzoną z portami Otwórz przychodzący sieci web (80,443) jest wyświetlane zalecenie zapory aplikacji sieci Web.

Centrum zabezpieczeń zaleca się, że przepisy toohelp zapory aplikacji sieci Web chronić przed atakami przeznaczonych dla aplikacji sieci web na maszynach wirtualnych i środowiska usługi aplikacji. Środowisko aplikacji (ASE) jest [Premium](https://azure.microsoft.com/pricing/details/app-service/) opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi App service. toolearn więcej informacji na temat ASE, zobacz hello [dokumentację środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

## <a name="implement-hello-recommendation"></a>Implementowanie hello zalecenia
1. W hello **zalecenia** bloku, wybierz opcję **zabezpieczenia aplikacji sieci web za pomocą zapory aplikacji sieci web**.
   ![Zabezpieczanie aplikacji sieci web][1]
2. W hello **zabezpieczenia aplikacji sieci web za pomocą zapory aplikacji sieci web** bloku, wybierz aplikację sieci web. Witaj **Dodawanie zapory aplikacji sieci Web** zostanie otwarty blok.
   ![Dodawanie zapory aplikacji sieci Web][2]
3. Można wybrać toouse istniejących zapory aplikacji sieci web Jeśli jest dostępna lub można utworzyć nowy. W tym przykładzie nie dostępnych żadnych istniejących WAFs, utworzymy zapory aplikacji sieci Web.
4. toocreate zapory aplikacji sieci Web, wybierz rozwiązanie z listy hello zintegrowane partnerów. W tym przykładzie mamy wybierz **zapory aplikacji sieci Web Barracuda**.
5. Witaj **zapory aplikacji sieci Web Barracuda** zostanie otwarty blok informacjami o hello rozwiązaniem partnerskim. Wybierz **Utwórz** w bloku informacji hello.

   ![Blok informacji zapory][3]

6. Witaj **Nowa Zapora aplikacji sieci Web** zostanie otwarty blok, których można wykonywać **konfiguracji maszyny Wirtualnej** kroki i podaj **informacji zapory aplikacji sieci Web**. Wybierz **konfiguracji maszyny Wirtualnej**.
7. W hello **konfiguracji maszyny Wirtualnej** bloku, wprowadź informacje wymagane toospin hello maszyny wirtualnej, który uruchamia hello zapory aplikacji sieci Web.
   ![Konfiguracja maszyny Wirtualnej][4]
8. Zwraca toohello **Nowa Zapora aplikacji sieci Web** bloku, a następnie wybierz **informacji zapory aplikacji sieci Web**. W hello **informacji zapory aplikacji sieci Web** bloku, należy skonfigurować zapory aplikacji sieci Web hello samej siebie. Krok 7 umożliwia maszynie wirtualnej hello tooconfigure na które hello zapory aplikacji sieci Web działa i kroku 8 umożliwia hello tooprovision zapory aplikacji sieci Web, sam.

## <a name="finalize-application-protection"></a>Finalizuj ochronę aplikacji
1. Zwraca toohello **zalecenia** bloku. Wygenerowano nowy wpis po utworzeniu hello zapory aplikacji sieci Web, nazywany **Finalizuj ochronę aplikacji**. Ten wpis informuje konieczność toocomplete hello proces faktycznie Podłączanie hello zapory aplikacji sieci Web w obrębie hello Azure Virtual Network, dzięki czemu można chronić aplikacji hello.

   ![Finalizuj ochronę aplikacji][5]

2. Wybierz **Finalizuj ochronę aplikacji**. Zostanie otwarty nowy blok. Widać, czy jest aplikacją sieci web wymagającego toohave ruch przekierowany.
3. Wybierz aplikację sieci web hello. Zostanie otwarty blok zawierający kroki dla finalizowanie ustawienia zapory aplikacji sieci web hello. Wykonaj kroki hello, a następnie wybierz **ograniczania ruchu**. Następnie Centrum zabezpieczeń hello w górę okablowania dla Ciebie.

   ![Ograniczanie ruchu][6]

> [!NOTE]
> Wiele aplikacji sieci web w Centrum zabezpieczeń można chronić przez dodanie tych aplikacji tooyour istniejące zapory aplikacji sieci Web wdrożenia.
>
>

Dzienniki Hello, w tym zapory aplikacji sieci Web teraz są w pełni zintegrowane. Automatycznie zbierania i analizowania dzienników hello, dzięki czemu jego powierzchni tooyou alerty zabezpieczeń ważne, można uruchomić Centrum zabezpieczeń.

## <a name="next-steps"></a>Następne kroki
Ten dokument pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Dodaj aplikację sieci web". toolearn więcej informacji o konfigurowaniu zapory aplikacji sieci web, zobacz następujące hello:

* [Konfigurowanie zapory aplikacji sieci Web (WAF) do środowiska usługi aplikacji](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
