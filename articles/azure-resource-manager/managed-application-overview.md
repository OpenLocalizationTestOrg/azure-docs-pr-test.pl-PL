---
title: "Omówienie usługi Azure zarządzane aplikacje | Dokumentacja firmy Microsoft"
description: "Zawiera opis pojęć dla platformy Azure zarządzanych aplikacji"
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 7ace8e1ea8038e0748bfed00c0cc0a4fa340588b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-overview"></a>Omówienie usługi Azure zarządzanych aplikacji

Dostawców, które używają usługi Azure może oferować rozwiązań klientów na całym świecie. Azure Marketplace jest galerii, która składa się z setki złożonych, multiresource szablonów dostawców firmy oraz innych firm. W ciągu minut klientów można wdrażać i rozpocząć korzystanie z platformy jako usługa (PaaS) i oprogramowania jako aplikacje usługi (SaaS). 

Chociaż witryny Marketplace to dobry sposób dla klientów szybko wdrożyć oferty, klient jest odpowiedzialna za utrzymanie i aktualizowanie rozwiązania. Poza rozliczeń obrazu maszyny wirtualnej, dostawców nie może nałożyć klientów do użycia w aplikacji. Ponadto dostawców nie uniemożliwiają klientów modyfikowanie zasobów krytycznych aplikacji. Również dostawców nie można zablokować dostęp do własności intelektualnej tworzącą aplikacji. Azure zarządzanych aplikacji Podaj rozwiązania tych problemów. 

Zarządzanej aplikacji jest podobny do szablon rozwiązania w witrynie Marketplace, z jedną różnicą klucza. W aplikacji zarządzanej zasoby są udostępnione do grupy zasobów, która jest zarządzana przez dostawcę. Grupa zasobów jest obecny w subskrypcji klienta, ale tożsamości w dzierżawie dostawca ma dostęp do grupy zasobów.

## <a name="advantages-of-managed-applications"></a>Korzyści wynikające z zarządzanych aplikacji

Zarządzane usługodawców (MSPs), niezależnym dostawcom oprogramowania, a firmowej centralnej zespoły IT za pomocą zarządzanych aplikacji rozwiązań za pomocą portalu Marketplace lub katalogu usług. Mimo że klienci wdrażać te aplikacje zarządzane w swoich subskrypcji, nie ma do obsługi, aktualizacji lub ich obsługi. Ponieważ dostawców zarządzanie i obsługę aplikacji, klienci nie mają do opracowywania wiedzy domeny specyficzne dla aplikacji do zarządzania tymi aplikacjami. Klienci mogą automatycznie uzyskiwać aktualizacje aplikacji bez konieczności martwić się o Rozwiązywanie problemów i diagnozowanie problemów z aplikacjami.

Dla dostawców i dostawców zarządzanych aplikacji utworzyć kanał sprzedaży infrastruktury i oprogramowaniem za pośrednictwem portalu Marketplace. Zarządzane aplikacje umożliwiają również dołączyć usług oraz obsługi do klientów platformy Azure. Dostawców można obciążania klientów przy użyciu usługi Azure systemów rozliczeniowych. Szablony użyciem do zarządzania cyklem życia wdrożone aplikacje. Tych rozwiązań jest niezależna i zapieczętowany klienta, więc dostawców zapewniają wysoką jakość usługi. Takie podejście przynosi korzyści PaaS i SaaS dostawców. Pomaga również zespoły firmy centralnej platformy i integratorów systemów. platforma (SIs) chcesz pakiet, a tym ich rozwiązania.

## <a name="managed-application-types"></a>Typy zarządzanych aplikacji
Zarządzane aplikacje platformy Azure są dostępne w dwóch typów: katalog usługi i portalu Marketplace.
 
### <a name="service-catalog"></a>Service Catalog  

Z katalogu usług klienci mogą tworzyć katalog rozwiązania zatwierdzone na platformie Azure mają być używane przez użytkowników w organizacji. Obsługa takie katalog rozwiązania jest przydatne do centralnej zespoły IT w przedsiębiorstwach. Katalogu można ich używać w celu zapewnienia zgodności z niektórych standardów organizacji, gdy zapewniają rozwiązania dla organizacji. Ich można kontrolować, aktualizacji i korzystanie z tych aplikacji. Pracownicy mogą korzystać z katalogu, aby łatwo odnaleźć bogaty zestaw aplikacji, które są zalecane i zatwierdzone przez ich działów IT. Klienci widzą aplikacji zarządzanych katalogu usług, które one utworzone. Zostanie również wyświetlona zarządzanych aplikacji, które udostępnić innym osobom w organizacji.
 
Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
 
Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
 
### <a name="marketplace"></a>Portal Marketplace

Zarządzane aplikacje są dostępne za pośrednictwem portalu Marketplace w portalu Azure. Po dostawcy publikuje te aplikacje, są one dostępne dla wszystkich wewnątrz lub na zewnątrz organizacji, aby korzystać z. Z tej metody MSPs, niezależnym dostawcom oprogramowania i SIs można oferowanie ich klientom rozwiązań wszystkich Azure. Klienci uzyskują zaletą używania tych złożonych rozwiązań bez konieczności inwestowania w zrozumienie i utrzymywanie rozwiązania. 

Obecnie wydawców można udostępnić ofert jako zarządzaną aplikację lub szablon rozwiązania który ma niezarządzane. Główne składniki publikowania aplikacji zarządzanej obejmują pliku szablonu i pliku definicji interfejsu użytkownika. Plik szablonu zawiera opis zasoby, które są obsługiwane. Plik definicji interfejsu użytkownika w tym artykule opisano sposób wyświetlania wymagają danych wejściowych do inicjowania obsługi tych zasobów w portalu. Wymagane pliki są w pliku .zip i przekazane za pośrednictwem portalu publikowania.
 
Informacje o publikowaniu zarządzanej aplikacji do witryny Marketplace, zobacz [Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-author-marketplace.md).

Aby dowiedzieć się, jak korzystanie z zarządzanych aplikacji z portalu Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-consume-marketplace.md).

## <a name="key-concepts"></a>Kluczowe pojęcia

### <a name="managed-resource-group"></a>Grupa zasobów zarządzanych
Grupa zasobów zarządzanych jest, gdzie wszystkie zasoby platformy Azure, które są udostępniane w szablonie są tworzone. Na przykład jeśli urządzenie jest używany do tworzenia konta magazynu, ta grupa zasobów zawiera zasobów konta magazynu. Nie zawiera zasobów urządzenia.

### <a name="appliance-package"></a>Pakiet urządzenia
Wydawca tworzy pakiet zawierający pliki szablonu i pliku createUIDefinition. W szczególności zawiera następujące pliki:

- **applianceMainTemplate.json**: plik szablonu definiuje wszystkie zasoby, które są udostępniane przez urządzenie. Ten plik jest plikiem regularne szablonu, który służy do tworzenia zasobów.

- **MainTemplate.json**: plik szablonu definiuje zasobów urządzenia (Microsoft.Solutions/appliances). Jedną właściwość klucza zdefiniowane w tym zasobie jest ManagedResourceGroupId. Ta właściwość wskazuje, w których grupa zasobów jest używany do obsługi rzeczywistych zasobów, które są zdefiniowane w applianceMainTemplate.json.

- **applianceCreateUIDefinition.json**: ten plik zawiera opis sposobu renderowania interfejsu użytkownika wymagane do parametrów zdefiniowanych w szablonie.

### <a name="authorization"></a>Autoryzacja
Wydawca należy określić uprawnień wymaganych przez dostawcę do zarządzania zasobami w imieniu klienta. Uprawnienie to ma zastosowanie do grupy zasobów zarządzanych. Ustaw następujące wartości:

- **PrincipalID**: Azure Active Directory (Azure AD) identyfikator użytkownika, grupę lub aplikację, która jest używana w celu udzielenia dostępu do grupy zasobów zarządzanych. Ten identyfikator należy do dzierżawy wydawcy.

- **Wartość RoleDefinitionID**: identyfikator usługi Azure AD od roli przypisanej do poprzedniego identyfikator podmiotu zabezpieczeń. Może być jedną z wbudowanych ról kontroli dostępu opartej na rolach w dzierżawie wydawcy. Aby uzyskać więcej informacji, zobacz [wbudowanych ról dla kontroli dostępu](../active-directory/role-based-access-built-in-roles.md).

## <a name="next-steps"></a>Następne kroki

* Uzyskać informacji dotyczących publikowania aplikacji zarządzanych do witryny Marketplace, zobacz [Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-author-marketplace.md).
* Aby dowiedzieć się, jak korzystanie z zarządzanych aplikacji z portalu Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-consume-marketplace.md).
* Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
* Aby utworzyć plik definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
