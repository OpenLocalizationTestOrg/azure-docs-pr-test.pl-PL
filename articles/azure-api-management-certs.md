---
title: "aaaUpload certyfikat interfejsu API zarządzania platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak athe tooupload interfejs API zarządzania certyfikatu dla hello klasycznego portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Przekaż certyfikat zarządzania interfejsem API zarządzania platformy Azure
Certyfikaty zarządzania Zezwalaj tooauthenticate z hello klasycznego modelu wdrażania dostarczany przez platformę Azure. Wiele programów i narzędzia (np. programu Visual Studio lub hello Azure SDK) należy użyć tych certyfikatów tooautomate Konfiguracja i wdrożenie różnych usług platformy Azure. 

> [!WARNING]
> Ostrożnie! Zezwalaj tych typów certyfikatów, każdy, kto jest uwierzytelniany w usłudze ich toomanage hello subskrypcji skojarzonych z nimi.
>
>

Jeśli chcesz więcej informacji o certyfikatach Azure (takie jak tworzenie certyfikatu z podpisem własnym), zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Można również użyć [usługi Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate kodu klienta dla celów automatyzacji.

## <a name="upload-a-management-certificate"></a>Przekazywanie certyfikatu zarządzania
Po utworzeniu utworzony certyfikat zarządzania, (plik cer z tylko klucz publiczny hello) można przekazać go do portalu hello. Gdy certyfikat hello jest dostępne w portalu hello, każda osoba mająca zgodnego certyfikatu (klucz prywatny) łączenie się za pośrednictwem zasobów hello interfejs API zarządzania i dostęp hello hello skojarzone subskrypcji.

1. Zaloguj się za toohello [portalu Azure](http://portal.azure.com).
2. Kliknij przycisk **więcej usług** na powitania Dolna lista usługi Azure, następnie wybierz **subskrypcje** w hello _ogólne_ grupy usług.

    ![Menu subskrypcji](./media/azure-api-management-certs/subscriptions_menu.png)

3. Upewnij się, tooselect hello poprawną subskrypcję, które mają tooassociate z certyfikatem hello.     
4. Po wybraniu hello poprawną subskrypcję, naciśnij klawisz **certyfikaty zarządzania** w hello _ustawienia_ grupy.

    ![Ustawienia](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Naciśnij klawisz hello **przekazać** przycisku.

    ![Przekaż na stronie certyfikatów](./media/azure-api-management-certs/certificates_page.png)
6. Wypełnianie hello okna dialogowego informacji i naciśnij klawisz **przekazać**.

    ![Ustawienia](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz certyfikat zarządzania skojarzony z subskrypcją (po zainstalowaniu hello dopasowania certyfikatu lokalnie) programowo podłączeniem toohello [klasycznego modelu wdrażania interfejsu API REST](https://msdn.microsoft.com/library/azure/mt420159.aspx) i automatyzacji Witaj różnych zasobów platformy Azure, które są również powiązaną z jego subskrypcją.
