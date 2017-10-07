---
title: "aaaHow Zarządzanie kontami użytkowników w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate lub zaprosić użytkowników w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Jak konta użytkowników toomanage w usłudze Azure API Management
W usłudze API Management Deweloperzy są użytkownikami hello hello interfejsów API, które można udostępnić przy użyciu interfejsu API zarządzania. Ten przewodnik przedstawia toohow toocreate i zaproszenia deweloperzy toouse hello interfejsów API i produktów należy toothem dostępne z wystąpieniem usługi API Management. Uzyskać informacji o programowe zarządzanie kontami użytkowników, zobacz hello [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w hello [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania.

## <a name="create-developer"></a>Tworzenie nowych developer
toocreate nowych deweloperów, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Trwa toohello zarządzanie interfejsami API wydawcy portalu. Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.

![Portal wydawcy][api-management-management-console]

Kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **dodać użytkownika**.

![Utwórz developer][api-management-create-developer]

Wprowadź hello **E-mail**, **hasło**, i **nazwa** hello nowych deweloperów, a następnie kliknij przycisk **zapisać**.

![Utwórz developer][api-management-add-new-user]

Domyślnie developer nowo utworzonego konta są **Active**wraz ze skojarzonymi z hello **deweloperzy** grupy.

![Nowe developer][api-management-new-developer]

Konta dewelopera, które znajdują się w **active** stanu mogą być używane tooaccess wszystkie interfejsy API hello, do którego mają zostać subskrypcji. tooassociate dewelopera hello nowo utworzone przy użyciu dodatkowych grup, zobacz [jak tooassociate grup z deweloperami][How tooassociate groups with developers].

## <a name="invite-developer"></a>Zaprosić dewelopera
tooinvite dewelopera, kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **zaprosić użytkowników**.

![Zaproś developer][api-management-invite-developer]

Wprowadź nazwę i adres e-mail adres hello dewelopera hello, a następnie kliknij przycisk **zaprosić**.

![Zaproś developer][api-management-invite-developer-window]

Zostanie wyświetlony komunikat potwierdzenia, ale Deweloper hello nowo zaproszenie nie ma listy hello do po zaakceptowaniu zaproszenia hello. 

![Zaproś potwierdzenia][api-management-invite-developer-confirmation]

Gdy poproszeni dewelopera toohello developer zostanie wysłana wiadomość e-mail. Ten adres e-mail jest generowana z użyciem szablonu i można dostosowywać. Aby uzyskać więcej informacji, zobacz [Konfigurowanie szablonów wiadomości e-mail][Configure email templates].

Po zaakceptowaniu zaproszenia hello konta hello staje się aktywny.

## <a name="block-developer"></a> Dezaktywuj lub ponownym uaktywnieniem konta dewelopera
Domyślnie są konta dewelopera nowo utworzone lub zaproszonych **Active**. Kliknij konto dewelopera toodeactivate **bloku**. Kliknij konto dewelopera zablokowanych tooreactivate **Aktywuj**. Konto dewelopera zablokowanych nie można uzyskać dostępu do portalu dla deweloperów hello lub zadzwoń wszystkie interfejsy API. toodelete konta użytkownika, kliknij przycisk **usunąć**.

![Blok developer][api-management-new-developer]

## <a name="reset-a-user-password"></a>Resetowanie hasła użytkownika
tooreset hello hasło dla konta użytkownika, kliknij nazwę hello hello konta.

![Resetowanie hasła][api-management-view-developer]

Kliknij przycisk **resetowania hasła** toosend łącze toohello użytkownika tooreset swoje hasło.

![Resetowanie hasła][api-management-reset-password]

tooprogrammatically pracy z kontami użytkowników, zobacz hello [jednostki użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx) dokumentacji w hello [interfejsu API REST zarządzania](https://msdn.microsoft.com/library/azure/dn776326.aspx) odwołania. tooreset użytkownika konta hasło tooa określoną wartość, można użyć hello [zaktualizowania użytkownika](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operację i określ hello wymagane hasło.

## <a name="pending-verification"></a>Oczekujące weryfikacji
![Oczekujące weryfikacji][api-management-pending-verification]

## <a name="next-steps"> </a>Następne kroki
Po utworzeniu konta dewelopera, można ją skojarzyć z rolami i subskrybowania go tooproducts i interfejsów API. Aby uzyskać więcej informacji, zobacz [jak toocreate i używania grup][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
