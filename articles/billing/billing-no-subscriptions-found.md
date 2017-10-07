---
title: "Subskrypcje aaaNo znaleziono błąd po spróbuj toosign w portalu tooAzure lub Centrum konta platformy Azure | Dokumentacja firmy Microsoft"
description: "Zapewnia hello rozwiązanie problemu, w którym subskrypcji nie znaleziono błąd występuje, gdy Zaloguj się w portalu tooAzure lub Centrum konta platformy Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Nie znaleziono żadnych subskrypcji błąd w portalu Azure lub Centrum konta platformy Azure
Może być pojawi się komunikat o błędzie "Nie można odnaleźć subskrypcji" podczas próby toosign w toohello [portalu Azure](https://portal.azure.com/) lub hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions). Ten artykuł zawiera rozwiązanie tego problemu.

## <a name="symptom"></a>Objaw

Podczas próby toosign w toohello [portalu Azure](https://portal.azure.com/) lub hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions), pojawi się następujący komunikat o błędzie hello: "Nie można odnaleźć subskrypcji".

## <a name="cause"></a>Przyczyna

Ten problem występuje, jeśli konto nie ma wystarczających uprawnień. 

## <a name="solution"></a>Rozwiązanie

Upewnij się, czy logujesz się jako administrator poprawne hello. Administrator konta ma dostęp tylko hello Centrum konta. Administratorzy usługi (SA) i Współadministratorzy (CA) mają tylko toohello uprawnienia dostępu do portalu Azure lub hello klasycznego portalu Azure.

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a>Scenariusz 1: Odebrano komunikat o błędzie w hello [portalu Azure](https://portal.azure.com)

toofix tego problemu:

* Upewnij się, tym hello poprawny katalogu platformy Azure jest zaznaczona, klikając konto w prawym górnym narożniku hello.

  ![Wybierz hello katalogu hello górnego prawego hello portalu Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Jeśli hello bezpośrednio do usługi Azure directory jest zaznaczony, ale nadal hello komunikat o błędzie, [swoje konto jako właściciela](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenariusz 2: Odebrano komunikat o błędzie w hello [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions)

Sprawdź, czy konto użyte hello hello konta administratora. tooverify, który hello administratora konta, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum hello wybierz **subskrypcji**.
3. Wybierz subskrypcję hello mają toocheck, a następnie wybierz **ustawienia**.
4. Wybierz **właściwości**. Witaj administratora konta subskrypcji hello jest wyświetlany w hello **administrator konta** pole.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget szybkie rozwiązanie problemu. 
