---
title: "aaaTasks dozwolone w różnych stanów oraz Stany w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Witaj w inny stan MABS dozwolone akcje/operations: Zatrzymaj, start, uruchom ponownie, wstrzymać, wznowić, Usuń, skalowania, aktualizacji konfiguracji i tworzenia kopii zapasowej"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Co można i nie można wykonać przy użyciu hello stan usługi BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

W zależności od hello bieżący stan hello usługi BizTalk ma działań, które mogą lub nie można wykonać na powitania usługi BizTalk.

Na przykład można udostępnić nową usługę BizTalk w hello klasycznego portalu Azure. Po pomyślnym ukończeniu, hello usługi BizTalk jest `active` stanu. W stanie aktywnym hello Zatrzymaj, Wstrzymaj, a usunąć hello usługi BizTalk. Jeśli Zatrzymaj usługę BizTalk hello i Zatrzymaj zakończy się niepowodzeniem, a następnie hello usługi BizTalk przechodzi tooa `StopFailed` stanu. W hello `StopFailed` stanu, możesz ponownie uruchomić usługę BizTalk hello. Jeśli spróbujesz operację, która nie jest dozwolona, takich jak wznowieniu występuje hello następujący błąd:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Możliwe stany hello widoku

Witaj poniższych tabelach operacje hello listy lub akcje, które można wykonać po hello usługi BizTalk w określonym stanie. ✔ oznacza, że operacja hello jest dozwolona w tym stanie. Pusty wpis oznacza, że nie można wykonać operacji hello znajduje się w tym stanie.

| Stan usługi | Uruchamianie | Stop | Ponowne uruchamianie | Wstrzymaj | Resume | Usuwanie | Skalowanie | Aktualizacja <br/> Konfiguracja | Tworzenie kopii zapasowych |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Aktywne |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Disabled (Wyłączony) |  |  |  |  |  | ✔ | |  |  | 
| Zawieszone |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Zatrzymane | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Aktualizacja usługi nie powiodło się |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Zobacz też
* [Utwórz usługę BizTalk przy użyciu hello klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Co można zrobić w kartach pulpitu nawigacyjnego, monitor i skalowania hello usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Pobierz hello Developer, podstawowa, standardowa i Premium Edition w usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Jak tooback zapasowych i przywracania usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Ograniczanie wyjaśniono w usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Pobrać hello usługi Service Bus i kontroli dostępu wystawcy nazwy i wystawców wartości klucza dla usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)

