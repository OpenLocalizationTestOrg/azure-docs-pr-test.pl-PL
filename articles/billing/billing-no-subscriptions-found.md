---
title: "Nie znaleziono żadnych subskrypcji błąd podczas próby Zaloguj się do portalu Azure lub Centrum konta platformy Azure | Dokumentacja firmy Microsoft"
description: "Zapewnia rozwiązanie problemu, w którym subskrypcji nie znaleziono błąd występuje, gdy Zaloguj się do portalu Azure lub Centrum konta platformy Azure."
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
ms.openlocfilehash: a4ce9b219c05f8469379c2aac5241fcfffd16033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a>Nie znaleziono żadnych subskrypcji błąd w portalu Azure lub Centrum konta platformy Azure
Może być pojawi się komunikat o błędzie "Nie można odnaleźć subskrypcji" podczas próby Zaloguj się do [portalu Azure](https://portal.azure.com/) lub [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions). Ten artykuł zawiera rozwiązanie tego problemu.

## <a name="symptom"></a>Objaw

Podczas próby Zaloguj się do [portalu Azure](https://portal.azure.com/) lub [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions), pojawi się następujący komunikat o błędzie: "Nie można odnaleźć subskrypcji".

## <a name="cause"></a>Przyczyna

Ten problem występuje, jeśli konto nie ma wystarczających uprawnień. 

## <a name="solution"></a>Rozwiązanie

Upewnij się zalogować jako administrator poprawne. Administrator konta ma dostęp do Centrum konta. Administratorzy usługi (SA) i Współadministratorzy urzędu certyfikacji ma uprawnienia dostępu tylko do portalu Azure lub klasycznego portalu Azure.

### <a name="scenario-1-error-message-is-received-in-the-azure-portalhttpsportalazurecom"></a>Scenariusz 1: Odebrano komunikat o błędzie w [portalu Azure](https://portal.azure.com)

Aby rozwiązać ten problem:

* Upewnij się, że wybrano poprawny katalog platformy Azure, klikając konto u góry po prawej.

  ![Wybierz katalog u góry po prawej z portalu Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* Jeśli wybrano katalog prawo platformy Azure, ale nadal otrzymywać komunikat o błędzie [swoje konto jako właściciela](billing-add-change-azure-subscription-administrator.md).

### <a name="scenario-2-error-message-is-received-in-the-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a>Scenariusz 2: Odebrano komunikat o błędzie w [Centrum konta platformy Azure](https://account.windowsazure.com/Subscriptions)

Sprawdź, czy konto używane jest konto administratora. Aby sprawdzić, który jest administratorem konta, wykonaj następujące kroki:

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. W menu Centrum wybierz **subskrypcji**.
3. Wybierz subskrypcję, którą chcesz sprawdzić, a następnie wybierz **ustawienia**.
4. Wybierz **właściwości**. Administratora konta subskrypcji jest wyświetlany w **administrator konta** pole.

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) uzyskać szybkie rozwiązanie problemu. 
