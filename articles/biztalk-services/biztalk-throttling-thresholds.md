---
title: "aaaLearn dotyczące ograniczenia przepustowości w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat ograniczania progów i wynikowa zachowanie w czasie wykonywania dla usługi BizTalk Services. Ograniczanie opiera się na użycie pamięci i liczbę komunikatów. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Usługi BizTalk Azure implementuje ograniczania usługi na podstawie dwóch warunków: pamięci użycia i hello liczbę jednoczesnych przetwarzania komunikatów. W tym temacie wymieniono hello ograniczania progów i opisano hello zachowania w czasie wykonywania, jeśli dławienia stan występuje.

## <a name="throttling-thresholds"></a>Progi ograniczania przepustowości
Witaj w następującej tabeli przedstawiono hello progi i ograniczania przepustowości źródła:

|  | Opis | Dolna wartość progowa | Górny próg |
| --- | --- | --- | --- |
| Memory (Pamięć) |% całkowitej systemu pamięci dostępne/PageFileBytes. <p><p>Całkowita liczba dostępnych PageFileBytes wynosi około 2 razy hello pamięci RAM hello systemu. |60% |70% |
| Przetwarzanie komunikatów |Liczba komunikatów przetwarzania jednocześnie |40 * liczba rdzeni |100 * Liczba rdzeni |

Po osiągnięciu progu wysokiego toothrottle zostaną uruchomione usługi BizTalk Azure. Ograniczanie zatrzymuje po osiągnięciu progu dolnego hello. Na przykład usługi używa 65% pamięci systemowej. W takiej sytuacji usługa hello nie ograniczenie przepustowości. Usługa uruchamia przy użyciu 70% pamięci systemowej. W takiej sytuacji usługa hello ogranicza i kontynuuje toothrottle, dopóki usługa hello używa pamięci systemowej (progu dolnego) 60%.

Usługi BizTalk Azure śledzi hello ograniczania stanu (normalnym stanie a stanu ograniczeniem przepustowości) i hello ograniczania czas trwania.

## <a name="runtime-behavior"></a>Zachowania w czasie wykonywania
Podczas usług BizTalk Azure przechodzi do stanu ograniczania przepustowości, występuje hello następujące czynności:

* Ograniczenie jest dla każdego wystąpienia roli. Na przykład:<br/>
  RoleInstanceA jest ograniczanie. Nie jest ograniczanie RoleInstanceB. W takim przypadku komunikatów w RoleInstanceB są przetwarzane zgodnie z oczekiwaniami. Komunikaty w RoleInstanceA zostaną odrzucone i zakończyć się niepowodzeniem z hello następujący błąd:<br/><br/>
  **Serwer jest zajęty. Spróbuj ponownie.**<br/><br/>
* Wszystkie źródła ściągania nie sondowania lub pobierania wiadomości. Na przykład:<br/>
  Potok ściąga komunikatów ze źródła zewnętrznego FTP. Pobiera wystąpienia roli Hello czynności ściągania hello stan ograniczania przepustowości. W takiej sytuacji potoku hello zatrzymuje pobieranie dodatkowych komunikatów, do momentu wystąpienia roli hello zatrzymuje ograniczania.
* Odpowiedź jest wysyłana toohello klienta, więc powitania klienta można ponownie przesłać wiadomość hello.
* Musisz poczekać, aż ograniczania hello zostanie rozwiązany. W szczególności należy poczekać, aż do osiągnięcia progu dolnego hello.

## <a name="important-notes"></a>Ważne uwagi
* Nie można wyłączyć ograniczenia przepustowości.
* Nie można zmodyfikować ograniczania progów.
* Ograniczanie zaimplementowano całego systemu.
* powitania serwera bazy danych SQL Azure ma również wbudowane ograniczenia przepustowości.

## <a name="additional-azure-biztalk-services-topics"></a>Dodatkowe tematy Azure BizTalk Services
* [Instalowanie hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Samouczki: Usługi Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Usługi Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Zobacz też
* [Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

