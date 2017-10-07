---
title: "aaaApp wymagania dotyczące usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach dotyczących powitania dla aplikacji, które mają toouse w usłudze Azure RemoteApp"
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
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Wymagania aplikacji
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp obsługuje przesyłania strumieniowego 32-bitowy lub 64-bitowej aplikacji systemu Windows za pomocą obrazu systemu Windows Server 2012 R2. Większość istniejących 32-bitowy lub 64-bitowej aplikacji systemu Windows uruchom "jako" w usłudze Azure RemoteApp (usług pulpitu zdalnego lub wcześniej znane jako usługi terminalowe) środowiska. Jednak ma różnicy między zainstalowany, a także — niektóre aplikacje działać prawidłowo i wykonaj, podczas gdy inne osoby nie. Witaj następujących informacji zawiera wskazówki dotyczące tworzenia aplikacji w środowisku usług pulpitu zdalnego i testowania zgodności tooensure.

Porada: Trwają prace nad tworzenia przykłady pracy aplikacji. Zostanie wyświetlone nowe tematy, które omówiono w nim przy użyciu programu Microsoft Access, QuickBooks i App-V w usłudze RemoteApp.

## <a name="requirements"></a>Wymagania
Te trzy wymagania, jeśli zostały wykonane, Pomoc aplikacji Uruchom również w usłudze RemoteApp:

1. Aplikacje, które spełniają wszystkie [wymagania dotyczące certyfikacji dla systemu Windows aplikacji klasycznych](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) i stosować zbyt[wytycznych programowania usług pulpitu zdalnego](https://msdn.microsoft.com/library/aa383490.aspx) będzie miał pełną zgodność z usługą RemoteApp.
2. Aplikacje powinny nigdy nie przechowywać dane lokalnie w obrazie hello lub wystąpienia usługi RemoteApp, które mogą zostać utracone.  Po utworzeniu kolekcji usługi RemoteApp wystąpień hello są klonowane i są bezstanowych i powinien zawierać wyłącznie aplikacje. Przechowywanie danych w zewnętrznym źródle lub w profilu użytkownika hello.
3. Niestandardowe obrazy nigdy nie powinna zawierać dane, które mogą zostać utracone.  

## <a name="testing-your-apps"></a>Testowanie aplikacji
Użyj tych aplikacji tootesting kroki:

1. Instalowanie systemu Windows Server 2012 R2 i aplikacji
2. Włączanie pulpitu zdalnego
3. Utwórz dwa konta użytkownika, Użytkownik_a i Użytkownik_b Dodawanie zarówno grupy zabezpieczeń Użytkownicy kont toohello pulpitu zdalnego.
4. Sprawdź zgodność wielu sesji podczas uruchamiania aplikacji hello, ustanawiając dwóch jednoczesnych toohello sesji usług pulpitu zdalnego komputera.
5. Sprawdź poprawność zachowanie aplikacji

## <a name="application-development-guidelines"></a>Wskazówki dotyczące programowania aplikacji
Użyj hello następujące wytyczne dotyczące tworzenia aplikacji dla usługi RemoteApp.

### <a name="multiple-users"></a>Wielu użytkowników
* Instalowanie [dla pojedynczego użytkownika ](https://msdn.microsoft.com/library/aa380661.aspx)można tworzyć problemy w środowisku wielodostępnym.
* Aplikacje powinny [przechowywania informacji o użytkowniku](https://msdn.microsoft.com/library/aa383452.aspx) w lokalizacjach specyficzne dla użytkownika, oddzielnie z globalnego informacji dotyczący tooall użytkowników.
* RemoteApp używa wielu [przestrzeni nazw dla obiektów jądra](https://msdn.microsoft.com/library/aa382954.aspx); globalnej przestrzeni nazw jest używana głównie przez usługi w aplikacji klient/serwer.
* Nie jest bezpieczne tooassume, który hello nazwę komputera lub hello [adres IP](https://msdn.microsoft.com/library/aa382942.aspx) przypisanej toohello komputera są skojarzone z pojedynczego użytkownika, ponieważ wielu użytkowników może być zalogowany jednocześnie tooa hosta sesji usług pulpitu zdalnego (sesji usług pulpitu zdalnego Serwer hosta).

### <a name="performance"></a>Wydajność
* Wyłącz [efekty graficzne](https://msdn.microsoft.com/library/aa380822.aspx) przed dodaniem tooRemoteApp Twojej aplikacji.
* dostępność toomaximize procesora CPU dla wszystkich użytkowników, albo wyłącz [zadania w tle ](https://msdn.microsoft.com/library/aa380665.aspx) lub Utwórz zadania tła wydajne, które nie są obciążający zasoby.
* Należy dostosować i zrównoważenia aplikacji [wątku użycia](https://msdn.microsoft.com/library/aa383520.aspx) w środowisku wielodostępnym, wieloprocesorowych.
* wydajność toooptimize jest dobrym rozwiązaniem dla aplikacji za[wykryć](https://msdn.microsoft.com/library/aa380798.aspx) czy są uruchomione w sesji klienta.

