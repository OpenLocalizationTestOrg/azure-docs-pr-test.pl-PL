---
title: "kolekcje w chmurze usługi RemoteApp aaaTroubleshoot — tworzenie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak błędy tworzenia kolekcji w chmurze tootroubleshoot programów RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>Rozwiązywanie problemów z kolekcji usługi RemoteApp tworzenia w chmurze
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Jeśli występują problemy z tworzeniem kolekcji w chmurze, zapoznaj się z następujących informacji hello.

## <a name="your-image-is-invalid"></a>Obraz jest nieprawidłowy
Jeśli zostanie wyświetlony komunikat, takie jak "GoldImageInvalid" podczas oczekiwania dla usługi Azure tooprovision kolekcji, oznacza to, że obraz szablonu nie spełnia wymagań hello [określone wymagania dotyczące obrazu](remoteapp-imagereqs.md). Tak, przejdź do odczytu tych [wymagania](remoteapp-imagereqs.md), Usuń obraz i spróbuj toocreate kolekcji ponownie.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Typowe błędy widoczne w portalu zarządzania Azure hello
    DNS server could not be reached
    ProvisioningTimeout

Kolekcje w chmurze często błędów podczas tworzenia z powodu możesz korzystają z niestandardowych obrazów.  Jeśli używasz kolekcji hello toocreate niestandardowego obrazu wystąpiła jedna z hello powyżej błędy, sprawdź, czy hello następujące czynności:

* Upewnij się, że obrazu niestandardowego hello przesłanych spełnia wymagania dotyczące obrazu.
* W większości przypadków hello powszechny problem jest ten obraz powitania nie została prawidłowo przetworzonej przez program Sysprep.  
* Sprawdź obraz powitania można uruchomić w ramach funkcji Hyper-V lub spróbuj utworzyć maszyn wirtualnych IAAS bezpośrednio w Twojej subskrypcji platformy Azure przy użyciu obrazu hello. Jeśli hello maszyny Wirtualnej nie powiedzie się tooboot i nie start, a następnie zwykle oznacza to, że danego hello niestandardowego obrazu nie został poprawnie przygotowany.  Sprawdź, czy hello niestandardowy obraz został utworzony po hello jak toocreate szablonu niestandardowego obrazu usługi RemoteApp

Jeśli korzystasz z jednego z obrazów Microsoft hello uwzględnionych w subskrypcji, spróbuj ponownie toocreate hello kolekcji. Jeśli hello problem będzie się powtarzać, skontaktuj się pomocy technicznej firmy Microsoft.

    PlatformImageTrialModeOnly

Jeśli zostanie wyświetlony błąd ten zwykle oznacza to, który został uaktualniony tooa płatne konto, lecz próbujesz toouse obrazu firmę Microsoft, który jest prawidłowy tylko w trakcie hello trybu wersji próbnej usługi hello. W takim przypadku spróbuj toocreate ponownie kolekcji chmury, ale można się toospecify hello prawidłowy obraz.

