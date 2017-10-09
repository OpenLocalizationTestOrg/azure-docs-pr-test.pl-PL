---
title: "aaaAzure usługi aplikacji i jej wpływ na istniejące usługi platformy Azure"
description: "Wyjaśniono, jak hello nowej usłudze Azure App Service i jej funkcji wpływ na istniejące usługi na platformie Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Usługa Azure App Service i istniejące usługi Azure
W tym artykule omówiono tooexisting zmiany hello Azure usługi jako część toobring zmiany hello razem kilka usług platformy Azure do [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/), zintegrowane nową ofertę.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Omówienie
[Usługa aplikacji Azure](https://azure.microsoft.com/services/app-service/) to usługa w chmurze nowych i unikatowych, który umożliwia deweloperom toocreate w sieci web i aplikacji mobilnych dla dowolnej platformy i każdego urządzenia. Usługi aplikacji jest toostreamline zintegrowane rozwiązanie przeznaczone powtarzane funkcji kodowania, zintegrować z przedsiębiorstwa i systemy SaaS i automatyzować procesy biznesowe spełniając wymagania użytkownika dotyczące bezpieczeństwa, niezawodności i skalowalności.

Usługi aplikacji, połączono powitania po Azure istniejących usług - [witryn sieci Web](https://azure.microsoft.com/services/websites/), [usług Mobile Services](https://azure.microsoft.com/services/mobile-services/), i [usługi Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) w pojedynczy połączone usługi, podczas Dodawanie nowe możliwości.  Usługi aplikacji umożliwia hello toohost następujące typy aplikacji:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

Witaj poniższej tabeli opisano sposób istniejących Azure tooApp typu usługi i hello aplikacji dostępne w nim mapy usług.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Istniejące usługi platformy Azure</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">Co zmieniono</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Azure Websites</td>
<td align="left">Web Apps</td>
<td align="left"><li>Dla witryny sieci Web Azure App Service jest ograniczone toochanging hello nazwa witryny sieci Web tooWeb aplikacji.
<p><li>Wszystkie wystąpienia istniejących witryn sieci Web są teraz aplikacje sieci Web w usłudze App Service.</p>
<p><li>Dostęp można uzyskać istniejących witryn sieci Web za pośrednictwem hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, gdzie można znaleźć wszystkich istniejących lokacji w obszarze <em>aplikacje sieci Web</em>.</p>
<p><li><em>Plan hostingu w sieci Web</em> jest teraz <em>planu usługi App Service</em>. <em>Planu usługi App Service</em> może obsługiwać dowolnego typu aplikacji usługi App Service, takich jak aplikacje sieci Web, mobilnych, logiki lub interfejsu API.</p>
<p><li>Aplikacje sieci Web usługi aplikacji platformy Azure jest ogólnie dostępności.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Dowiedz się więcej o aplikacjach sieci Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Services</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Usługi Mobile Services nadal dostępna jako autonomiczna usługa toobe i pozostają w pełni obsługiwane.</p>
<p><li>Aplikacje mobilne nie jest typem aplikacji w usłudze App Service, która integruje wszystkie funkcje hello usług Mobile Services i inne.</p>
<p><li>Łatwo jest zbyt<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migracji z usług Mobile Services tooMobile aplikacji</a>.</p>
<p><li>W ramach usługi App Service Mobile Apps pobrać nowe możliwości poza usługi mobilne, takie jak integracji z lokalnymi i systemy SaaS przemieszczania miejsc, zadań Webjob, opcje lepiej skalowania i.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Dowiedz się więcej o Mobile Apps</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>Aplikacje interfejsu API jest nowy typ aplikacji w usłudze App Service, która umożliwia łatwe tworzenie i korzystanie z interfejsów API w chmurze hello.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Dowiedz się więcej o aplikacjach interfejsu API</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Logic Apps jest nowy typ aplikacji w usłudze App Service pozwala łatwo automatyzować procesy biznesowe.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Dowiedz się więcej o aplikacjach Logic Apps</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Usługa Azure BizTalk Services</td>
<td align="left">Aplikacje interfejsu API BizTalk</td>
<td align="left">
<li><p>Usługi BizTalk Services nadal dostępna jako autonomiczna usługa toobe i pozostają w pełni obsługiwane.</p>
<li><p>Wszystkie hello możliwości usługi BizTalk Services są zintegrowane z usługi aplikacji jako aplikacji interfejsu API umożliwienie użytkownikom tooperform enterprise integracji aplikacji i scenariusze B2B integracji ze wszystkimi typami aplikacji hello w usłudze App Service.</p>
<li><p>Dzięki aplikacjom logiki można teraz automatyzować procesy biznesowe, za pomocą visual Projektowanie przepływów pracy toocreate środowisko.</p></td>
</tr>
</tbody>
</table>

toolearn więcej, odwiedź stronę [dokumentacji usługi aplikacji](https://azure.microsoft.com/documentation/services/app-service/).

