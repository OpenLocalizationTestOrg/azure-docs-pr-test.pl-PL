---
title: "Usługi BizTalk aaaTroubleshoot przy użyciu dzienników operacji | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z usługi BizTalk Services przy użyciu dzienników operacji. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Usługi BizTalk Services: Rozwiązywanie problemów przy użyciu dzienników operacji

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Co to są dzienniki operacji hello
Dzienniki operacji to funkcja usługi zarządzania dostępnych w hello klasycznego portalu Azure, umożliwiający tooview historycznych dzienniki operacji wykonywanych na usługami Azure, takich jak usługi BizTalk. Dzięki temu dane historyczne tooview toomanagement operacje w ramach subskrypcji usługi BizTalk, nawet sprzed 180 dni.

> [!NOTE]
> Ta funkcja przechwytuje tylko dzienniki dla operacji zarządzania na usługi BizTalk Services, takich jak uruchomienia usługi hello, kopie włączone, i tak dalej. Takie operacje są śledzone niezależnie od tego, czy są wykonywane z hello klasycznego portalu Azure lub przy użyciu hello [interfejsów API REST usługi BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Aby uzyskać pełną listę działań, które są śledzone za pomocą usług zarządzania, zobacz [operacji śledzone za pomocą zarządzania usług Azure](#bizops).<br/><br/>
> To nie przechwytywać hello dzienniki dla działań powiązanych tooBizTalk środowiska uruchomieniowego usługi (na przykład komunikatów przetwarzanych przez mostków itd.). tooview te dzienniki, użyj hello widoku śledzenia z portalu usługi BizTalk Services hello. Aby uzyskać więcej informacji, zobacz [komunikatów śledzenia](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Wyświetl dzienniki operacji usługi BizTalk
1. Hello klasycznego portalu Azure, wybierz **usług zarządzania**, a następnie wybierz hello **dzienniki operacji** kartę.
2. Można filtrować hello dzienniki na podstawie różnych parametrów, takich jak subskrypcji, zakres dat, typ usługi (np. usługi BizTalk Services), nazwę usługi lub stan operacji hello (Powodzenie, niepowodzenie).
3. Wybierz hello znacznikiem wyboru tooview hello wyfiltrowanej listy. Witaj poniższy obraz przedstawia tootestbiztalkservice powiązanych działań: ![Sprawdź dzienniki operacji][ViewLogs] 
4. tooview więcej informacji na temat określonej operacji, zaznacz wiersz hello, a następnie kliknij przycisk **szczegóły** hello pasku zadań u dołu hello.

## <a name="bizops"></a>Operacje śledzone za pomocą usług zarządzania platformy Azure
Witaj Poniższa tabela zawiera listę operacji hello, które są śledzone za pomocą usług zarządzania hello Azure:

| Nazwa operacji | Zadanie |
| --- | --- |
| CreateBizTalkService |Operacja toocreate nową usługę BizTalk |
| DeleteBizTalkService |Operacja toodelete usługi BizTalk |
| RestartBizTalkService |Operacja toorestart usługi BizTalk |
| StartBizTalkService |Operacja toostart usługi BizTalk |
| StopBizTalkService |Operacja toostop usługi BizTalk |
| DisableBizTalkService |Operacja toodisable usługi BizTalk |
| EnableBizTalkService |Operacja tooenable usługi BizTalk |
| BackupBizTalkService |Operacja tooback usługi BizTalk |
| RestoreBizTalkService |Operacja toorestore usługi BizTalk z określonej kopii zapasowej |
| SuspendBizTalkService |Operacja toosuspend usługi BizTalk |
| ResumeBizTalkService |Operacja tooresume usługi BizTalk |
| ScaleBizTalkService |Tooscale operacji usługi BizTalk w górę lub w dół |
| ConfigUpdateBizTalkService |Operacja tooupdate hello konfiguracji usługi BizTalk |
| ServiceUpdateBizTalkService |Operacja tooupgrade lub starszą wersję usługi BizTalk tooa innej wersji |
| PurgeBackupBizTalkService |Kopie zapasowe toopurge operacji hello usługi BizTalk poza okresem przechowywania hello |

## <a name="see-also"></a>Zobacz też
* [Usługi BizTalk kopii zapasowej](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Przywracanie z kopii zapasowej usługi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

