---
title: "aaaAzure aplikacji usługi Active Directory i obiektów nazwy głównej usługi | Dokumentacja firmy Microsoft"
description: "Omówienie hello relacja między aplikacją i obiekty główne usługi w usłudze Azure Active Directory"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Aplikacji i usług obiektów principal w usłudze Azure Active Directory (Azure AD)
Czasami hello znaczenie hello termin "aplikacja" może być błędnie interpretowane, gdy są używane w kontekście hello Azure AD. Witaj celem tego artykułu jest toomake go jaśniejszy przez wyjaśnienie koncepcyjne i konkretnych aspektów integracji aplikacji usługi Azure AD, z ilustrację rejestracji i zgody na [wielodostępnych aplikacji](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Omówienie
Aplikacja jest zintegrowana z usługą Azure AD implikacje wykracza poza hello oprogramowania proporcji. "Aplikacja" jest często używany jako termin pojęciach, odwoływanie toonot tylko hello hello aplikacji, ale również jego rejestracji w usłudze Azure AD i roli w uwierzytelniania/autoryzacji "konwersacji" w czasie wykonywania. Zgodnie z definicją aplikacji może działać w [klienta](active-directory-dev-glossary.md#client-application) roli (Korzystanie z zasobów), [serwer zasobów](active-directory-dev-glossary.md#resource-server) roli (uwidaczniającą tooclients interfejsów API) i/lub nawet. Protokół konwersacji Hello jest definiowana za pomocą [przepływ udzielania autoryzacji OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), dzięki czemu tooaccess/ochrona powitalnych klienta/zasobów danych zasobu odpowiednio. Teraz przejdźmy poziom głębiej i zobacz, jak model aplikacji hello Azure AD reprezentuje aplikacji w czasie projektowania i w czasie wykonywania. 

## <a name="application-registration"></a>Rejestracja aplikacji
Podczas rejestrowania aplikacji usługi Azure AD w hello [portalu Azure][AZURE-Portal], dwa obiekty są tworzone w dzierżawie usługi Azure AD: obiekt aplikacji, a obiekt główny usługi.

#### <a name="application-object"></a>Obiekt aplikacji
Aplikację usługi Azure AD jest definiowany przez jego jedno i tylko obiekt aplikacji, który znajduje się w dzierżawie usługi Azure AD hello rejestracji aplikacji hello, znany jako aplikacji hello dzierżawy "home". Hello Azure AD Graph [jednostek aplikacji] [ AAD-Graph-App-Entity] definiuje hello schemat dla właściwości obiektu aplikacji. 

#### <a name="service-principal-object"></a>Obiekt główny usługi
Obiekt główny usługi Hello definiuje hello zasady i uprawnienia do stosowania w określonym dzierżawcy, dostarczanie hello podstawę dla aplikacji hello toorepresent głównej zabezpieczeń w czasie wykonywania. Hello Azure AD Graph [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity] definiuje hello schemat dla właściwości obiektu główną usługi. 

#### <a name="application-and-service-principal-relationship"></a>Aplikacji i ich relacji głównej usługi
Należy wziąć pod uwagę obiektu aplikacji hello jako hello *globalne* reprezentację aplikacji do użycia we wszystkich dzierżaw i nazwy głównej usługi hello jako hello *lokalnego* reprezentacja do użycia w określonej Dzierżawca. Witaj obiektu aplikacji stanowi hello szablonu, z których typowe i domyślne właściwości są *pochodnych* do użytku przy tworzeniu odpowiednie obiekty główne usługi. Obiekt aplikacji w związku z tym ma relację 1:1 z aplikacji hello i relację 1: duży zakres z odpowiednich obiektów głównych usługi.

W przypadku, gdy aplikacja hello będzie używany, umożliwiając tooestablish tożsamości dla logowania i/lub tooresources dostępu są chronione przez dzierżawcę hello nazwy głównej usługi należy utworzyć w każdej dzierżawy. Stosowanie pojedynczej dzierżawy będą mieć tylko jedną nazwę główną usługi (w jego macierzystego dzierżawcy), zwykle tworzone i zgodę do użycia podczas rejestracji aplikacji. Wielodostępne aplikacji/interfejs API sieci Web będą także mieć nazwy głównej usługi utworzone w każdej dzierżawy gdzie zgodził Użyj tooits użytkownika z tej dzierżawy.  

> [!NOTE]
> Wszelkie zmiany wprowadzone obiekt application tooyour, również są odzwierciedlane w głównym celem usługi w aplikacji hello macierzystego dzierżawy tylko (hello dzierżawy, którym został on zarejestrowany). Na aplikacje wielodostępne obiektu aplikacji toohello zmiany nie są uwzględniane w obiekty główne usługi żadni dzierżawcy konsumenta, aż do usunięcia hello dostęp za pośrednictwem hello [panelu dostępu aplikacji](https://myapps.microsoft.com) i ponownie przyznane.
><br>  
> Należy również zauważyć, że natywnych aplikacji jest zarejestrowana jako wielodostępnej domyślnie.
> 
> 

## <a name="example"></a>Przykład
Witaj poniższym diagramie przedstawiono hello relację w aplikacji obiektu aplikacji odpowiedniej usługi obiektów principal w kontekście hello przykładowej aplikacji wielu dzierżawców o nazwie **aplikacji HR**. W tym scenariuszu istnieją trzy dzierżaw usługi Azure AD: 

* **Adatum** — Witaj dzierżawy używanej przez hello firmy, która opracowała hello **HR aplikacji**
* **Contoso** — Witaj dzierżawy używanej przez hello organizacji Contoso, czyli konsumenta hello **HR aplikacji**
* **Firma Fabrikam** — Witaj dzierżawy używanej przez hello organizacji firmy Fabrikam, co także zużywa hello **HR aplikacji**

![Relacja między obiektem aplikacji i obiekt główny usługi](./media/active-directory-application-objects/application-objects-relationship.png)

W hello poprzedni diagram kroku 1 jest hello proces tworzenia aplikacji hello i obiekty główne usługi w dzierżawie macierzystego aplikacji hello.

W kroku 2 gdy Administratorzy Contoso i Fabrikam wykonać zgody, obiekt główny usługi jest tworzony w firmowych dzierżawy usługi Azure AD i hello przypisane uprawnienia administrator hello przyznane. Należy również zauważyć, że danej aplikacji hello HR może być skonfigurowany zaprojektowane tooallow zgody przez użytkowników do użytku w poszczególnych.

W kroku 3 powitania klienta dzierżawami hello HR aplikacji (Contoso i Fabrikam) każdego ma swoje własne obiekt główny usługi. Ich użycie wystąpienie aplikacji hello w czasie wykonywania, podlega postanowieniom powitalne zgodę uprawnienia administrator odpowiednich hello każdy reprezentuje.

## <a name="next-steps"></a>Następne kroki
Aplikacji obiektu aplikacji można uzyskać dostęp za pośrednictwem hello API Azure AD Graph hello [portalu Azure] [ AZURE-Portal] edytora manifestu aplikacji, lub [poleceń cmdlet programu PowerShell usługi Azure AD](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), reprezentowany przez jej OData [jednostek aplikacji][AAD-Graph-App-Entity].

Obiekt główny usługi aplikacji można uzyskać dostęp za pośrednictwem interfejsu API usługi Azure AD Graph hello lub [poleceń cmdlet programu Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), reprezentowany przez jej OData [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity].

Witaj [Explorer Azure AD Graph](https://graphexplorer.azurewebsites.net/) przydaje się do zapytań zarówno aplikacji hello i obiekty główne usługi.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
