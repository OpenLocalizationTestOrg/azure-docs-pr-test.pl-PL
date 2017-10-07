---
title: "aaaAzure zarządzanych aplikacji hello Marketplace | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Azure zarządzane aplikacje, które są dostępne za pośrednictwem hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Azure zarządzanych aplikacji hello Marketplace

 MSPs, niezależnym dostawcom oprogramowania i integratorów systemów. platforma (SIs) mogą korzystać z usługi Azure zarządzane aplikacje toooffer swoim klientom rozwiązań tooall portalu Azure Marketplace. W przypadku takich rozwiązań zmniejszyć hello konserwacji i obsługi obciążenia dla klientów. Wydawcy sprzedać infrastruktury i oprogramowaniem za pośrednictwem hello Marketplace. Ich można dołączyć usługi i aplikacje toomanaged operacyjne pomocy technicznej. Aby uzyskać więcej informacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).

W tym artykule opisano, jak MSP, niezależnego dostawcy oprogramowania lub SI publikowania aplikacji toohello Marketplace i stał się toocustomers szeroko dostępne.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Wymagania wstępne dotyczące publikowania aplikacji zarządzanej

Wymagania wstępne toolisting w hello Marketplace:

* Techniczne

    *  Uzyskać informacje o podstawowej struktury hello i składni szablonów usługi Azure Resource Manager, zobacz [szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).
    *  tooview pełny szablon rozwiązania, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/en-us/documentation/templates/) lub hello [repozytorium szablonów Szybki Start](https://github.com/azure/azure-quickstart-templates).
    *  Informacje, jak toocreate hello interfejs dla klientów, którzy wdrażania aplikacji za pośrednictwem hello Marketplace, zobacz [Utwórz plik definicji interfejsu użytkownika](managed-application-createuidefinition-overview.md).

* Nietechnicznym (wymagania biznesowe)

    *   Firmy lub zależnemu musi znajdować się w danym kraju, w którym sprzedaży są obsługiwane przez hello Marketplace.
    *   W taki sposób, który jest zgodny z rozliczeń modeli obsługiwanych przez hello Marketplace muszą mieć licencję na produkt.
    *   Wszystko jest odpowiedzialny za tworzenie toocustomers dostępna Pomoc techniczna w sposób uzasadnione ekonomicznie. Obsługa Hello można wolny, płatną, lub za pośrednictwem społeczności obsługuje.
    *   Wszystko jest odpowiedzialny za Licencjonowanie oprogramowanie oraz wszystkie zależności oprogramowania innych firm.
    *   Należy udostępnić zawartość, która spełnia kryteria dotyczące Twojej oferty toobe wymienione w hello Marketplace hello portalu Azure.
    *   Musisz zaakceptować warunki toohello hello Azure Marketplace udział zasad i umowy wydawcy.
    *   Musisz zaakceptować toocomply hello warunki użytkowania, zasady zachowania poufności informacji firmy Microsoft i certyfikowane umowę programu Microsoft Azure.

## <a name="create-a-new-azure-application-offer"></a>Tworzenie nowej oferty aplikacji Azure

Po hello wymagania wstępne zostały spełnione, wszystko jest gotowe toocreate ofertę zarządzanej aplikacji. Spójrzmy szybki przegląd oferty i jednostki SKU.

### <a name="offer"></a>Oferta

Oferta Hello zarządzanych aplikacji odpowiada klasy tooa produktu oferty od wydawcy. Jeśli masz nowy typ aplikacji rozwiązania, które mają toomake dostępne w portalu Marketplace hello, można go skonfigurować jako nowej oferty. Oferta jest kolekcją jednostki SKU. Każdy oferty jest wyświetlany jako własnej jednostce w hello Marketplace.

### <a name="sku"></a>SKU

Jednostka SKU jest hello najmniejszej płatnej wersji jednostki oferty. SKU w hello można użyć tego samego produktu toodifferentiate klasy (Oferta) między:

* Różne funkcje, które są obsługiwane.
* Określa, czy oferta hello jest zarządzane lub niezarządzane.
* Modele rozliczeń, które są obsługiwane.

Jednostka SKU jest wyświetlany w obszarze hello nadrzędnego oferty w hello Marketplace. Wygląda na to jako własnej jednostce oferowane w hello portalu Azure.

### <a name="set-up-an-offer"></a>Konfigurowanie oferty

1. Zaloguj się toohello [portalu dla partnerów chmury](https://cloudpartner.azure.com/).

2. W okienku nawigacji hello powitania po lewej stronie wybierz **+ nowe oferty** > **aplikacji Azure**.

    ![Nowa oferta](./media/managed-application-author-marketplace/newOffer.png)

3. Wypełnianie formularzy hello, pojawiające się na powitania w hello **edytor** widoku. Wymagane pola są oznaczone czerwoną gwiazdką (*).

    ![Ustawienia oferty](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Cztery główne formularze są używane toocreate zarządzanej aplikacji:

    a. Ustawienia oferty

    b. Jednostki SKU

    c. Portal Marketplace

    d. Pomoc techniczna

Formularze są opisane bardziej szczegółowo na powitania następujące sekcje.

## <a name="offer-settings-form"></a>Formularz Ustawienia oferty
Użyj tego formularza podstawowego toospecify hello oferta ustawień.

1. Wypełnij hello **oferują ustawienia** formularza. są polami Hello:

    a. **Identyfikator oferty**: ten unikatowy identyfikator identyfikuje oferta hello w profilu wydawcy. Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń. Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-). Identyfikator Hello nie może kończyć się łącznikiem. Jest ograniczona tooa maksymalnie 50 znaków. Po ofertę odbywa się na żywo, to pole jest zablokowane.

    b. **Identyfikator wydawcy**: za pomocą tej listy rozwijanej toochoose hello wydawcy profilu ma toopublish tej oferty, w obszarze. Po ofertę odbywa się na żywo, to pole jest zablokowane.

    c. **Nazwa**: Ta nazwa wyświetlana dla danej oferty pojawia się w hello Marketplace oraz w portalu hello. Może mieć maksymalnie 50 znaków. Obejmują rozpoznawalną nazwę markę produktu. Nie zawierają nazwę swojej firmy, chyba że jest sposób jest ona sprzedawane. Jeśli ta oferta jest marketingu na własne witryny sieci Web, upewnij się, czy nazwa hello jest dokładnie sposobu jej wyświetlania w witrynie sieci Web.

2. Wybierz **zapisać** toosave postęp. 

## <a name="skus-form"></a>Formularz jednostki SKU
Witaj następnym krokiem jest jednostki SKU tooadd dla danej oferty.

1. Wybierz **jednostki SKU** > **nowe jednostki SKU**. 

    ![Wybierz nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Wprowadź **identyfikator jednostki SKU**. Identyfikator jednostki SKU to unikatowy identyfikator dla hello SKU oferta. Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń. Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-). Identyfikator Hello nie może kończyć się kreską i jest ograniczone tooa maksymalnie 50 znaków. Po ofertę odbywa się na żywo, to pole jest zablokowane. Może mieć wiele jednostek SKU oferta. Należy jednostki SKU dla każdego obrazu planujesz toopublish.

3. Wypełnianie hello **szczegóły jednostki SKU** sekcji na powitania następującej postaci:

    ![Podaj nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Wypełnianie hello następujące pola:
    
    a. **Tytuł**: Podaj tytuł tej jednostki SKU. Ten tytuł pojawi się w galerii powitania dla tego elementu.

    b. **Podsumowanie**: Podaj krótkie podsumowanie dla tej wersji produktu. Ten tekst jest wyświetlany poniżej hello tytułu.

    c. **Opis elementu**: Podaj szczegółowy opis hello jednostki SKU.

    d. **Typ jednostki SKU**: hello dozwolone wartości to **zarządzanej aplikacji** i **szablony rozwiązań**. W tym przypadku wybierz **zarządzanej aplikacji**.

4. Wypełnianie hello **informacje szczegółowe dotyczące pakietu** sekcji na powitania następującej postaci:

    ![Pakiet](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Wypełnianie hello następujące pola:

    a. **Bieżąca wersja**: wprowadź wersję pakietu hello przekazywania. Powinna być w formacie hello `{number}.{number}.{number}{number}`.

    b. **Wybierz plik pakietu**: ten pakiet zawiera następujące pliki, które są kompresowane do pliku zip hello:
    * **applianceMainTemplate.json**: hello wdrażania szablonu pliku, który został użyty hello toodeploy rozwiązania/aplikacji. Aby uzyskać informacje na temat toocreate plików szablonu wdrażania, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: ten plik jest używany przez interfejs użytkownika hello Azure toogenerate portalu hello, który został użyty tooprovision rozwiązania/aplikacji. Aby uzyskać więcej informacji, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: ten plik szablonu zawiera tylko hello Microsoft.Solution/appliances zasobu. Plik mainTemplate Hello zawiera hello następujące właściwości:

        *  **rodzaj**: Użyj **Marketplace** zarządzanych aplikacji w hello Marketplace.
        *  **ManagedResourceGroupId**: Ta grupa zasobów w subskrypcji powitania klienta jest wdrożonym wszystkie zasoby hello zdefiniowane w applianceMainTemplate.json.
        *  **PublisherPackageId**: ten ciąg unikatowo identyfikujący hello pakietu. Podaj wartość hello w formacie hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Uzyskaj hello **identyfikator oferty** i **identyfikator wydawcy** z hello publikowania portalu, jak pokazano w powitania po obrazu:

![Identyfikator oferty](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Uzyskaj hello **identyfikator jednostki SKU**, jak pokazano w powitania po obrazu:

![IDENTYFIKATOR JEDNOSTKI SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Uzyskiwanie pakietu hello **wersji**, jak pokazano w powitania po obrazu:

![Wersja pakietu](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  Oparte na powitania poprzedzających przykłady, hello wartość **PublisherPackageId** jest `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Przykładowe mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Ten pakiet powinien zawierać zagnieżdżone szablony i skrypty, które są wymagane toosuccessfully inicjowania obsługi administracyjnej tej aplikacji. Witaj mainTemplate.json, applianceMainTemplate.json i applianceCreateUIDefinition.json pliki muszą znajdować się w folderze głównym hello.

* **Autoryzacje**: Ta właściwość określa, kto otrzymuje dostęp i hello poziom dostępu toohello zasobów w subskrypcji klientów. Wydawca Hello można użyć aplikacji hello toomanage w imieniu powitania klienta.
* **PrincipalId**: Ta właściwość jest hello Azure Active Directory (Azure AD) identyfikator użytkownika, grupy użytkowników lub aplikacji, która ma pewne uprawnienia na powitania zasobów w subskrypcji powitania klienta. Witaj definicji roli opisano hello uprawnienia. 
* **Definicja roli**: Ta właściwość jest lista wszystkich hello wbudowanych kontroli dostępu opartej na rolach (RBAC) ról dostarczane przez usługę Azure AD. Możesz wybrać hello roli, która jest najbardziej odpowiednia toouse toomanage hello zasobów w imieniu powitania klienta.

Można dodać wiele zezwolenia. Zaleca się utworzenie grupy użytkowników usługi AD i określić jej identyfikator w **PrincipalId**. W ten sposób można dodać więcej użytkowników toohello grupy użytkowników bez hello potrzeby tooupdate hello jednostki SKU.

Aby uzyskać więcej informacji o RBAC, zobacz [wprowadzenie RBAC w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Formularz Marketplace

Hello formularza Marketplace wprowadza się pola, które są widoczne na powitania [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i na powitania [portalu Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Identyfikatory subskrypcji w wersji zapoznawczej

Wprowadź listę identyfikatorów, które mogą uzyskiwać dostęp do oferty powitania po opublikowaniu subskrypcji platformy Azure. Można użyć tych oferta hello podglądu tootest wymienione biały subskrypcji przed wprowadzeniem jej na żywo. Kompiluje listę biały się too100 subskrypcji w portalu dla partnerów hello.

### <a name="suggested-categories"></a>Kategorii sugerowanych

Wybierz się toofive kategorii z listy hello ofertę może być najlepiej skojarzone z. Te kategorie są używane toomap kategorie produktów toohello oferta dostępnych w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i hello [portalu Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Podsumowanie Hello zarządzanych aplikacji wyświetla hello następujące pola:

![Podsumowanie witryny Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Witaj **omówienie** karcie dla aplikacji zarządzanej Wyświetla hello następujące pola:

![Omówienie portalu Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Witaj **planów + cennik** karcie dla aplikacji zarządzanej Wyświetla hello następujące pola:

![Plany Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Azure Portal

Podsumowanie Hello zarządzanych aplikacji wyświetla hello następujące pola:

![Portal podsumowania](./media/managed-application-author-marketplace/publishvm12.png)

Omówienie Hello aplikacji zarządzanej Wyświetla hello następujące pola:

![Przegląd portalu](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Wytycznych dotyczących logo

Skorzystaj z następujących wskazówek dla dowolnego logo, które należy przekazać w portalu dla partnerów chmury hello:

*   Hello Azure projekt ma paletę kolorów proste. Ogranicz liczbę hello podstawowym i pomocniczym kolorów na logo.
*   kolorów motywu Hello portalu hello są białe i czarne. Nie używaj kolorów te jako kolor tła hello logo. Użyj kolor, który umożliwia widoczne w portalu hello logo. Zaleca się proste kolorów podstawowych. *Jeśli używasz przezroczyste tło, upewnij się, hello logo i tekst są białe, czarne lub niebieski.*
*   Nie używaj gradientu tła na powitania logo.
*   Nie należy umieszczać na powitania logo, nawet Twoja firma lub marką tekstu. Witaj wygląd i działanie logo powinny być płaski i uniknąć gradienty.
*   Upewnij się, że nie jest rozciągana hello logo.

#### <a name="hero-logo"></a>Logo bohater

logo bohater Hello jest opcjonalna. Wydawca Hello można nie tooupload logo bohater. Po przekazaniu hello bohater ikony, nie można usunąć. W tym czasie partnera hello musi występować po hello Marketplace wytyczne dotyczące bohater ikon.

Skorzystaj z następujących wskazówek dla ikony logo bohater hello:

*   Nazwa wyświetlana Hello wydawcy, tytuł planu hello i długie Podsumowanie oferty hello są wyświetlane w biały. W związku z tym nie należy używać jasny kolor tła hello hello bohater ikony. Czarne, białe lub przezroczyste tło nie jest dozwolona dla bohater ikon.
*   Po oferta hello jest wyświetlana, hello wydawcy nazwę wyświetlaną, tytuł planu hello, długie Podsumowanie oferty hello i hello **Utwórz** przycisk programowo osadzone wewnątrz hello bohater logo. W rezultacie nie wprowadź tekst, podczas projektowania hello bohater logo. Pozostaw puste miejsce na powitania prawo ponieważ hello tekst jest uwzględniany programowo w tym miejscu. Witaj wolnego miejsca dla tekstu hello powinna być 415 x 100 pikseli na powitania prawo. Jest on przesunięcia pikseli 370 od lewej hello.

    ![Przykład logo bohater](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Obsługa formularza

Wypełnianie hello **obsługuje** formularza z obsługą kontaktuje się z Twojej firmy. Te informacje mogą inżynierii, kontaktów i kontaktów pomocy technicznej klienta.

## <a name="publish-an-offer"></a>Publikowanie oferty

Po wypełnieniu wszystkie sekcje hello wybierz **publikowania** toostart hello procesu, który sprawia, że Twoje toocustomers dostępne oferty.

## <a name="next-steps"></a>Następne kroki

* Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).
* Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).
* Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).
