---
title: "Aplikacja usługi Azure Active Directory i obiektów nazwy głównej usługi | Dokumentacja firmy Microsoft"
description: "Omówienie relacja między aplikacją i obiekty główne usługi w usłudze Azure Active Directory"
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
ms.openlocfilehash: 4c75ade5f4e47ef64ccc0fe8af4b174c377dc7bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Aplikacji i usług obiektów principal w usłudze Azure Active Directory (Azure AD)
Czasami znaczenie "aplikacja" może być błędnie interpretowane w kontekście usługi Azure AD. Celem tego artykułu jest stał się jaśniejszy, przez wyjaśnienie koncepcyjne i konkretnych aspektów integracji aplikacji usługi Azure AD, z ilustracja rejestracji i zgoda na [wielodostępnych aplikacji](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Omówienie
Aplikacji, które zostało zintegrowane z usługą Azure AD ma znaczenie, które wykraczają poza aspekt oprogramowania. "Aplikacja" jest często używane jako koncepcyjnej terminu odwołujących się do nie tylko aplikacji, ale również rejestracji usługi Azure AD i role w uwierzytelniania/autoryzacji "konwersacji" w czasie wykonywania. Zgodnie z definicją aplikacji może działać w [klienta](active-directory-dev-glossary.md#client-application) roli (Korzystanie z zasobów), [serwer zasobów](active-directory-dev-glossary.md#resource-server) roli (uwidaczniającą API klientom) i/lub nawet. Protokół konwersacji jest definiowana za pomocą [przepływ udzielania autoryzacji OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), dzięki czemu klient/zasobu dostępu/ochrony zasobów danych odpowiednio. Teraz przejdźmy poziom głębiej i zobacz, jak model aplikacji usługi Azure AD reprezentuje aplikacji w czasie projektowania i w czasie wykonywania. 

## <a name="application-registration"></a>Rejestracja aplikacji
Podczas rejestrowania aplikacji usługi Azure AD w [portalu Azure][AZURE-Portal], dwa obiekty są tworzone w dzierżawie usługi Azure AD: obiekt aplikacji, a obiekt główny usługi.

#### <a name="application-object"></a>Obiekt aplikacji
Aplikację usługi Azure AD jest zdefiniowana przez jego jedno i tylko obiekt aplikacji, który znajduje się w dzierżawie usługi Azure AD, gdzie aplikacja została zarejestrowana, nazywany "home" dzierżawy aplikacji. Azure AD Graph [jednostek aplikacji] [ AAD-Graph-App-Entity] definiuje schemat dla właściwości obiektu aplikacji. 

#### <a name="service-principal-object"></a>Obiekt główny usługi
Obiekt główny usługi definiuje zasady i uprawnienia do użytku w aplikacji w określonych dzierżawy, zapewniając podstawę do aplikacji w czasie wykonywania reprezentowania podmiotu zabezpieczeń. Azure AD Graph [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity] definiuje schemat dla właściwości obiektu główną usługi. 

#### <a name="application-and-service-principal-relationship"></a>Aplikacji i ich relacji głównej usługi
Należy wziąć pod uwagę obiektu aplikacji jako *globalne* reprezentację aplikacji do użycia dla wszystkich dzierżawców i nazwy głównej usługi jako *lokalnego* reprezentacja do użycia w określonym dzierżawcy. Służy obiekt aplikacji jako szablonu, z których typowe i domyślne właściwości są *pochodnych* do użytku przy tworzeniu odpowiednie obiekty główne usługi. Obiekt aplikacji w związku z tym ma relację 1:1 z aplikacją oprogramowania i relację 1: duży zakres z odpowiednich obiektów głównych usługi.

Nazwy głównej usługi muszą zostać utworzone w każdej dzierżawy, w której aplikacja będzie używany, umożliwiających jej ustalenie tożsamości dla logowania i/lub dostęp do zasobów, które są zabezpieczone przez dzierżawcę. Stosowanie pojedynczej dzierżawy będą mieć tylko jedną nazwę główną usługi (w jego macierzystego dzierżawcy), zwykle tworzone i zgodę do użycia podczas rejestracji aplikacji. Wielodostępne aplikacji/interfejs API sieci Web będą także mieć nazwy głównej usługi utworzone w każdej dzierżawy gdzie użytkownika z tej dzierżawy wyraziła zgodę na jego użycie.  

> [!NOTE]
> Wszelkie zmiany wprowadzone do obiektu aplikacji, również są odzwierciedlane w głównym celem usługi w aplikacji macierzystego dzierżawy tylko (dzierżawy, w którym zarejestrowano). Na aplikacje wielodostępne zmiany do obiektu aplikacji nie są widoczne w obiekty główne usługi żadni dzierżawcy konsumenta, do momentu usunięcia dostęp za pośrednictwem [panelu dostępu aplikacji](https://myapps.microsoft.com) i ponownie przyznane.
><br>  
> Należy również zauważyć, że natywnych aplikacji jest zarejestrowana jako wielodostępnej domyślnie.
> 
> 

## <a name="example"></a>Przykład
Na poniższym diagramie przedstawiono relację między aplikacji obiektu aplikacji i odpowiedniej usługi obiektów principal w kontekście wielodostępne przykładowej aplikacji o nazwie **aplikacji HR**. W tym scenariuszu istnieją trzy dzierżaw usługi Azure AD: 

* **Adatum** -dzierżawy używane przez firmę, która opracowała **HR aplikacji**
* **Contoso** — dzierżawy używane w organizacji Contoso, który jest klient korzystający z **HR aplikacji**
* **Firma Fabrikam** -dzierżawy używane przez organizację firmy Fabrikam, która zajmuje także **HR aplikacji**

![Relacja między obiektem aplikacji i obiekt główny usługi](./media/active-directory-application-objects/application-objects-relationship.png)

W poprzedni diagram kroku 1 jest przez proces tworzenia aplikacji i usługi obiektów principal w dzierżawie macierzystego aplikacji.

W kroku 2 gdy Administratorzy Contoso i Fabrikam wykonać zgody, obiekt główny usługi jest utworzony w dzierżawie usługi Azure AD firmy i przypisane uprawnienia przyznane przez administratora. Należy również zauważyć, że aplikacji HR może być skonfigurowany/umożliwia zgody przez użytkowników do użytku w poszczególnych.

W kroku 3 dzierżawy konsumenta, HR aplikacji (Contoso i Fabrikam) każdego mają własne obiekt główny usługi. Każdy reprezentuje zgodę ich używania wystąpienie aplikacji w czasie wykonywania, podlega postanowieniom uprawnienia administrator odpowiednich.

## <a name="next-steps"></a>Następne kroki
Obiekt aplikacji aplikacji można uzyskać dostęp za pomocą interfejsu API Azure AD Graph, [portalu Azure] [ AZURE-Portal] edytora manifestu aplikacji, lub [poleceń cmdlet programu Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), jako reprezentowany przez jej OData [jednostek aplikacji][AAD-Graph-App-Entity].

Obiekt główny usługi aplikacji można uzyskać dostęp za pomocą interfejsu API Azure AD Graph lub [poleceń cmdlet programu Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), reprezentowany przez jej OData [jednostki ServicePrincipal] [ AAD-Graph-Sp-Entity].

[Explorer Azure AD Graph](https://graphexplorer.azurewebsites.net/) przydaje się do wykonywania zapytań w aplikacji i obiekty główne usługi.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
