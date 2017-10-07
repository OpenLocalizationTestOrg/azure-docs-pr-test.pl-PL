---
title: "problemy z wdrażaniem usługi chmury aaaTroubleshoot | Dokumentacja firmy Microsoft"
description: "Istnieje kilka typowych problemów, które mogą napotkać podczas wdrażania tooAzure usługi chmury. Ten artykuł zawiera toosome rozwiązania ich."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Rozwiązywanie problemów z wdrażaniem usługi chmury
Podczas wdrażania tooAzure pakietu chmury usługi aplikacji można uzyskać informacji o wdrażaniu hello z hello **właściwości** okienka w hello portalu Azure. Szczegóły hello można użyć w tym toohelp okienko jest rozwiązywanie problemów z usługą w chmurze hello oraz udostępniać ten tooAzure informacje pomocy technicznej podczas otwierania nowe żądanie pomocy technicznej.

Można znaleźć hello **właściwości** okienko w następujący sposób:

* W portalu Azure Witaj, kliknij hello wdrażania usługi w chmurze, kliknij **wszystkie ustawienia**, a następnie kliknij przycisk **właściwości**.
* W hello klasycznego portalu Azure kliknij hello wdrażania usługi w chmurze, kliknij przycisk **pulpitu NAWIGACYJNEGO**, który znajduje się w hello prawym dolnym rogu strony hello (w obszarze **szybkiego dostępu**). Należy pamiętać, że w tym okienku Brak etykiety "Właściwości".

> [!NOTE]
> Możesz skopiować zawartość hello hello **właściwości** Schowka toohello okienko, klikając ikonę hello w hello prawym górnym rogu okienka hello.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problem: nie można uzyskać dostęp do witryny sieci Web, ale Moje wdrożenie zostanie uruchomione i wszystkich wystąpień ról są gotowe
link do adresu URL witryny internetowej Hello wyświetlana w portalu hello nie obejmuje hello portu. Witaj domyślny port dla witryn sieci Web to 80. Jeśli aplikacja jest skonfigurowany toorun w innego portu, należy dodać adres URL toohello numeru hello poprawnego portu podczas uzyskiwania dostępu do witryny sieci Web hello.

1. Hello portalu Azure kliknij hello wdrażania usługi w chmurze.
2. W hello **właściwości** hello portów dla wystąpień roli hello Sprawdź okienko hello portalu Azure (w obszarze **danych wejściowych punktów końcowych**).
3. Jeśli hello port nie jest 80, Dodaj URL toohello wartość poprawnego portu hello, gdy uzyskujesz dostęp do aplikacji hello. toospecify z systemem innym niż domyślny port, wpisz adres URL hello, z dwukropkiem (:) i numer portu hello, nie może zawierać spacji.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problem: Moje wystąpień ról poddanych recyklingowi bez żadnego działania do mnie
Naprawianie usługi odbywa się automatycznie, gdy Azure wykryje problem węzłów i w związku z tym przenosi węzłów toonew wystąpień roli. W takim przypadku można napotkać odtwarzania automatycznie wystąpienia roli. toofind sprawdzanie, czy usługi, naprawianie wystąpił:

1. Hello portalu Azure kliknij hello wdrażania usługi w chmurze.
2. W hello **właściwości** okienko hello portalu Azure, przejrzyj informacje o hello i określenia, czy naprawą usługi wystąpiły w czasie hello obserwowanych ról hello odtwarzania.

Role również odtwarzana około raz w miesiącu podczas systemu operacyjnego hosta i aktualizacje systemu operacyjnego gościa.  
Aby uzyskać więcej informacji, zobacz hello blogu [roli wystąpienia uruchamia ponownie z powodu uaktualnienia tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problem: nie można wykonać wymiany wirtualnych adresów IP i komunikat o błędzie
Wymiany wirtualnych adresów IP jest niedozwolona, jeśli aktualizacja wdrożenia jest w toku. Wdrożenia aktualizacji mogą być wykonywane automatycznie po:

* Nowy system operacyjny gościa jest dostępna i skonfigurowane aktualizacje automatyczne.
* Naprawianie usługi występuje.

toofind limit aktualizacji automatyczne uniemożliwia wykonanie wymiany wirtualnych adresów IP:

1. Hello portalu Azure kliknij hello wdrażania usługi w chmurze.
2. W hello **właściwości** okienko hello portalu Azure, przyjrzeć się wartość hello **stan**. Jeśli jest **gotowe**, następnie sprawdź **Ostatnia operacja** toosee, jeśli jeden ostatnio miejsce, które mogą uniemożliwić wymiany hello adresu VIP.
3. Powtórz kroki 1 i 2 dla hello wdrożenia produkcyjnego.
4. Jeśli aktualizacje automatyczne jest w toku, zaczekaj na jej toofinish przed w trakcie toodo hello VIP wymiany.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problem: Wystąpienie roli jest pętli między rozpoczęte, inicjowanie zajęty i zatrzymane
Ten stan może wskazywać na problem z kodem, pakietem lub plikiem konfiguracyjnym aplikacji. W takim przypadku powinno być możliwe toosee hello stan zmiana co kilka minut i hello portalu Azure może wskazywać przypominać **odtwarzanie**, **zajęty**, lub **inicjowanie**. Oznacza to, że jest wystąpiły problemy z aplikacją hello, który może być utrzymywanie wystąpienia roli hello uruchamianie.

Aby uzyskać więcej informacji na temat tootroubleshoot tego problemu, zobacz hello blogu [dane diagnostyczne obliczeniowe PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) i [typowe problemy z tym toorecycle ról Przyczyna](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problem: Moja aplikacja przestała działać
1. W portalu Azure hello kliknij hello wystąpienia roli.
2. W hello **właściwości** okienko hello portalu Azure, należy wziąć pod uwagę następujące warunki tooresolve hello problemu:
   * Jeśli ostatnio zatrzymał wystąpienie roli hello (można sprawdzić wartość hello **liczba przerwań**), można aktualizować hello wdrożenia. Poczekaj toosee, jeśli wystąpienia roli hello wznawia działanie samodzielnie.
   * W przypadku wystąpienia roli hello **zajęty**, określ, czy Twoje toosee kodu aplikacji hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) zdarzenie jest obsługiwane. Może być konieczne tooadd lub Usuń kod obsługujący to zdarzenie.
   * Przejść przez hello danych diagnostycznych i rozwiązywania problemów scenariusze w blogu hello [dane diagnostyczne obliczeniowe PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Jeśli Kosz usługi w chmurze, można zresetować hello właściwości wdrożenia hello skutecznie wymazywanie hello informacje dotyczące hello oryginalnego problemu.
>
>

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej [Rozwiązywanie problemów z artykułów](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.

toolearn jak roli usługi w chmurze tootroubleshoot problemów przy użyciu danych diagnostycznych komputera Azure PaaS, zobacz [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
