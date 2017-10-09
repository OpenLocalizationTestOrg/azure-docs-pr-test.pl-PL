---
title: "aaaTroubleshoot wdrożone urządzenie StorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toodiagnose i napraw błędy występujące na urządzeniu StorSimple, który jest obecnie wdrożone i działa."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Rozwiązywanie problemów z działającego urządzenia StorSimple
## <a name="overview"></a>Omówienie
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów przydatne w celu rozwiązania problemów z konfiguracją czy mogą wystąpić po urządzenia StorSimple jest wdrożone i działa. Opisuje typowych problemów, możliwe przyczyny i toohelp zalecane kroki rozwiązywania problemów, które mogą wystąpić po uruchomieniu programu Microsoft Azure StorSimple. Te informacje dotyczą urządzenia fizycznego StorSimple lokalnymi tooboth hello i hello urządzenia wirtualnego StorSimple.

Na końcu hello w tym artykule, które można znaleźć listę kodów błędów, które można napotkać podczas operacji Microsoft Azure StorSimple oraz czynności może potrwać tooresolve hello błędy. 

## <a name="setup-wizard-process-for-operational-devices"></a>Proces Kreatora konfiguracji działających urządzeń
Użyj Kreatora instalacji hello ([Invoke HcsSetupWizard][1]) toocheck hello Konfiguracja urządzenia i podjąć działania naprawcze w razie potrzeby.

Po uruchomieniu Kreatora instalacji hello na urządzeniu wcześniej skonfigurowana i działa, przepływ procesu hello jest inny. Można zmienić tylko hello następujące wpisy:

* Adres IP, maski podsieci i bramy
* Podstawowy serwer DNS
* Podstawowy serwer NTP
* Konfiguracja serwera proxy sieci web opcjonalne

Kreator instalacji Hello nie wykonuje hello operacji powiązanych toopassword kolekcji i usługi rejestracji urządzeń.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Błędów występujących podczas kolejnych uruchomieniach hello Kreatora instalacji
Witaj w poniższej tabeli opisano hello błędy, które można napotkać podczas uruchamiania Kreatora instalacji hello na urządzeniu z systemem operacyjny, możliwe przyczyny błędów hello i zalecane akcje tooresolve je. 

| Nie. | Komunikat o błędzie lub warunku | Możliwe przyczyny | Zalecane działanie |
|:--- |:--- |:--- |:--- |
| 1 |Błąd 350032: Już zostało zdezaktywowane tego urządzenia. |Zostanie wyświetlony ten błąd, po uruchomieniu Kreatora konfiguracji hello na urządzeniu jest dezaktywowana. |[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) dalsze czynności. Nie można umieścić dezaktywować urządzenie w usłudze. Resetowanie do ustawień fabrycznych mogą być wymagane w celu aktywowania urządzeń hello ponownie. |
| 2 |Invoke-HcsSetupWizard: ERROR_INVALID_FUNCTION (wyjątek od HRESULT: 0x80070001) |Aktualizacja serwera DNS Hello kończy się niepowodzeniem. Ustawienia DNS są ustawieniami globalnymi i są stosowane we wszystkich interfejsach sieciowych hello włączone. |Włącz interfejs hello i ponownie Zastosuj ustawienia DNS hello. To może zakłócić hello sieci dla innych interfejsów włączone, ponieważ te ustawienia są globalne. |
| 3 |urządzenie Hello jest wyświetlany toobe w trybie online w portalu usługi Menedżer StorSimple hello, ale po spróbuj toocomplete hello minimalnej konfiguracji i zapisać konfigurację hello hello operacja nie powiedzie się. |Podczas początkowej konfiguracji serwera proxy sieci web hello nie został skonfigurowany, nawet jeśli było serwera proxy rzeczywistych. |Użyj hello [polecenia cmdlet Test-HcsmConnection] [ 2] toolocate hello błędu. [Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) przypadku toocorrect hello problem. |
| 4 |Invoke-HcsSetupWizard: Wartość nie wchodzi w zakres hello oczekiwano. |Niepoprawna maska podsieci tworzy tego błędu. Możliwe przyczyny to: <ul><li> Maska podsieci Hello jest lub jest pusty.</li><li>format prefiks Ipv6 Hello jest nieprawidłowy.</li><li>Interfejs Hello jest włączone w chmurze, ale brama hello jest niewystarczające lub niepoprawne.</li></ul>Należy pamiętać, że interfejs DATA 0 ma automatycznie włączoną obsługę chmury Jeśli skonfigurowana za pośrednictwem hello Kreatora instalacji. |toodetermine hello problem, użyj podsieci 0.0.0.0 lub 256.256.256.256 i przyjrzyj się hello danych wyjściowych. Wprowadź prawidłowe wartości hello maski podsieci, bramy i prefiks Ipv6, zgodnie z potrzebami. |

## <a name="error-codes"></a>Kody błędów
Błędy są wyświetlane w kolejności numerycznej.

| Numer błędu | Tekst błędu lub opisu | Akcja użytkownika zalecane |
|:--- |:--- |:--- |
| 10502 |Napotkano błąd podczas uzyskiwania dostępu do konta magazynu. |Poczekaj kilka minut, a następnie spróbuj ponownie. Jeśli hello błąd będzie się powtarzał, skontaktuj się z pomocą techniczną firmy Microsoft dalsze czynności. |
| 40017 |Witaj operacji tworzenia kopii zapasowej nie powiodło się, zgodnie z określonym w zasadach tworzenia kopii zapasowej hello wolumin nie został znaleziony na powitania urządzenia. |Ponów operację tworzenia kopii zapasowej hello, jeśli hello błąd będzie się powtarzał, skontaktuj się z Microsoft Support. dalsze czynności. |
| 40018 |Witaj operacji tworzenia kopii zapasowej nie powiodło się, zgodnie z określonym w zasadach tworzenia kopii zapasowej hello woluminów hello nie znaleziono żadnych na urządzeniu hello. |Ponów operację tworzenia kopii zapasowej hello, jeśli hello błąd będzie się powtarzał, skontaktuj się z Microsoft Support. dalsze czynności. |
| 390061 |Witaj system jest zajęty lub niedostępny. |Poczekaj kilka minut, a następnie spróbuj ponownie. Jeśli hello błąd będzie się powtarzał, skontaktuj się z pomocą techniczną firmy Microsoft dalsze czynności. |
| 390143 |Wystąpił błąd z kodem błędu 390143. (Nieznany błąd.) |Jeśli hello błąd będzie się powtarzał, skontaktuj się z Microsoft Support, dalsze czynności. |

## <a name="next-steps"></a>Następne kroki
Jeśli masz problem hello tooresolve, [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) Aby uzyskać pomoc. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
