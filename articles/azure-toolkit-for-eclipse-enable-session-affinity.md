---
title: "za pomocą koligacji sesji aaaEnable hello zestawu narzędzi platformy Azure dla programu Eclipse"
description: "Dowiedz się, jak za pomocą koligacji sesji tooenable hello zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Włącz koligacji sesji
W ramach hello zestawu narzędzi platformy Azure dla programu Eclipse można włączyć koligacji sesji HTTP, lub "trwałe sesje", dla poszczególnych ról. Witaj poniższy obraz przedstawia hello **równoważenia obciążenia** funkcji koligacji sesji hello tooenable użyć okna dialogowego właściwości:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>tooenable koligacji sesji dla roli użytkownika
1. Kliknij prawym przyciskiem myszy rolę hello w obszarze Eksplorator projektów programu Eclipse na, kliknij przycisk **Azure**, a następnie kliknij przycisk **równoważenia obciążenia**.

2. W hello **właściwości WorkerRole1 Równoważenie obciążenia sieciowego** okna dialogowego:

   a. Sprawdź **koligacji sesji HTTP włączyć (trwałe sesje) dla tej roli.**

   b. Dla **wejściowy punkt końcowy toouse**, na przykład wybierz toouse wejściowy punkt końcowy **http (publicznego: 80, private: 8080)**. Aplikacja musi używać tego punktu końcowego, jako jego punkt końcowy HTTP. Można włączyć wiele punktów końcowych dla roli użytkownika, ale można wybrać tylko jedną z nich toosupport trwałe sesje.

   c. Aplikacja jest ponownie kompilowana.

Po włączeniu, jeśli masz więcej niż jedno wystąpienie roli, pochodzących z określonego klienta żądań HTTP będą nadal obsługiwane przez hello takie same wystąpienia roli.

Hello Eclipse Toolkit umożliwia to przez zainstalowanie specjalne moduł usług IIS do każdego wystąpienia roli o nazwie Routing żądań aplikacji (ARR). Moduł ARR zmienia trasę wystąpienia odpowiedniej roli toohello żądania HTTP. zestaw narzędzi Hello automatycznie skonfiguruje hello wybrany punkt końcowy tak, aby ruch przychodzący HTTP hello pierwszy routingiem toohello ARR oprogramowania. Hello toolkit tworzy nowy wewnętrzny punkt końcowy, który serwer Java jest skonfigurowany toolisten do. To jest punkt końcowy hello używane przez wystąpienie odpowiedniej roli toohello ruch HTTP ARR tooreroute hello. W ten sposób każde wystąpienie roli we wdrożeniu w wielu wystąpieniach służy jako zwrotny serwer proxy dla wszystkich hello innych przypadkach włączenie trwałe sesje.

## <a name="notes-about-session-affinity"></a>Uwagi dotyczące koligacji sesji
* Koligacji sesji nie działa w emulatorze obliczeń hello. Ustawienia Hello mogą być stosowane w emulatorze obliczeń hello bez zakłócania w procesie kompilacji lub wykonywania emulatora obliczeniowe, ale funkcja hello nie działa w ramach hello emulatora obliczeń.

* Włączenie koligacji sesji spowoduje zwiększenie hello ilość miejsca na dysku zajmowanego przez wdrożenia na platformie Azure jako dodatkowego oprogramowania zostanie pobrany i zainstalowany w wystąpienia roli, po uruchomieniu usługi w hello chmury Azure.

* tooinitialize czasu Hello każdej roli będzie trwać dłużej.

* Wewnętrzny punkt końcowy toofunction jako rerouter ruchu, jak wspomniano powyżej, zostaną dodane.


## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
