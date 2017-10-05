---
title: "Usługa Azure RemoteApp Rozwiązywanie problemów — błędy połączenia i uruchamiania aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywać problemy z uruchamianiem i podłączania do aplikacji w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fc9d538991adce7fc13e9654b9a7c6d113d03fde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Rozwiązywanie problemów z usługą Azure RemoteApp — błędy połączenia i uruchamiania aplikacji
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Aplikacje hostowane w usłudze Azure RemoteApp można nie można uruchomić kilka przyczyn istnienia. W tym artykule opisano różnych powodów i komunikaty o błędach użytkowników może zostać wyświetlony podczas próby uruchomienia aplikacji. Wspomniana również błędów połączenia. (Ale w tym artykule nie opisano problemy przy logowaniu się do klienta usługi Azure RemoteApp).  

Poniżej podano informacje o typowe komunikaty o błędach z powodu błędów połączenia i uruchamiania aplikacji.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Trwa konfigurowanie... Spróbuj ponownie za 10 minut.
Ten błąd oznacza, że usługi Azure RemoteApp jest skalowaniu aby sprostać wymaganiom pojemności użytkowników. W tle więcej wystąpień maszyny Wirtualnej Azure RemoteApp jest tworzone są do obsługi wymagań wydajności użytkowników. Zwykle to trwa około pięciu minut, ale może potrwać do 10 minut. Czasami niezbyt tyle szybko i zasobów potrzebnych natychmiast. Na przykład 9 AM scenariusz, w której wiele użytkownicy musieli używać aplikacji w usłudze Azure RemoteAppn w tym samym czasie. Jeśli występuje użytkownikowi można włączyć obsługę **tryb pojemności** wewnętrznych. Aby zrobić to otwarcie biletu pomocy technicznej platformy Azure. Zadbaj uwzględnić identyfikator subskrypcji w żądaniu.  

![Możemy Ci skonfigurować uzyskiwania](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-to-your-applications-please-re-launch-your-application"></a>Nie można ponownie do automatycznego do aplikacji, ponownie uruchom aplikację
Ten komunikat o błędzie często jest widoczna, jeśli zostały przy użyciu usługi Azure RemoteApp, a następnie umieść komputera w tryb uśpienia dłużej niż 4 godziny następnie wznowił działanie komputera i klienta usługi Azure RemoteApp próby automatycznego ponownego połączenia i został przekroczony limit czasu.  Poinstruować użytkowników, aby powrócić do aplikacji i spróbuj otworzyć go z klienta usługi Azure RemoteApp.

![Nie można automatycznie-ponownie podłączyć do aplikacji](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-the-temp-profile"></a>Problemy z profilu tymczasowego
Ten błąd występuje, gdy profilu użytkownika (dysku profilu użytkownika), nie udało się zainstalować, a użytkownik otrzymał profilem tymczasowym.  Administratorzy powinien przejść do kolekcji w portalu Azure, a następnie przejdź do **sesji** karcie i podejmij próbę ich **Wyloguj** użytkownika. Będzie to wymusić pełną wyloguje sesji użytkownika — a następnie użytkownik próbuje ponownie uruchomić aplikację. W przypadku niepowodzenia skontaktuj się z pomocą techniczną platformy Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Usługa Azure RemoteApp przestał działać
Ten komunikat o błędzie oznacza, że klient usługi Azure RemoteApp ma problem i musi zostać uruchomiony ponownie. Poinstruować użytkowników, aby zamknąć: Wybierz **Zamknij program** , a następnie ponownie uruchom klienta usługi Azure RemoteApp.  Jeśli problem będzie nadal występował, Otwórz i biletu pomocy technicznej platformy Azure.

![Usługa Azure RemoteApp przestał działać](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-the-connection-or-contact-your-system-administrator"></a>Wystąpił błąd podczas podłączania pulpitu zdalnego dostępu do tego zasobu. Spróbuj połączyć się ponownie lub skontaktuj się z administratorem systemu
To jest ogólny komunikat o błędzie — skontaktuj się z pomocą techniczną platformy Azure, możemy zbadać. 

![Komunikat ogólny usługi Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

