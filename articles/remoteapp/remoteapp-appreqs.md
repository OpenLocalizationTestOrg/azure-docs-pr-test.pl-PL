---
title: "Wymagania dotyczące aplikacji dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach dotyczących aplikacji, które mają być używane w usłudze Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a>Wymagania aplikacji
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Usługa Azure RemoteApp obsługuje przesyłania strumieniowego 32-bitowy lub 64-bitowej aplikacji systemu Windows za pomocą obrazu systemu Windows Server 2012 R2. Większość istniejących 32-bitowy lub 64-bitowej aplikacji systemu Windows uruchom "jako" w usłudze Azure RemoteApp (usług pulpitu zdalnego lub wcześniej znane jako usługi terminalowe) środowiska. Jednak ma różnicy między zainstalowany, a także — niektóre aplikacje działać prawidłowo i wykonaj, podczas gdy inne osoby nie. Poniżej znajdują się wskazówki dotyczące tworzenia aplikacji w środowisku usług pulpitu zdalnego i testy w celu zapewnienia zgodności.

Porada: Trwają prace nad tworzenia przykłady pracy aplikacji. Zostanie wyświetlone nowe tematy, które omówiono w nim przy użyciu programu Microsoft Access, QuickBooks i App-V w usłudze RemoteApp.

## <a name="requirements"></a>Wymagania
Te trzy wymagania, jeśli zostały wykonane, Pomoc aplikacji Uruchom również w usłudze RemoteApp:

1. Aplikacje, które spełniają wszystkie [wymagania dotyczące certyfikacji dla systemu Windows aplikacji klasycznych](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) i być zgodne z [wytycznych programowania usług pulpitu zdalnego](https://msdn.microsoft.com/library/aa383490.aspx) będzie miał pełną zgodność z usługą RemoteApp.
2. Aplikacje powinny nigdy nie przechowują dane lokalnie w obrazie lub wystąpienia usługi RemoteApp, które mogą zostać utracone.  Po utworzeniu kolekcji usługi RemoteApp wystąpienia są klonowane i są bezstanowych i powinien zawierać wyłącznie aplikacje. Przechowywanie danych w zewnętrznym źródle lub w profilu użytkownika.
3. Niestandardowe obrazy nigdy nie powinna zawierać dane, które mogą zostać utracone.  

## <a name="testing-your-apps"></a>Testowanie aplikacji
Wykonaj następujące kroki w celu testowania aplikacji:

1. Instalowanie systemu Windows Server 2012 R2 i aplikacji
2. Włączanie pulpitu zdalnego
3. Utwórz dwa konta użytkownika, Użytkownik_a i Użytkownik_b Dodawanie oba konta użytkownika do grupy zabezpieczeń usług pulpitu zdalnego.
4. Sprawdź zgodność wiele sesji, ustanawiając dwóch jednoczesnych RDS sesji do komputera podczas uruchamiania aplikacji.
5. Sprawdź poprawność zachowanie aplikacji

## <a name="application-development-guidelines"></a>Wskazówki dotyczące programowania aplikacji
Skorzystaj z poniższych wskazówek do opracowywania aplikacji dla usługi RemoteApp.

### <a name="multiple-users"></a>Wielu użytkowników
* Instalowanie [dla pojedynczego użytkownika ](https://msdn.microsoft.com/library/aa380661.aspx)można tworzyć problemy w środowisku wielodostępnym.
* Aplikacje powinny [przechowywania informacji o użytkowniku](https://msdn.microsoft.com/library/aa383452.aspx) w lokalizacjach specyficzne dla użytkownika, niezależnie od globalne informacje, która ma zastosowanie do wszystkich użytkowników.
* RemoteApp używa wielu [przestrzeni nazw dla obiektów jądra](https://msdn.microsoft.com/library/aa382954.aspx); globalnej przestrzeni nazw jest używana głównie przez usługi w aplikacji klient/serwer.
* Nie jest bezpieczne przyjęto założenie, że nazwa komputera lub [adres IP](https://msdn.microsoft.com/library/aa382942.aspx) przypisane do komputera są skojarzone z pojedynczego użytkownika, ponieważ wielu użytkowników może być zalogowany jednocześnie z serwerem hosta sesji usług pulpitu zdalnego (Host sesji usług pulpitu zdalnego).

### <a name="performance"></a>Wydajność
* Wyłącz [efekty graficzne](https://msdn.microsoft.com/library/aa380822.aspx) przed dodaniem aplikacji do usługi RemoteApp.
* Aby zmaksymalizować dostępności procesora CPU dla wszystkich użytkowników, albo wyłącz [zadania w tle ](https://msdn.microsoft.com/library/aa380665.aspx) lub Utwórz zadania tła wydajne, które nie są obciążający zasoby.
* Należy dostosować i zrównoważenia aplikacji [wątku użycia](https://msdn.microsoft.com/library/aa383520.aspx) w środowisku wielodostępnym, wieloprocesorowych.
* Aby zoptymalizować wydajność, dobrym rozwiązaniem dla aplikacji jest [wykryć](https://msdn.microsoft.com/library/aa380798.aspx) czy są uruchomione w sesji klienta.

