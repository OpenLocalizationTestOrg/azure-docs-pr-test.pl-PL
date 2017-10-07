---
title: "aaaAzure punktów końcowych usług"
description: "Opisuje ustawienia punktu końcowego usługi Azure hello w hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Punktami końcowymi usług Azure
Punktami końcowymi usług Azure określają, czy aplikacja jest wdrożony tooand zarządza hello globalne platformy Azure, Azure obsługiwany przez 21Vianet w Chinach lub prywatnej platformy Azure. Witaj **punktów końcowych usługi** okno dialogowe pozwala toospecify, który ma toouse punkty końcowe usługi. tooopen hello **punktów końcowych usługi** okna dialogowego, w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure**, a następnie kliknij przycisk **Punkty końcowe usługi**. Ustawienie hello **ustawić Active** Określa, w których usługa Azure punktów końcowych, które będą używane dla hello Azure projektów w bieżącym obszarze roboczym.

Witaj poniżej pokazano hello **punktów końcowych usługi** okna dialogowego.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>punkty końcowe usługi hello tooset
W hello **punktów końcowych usługi** okno dialogowe, wykonaj jedną z hello następujące akcje:

* Jeśli chcesz, aby toouse hello globalne platformy Azure, z hello **ustawić Active** listy rozwijanej wybierz **windowsazure.com** i kliknij przycisk **OK**.

* Jeśli chcesz, aby toouse Azure obsługiwany przez 21Vianet w Chinach, z hello **ustawić Active** listy rozwijanej wybierz **windowsazure.cn (Chiny)** i kliknij przycisk **OK**.

* Jeśli chcesz, aby toouse prywatnej platformy Azure:

  1. Kliknij pozycję **Edytuj**.

  2. Otwiera okno dialogowe informujące, że hello **punktów końcowych usługi** okno dialogowe zostanie zamknięte i hello preferencji ustawia plik zostanie otwarty. Kliknij przycisk **OK**.

  3. W pliku preferencesets.xml hello, Utwórz nową `preferenceset` elementu. Dla tego nowego elementu tworzenia `name`, `blob`, `management`, `portalURL` i `publishsettings` atrybutów, a następnie dodaj wartości dla nich odpowiadające tooyour prywatnej platformy Azure. Możesz użyć wartości hello podany dla istniejących hello `preferenceset` elementów jako szablon. **Uwaga**: hello wartość używana dla hello `blob` atrybutu musi zawierać tekst hello "blob" w adresie URL hello.

  4. Zapisz i zamknij preferencesets.xml.

  5. Otwórz ponownie hello **punktów końcowych usługi** okna dialogowego.

  6. Z hello **ustawić Active** listy rozwijanej wybierz hello aktywny ustawić utworzone, a następnie kliknij przycisk **OK**.

  7. Po utworzeniu prywatnej platformy Azure `preferenceset` elementu, można zmienić tooit przypisanych wartości hello klikając hello **Edytuj** przycisku na powitania **punktu końcowego usługi** okna dialogowego. Można również tworzyć wiele prywatnych platformy Azure `preferenceset` elementy, jeśli jest to wymagane.

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
