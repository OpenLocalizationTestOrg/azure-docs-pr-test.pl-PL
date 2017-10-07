---
title: "role niestandardowe kontroli dostępu opartej na rolach aaaCreate i przypisać toointernal i użytkowników zewnętrznych na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przypisz role RBAC niestandardowe utworzone przy użyciu programu PowerShell i interfejsu wiersza polecenia dla użytkowników wewnętrznych i zewnętrznych"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Wprowadzenie dotyczących kontroli dostępu opartej na rolach

Kontrola dostępu oparta na rolach to Azure portalu tylko funkcja umożliwia hello właściciele subskrypcji tooassign szczegółowego ról tooother użytkownikom, którzy mogą zarządzać zasobów dla określonych zakresów w swoim środowisku.

RBAC umożliwia lepsze zarządzanie zabezpieczeniami dla dużych organizacji oraz dla małych i średnich firmach praca z zewnętrznym współpracownikom, dostawców lub freelancers, które wymagają dostępu do zasobów toospecific w danym środowisku, ale niekoniecznie toohello całej infrastruktury lub w dowolnej zakresy związanych z rozliczeniami. RBAC zapewnia elastyczność hello będący właścicielem jedną subskrypcją platformy Azure zarządza hello konta administratora (usługi roli administrator na poziomie subskrypcji) i ma wiele toowork zaproszonych użytkowników w obszarze hello tej samej subskrypcji ale bez żadnych administracyjnych prawa dla niego. Zarządzanie i rozliczeń funkcji RBAC hello okaże się toobe czas i zarządzanie wydajne opcji korzystania z funkcji Azure w różnych scenariuszach.

## <a name="prerequisites"></a>Wymagania wstępne
Przy użyciu funkcji RBAC w hello środowiska platformy Azure wymaga:

* O autonomiczny subskrypcji platformy Azure przypisane toohello użytkownika jako właściciela (rola subskrypcji)
* Ma rolę właściciela hello hello subskrypcji platformy Azure
* Ma dostęp toohello [portalu Azure](https://portal.azure.com)
* Upewnij się, że hello toohave następujących dostawców zasobów zarejestrowany dla subskrypcji użytkownika hello: **Microsoft.Authorization**. Aby uzyskać więcej informacji dotyczących sposobu tooregister hello dostawców zasobów, zobacz [dostawców usługi Resource Manager, regiony, wersje interfejsu API i schematów](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Licencje usługi Azure Active Directory lub subskrypcji usługi Office 365 (na przykład: dostęp do usługi Active Directory tooAzure) pobranego z portalu nie jakości przy użyciu funkcji RBAC hello usługi Office 365.

## <a name="how-can-rbac-be-used"></a>Jak można użyć RBAC
RBAC można zastosować na trzy różne zakresy na platformie Azure. Z hello najwyższy toohello zakres jednej najniższy są następujące:

* Subskrypcja (najwyższy)
* Grupa zasobów
* Zakres zasobów (hello najniższy poziom dostępu oferty uprawnienia docelowego zakresu poszczególnych zasobów platformy Azure tooan)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Przypisz role RBAC w zakresie subskrypcji hello
Istnieją dwie typowe przykłady dotyczące RBAC jest używana (między innymi):

* Użytkowników zewnętrznych z hello organizacji (nie jest częścią dzierżawy usługi Azure Active Directory użytkownika administratora hello) zaproszenie toomanage niektórych zasobów lub subskrypcji całego hello
* Praca z użytkownikami w organizacji hello (są one częścią hello użytkownik dzierżawy usługi Azure Active Directory), ale należy do różnych zespołów lub grup, które wymagają dostępu szczegółowe albo toohello całej subskrypcji lub grupy zasobów toocertain lub zasobu zakresów w hello środowisko

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Udziel dostępu na poziomie subskrypcji dla użytkownika poza usługą Azure Active Directory
Role RBAC może zostać przydzielony tylko przez **właścicieli** hello subskrypcji w związku z tym hello administrator musi być zalogowany z nazwą użytkownika, które tej roli wstępnie przypisany lub został utworzony hello subskrypcji platformy Azure.

Z hello portalu Azure po zalogować jako administrator, wybierz pozycję "Subskrypcje" i wybierz opcję hello żądana jeden.
![bloku subskrypcji w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) domyślnie, jeśli administrator hello kupiła hello subskrypcji platformy Azure, hello użytkownika będzie wyświetlany jako **administrator konta**, to jest rola subskrypcji hello. Więcej szczegółów na powitania ról subskrypcji platformy Azure, zobacz [Dodawanie lub zmienianie role administratora platformy Azure, zarządzających hello subskrypcji lub usługi](/billing/billing-add-change-azure-subscription-administrator.md).

W tym przykładzie hello użytkownika "alflanigan@outlook.com" hello jest **właściciela** z hello "Bezpłatnej wersji próbnej" subskrypcji w hello AAD dzierżawy "Dzierżawy Azure Default". Ponieważ ten użytkownik jest twórca hello hello subskrypcji platformy Azure z hello początkowa Account Microsoft "Outlook" (Account Microsoft = programu Outlook, Live itp.) będzie domyślna nazwa domeny dla wszystkich innych użytkowników dodane w tej dzierżawie powitalnych **"@alflaniganuoutlook.onmicrosoft.com"**. Zgodnie z projektem hello składni nowej domeny hello jest tworzony przez zestawienie hello nazwy użytkownika i nazwy domen hello użytkownika, który utworzył hello dzierżawy oraz dodawania rozszerzenia hello **". onmicrosoft.com"**.
Ponadto użytkownicy mogą logowania z niestandardowej nazwy domeny w dzierżawie powitalnych po dodaniu i weryfikowanie jego dla nowej dzierżawy hello. Aby uzyskać więcej informacji na tooverify niestandardowej nazwy domeny w dzierżawie usługi Azure Active Directory, zobacz temat [Dodaj katalog tooyour nazwy domeny niestandardowej](/active-directory/active-directory-add-domain).

W tym przykładzie katalog hello "domyślna dzierżawa usługi Azure" zawiera tylko użytkownicy z nazwą domeny hello "@alflanigan.onmicrosoft.com".

Po wybraniu subskrypcji hello, musisz kliknąć przycisk Administrator hello **kontroli dostępu (IAM)** , a następnie **dodania roli**.





![Funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![Dodaj nowego użytkownika w funkcja IAM kontroli dostępu w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

Witaj następnym krokiem jest toobe roli hello tooselect przypisane i hello użytkownika, którego hello RBAC roli zostanie przypisana do. W hello **roli** listy rozwijanej menu hello administratora użytkownik widzi tylko hello wbudowanych RBAC role, które są dostępne w systemie Azure. Aby uzyskać bardziej szczegółowe wyjaśnienia dotyczące poszczególnych ról i ich zakresy możliwe do przypisania, zobacz [wbudowanych ról dla kontroli dostępu](/active-directory/role-based-access-built-in-roles.md).

Witaj administrator musi następnie tooadd hello adres e-mail użytkownika zewnętrznego hello. Hello oczekuje się, że zachowanie jest hello użytkownika zewnętrznego toonot będą wyświetlane w hello istniejącej dzierżawy. Po zaproszono hello użytkownika zewnętrznego, on będą widoczne w obszarze **subskrypcji > kontroli dostępu (IAM)** wszystkim użytkownikom bieżącego hello, które są obecnie przypisane roli RBAC na powitania zakres subskrypcji.





![Dodaj rolę RBAC toonew uprawnień](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![Lista ról RBAC na poziomie subskrypcji](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

Użytkownik Hello "chessercarlton@gmail.com" został zaproszony toobe **właściciela** dla subskrypcji "Bezpłatnej wersji próbnej" hello. Po wysłaniu hello zaproszenia, hello zewnętrznych użytkownik otrzyma wiadomość e-mail z potwierdzeniem z link aktywacji.
![wiadomość e-mail z zaproszeniem dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Stanowi organizacji toohello zewnętrznych, hello nowego użytkownika nie ma żadnych istniejących atrybutów w katalogu "Dzierżawy Azure Default" hello. Będzie można utworzyć po toobe zgody rejestrowane w katalogu hello, który jest skojarzony z subskrypcją hello, który został przydzielony do roli użytkownika zewnętrznego hello.





![wiadomość e-mail zaproszenia dla roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

Użytkownik zewnętrzny Hello pokazuje w hello dzierżawy usługi Azure Active Directory od teraz jako użytkownik zewnętrzny i to można wyświetlić zarówno w hello portalu Azure, jak i w portalu klasycznym hello.





![Użytkownicy portalu Azure usługi active directory bloku azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![Użytkownicy bloku usługi azure active directory klasycznego portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

W hello **użytkowników** widoku w obu portalach użytkowników zewnętrznych hello mogą być rozpoznawane przez:

* Wpisz inną ikonę Hello hello portalu Azure
* Witaj różnych sourcing punktu w portalu klasycznym hello

Jednak udzielanie **właściciela** lub **współautora** tooan dostępu użytkownika zewnętrznego w hello **subskrypcji** zakresu, nie zezwala na powitania dostępu toohello administratora katalogu użytkownika, o ile hello **administratora globalnego** pozwala. W ich właściwości użytkownika hello, hello **typ użytkownika** mającego dwóch parametrów typowych, **elementu członkowskiego** i **gościa** mogą zostać zidentyfikowane. Element członkowski jest użytkownik, który jest zarejestrowany w katalogu hello podczas Gość jest katalogiem toohello zaproszonych użytkowników ze źródła zewnętrznego. Aby uzyskać więcej informacji, zobacz [jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Upewnij się, że po wprowadzeniu poświadczeń hello w portalu hello, użytkownik zewnętrzny hello wybiera poprawny katalog hello toosign w celu. Hello tego samego użytkownika ma katalogów toomultiple dostępu i można wybrać jedną z nich, klikając nazwę użytkownika hello w hello góry po prawej stronie w portalu Azure hello i następnie wybierz z listy rozwijanej hello hello odpowiedniego katalogu.

Będąc gościa w katalogu hello użytkownika zewnętrznego hello można zarządzać wszystkie zasoby hello subskrypcji platformy Azure, ale nie można uzyskać dostępu do katalogu hello.





![dostęp do portalu Azure tooazure ograniczone usługi active directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory i subskrypcji platformy Azure nie ma relacji relacji nadrzędny podrzędny, takich jak innych zasobów platformy Azure (na przykład: maszyn wirtualnych, sieci wirtualnych, aplikacje sieci web, magazynu itp.) z subskrypcją platformy Azure. Wszystkie ostatnie hello jest tworzony, zarządzane i rozliczane w ramach subskrypcji platformy Azure, gdy subskrypcja platformy Azure jest używana toomanage hello dostępu tooan katalogu platformy Azure. Aby uzyskać więcej informacji, zobacz [jak Azure subskrypcji jest powiązane tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Ze wszystkich hello wbudowanych RBAC ról **właściciela** i **współautora** oferują pełnego dostępu do zasobów tooall w środowisku hello, hello różnica podpisu współautora nie można utworzyć i usuwania nowych Role RBAC. Witaj innych wbudowanych ról, takich jak **współautora maszyny wirtualnej** oferują dostęp do pełnego zarządzania tylko zasoby toohello wskazywanym przez nazwę hello, niezależnie od hello **grupy zasobów** ich tworzenia do.

Przypisywanie hello wbudowanych RBAC roli **współautora maszyny wirtualnej** na poziomie subskrypcji, oznacza tej roli hello przypisane przez użytkownika hello:

* Można wyświetlić wszystkich maszyn wirtualnych niezależnie od ich wdrożenia daty i hello grup zasobów, które są częścią
* Zawiera maszyny wirtualne toohello dostęp do pełnego zarządzania w ramach subskrypcji hello
* Nie można wyświetlić inne typy zasobów w subskrypcji hello
* Nie można wykonać operacji zmiany z punktu widzenia rozliczeń

> [!NOTE]
> RBAC jest funkcją Azure tylko portalu, nie udziela dostępu toohello klasycznego portalu.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Przypisz wbudowanych RBAC roli tooan użytkownika zewnętrznego
Do innego scenariusza w teście hello użytkownika zewnętrznego "alflanigan@gmail.com" zostanie dodany jako **Współautor·maszyny·wirtualnej**.




![wbudowana Rola współautora maszyny wirtualnej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

Hello jest ich normalne zachowanie dla tego użytkownika zewnętrznego z tą rolą wbudowanych jest toosee i zarządzaj nimi tylko dla maszyn wirtualnych i ich sąsiadujących ze sobą Menedżer zasobów tylko zasoby niezbędne podczas wdrażania. Zgodnie z projektem, te role ograniczone oferować dostęp tylko zasoby odpowiedniego tootheir utworzone w portalu Azure hello, niezależnie od tego niektóre nadal można wdrożyć w hello również klasyczny portal (na przykład: maszyn wirtualnych).





![Omówienie roli współautora maszyny wirtualnej w portalu azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Udziel dostępu na poziomie subskrypcji dla użytkownika w hello sam katalogu
przepływ procesu Hello jest identyczne tooadding użytkownika zewnętrznego, zarówno z hello perspektywy udzielającym hello RBAC rolę administratora, a także hello użytkownika zostanie im przyznany dostęp toohello roli. Hello różnicą jest ten użytkownik hello zaproszenie nie będą otrzymywać żadnych zaproszeń do skorzystania z poczty e-mail jako wszystkie zakresy zasobów hello w ramach subskrypcji hello będą dostępne na pulpicie nawigacyjnym powitania po zalogowaniu się.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Przypisz role RBAC w zakresie grupy zasobów hello
Przypisywanie roli RBAC **grupy zasobów** zakres ma taki sam proces przypisywania roli hello na poziomie subskrypcji hello, dla obu typów użytkownicy — zewnętrznym lub wewnętrznym (część hello tego samego katalogu). Witaj użytkowników, którzy mają przypisaną rolę RBAC hello jest toosee w swoim środowisku tylko grupy zasobów hello z przypisanym dostępu z hello **grup zasobów** ikonę w hello portalu Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Przypisz role RBAC w zakresie zasobów hello
Przypisywanie roli RBAC w zakresie zasobów na platformie Azure mają taki sam proces przypisywania roli hello na poziomie subskrypcji hello lub na poziomie grupy zasobów hello, następujące hello sam przepływ pracy oba scenariusze. Ponownie hello użytkowników, którzy mają przypisaną rolę RBAC hello widzą tylko elementy hello czy przypisano dostęp do obu hello w **wszystkie zasoby** kartę lub bezpośrednio w ich pulpitu nawigacyjnego.

Istotnym elementem do RBAC zarówno w zakresie grupy zasobów lub zasobów zakresie dotyczy hello użytkowników toomake toohello się, że toosign w poprawnym katalogu.





![katalog logowania w portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Przypisz role RBAC dla grupy usługi Azure Active Directory
Wszystkie scenariusze hello przy użyciu funkcji RBAC na trzy różne zakresy hello w uprawnień hello platformy Azure, zarządzanie, wdrażanie i administrowanie różnych zasobów jako przypisany użytkownik bez hello konieczne Zarządzanie subskrypcją osobistych. Dla subskrypcji, grupy zasobów lub zasobów zakresu przypisano rolę RBAC hello niezależnie od tego, wszystkie zasoby hello utworzone dalej przez użytkowników hello przypisane są rozliczane w ramach subskrypcji platformy Azure z jednego hello której hello użytkownicy mają dostęp do. Dzięki temu hello użytkowników, którzy mają rozliczeń uprawnień administratora dla całej subskrypcji platformy Azure ma pełny przegląd zużycia hello, niezależnie od tego, kto jest zarządzanie zasobami hello.

W przypadku większych organizacji role RBAC można zastosować w hello taki sam sposób dla grup usługi Azure Active Directory uwzględnieniu perspektywy hello tego użytkownika administracyjnego hello potrzebuje dostępu szczegółowego hello toogrant dla zespołów lub całego działów, indywidualnie dla każdego użytkownika, w związku z tym biorąc pod uwagę go jako bardzo czas i zarządzanie wydajne opcji. tooillustrate ten przykład, hello **współautora** dodano rolę tooone grup hello w dzierżawie powitalnych na poziomie subskrypcji hello.





![Dodaj rolę RBAC dla grup usługi AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Te grupy są grupami zabezpieczeń, które są udostępniane i zarządzane tylko w ramach usługi Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Utwórz niestandardowe Obsługa tooopen roli RBAC żądania przy użyciu programu PowerShell
określone poziomy uprawnień na podstawie dostępnych zasobów hello w środowisku hello upewnij się, Hello wbudowanych RBAC role, które są dostępne w systemie Azure. Jednak jeśli żadna z tych ról potrzeb użytkownika administratora hello, jest dostępny hello opcja toolimit jeszcze więcej, tworząc niestandardowe role RBAC.

Tworzenie niestandardowych ról RBAC wymaga jednej wbudowanej roli tootake, edytować, a następnie zaimportuj go ponownie w środowisku hello. Hello pobierania i przekazywanie roli hello są zarządzane przy użyciu programu PowerShell lub interfejsu wiersza polecenia.

Jest ważne toounderstand hello wymagania wstępne tworzenie niestandardowej roli zabezpieczeń, które można przyznać szczegółowego dostęp na poziomie subskrypcji hello i również umożliwić hello zaproszonych użytkowników hello elastyczność otwarcia żądania pomocy technicznej.

Dla tej roli wbudowanych hello przykład **czytnika** co pozwala użytkownikom dostępu tooview zasobów hello wszystkich zakresów ale nie tooedit je lub utworzyć nowe został dostosowany tooallow hello użytkownika hello możliwością otwarcia żądania pomocy technicznej.

Witaj pierwszą akcją eksportowania hello **czytnika** roli toobe musi ukończyć w programie PowerShell został uruchomiony z podwyższonym poziomem uprawnień administratora.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Zrzut ekranu programu PowerShell dla roli czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Następnie należy tooextract hello JSON szablonu hello roli.





![Szablon JSON dla niestandardowej roli zabezpieczeń czytnika RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Typowa rola RBAC składa się z trzech głównych sekcji, **akcje**, **NotActions** i **AssignableScopes**.

W hello **akcji** sekcji są wyświetlane wszystkie hello dozwolonych operacji dla tej roli. Jest ważne toounderstand, każda akcja przypisany od dostawcy zasobów. W takim przypadku służący do tworzenia hello biletów pomocy technicznej **Microsoft.Support** musi być wymieniona dostawcy zasobów.

toosee stanie toobe hello wszystkich dostawców zasobów dostępnych i zarejestrowanych w ramach subskrypcji, możesz użyć programu PowerShell.
```
Get-AzureRMResourceProvider

```
Ponadto możesz sprawdzić hello wszystkich hello dostępne PowerShell polecenia cmdlet toomanage hello dostawców zasobów.
    ![Zrzut ekranu programu PowerShell do zarządzania dostawcy zasobów](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

Witaj wszystkie akcje dla konkretnej roli RBAC zasobów dostawcy są wymienione w sekcji hello toorestrict **NotActions**.
Ostatnio jest to konieczne, że tej roli RBAC hello zawiera jawne subskrypcji hello identyfikatorów, w którym została użyta. Witaj identyfikatorów subskrypcji są wyświetlane w obszarze hello **AssignableScopes**, w przeciwnym razie użytkownik nie będzie można tooimport hello roli w ramach subskrypcji.

Po utworzeniu i dostosowywanie hello RBAC roli, musi on toobe importowanych hello wstecz środowiska.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

W tym przykładzie hello niestandardową nazwę dla tej roli RBAC jest "Czytnika obsługi biletów poziom dostępu" stosowanie wszystko hello tooview użytkownika w subskrypcji hello, a także tooopen żądania pomocy technicznej.

> [!NOTE]
> Witaj tylko dwa wbudowane role RBAC, umożliwiając akcji hello otwarcia żądania pomocy technicznej są **właściciela** i **współautora**. Dla użytkownika toobe stanie tooopen żądania pomocy technicznej on musi posiadać rolę RBAC tylko w zakresie subskrypcji hello, ponieważ wszystkie żądania pomocy technicznej są tworzone na podstawie subskrypcji platformy Azure.

Ta nowa rola niestandardowych przypisano tooan użytkownika z hello tego samego katalogu.





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC zaimportowana hello portalu Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![Zrzut ekranu przedstawiający przypisywanie niestandardowych toouser roli RBAC importowanych w hello tym samym katalogu](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![Zrzut ekranu przedstawiający uprawnienia niestandardowe importowanych roli RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

przykład Witaj został dalsze szczegółowe tooemphasize limitów hello tę rolę niestandardową RBAC w następujący sposób:
* Można tworzyć nowe żądania pomocy technicznej
* Nie można utworzyć nowe zakresy zasobów (na przykład: maszyny wirtualnej)
* Nie można utworzyć nowej grupy zasobów





![Zrzut ekranu przedstawiający niestandardową rolę RBAC tworzenia żądań obsługi](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC nie jest w stanie toocreate maszyny wirtualne](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![Zrzut ekranu przedstawiający niestandardowej roli zabezpieczeń RBAC nie jest w stanie toocreate RGs nowy](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Utwórz niestandardowe Obsługa tooopen roli RBAC żądań przy użyciu wiersza polecenia platformy Azure
Uruchomiony na komputerze Mac i bez potrzeby dostępu tooPowerShell, Azure CLI jest hello toogo sposób.

toocreate kroki Hello niestandardowej roli zabezpieczeń są powitalne takie same, z wyjątkiem wyłącznie hello, że przy użyciu interfejsu wiersza polecenia hello roli nie można pobrać szablonu JSON, ale można je wyświetlać w hello interfejsu wiersza polecenia.

W tym przykładzie wybrano I role wbudowane hello **czytnika kopii zapasowej**.

```

azure role show "backup reader" --json

```





![Pokaż zrzut ekranu interfejsu wiersza polecenia rolę czytelnika kopii zapasowej](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Edytowanie hello roli w programie Visual Studio po skopiowaniu hello ich właściwości w szablonie JSON, hello **Microsoft.Support** dostawca zasobów został dodany w hello **akcje** sekcje, tak aby mogli otworzyć tego użytkownika żądania pomocy technicznej, pozostawiając toobe czytnik hello magazynów kopii zapasowych. Ponownie jest identyfikator subskrypcji hello niezbędne tooadd gdy ta rola będzie używany w hello **AssignableScopes** sekcji.

```

azure role create --inputfile <path>

```





![Zrzut ekranu interfejsu wiersza polecenia importowania niestandardowej roli zabezpieczeń RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

Nowa rola Hello jest teraz dostępna w portalu Azure hello i procesu assignation hello jest hello takie same jak w poprzednich przykładach hello.





![Azure portalu zrzut ekranu przedstawiający niestandardową rolę RBAC utworzone za pomocą interfejsu wiersza polecenia 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

Począwszy od hello 2017 najnowszej kompilacji, hello powłoki chmury Azure jest ogólnie dostępna. Powłoka chmury Azure to tooIDE dopełnienia i hello portalu Azure. Z tą usługą Pobierz powłoką bazujące na przeglądarce, która jest uwierzytelniane i hostowanej na platformie Azure i można go użyć zamiast interfejsu wiersza polecenia na komputerze jest zainstalowany.





![Powłoka w chmurze Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
