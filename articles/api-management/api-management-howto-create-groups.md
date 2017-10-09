---
title: "przy użyciu grup w usłudze Azure API Management konta dewelopera aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak kont przy użyciu narzędzia Projektant toomanage grup w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Jak developer toomanage grup toocreate i używania kont w usłudze Azure API Management
W usłudze API Management grupy są używane toomanage widoczność hello toodevelopers produktów. Produkty są pierwszy dokonano toogroups widoczne, a następnie deweloperów w tych grupach można wyświetlić i toohello produktów, które są skojarzone z grupami hello subskrypcji. 

Zarządzanie interfejsami API ma hello następujące grupy systemu niezmienialny.

* **Administratorzy** — do tej grupy należą administratorzy subskrypcji platformy Azure. Administratorzy Zarządzanie wystąpieniami usługi Zarządzanie interfejsami API, tworzenie hello interfejsów API, operacje i produktów, które są używane przez deweloperów.
* **Deweloperzy** — do tej grupy należą uwierzytelnieni użytkownicy portalu dla deweloperów. Deweloperzy są hello klientów, którzy tworzyć aplikacje przy użyciu swoje interfejsy API. Deweloperzy otrzymują dostęp do portalu dla deweloperów toohello i tworzenia aplikacji wywołujących hello operacje interfejsu API.
* **Goście** -nieuwierzytelnionych użytkowników portalu deweloperów, na przykład potencjalni klienci odwiedzający hello portalu dla deweloperów programu spadek wystąpienia interfejsu API zarządzania do tej grupy. Może zostać przydzielony niektórych dostęp tylko do odczytu, takich jak tooview możliwości hello interfejsów API, ale nie połączeń telefonicznych z nimi.

Dodanie toothese systemu grup, Administratorzy mogą tworzyć niestandardowe grupy lub [korzystać z zewnętrznej grupy w skojarzonych dzierżaw usługi Azure Active Directory][leverage external groups in associated Azure Active Directory tenants]. Niestandardowe zewnętrznych grup można używać razem grup systemu w zapewniając wgląd w deweloperzy i uzyskują dostęp do tooAPI produktów. Na przykład można utworzyć jedną grupę niestandardowych dla deweloperów powiązane z konkretną organizacji partnera i zezwolić im dostępu toohello interfejsy API z produktu, zawierający tylko odpowiednich interfejsów API. Użytkownik może należeć do więcej niż jednej grupy.

W tym przewodniku pokazano, jak Administratorzy wystąpienia interfejsu API zarządzania mogą dodawać nowe grupy i skojarzyć je z produktami i deweloperów.

> [!NOTE]
> Ponadto toocreating grup i zarządzanie nimi w portalu wydawcy hello, możesz utworzyć i zarządzanie grupami za pomocą interfejsu API REST zarządzania interfejsu API hello [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.
> 
> 

## <a name="create-group"></a>Utwórz grupę
toocreate nową grupę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Kliknij przycisk **grup** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Dodaj grupę**.

![Dodaj nową grupę][api-management-add-group]

Wprowadź unikatową nazwę grupy hello i opcjonalny opis, a następnie kliknij przycisk **zapisać**.

![Dodaj nową grupę][api-management-add-group-window]

Witaj Nowa grupa zostanie wyświetlona w hello grup kartę tooedit hello **nazwa** lub **opis** hello grupy, kliknij nazwę hello hello grupy na liście hello. toodelete hello grupy, kliknij przycisk **usunąć**.

![Grupy dodane][api-management-new-group]

Teraz, gdy hello zostanie utworzona grupa, może być skojarzony z produktami i deweloperów.

## <a name="associate-group-product"></a>Skojarzyć grupy z produktem
tooassociate grupy z produktem, kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij hello nazwa produktu żądaną hello.

![Ustaw widoczność][api-management-add-group-to-product]

Wybierz hello **widoczność** karcie tooadd i usuwanie grup oraz tooview hello bieżących grup hello produktu. tooadd lub Usuń grupy, zaznacz lub usuń zaznaczenie pola wyboru hello, dla żądanego hello grupy i kliknij przycisk **zapisać**.

![Ustaw widoczność][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd grupy usługi Azure Active Directory, zobacz [jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory w usłudze Azure API Management](api-management-howto-aad.md).
> 
> grupy tooconfigure z hello **widoczność** produktu, kliknij pozycję **Zarządzaj grupami**.
> 
> 

Jeśli produkt jest skojarzona z grupą, deweloperzy w tej grupie można wyświetlać i subskrybowania toohello produktu.

## <a name="associate-group-developer"></a>Kojarzyć grup z deweloperami
grupy tooassociate z deweloperami, kliknij przycisk **użytkowników** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie hello pole obok hello deweloperzy mają tooassociate z grupy.

![Dodaj developer toogroup][api-management-add-group-to-developer]

Po hello pożądane, deweloperzy są zaznaczone, kliknij odpowiednią grupę hello w hello **dodać tooGroup** listy rozwijanej. Deweloperzy mogą zostać usunięte z grup za pomocą hello **Usuń z grupy** listy rozwijanej. 

![Deweloperzy][api-management-add-group-to-developer-saved]

Po dodaniu skojarzenia hello między hello deweloperów i hello grupy można wyświetlić ją w hello **użytkowników** kartę.

## <a name="next-steps"> </a>Następne kroki
* Po dodaniu dewelopera tooa grupy mogą wyświetlać i subskrybować produktów toohello skojarzonych z tej grupy. Aby uzyskać więcej informacji, zobacz [jak tworzyć i publikować w usłudze Azure API Management produktu][How create and publish a product in Azure API Management],
* Ponadto toocreating grup i zarządzanie nimi w portalu wydawcy hello, możesz utworzyć i zarządzanie grupami za pomocą interfejsu API REST zarządzania interfejsu API hello [grupy](https://msdn.microsoft.com/library/azure/dn776329.aspx) jednostki.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
