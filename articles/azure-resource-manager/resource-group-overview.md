---
title: "aaaAzure omówienie Resource Manager | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse usługi Azure Resource Manager do wdrażania, zarządzania i kontroli dostępu do zasobów na platformie Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Omówienie usługi Azure Resource Manager
Hello infrastruktura aplikacji zwykle obejmuje wiele składników — może być maszynę wirtualną, konta magazynu i sieci wirtualnej lub aplikacji sieci web, bazy danych, serwer bazy danych i 3 usług firm. Te składniki nie są widoczne jako osobne jednostki, tylko jako powiązane i zależne od siebie nawzajem części jednej całości. Mają toodeploy, zarządzanie i monitorowanie ich jako grupa. Usługa Azure Resource Manager umożliwia toowork z zasobami hello w rozwiązaniu jako grupa. Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby powitania dla danego rozwiązania w jednej, skoordynowanej operacji. Wdrażanie wykonuje się przy użyciu szablonu, którego można następnie używać w różnych środowiskach (testowanie, etap przejściowy i produkcja). Usługa Resource Manager zapewnia zabezpieczeń, inspekcji i znakowanie toohelp funkcje zarządzania zasobami po wdrożeniu. 

## <a name="terminology"></a>Terminologia
W przypadku nowych tooAzure Resource Manager istnieją terminy, nie może być zapoznać się z.

* **Zasób** — dostępny za pośrednictwem platformy Azure element, którym można zarządzać. Niektóre typowe zasoby to: maszyna wirtualna, konto magazynu, aplikacja sieci Web czy sieć wirtualna. Istnieje ich jednak wiele więcej.
* **Grupa zasobów** — kontener, który zawiera powiązane zasoby rozwiązania dla platformy Azure. Grupa zasobów Hello mogą obejmować wszystkie zasoby hello hello rozwiązania lub tylko tych zasobów, które mają toomanage jako grupa. Możesz zdecydować, jak zasoby tooallocate tooresource grupy oparte na to, co sprawia, że hello najbardziej odpowiednie dla Twojej organizacji. Zobacz [Grupy zasobów](#resource-groups).
* **Dostawca zasobów** — usługa dostarczająca zasoby hello można wdrażać i zarządzać za pomocą Menedżera zasobów. Każdy dostawca zasobów udostępnia operacje do pracy z zasobami hello, które zostały wdrożone. Niektóre typowe dostawców zasobów są Microsoft.Compute, która dostarcza hello zasobu maszyny wirtualnej, Microsoft.Storage, która dostarcza zasobów konta magazynu hello, i Microsoft.Web, która dostarcza aplikacji tooweb powiązane zasoby. Zobacz [Dostawcy zasobów](#resource-providers).
* **Szablon usługi Resource Manager** -pliku A JavaScript Object Notation (JSON), który definiuje co najmniej jeden zasobów toodeploy tooa grupy zasobów. Definiuje również zależności hello między zasobami hello wdrożone. Szablon Hello może być używane toodeploy hello zasobów, spójne i wielokrotnie. Zobacz [Wdrażanie na podstawie szablonu](#template-deployment).
* **składni deklaratywnej** — stan składnię, która umożliwia "Oto I mają toocreate" bez konieczności programowania toocreate polecenia sekwencji hello toowrite go. Szablon usługi Resource Manager Hello jest przykład składni deklaratywnej. W pliku hello można zdefiniować właściwości hello hello infrastruktury toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>Zalety Hello za pomocą Menedżera zasobów
Usługa Resource Manager zapewnia kilka korzyści:

* Można wdrożyć, zarządzanie i monitorowanie wszystkich zasobów hello do rozwiązania jako grupy zamiast obsługiwania zasobów pojedynczo.
* Można wielokrotnie wdrażania rozwiązania w całym cyklu programistycznym hello i mieć pewność, zasoby są wdrażane w spójnym stanie.
* Możliwość zarządzania infrastrukturą przy użyciu szablonów deklaratywnych zamiast skryptów.
* Można zdefiniować hello zależności między zasobami w celu wdrażania ich w odpowiedniej kolejności hello.
* Można zastosować usług tooall kontroli dostępu w grupie zasobów, ponieważ na platformie zarządzania hello natywnej integracji funkcji kontroli dostępu opartej na rolach (RBAC).
* Możliwość dodawania tagów tooresources toologically organizowanie wszystkie zasoby hello w ramach subskrypcji.
* Można również uprościć rozliczenia w organizacji, wyświetlając kosztów dla grupy zasobów udostępnianie hello na tym samym tagiem.  

Menedżer zasobów udostępnia nowe toodeploy sposób rozwiązań i zarządzania nimi. Jeśli używasz hello wcześniejszego modelu wdrożenia i mają toolearn o zmianach hello, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Spójna warstwa zarządzania
Menedżer zasobów zapewnia warstwę spójnego sposobu zarządzania dla hello zadań, które można wykonywać za pomocą programu Azure PowerShell, interfejsu wiersza polecenia Azure, portalu Azure, interfejsu API REST i narzędzia deweloperskie. Wszystkie narzędzia hello korzystanie ze wspólnego zestawu działań. Możesz narzędzia hello najlepsza, które można używać ich zamiennie bez obaw o zgodność. 

Witaj poniższy obraz przedstawia sposób interakcyjnie wszystkie narzędzia hello hello tego samego interfejsu API Menedżera zasobów Azure. Witaj interfejsu API przekazuje żądania usługi Resource Manager toohello, która uwierzytelnia i autoryzuje hello żądania. Menedżer zasobów, a następnie trasy hello żądań toohello odpowiedni zasób dostawców.

![Model żądań usługi Resource Manager](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Wskazówki
Witaj poniższe sugestie pomóc w pełni wykorzystać możliwości usługi Resource Manager podczas pracy z rozwiązaniami.

1. Definiowanie i wdrażaj infrastrukturę za pomocą składni deklaratywnej hello w szablonach usługi Resource Manager, a nie za pomocą poleceń imperatywnych.
2. Wszystkie kroki wdrażania i konfiguracji należy zdefiniować w szablonie hello. W konfiguracji rozwiązania nie powinno być żadnych etapów ręcznych.
3. Uruchamianie poleceń imperatywnych toomanage zasobów, takich jak toostart lub zatrzymywania aplikacji lub komputera.
4. Rozmieść zasoby z hello tego samego cyklu życia w grupie zasobów. We wszystkich pozostałych operacjach związanych z organizacją zasobów używaj tagów.

Aby uzyskać zalecenia dotyczące szablonów, zobacz [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md) (Najlepsze rozwiązania dotyczące tworzenia szablonów usługi Azure Resource Manager).

Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Grupy zasobów
Istnieją pewne ważne czynniki tooconsider podczas definiowania grupie zasobów:

1. Wszystkie zasoby hello w grupie powinny współużytkować hello sam cykl życia. Są one wdrażane, aktualizowane i usuwane razem. Jeśli jakiś zasób, takich jak serwer bazy danych musi tooexist na inny cykl wdrażania należy się w innej grupie zasobów.
2. Każdy zasób może znajdować się tylko w jednej grupie zasobów.
3. Można dodać lub usunąć grupę zasobów tooa zasobów w dowolnej chwili.
4. Zasoby można przenosić między grupami tooanother grupy zasobów. Aby uzyskać więcej informacji, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](resource-group-move-resources.md).
5. Grupa zasobów może zawierać zasoby, które znajdują się w różnych regionach.
6. Grupa zasobów może być używana dla działania administracyjne tooscope kontroli dostępu.
7. Zasób może wchodzić w interakcję z zasobami znajdującymi się w innych grupach zasobów. Interakcji jest typowe w przypadku, gdy hello dwa zasoby dotyczące, ale nie mają hello tego samego cyklu życia (na przykład aplikacje sieci web łączenie tooa bazy danych).

Podczas tworzenia grupy zasobów, należy tooprovide lokalizacji dla danej grupy zasobów. Być może zastanawiasz się, „Dlaczego grupa zasobów wymaga określenia lokalizacji? I, jeśli hello zasobów może mieć różne lokalizacje niż hello grupy zasobów, dlaczego ma lokalizacja grupy zasobów hello znaczenia w ogóle?" Grupa zasobów Hello są przechowywane metadane dotyczące hello zasobów. W związku z tym po określeniu lokalizacji dla grupy zasobów hello określisz przechowywania tych metadanych. Ze względu na zgodność może być konieczne tooensure danych przechowywanych w określonym regionie.

## <a name="resource-providers"></a>Dostawcy zasobów
Każdy dostawca zasobów udostępnia zestaw zasobów i operacji do pracy z usługą platformy Azure. Na przykład, jeśli chcesz toostore kluczy i kluczy tajnych, pracy z hello **Microsoft.KeyVault** dostawcy zasobów. Ten dostawca zasobów udostępnia typ zasobu o nazwie **magazynów** tworzenia hello magazynu kluczy. 

Nazwa Hello typu zasobu jest w formacie hello: **{dostawcy zasobów} / {typ zasobu}**. Na przykład typ magazynu kluczy hello jest **Microsoft.KeyVault/vaults**.

Przed rozpoczęciem pracy z zasobami wdrażania, należy uzyskać zrozumienia hello dostępnych dostawców zasobów. Znajomość hello nazwy zasobu dostawców i zasobów pozwala zdefiniować zasoby, które mają toodeploy tooAzure. Ponadto należy tooknow hello prawidłowych lokalizacji i wersje interfejsu API dla każdego typu zasobu. Aby uzyskać więcej informacji, zobacz [Dostawcy zasobów i ich typy](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Wdrażanie na podstawie szablonu
Usługa Resource Manager można utworzyć szablon (w formacie JSON), który definiuje hello infrastrukturze i konfiguracji rozwiązania Azure. Dzięki szablonowi można wielokrotnie wdrażać rozwiązanie w całym jego cyklu życia z gwarancją spójnego stanu zasobów po każdym wdrożeniu. Po utworzeniu rozwiązania z portalu hello hello rozwiązanie automatycznie zawiera szablon wdrożenia. Nie masz toocreate szablonu od początku, ponieważ można uruchomić z szablonem hello rozwiązania i dostosować go toomeet określonych potrzeb. Szablon dla istniejącej grupy zasobów można pobrać przez eksportowanie hello bieżący stan grupy zasobów hello lub wyświetlanie hello szablon używany do konkretnego wdrożenia. Wyświetlanie hello [wyeksportowanego szablonu](resource-manager-export-template.md) jest pomocny sposób toolearn o składni szablonu hello.

toolearn o formacie hello hello szablonu i konstrukcji, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md). Witaj tooview składni JSON dla typów zasobów, zobacz [zdefiniować zasoby w szablonach usługi Azure Resource Manager](/azure/templates/).

Menedżer zasobów przetwarza hello szablonu, podobnie jak inne żądanie (zobacz obraz powitania [spójna warstwa zarządzania](#consistent-management-layer)). Analizuje szablon hello, a konwertuje jego składni na operacje interfejsu API REST dla dostawców zasobów odpowiednie hello. Na przykład gdy Menedżer zasobów otrzymuje szablonu z powitania po definicji zasobu:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Konwertuje następującej operacji interfejsu API REST, który jest wysyłany dostawcy zasobów Microsoft.Storage toohello toohello definicji hello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Jak zdefiniować szablony i grupy zasobów to całkowicie maksymalnie tooyou oraz sposób toomanage rozwiązania. Na przykład w przypadku wdrażania aplikacji trzy warstwy za pomocą jednego szablonu tooa pojedyncza grupa zasobów.

![szablon trójwarstwowy](./media/resource-group-overview/3-tier-template.png)

Jednak nie ma toodefine całej infrastruktury w jednym szablonie. Często dobrym toodivide znaczeniu wymagań dotyczących wdrożenia do zestawu docelowego, specyficzne dla celu szablonów. Te szablony mogą bez problemu być używane wielokrotnie w różnych rozwiązaniach. toodeploy danego rozwiązania, utworzyć szablon wzorcowy połączony wszystkie szablony hello wymagane. Witaj Poniższa ilustracja przedstawia przykładowy sposób toodeploy rozwiązania trzy warstwy za pomocą szablonu nadrzędnego, który obejmuje trzy zagnieżdżone szablony.

![zagnieżdżony szablon warstwowy](./media/resource-group-overview/nested-tiers-template.png)

Jeśli zgodnie z warstw mających oddzielne cykle, można wdrożyć trzy warstwy tooseparate grupy zasobów. Powiadomienie hello zasobami nadal mogą być połączone tooresources w innych grup zasobów.

![szablon warstwowy](./media/resource-group-overview/tier-templates.png)

Więcej rozwiązań dotyczących projektowania szablonów można znaleźć w temacie [Patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md) (Wzorce projektowania szablonów usługi Azure Resource Manager). Informacje dotyczące szablonów zagnieżdżonych można znaleźć w temacie [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md) (Używanie szablonów połączonych w usłudze Azure Resource Manager).

Usługa Azure Resource Manager analizuje zależności tooensure zasoby są tworzone we właściwej kolejności hello. Jeśli jeden zasób opiera się na wartości z innego zasobu (na przykład maszyna wirtualna wymagająca konta magazynu na potrzeby dysków), ustawiana jest zależność. Aby uzyskać więcej informacji, zobacz [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md) (Definiowanie zależności w szablonach usługi Azure Resource Manager).

Umożliwia także szablonu hello infrastruktury toohello aktualizacji. Można na przykład dodać rozwiązanie tooyour zasobów i dodać reguły konfiguracji hello zasobów, które są już wdrożone. Jeśli szablon hello określa tworzenie zasobu, ale ten zasób już istnieje, usługi Azure Resource Manager przeprowadzi aktualizację, zamiast tworzyć nowy zasób. Azure Resource Manager aktualizacje hello istniejących zasobów toohello sam stan, ponieważ byłaby nowego.  

Resource Manager zapewnia rozszerzenia dla scenariuszy, gdy potrzebne są dodatkowe operacje, takie jak zainstalowanie konkretnego oprogramowania, które nie są uwzględnione w Instalatorze hello. Jeśli używasz już usługi do zarządzania konfiguracją, takiej jak DSC, Chef lub Puppet, dzięki rozszerzeniom możesz z nią dalej bez przeszkód pracować. Aby uzyskać informacje o rozszerzeniach i funkcjach maszyn wirtualnych, zobacz [Informacje o rozszerzeniach i funkcjach maszyn wirtualnych](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Na koniec szablon hello staje się częścią hello kodu źródłowego aplikacji. Można go zaewidencjonować repozytorium kodu źródłowego tooyour i aktualizować w miarę rozwijania aplikacji. Można edytować hello szablonu za pomocą programu Visual Studio.

Po zdefiniowaniu szablonu, wszystko jest gotowe toodeploy hello zasobów tooAzure. Hello polecenia toodeploy hello zasobów Zobacz:

* [Deploy resources with Resource Manager templates and Azure PowerShell (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i programu Azure PowerShell)](resource-group-template-deploy.md)
* [Deploy resources with Resource Manager templates and Azure CLI (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu wiersza polecenia platformy Azure)](resource-group-template-deploy-cli.md)
* [Deploy resources with Resource Manager templates and Azure portal (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i witryny Azure Portal)](resource-group-template-deploy-portal.md)
* [Deploy resources with Resource Manager templates and Resource Manager REST API (Wdrażanie zasobów za pomocą szablonów usługi Resource Manager i interfejsu API REST usługi Resource Manager)](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Tagi
Resource Manager udostępnia funkcję tagowania umożliwiającą toocategorize zasobów zgodnie z wymaganiami tooyour zarządzania lub rozliczeń. Używaj tagów po złożonych kolekcji grup zasobów i zasobów oraz muszą toovisualize tych zasobów w hello sposób hello większości tooyou znaczeniu. Na przykład znakować zasoby, które pełnią podobną rolę w organizacji lub należą toohello samego działu. Bez tagów, użytkownicy w organizacji można utworzyć wiele zasobów, które mogą być trudne toolater identyfikowania i zarządzania nim. Na przykład możesz toodelete wszystkie zasoby hello z określonego projektu. Jeśli te zasoby nie są oznaczone dla projektu hello, należy je znaleźć toomanually. Tagowanie może być istotnym sposobem tooreduce niepotrzebnych kosztów w ramach subskrypcji. 

Zasoby nie są tooreside w hello tego samego zasobu grupy tooshare tag. Możesz utworzyć własne tooensure taksonomii tag, że wszyscy użytkownicy w organizacji używać typowych tagów zamiast użytkowników przypadkowo stosowania nieco inne tagów (na przykład "Wydział" zamiast "dział").

Witaj poniższy przykład przedstawia maszynę wirtualną tooa Znacznik zastosowany.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

Użyj wszystkich zasobów hello z wartością tagu tooretrieve hello następującego polecenia cmdlet programu PowerShell:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

Lub hello następujące polecenia 2.0 interfejsu wiersza polecenia platformy Azure:

```azurecli
az resource list --tag costCenter=Finance
```

Można również wyświetlić oznakowanych zasobów za pomocą hello portalu Azure.

Witaj [raport użycia](../billing/billing-understand-your-bill.md) dla Twoja subskrypcja obejmuje tag nazwy i wartości, co pozwala toobreak limit koszty według znaczników. Aby uzyskać więcej informacji na temat tagów, zobacz [używanie tagów tooorganize zasobów platformy Azure](resource-group-using-tags.md).

## <a name="access-control"></a>Kontrola dostępu
Menedżer zasobów pozwala toocontrol mającego dostęp toospecific akcje dla Twojej organizacji. Natywnie integruje kontroli dostępu opartej na rolach (RBAC) hello platformy zarządzania i stosuje tej usługi tooall kontroli dostępu w grupie zasobów. 

Istnieją dwa główne pojęcia toounderstand podczas pracy z kontroli dostępu opartej na rolach:

* Definicje ról — opisują zestaw uprawnień i można ich używać w wielu przypisaniach.
* Przypisania ról — kojarzą definicję z tożsamością (użytkownikiem lub grupą) dla określonego zakresu (subskrypcji, grupy zasobów lub zasobu). Przypisanie Hello jest dziedziczona przez niższe zakresów.

Możesz dodać platformy zdefiniowane toopre użytkowników i ról określonych zasobów. Na przykład można wykorzystać hello wstępnie zdefiniowanej roli o nazwie Reader, który pozwala użytkownikom tooview zasobów, ale nie można ich zmienić. Dodawanie użytkowników w organizacji, którzy potrzebują tego typu rolę czytelnika toohello dostępu i Zastosuj hello roli toohello subskrypcji, grupy zasobów lub zasobów.

Platforma Azure udostępnia następujące cztery role platformy hello:

1. Właściciel — może zarządzać wszystkim, łącznie z dostępem
2. Współautor — może zarządzać wszystkim oprócz dostępu
3. Czytelnik — może przeglądać wszystko, ale nie może wprowadzać zmian
4. Administrator dostępu użytkowników — zarządzanie zasobami tooAzure dostępu użytkownika

Platforma Azure udostępnia kilka ról specyficznych dla zasobów. Niektóre typowe z nich to:

1. Współautor maszyny wirtualnej — można zarządzać maszynami wirtualnymi, ale nie przyznania dostępu toothem i nie może zarządzać hello wirtualnych sieci lub magazynu konta toowhich gdy są połączeni
2. Współautor sieci — zarządzanie wszystkich zasobów sieciowych, ale nie przyznania dostępu toothem
3. Współautor konta magazynu — Zarządzanie kontami magazynu, ale nie przyznania dostępu toothem
4. Współautor serwera SQL — może zarządzać bazami danych i serwerami SQL, ale nie ich zasadami związanymi z zabezpieczeniami
5. Współautor witryny sieci Web — Zarządzanie witryn sieci Web, ale nie hello toowhich planów sieci web, które są połączone

Witaj pełną listę ról i dozwolonych akcji, zobacz [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md). Aby uzyskać więcej informacji na temat kontroli dostępu na podstawie ról, zobacz temat [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md) (Kontrola dostępu na podstawie ról na platformie Azure). 

W niektórych przypadkach ma toorun kod lub skrypt, który uzyskuje dostęp do zasobów, ale nie chcesz toorun go w ramach poświadczeń użytkownika. Zamiast tego chcesz toocreate tożsamości o nazwie Usługa główna aplikacji hello i przypisz hello odpowiednią rolę dla nazwy głównej usługi hello. Menedżer zasobów pozwala toocreate poświadczenia dla aplikacji hello i programowo uwierzytelniania aplikacji hello. toolearn o tworzeniu nazwy główne usług, zobacz jedną z następujących tematach:

* [Użyj programu Azure PowerShell toocreate zasobów tooaccess głównej usługi](resource-group-authenticate-service-principal.md)
* [Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi](resource-group-authenticate-service-principal-cli.md)
* [Użyj portalu toocreate aplikacji usługi Azure Active Directory i nazwy głównej usługi, który ma dostęp do zasobów](resource-group-create-service-principal-portal.md)

Można również jawnie zablokować kluczowych zasobów tooprevent użytkownikom ich usuwanie i modyfikowanie. Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).

## <a name="activity-logs"></a>Dzienniki aktywności
Usługa Resource Manager rejestruje wszystkie operacje służące do tworzenia, modyfikowania lub usuwania zasobu. Możesz użyć toofind Dzienniki aktywności hello wystąpił błąd podczas rozwiązywania problemu lub toomonitor jak użytkownik w organizacji zmienić zasobu. toosee hello dzienników, wybierz **Dzienniki aktywności** w hello **ustawienia** bloku grupy zasobów. Dzienniki hello można filtrować według wielu różnych wartości w tym która operacja hello zainicjowanej przez użytkownika. Uzyskać informacji na temat pracy z dziennikami działania hello, zobacz [toomanage Azure Dzienniki aktywności widok zasobów](resource-group-audit.md).

## <a name="customized-policies"></a>Zasady niestandardowe
Menedżer zasobów pozwala toocreate dostosowane zasady zarządzania zasobami. Witaj typów można tworzyć zasady mogą obejmować różnych scenariuszy. Można wymusić konwencję nazewnictwa zasobów, ograniczyć typy i wystąpienia zasobów, które można wdrożyć, lub wprowadzić ograniczenia dotyczące regionów, które mogą hostować dany typ zasobu. Możesz wymagać wartości tagów na zasoby tooorganize rozliczeń według działów. Tworzenie zasad toohelp obniżenie kosztów i zachowanie spójności w ramach subskrypcji. 

Zasady są definiowane za pomocą pliku JSON, a następnie stosowane w ramach subskrypcji lub grupy zasobów. Zasady są inne niż kontroli dostępu opartej na rolach, ponieważ są one stosowane tooresource typów.

Witaj poniższy przykład przedstawia zasady, które powodują tag spójności, określając, że wszystkie zasoby obejmują costCenter tag.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Można utworzyć o wiele więcej typów zasad. Aby uzyskać więcej informacji, zobacz [zasady toomanage zasobów i kontroli dostępu](resource-manager-policy.md).

## <a name="sdks"></a>Zestawy SDK
Zestawy Azure SDK są dostępne dla wielu języków i platform. Implementacje dla poszczególnych języków są dostępne za pośrednictwem menedżera pakietów danego ekosystemu oraz w usłudze GitHub.

Oto nasze repozytoria zestawów SDK typu open source. Zachęcamy do wysyłania opinii, zgłaszania problemów i przesyłania żądań ściągnięcia.

* [Zestaw Azure SDK dla platformy .NET](https://github.com/Azure/azure-sdk-for-net)
* [Biblioteki zarządzania Azure dla języka Java](https://github.com/Azure/azure-sdk-for-java)
* [Zestaw Azure SDK dla środowiska Node.js](https://github.com/Azure/azure-sdk-for-node)
* [Zestaw Azure SDK dla środowiska PHP](https://github.com/Azure/azure-sdk-for-php)
* [Zestaw Azure SDK dla środowiska Python](https://github.com/Azure/azure-sdk-for-python)
* [Zestaw Azure SDK dla środowiska Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Aby uzyskać informacje na temat korzystania z tych języków do obsługi zasobów, zobacz:

* [Azure dla deweloperów platformy .NET](/dotnet/azure/?view=azure-dotnet)
* [Azure dla deweloperów języka Java](/java/azure/)
* [Azure dla deweloperów oprogramowania Node.js](/nodejs/azure/)
* [Azure dla deweloperów języka Python](/python/azure/)

> [!NOTE]
> Jeśli hello zestawu SDK nie hello wymagane funkcje, należy także wywołać toohello [interfejsu API REST Azure](https://docs.microsoft.com/rest/api/resources/) bezpośrednio.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Aby tooworking krótkie wprowadzenie z szablonami, zobacz [Eksportowanie szablonu usługi Azure Resource Manager z istniejących zasobów](resource-manager-export-template.md).
* Bardziej szczegółowe instrukcje dotyczące tworzenia szablonu zawiera artykuł [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).
* Funkcje hello toounderstand można użyć w szablonie, zobacz [funkcje szablonów](resource-group-template-functions.md)
* Aby uzyskać informacje dotyczące korzystania z programu Visual Studio w połączeniu z usługą Resource Manager, zobacz [Tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Oto film z omówieniem tego zagadnienia:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
