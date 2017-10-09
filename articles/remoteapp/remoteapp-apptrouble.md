---
title: "aaaAzure RemoteApp Rozwiązywanie problemów — błędy połączenia i uruchamiania aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot problemy z uruchamianiem i łączenie tooapplications w usłudze Azure RemoteApp."
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
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Rozwiązywanie problemów z usługą Azure RemoteApp — błędy połączenia i uruchamiania aplikacji
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Aplikacje hostowane w usłudze Azure RemoteApp może się nie powieść toolaunch kilka przyczyn. W tym artykule opisano różnych powodów i komunikaty o błędach użytkowników może zostać wyświetlony podczas próby toolaunch aplikacji. Wspomniana również błędów połączenia. (Ale w tym artykule nie opisano problemy przy logowaniu do powitania klienta usługi Azure RemoteApp).  

Poniżej informacji na temat komunikatów o błędach z powodu niepowodzenia tooapp uruchamiania i połączenia.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Trwa konfigurowanie... Spróbuj ponownie za 10 minut.
Ten błąd oznacza, że usługi Azure RemoteApp jest skalowaniu toomeet hello pojemności potrzeby użytkowników. W tle hello więcej wystąpień maszyny Wirtualnej Azure RemoteApp tworzonych toohandle hello pojemności potrzeb użytkowników. Zwykle to trwa około pięciu minut, ale może potrwać too10 minut. Czasami niezbyt tyle szybko i zasobów potrzebnych natychmiast. Na przykład 9 AM scenariusz, w których wielu użytkowników musi toouse aplikacji w usłudze Azure RemoteAppn na powitania tym samym czasie. W takim przypadku tooyou można włączyć obsługę **tryb pojemności** na powitania zaplecza. toodo tym Otwórz bilet pomocy technicznej platformy Azure. Być niektórych tooinclude identyfikator subskrypcji w żądaniu hello.  

![Możemy Ci skonfigurować uzyskiwania](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Nie można automatycznie-ponownie podłączyć tooyour aplikacje, ponownie uruchom aplikację
Ten komunikat o błędzie pojawia się często, jeśli zostały przy użyciu usługi Azure RemoteApp i następnie put z więcej niż 4 godziny toosleep PC i następnie wznowił działanie komputera i ponownie tooauto próba klienta usługi Azure RemoteApp hello i został przekroczony limit czasu.  Poinstruuj użytkowników toonavigate wstecz toohello aplikacji i spróbuj tooopen z powitania klienta usługi Azure RemoteApp.

![Nie można automatycznie-ponownie podłączyć tooyour aplikacji](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problemy z hello profilu tymczasowego
Ten błąd występuje, gdy profilu użytkownika (dysku profilu użytkownika) nie powiodło się toomount i użytkownika hello odebranych profilem tymczasowym.  Administratorzy powinien Przejdź toohello kolekcji w hello portalu Azure, a następnie przejdź toohello **sesji** karcie i podjąć próbę zbyt**Wyloguj** hello użytkownika. To spowoduje wymusić pełną wyloguje sesji użytkownika hello — a następnie toolaunch próba użytkownika hello aplikację ponownie. W przypadku niepowodzenia skontaktuj się z pomocą techniczną platformy Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Usługa Azure RemoteApp przestał działać
Ten komunikat o błędzie oznacza powitania klienta usługi Azure RemoteApp ma problem i musi toobe ponownego uruchomienia. Poinstruuj użytkowników tooclose: Wybierz **Zamknij program** , a następnie ponownie uruchom powitania klienta usługi Azure RemoteApp.  Jeśli hello problem nie ustąpi, Otwórz i biletu pomocy technicznej platformy Azure.

![Usługa Azure RemoteApp przestał działać](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Wystąpił błąd podczas podłączania pulpitu zdalnego dostępu do tego zasobu. Ponów próbę połączenia hello, lub skontaktuj się z administratorem systemu
To jest ogólny komunikat o błędzie — skontaktuj się z pomocą techniczną platformy Azure, możemy zbadać. 

![Komunikat ogólny usługi Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

