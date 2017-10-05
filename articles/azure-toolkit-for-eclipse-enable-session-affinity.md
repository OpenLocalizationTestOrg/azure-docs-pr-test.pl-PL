---
title: "Włącz koligacji sesji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse"
description: "Dowiedz się, jak włączyć koligacji sesji przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a>Włącz koligacji sesji
W ramach zestawu narzędzi platformy Azure dla programu Eclipse można włączyć koligacji sesji HTTP, lub "trwałe sesje", dla poszczególnych ról. Poniższy obraz przedstawia **równoważenia obciążenia** używane do włączania funkcji koligacji sesji okno dialogowe właściwości:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>Aby włączyć koligacji sesji dla roli użytkownika
1. Kliknij prawym przyciskiem myszy rolę, w obszarze Eksplorator projektów programu Eclipse na, kliknij przycisk **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**.

2. W **właściwości WorkerRole1 Równoważenie obciążenia sieciowego** okna dialogowego:

   a. Sprawdź **koligacji sesji HTTP włączyć (trwałe sesje) dla tej roli.**

   b. Aby uzyskać **wejściowy punkt końcowy do użycia**, wybierz wejściowy punkt końcowy do użycia, na przykład **http (publicznego: 80, private: 8080)**. Aplikacja musi używać tego punktu końcowego, jako jego punkt końcowy HTTP. Można włączyć wiele punktów końcowych dla roli użytkownika, ale można wybrać tylko jeden z nich do obsługi trwałe sesje.

   c. Aplikacja jest ponownie kompilowana.

Po włączeniu, jeśli masz więcej niż jedno wystąpienie roli, pochodzących z określonego klienta żądań HTTP będą nadal obsługiwane przez tego samego wystąpienia roli.

Zestaw narzędzi Eclipse umożliwia to przez zainstalowanie specjalne moduł usług IIS do każdego wystąpienia roli o nazwie Routing żądań aplikacji (ARR). Moduł ARR zmienia trasę żądania HTTP do wystąpienia odpowiedniej roli. Zestaw narzędzi automatycznie skonfiguruje wybranego punktu końcowego, tak aby ruch przychodzący HTTP najpierw jest kierowane do oprogramowania ARR. Zestaw narzędzi również tworzy nowy wewnętrzny punkt końcowy który serwer Java jest skonfigurowany do nasłuchiwania. To punktowi końcowemu używanemu przez moduł ARR do przekierowywania ruchu HTTP do wystąpienia odpowiedniej roli. W ten sposób każde wystąpienie roli we wdrożeniu w wielu wystąpieniach służy jako zwrotny serwer proxy dla wszystkich innych przypadkach włączenie trwałe sesje.

## <a name="notes-about-session-affinity"></a>Uwagi dotyczące koligacji sesji
* Koligacja sesji nie działa w emulatorze obliczeń. Ustawienia mogą być stosowane w emulatorze obliczeń bez zakłócania w procesie kompilacji lub wykonywania emulatora obliczeniowe, ale sama ta funkcja nie działa w ramach emulatora obliczeń.

* Włączenie koligacji sesji spowoduje zwiększenie ilości miejsca na dysku zajmowanego przez wdrożenia na platformie Azure jako dodatkowego oprogramowania zostanie pobrany i zainstalowany w wystąpienia roli, po uruchomieniu usługi w chmurze Azure.

* Czas inicjowania każdej roli będzie trwać dłużej.

* Wewnętrzny punkt końcowy, do działania jako rerouter ruchu, jak wspomniano powyżej, zostaną dodane.


## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse] 

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
