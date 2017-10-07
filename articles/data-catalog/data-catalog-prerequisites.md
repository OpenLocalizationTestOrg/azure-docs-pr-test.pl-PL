---
title: "wymagania wstępne dotyczące aaaAzure Data Catalog | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach wstępnych hello, potrzebne tooget pracę z usługą Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Wymagania wstępne usługi Azure Data Catalog

Należy tootake nad kilka rzeczy, przed rozpoczęciem konfigurowania usługi Azure Data Catalog. Nie martw się, ten proces nie długo.

## <a name="azure-subscription"></a>Subskrypcja platformy Azure
tooset się wykaz danych musi być właścicielem hello lub współwłaściciel subskrypcji platformy Azure.

Subskrypcje platformy Azure ułatwić organizowanie dostęp do zasobów usługi toocloud, takie jak Data Catalog. Subskrypcje można także kontrolować sposób użycia zasobów jest zgłaszane, rozliczane i uregulowaniu płatności. Każda subskrypcja może mieć oddzielne ustawienia rozliczeń i płatności, więc można dodać subskrypcji i plany, które zależą od działów, projektów, biuro regionalne i tak dalej. Co usługa w chmurze należy tooa subskrypcji, i potrzebujesz toohave subskrypcji przed rozpoczęciem konfigurowania usługi Data Catalog. toolearn więcej, zobacz [Zarządzanie kontami, subskrypcje i ról administracyjnych](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Usługa Azure Active Directory
tooset się wykaz danych, użytkownik musi zalogować się przy użyciu konta użytkownika usługi Azure Active Directory (Azure AD).

Usługa Azure AD zapewnia prosty sposób dla firm toomanage tożsamości i dostępu, zarówno w chmurze hello i lokalnymi. Użytkownicy mogą używać jednego konta firmowego lub szkolnego dla pojedynczego tooany logowania w chmurze i lokalnych aplikacji sieci web. Data Catalog używa usługi Azure AD tooauthenticate logowania. toolearn więcej, zobacz [co to jest usługa Azure Active Directory?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Za pomocą hello [portalu Azure](http://portal.azure.com/), aby móc zalogować się za pomocą osobistego konta Microsoft lub Azure Active Directory konto służbowe. tooset się wykaz danych przy użyciu albo hello portalu Azure lub hello [portalu wykazu danych](http://www.azuredatacatalog.com), należy zalogować się przy użyciu konta usługi Azure Active Directory, a nie konta osobistego.
>
>

## <a name="active-directory-policy-configuration"></a>Konfiguracja zasad w usłudze Active Directory
Może wystąpić sytuacja, w których możesz zarejestrować się w portalu wykazu danych toohello, ale podczas próby toosign w narzędzia rejestracji źródła danych toohello, wystąpi komunikat o błędzie, który uniemożliwia rejestrowanie. To zachowanie problem może wystąpić tylko wtedy, gdy komputer znajduje się w sieci firmowej hello lub może wystąpić, tylko jeśli łączysz się z hello poza siecią firmową.

narzędzia rejestracji źródła danych Hello korzysta z uwierzytelniania formularzy toovalidate poświadczenia użytkownika w usłudze Active Directory. toohelp logowania pomyślnie, administrator usługi Active Directory należy włączyć uwierzytelnianie formularzy w hello globalne zasady uwierzytelniania.

Hello globalne zasady uwierzytelniania metody uwierzytelniania można połączeń włączone oddzielnie dla intranetu i ekstranetu, pokazane na powitania po zrzut ekranu. Mogą wystąpić błędy logowania, jeśli nie włączono uwierzytelniania formularzy hello sieci, z którym się łączysz.

 ![Usługi Active Directory globalnych zasad uwierzytelniania](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).
