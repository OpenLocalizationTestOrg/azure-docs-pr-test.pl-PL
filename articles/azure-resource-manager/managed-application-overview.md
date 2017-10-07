---
title: "aplikacje zarządzane aaaOverview Azure | Dokumentacja firmy Microsoft"
description: "Zawiera opis pojęć dotyczących hello Azure zarządzane aplikacje"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 2fd1844a442515f4492c890c9798073475a66f88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-overview"></a>Omówienie usługi Azure zarządzanych aplikacji

Dostawców, które używają usługi Azure może oferować toocustomers rozwiązań wokół hello world. Azure Marketplace jest galerii, która składa się z setki złożonych, multiresource szablonów dostawców firmy oraz innych firm. W ciągu minut klientów można wdrażać i rozpocząć korzystanie z platformy jako usługa (PaaS) i oprogramowania jako aplikacje usługi (SaaS). 

Chociaż hello Marketplace zawiera doskonały sposób tooquickly klientów można wdrożyć w ofercie, powitania klienta jest odpowiedzialna za utrzymanie i aktualizowanie hello rozwiązania. Poza hello rozliczeń obrazu maszyny wirtualnej, dostawców nie może pobierać klientom Witaj do użytku aplikacji. Ponadto dostawców nie uniemożliwiają klientów modyfikowanie zasobów krytycznych aplikacji. Również dostawców nie można zablokować dostęp toointellectual właściwość, która tworzy aplikację. Azure zarządzanych aplikacji Podaj rozwiązania tych problemów. 

Zarządzanej aplikacji jest podobne szablon rozwiązania tooa w hello Marketplace, z jedną różnicą klucza. W zarządzanej aplikacji hello zasoby są udostępnione tooa grupę zasobów, która jest zarządzana przez dostawcę hello. Grupa zasobów Hello znajduje się w subskrypcji powitania klienta, ale w dzierżawie powitalnych dostawcy tożsamości ma grupy zasobów toohello dostępu.

## <a name="advantages-of-managed-applications"></a>Korzyści wynikające z zarządzanych aplikacji

Zarządzane usługodawców (MSPs), niezależnym dostawcom oprogramowania, i firmowej centralnej zespoły IT można używać rozwiązania toodeliver zarządzanych aplikacji za pośrednictwem portalu Marketplace hello lub hello katalogu usług. Mimo że klienci wdrażać te aplikacje zarządzane w swoich subskrypcji, nie mają one toomaintain, zaktualizować lub ich usługi. Ponieważ dostawców zarządzania i obsługi aplikacji hello, klienci nie mają toodevelop domeny specyficzne dla aplikacji wiedzy toomanage te aplikacje. Klienci mogą automatycznie uzyskiwać aktualizacje aplikacji bez hello tooworry potrzeby dotyczące rozwiązywania problemów i diagnozowanie problemów z aplikacjami hello.

Dla dostawców i dostawców zarządzanych aplikacji utworzyć kanał toosell infrastruktury i oprogramowaniem za pośrednictwem hello Marketplace. Zarządzane aplikacje udostępniają tooattach sposób usług i klientów tooAzure operacyjne pomocy technicznej. Dostawców można obciążania klientów przy użyciu hello Azure systemów rozliczeniowych. Odbiorca może użyć szablonów toomanage hello cyklem życia wdrożone aplikacje. Tych rozwiązań jest niezależna i zapieczętowany toohello klienta, więc dostawców zapewniają wysoką jakość usługi. Takie podejście przynosi korzyści PaaS i SaaS dostawców. Pomaga również zespoły firmy centralnej platformy i integratorów systemów. platforma (SIs) osób, które mają toopackage i sprzedać ich rozwiązania.

## <a name="managed-application-types"></a>Typy zarządzanych aplikacji
Zarządzane aplikacje platformy Azure są dostępne w dwóch typów: katalog usługi i portalu Marketplace.
 
### <a name="service-catalog"></a>Service Catalog  

Z hello katalogu usług klienci mogą tworzyć wykaz zatwierdzonych rozwiązania Azure toobe używane przez użytkowników w organizacji. Obsługa takie katalog rozwiązania jest przydatne do centralnej zespoły IT w przedsiębiorstwach. Użytkownicy mogą korzystać hello katalogu tooensure zgodności z niektórych standardów organizacji, gdy zapewniają rozwiązania dla organizacji. Ich można kontrolować, aktualizacji i korzystanie z tych aplikacji. Pracownicy mogą korzystać z tooeasily katalogu hello odnajdywanie hello bogaty zestaw aplikacji, które są zalecane i zatwierdzone przez ich działów IT. Klienci widzą hello katalog usługi zarządzane aplikacje, które one utworzone. Również widzą hello zarządzanych aplikacji innych osób w ich udział organizacji z nimi.
 
Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
 
Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
 
### <a name="marketplace"></a>Portal Marketplace

Zarządzane aplikacje są dostępne za pośrednictwem hello Marketplace w hello portalu Azure. Po hello dostawców publikuje te aplikacje, są one dostępne dla wszystkich użytkowników lub poza tooconsume organizacji. Z tej metody MSPs, niezależnym dostawcom oprogramowania i SIs można zaoferować ich tooall rozwiązań klientów platformy Azure. Klienci uzyskują hello korzyścią z używania tych złożonych rozwiązań bez tooinvest potrzeby hello w zrozumienie i utrzymywanie hello rozwiązania. 

Obecnie wydawców można udostępnić ofert jako zarządzaną aplikację lub szablon rozwiązania który ma niezarządzane. głównymi składnikami Hello publikowania aplikacji zarządzanej zawierają hello pliku szablonu i pliku definicji hello interfejsu użytkownika. Plik szablonu Hello opisuje hello zasoby, które są obsługiwane. Plik definicji interfejsu użytkownika Hello opisano, jak hello wymagane dane wejściowe dla udostępniania tych zasobów są wyświetlane w portalu hello. Witaj wymagane pliki są w pliku .zip i przekazane za pośrednictwem portalu publikowania hello.
 
Aby uzyskać informacji dotyczących publikowania aplikacji zarządzanej toohello Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).

Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Kluczowe pojęcia

### <a name="managed-resource-group"></a>Grupa zasobów zarządzanych
Witaj zarządzanych grupa zasobów jest gdzie wszystkie hello Azure zasoby, które są udostępniane w szablonie hello są tworzone. Na przykład jeśli urządzenia hello jest używany toocreate konta magazynu, ta grupa zasobów zawiera zasobów konta magazynu hello. Nie zawiera on hello zasobów urządzenia.

### <a name="appliance-package"></a>Pakiet urządzenia
Wydawca Hello tworzy pakiet zawierający pliki szablonów hello i hello createUIDefinition pliku. W szczególności ten przewodnik zawiera następujące pliki hello:

- **applianceMainTemplate.json**: plik szablonu definiuje wszystkie zasoby hello, które są udostępniane przez hello urządzenia. Ten plik jest plikiem regularne szablonu, który został użyty toocreate zasobów.

- **MainTemplate.json**: plik szablonu definiuje hello urządzenia zasobów (Microsoft.Solutions/appliances). Jedną właściwość klucza zdefiniowane w tym zasobie jest ManagedResourceGroupId. Ta właściwość wskazuje, grupy zasobów, które jest używane toohost hello rzeczywiste zasoby, które są zdefiniowane w applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: ten plik zawiera opis sposobu renderowania hello potrzebne hello parametrów zdefiniowanych w szablonie hello interfejsu użytkownika.

### <a name="authorization"></a>Autoryzacja
Wydawca Hello musi określać hello uprawnienia wymagane przez hello dostawcy toomanage hello zasobów w imieniu powitania klienta. To uprawnienie dotyczy toohello grupy zasobów zarządzanych. Ustaw hello następujące wartości:

- **PrincipalID**: hello hello użytkownika, grupę lub aplikację, która została użyta grupa zasobów zarządzanych toohello dostępu toogrant identyfikator usługi Azure Active Directory (Azure AD). Ten identyfikator należy dzierżawy toohello wydawcy.

- **Wartość RoleDefinitionID**: hello Azure AD identyfikator toohello przypisanej roli hello poprzedzających identyfikator podmiotu zabezpieczeń. Może być jedną z wbudowanych ról kontroli dostępu opartej na rolach hello w dzierżawie powitalnych wydawcy. Aby uzyskać więcej informacji, zobacz [wbudowanych ról dla kontroli dostępu](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać informacji na temat publikowania aplikacji zarządzanych toohello Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).
* Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
* Zobacz toocreate plik definicji interfejsu użytkownika [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
