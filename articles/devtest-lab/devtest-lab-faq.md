---
title: "aaaAzure DevTest Labs — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Znajdź odpowiedzi na pytania dotyczące usługi Azure DevTest Labs toocommon"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Azure DevTest Labs — często zadawane pytania
Ten artykuł zawiera odpowiedzi na niektóre hello często zadawane pytania dotyczące usługi Azure DevTest Labs.

**Ogólne**
## <a name="what-if-my-question-isnt-answered-here"></a>Co zrobić, jeśli mojego pytania nie ma odpowiedzi w tym miejscu?
Jeśli Twoje pytanie nie ma na liście, Daj nam znać, możemy pomóc Ci znaleźć odpowiedź.

* Opublikuj pytanie na powitania [wątku usługi Disqus](#comments) na końcu hello tych często zadawanych PYTAŃ i kontaktowaniu się z team pamięć podręczna Azure hello i innymi członkami społeczności informacje w tym artykule.
* tooreach większej liczby osób, Zadaj pytanie na powitania [forum Azure DevTest Labs w witrynie MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)i skontaktuj się z hello Azure DevTest Labs zespołu i innych członków społeczności hello.
* toomake żądanie funkcji przesyłania toohello Twojego żądania i pomysły [Azure DevTest Labs User Voice](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Dlaczego warto używać usługi Azure DevTest Labs?
Azure DevTest Labs można zapisać Twojego zespołu czas i pieniądze. Deweloperzy można tworzyć własne środowisk przy użyciu kilku różnych podstaw i używać artefaktów tooquickly wdrażania i konfigurowania aplikacji. Przy użyciu niestandardowych obrazów i formuły, maszyny wirtualne można zapisać jako szablon i łatwo odtworzyć. Ponadto labs oferuje kilka można skonfigurować zasady, które pozwalają administratorom laboratorium tooreduce odpady i zarządzać środowiskami zespołu. Zasady te obejmują automatyczne zamykanie, próg koszt maksymalną maszyn wirtualnych dla użytkowników i maksymalne rozmiary maszyny Wirtualnej. Aby uzyskać szczegółowe informacje o usłudze Azure DevTest Labs, przeczytaj hello [omówienie](devtest-lab-overview.md) lub hello czujki [wprowadzenie wideo](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>Co to znaczy "obaw, Samoobsługowe"?
"Bez obaw samoobsługi" oznacza, że deweloperów i testerów utworzyć środowiska własnych potrzeb, a administratorzy mają hello bezpieczeństwa wiedząc, że Azure DevTest Labs pomaga zminimalizować odpady i kontrolować koszty. Administratorzy mogą określić rozmiarów maszyn wirtualnych, które są dozwolone, hello maksymalną liczbę maszyn wirtualnych, a po maszyny wirtualne są uruchomione i zamknąć. Azure DevTest Labs również umożliwia łatwe toomonitor kosztów i Ustaw alerty toostay wiedzieć, jak są używane zasoby w laboratorium hello.

## <a name="how-can-i-use-azure-devtest-labs"></a>Jak używać usługi Azure DevTest Labs?
Azure DevTest Labs przydaje się w dowolnym momencie wymagają deweloperów lub środowisk testowania i chcesz tooreproduce je szybko i/lub zarządzanie nimi kosztów zapisywania zasad.

Poniżej przedstawiono kilka scenariuszy, używające klientów w usłudze Azure DevTest Labs dla:

* Zarządzanie środowiskach programistycznych i testowych w jednym miejscu, przy użyciu zasad tooreduce kosztów i niestandardowych obrazów tooshare kompilacje między elementami zespołu hello.
* Projektowanie aplikacji przy użyciu niestandardowych obrazów toosave hello dysku stanu etapach rozwoju hello.
* Śledzenie kosztów hello w tooprogress relacji.
* Tworzenie środowisk testowych masowego do testowania zapewnienia jakości.
* Przy użyciu artefaktów i formuły tooeasily skonfigurować i odtworzyć aplikacji w różnych środowiskach.
* Dystrybucja maszyn wirtualnych dla hackathons (programistycznych lub test współpracy), a następnie łatwo cofnąć udostępnienie ich podczas kończenia hello zdarzeń.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Jak m opłaty naliczane za Azure DevTest Labs?
Azure DevTest Labs jest darmowa, co oznacza tworzenie labs i konfigurowania zasad hello, szablonów i artefakty jest bezpłatna. Płacisz tylko za hello Azure zasoby używane w ramach labs, na przykład maszyny wirtualne, konta magazynu i sieci wirtualnych. Aby uzyskać więcej informacji na powitania koszt zasobów laboratorium, przeczytaj o [cennik usługi Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Bezpieczeństwo**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Co to są hello różnymi poziomami zabezpieczeń w usłudze Azure DevTest Labs?
Dostęp zabezpieczeń jest określany przez [based kontroli dostępu (RBAC)](../active-directory/role-based-access-built-in-roles.md). toounderstand sposób uzyskiwania dostępu do działania, ale toounderstand hello różnice między uprawnienia roli i zakres zgodnie z definicją RBAC.

* **Uprawnienie** -uprawnienie jest tooa zdefiniowanych dostępu do określonej akcji. Uprawnienia można na przykład maszyny wirtualne tooall dostęp do odczytu.
* **Rola** -Rola to zestaw uprawnień, które mogą być grupowane i przypisany użytkownik tooa. Na przykład "właściciel subskrypcji" ma dostęp do zasobów tooall w ramach subskrypcji.
* **Zakres** -zakres jest poziom w hierarchii hello zasobów platformy Azure. Na przykład zakres można grupę zasobów lub pojedynczy laboratorium lub hello całej subskrypcji.

W zakresie hello Azure DevTest Labs, istnieją dwa typy uprawnień użytkownika toodefine ról: laboratorium właściciela i użytkownika laboratorium.

* **Właściciela laboratorium** -właściciela laboratorium ma hello dostęp do tooany zasobów w ramach laboratorium hello. W związku z tym ich można modyfikować zasady, zapisywania i odczytywania żadnej maszyny wirtualnej, zmień hello sieci wirtualnej, a itd.
* **Użytkownik laboratorium** — użytkownik laboratorium można wyświetlić wszystkie zasoby laboratorium, takich jak maszyny wirtualne, zasady i sieci wirtualne, ale nie mogą modyfikować zasady lub żadnych maszyn wirtualnych utworzonych przez innych użytkowników. Możliwe jest również możliwe toocreate role niestandardowe w usłudze Azure DevTest Labs i Dowiedz się jak toodo w artykule hello [przyznawanie uprawnień użytkownikom zasad laboratorium toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Ponieważ zakresy są hierarchiczne, jeśli użytkownik ma uprawnienia w zakresie niektórych, automatycznie otrzymują tych uprawnień w zakresie niższego poziomu, co razem. Na przykład jeśli użytkownik jest przypisany toohello roli właściciela subskrypcji, następnie mają dostęp do zasobów tooall w ramach subskrypcji. Te zasoby obejmują wszystkie maszyny wirtualne, wszystkie sieci wirtualne i laboratoriów wszystkie. W związku z tym właściciela subskrypcji automatycznie dziedziczy hello roli właściciela laboratorium. Jednak hello przeciwną nie jest prawdziwe. Właściciela laboratorium ma laboratorium tooa dostępu, które jest zakresem niższym niż poziom subskrypcji hello. W związku z tym właściciela laboratorium nie jest możliwe toosee maszyn wirtualnych lub sieci wirtualne lub wszystkie zasoby, które znajdują się poza hello laboratorium.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Jak utworzyć rolę tooallow użytkowników tooperform określonego zadania?
Kompleksowe artykuł o jak role niestandardowe toocreate i przypisz uprawnienia toothat roli można znaleźć tutaj. Poniżej przedstawiono przykładowy skrypt, który tworzy rolę hello "DevTest Labs zaawansowane użytkownik", który ma uprawnienia toostart i zatrzymanie wszystkich maszyn wirtualnych w laboratorium hello:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Integracja elementu konfiguracji/CD i automatyzacji**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>Czy Azure DevTest Labs można zintegrować z łańcuchem narzędzi Moje CI/CD?
Jeśli używasz programu VSTS [rozszerzenie Azure DevTest Labs zadania](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) pozwala tooautomate publikowania w usłudze Azure DevTest Labs w potoku. Witaj używa tego rozszerzenia, należą:

* Tworzenie i wdrażanie maszyny Wirtualnej automatycznie i konfigurowanie go z ostatniej kompilacji hello przy użyciu zadania kopiowania plików na platformę Azure lub programu PowerShell programu VSTS.
* Automatycznie przechwytywania stanu hello maszyny wirtualnej po zakończeniu testowania tooreproduce usterki na hello tej samej maszyny Wirtualnej w celu dokładniejszego zbadania.
* Usuwanie hello VM końcu hello hello Zwolnij potoku, gdy nie jest już potrzebne.

Witaj następujących wpisach w blogu zawiera wskazówki i informacje o przy użyciu rozszerzenia programu VSTS hello:

* [Azure DevTest Labs — rozszerzenie programu VSTS](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Wdrożenie nowej maszyny Wirtualnej w istniejących AzureDevTestLab z programu VSTS](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [Za pomocą zarządzania zleceniami programu VSTS dla tooAzureDevTestLabs ciągłe wdrażanie](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Dla innych toolchains CI/CD hello wszystkie wymienione wcześniej scenariusze, które można osiągnąć za pomocą hello rozszerzenie zadania programu VSTS podobnie uzyskuje się poprzez wdrożenie [szablonów usługi Azure Resource Manager](https://aka.ms/dtlquickstarttemplate) przy użyciu [ Polecenia cmdlet programu PowerShell systemu Azure](../azure-resource-manager/resource-group-template-deploy.md) i [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). Można również użyć [interfejsów API REST dla DevTest Labs](http://aka.ms/dtlrestapis) toointegrate z z łańcuchem narzędzi.  


**Virtual Machines**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Dlaczego nie widzę niektórych maszyn wirtualnych w bloku maszyny wirtualne Azure hello, wyświetlanego w usłudze Azure DevTest Labs
Po utworzeniu maszyny Wirtualnej w usłudze Azure DevTest Labs uprawnienia są podane tooaccess tej maszyny Wirtualnej. Są tooview może ona zarówno w bloku labs hello i hello **maszyn wirtualnych** bloku. Użytkownicy w roli DevTest Labs hello widzą wszystkie maszyny wirtualne utworzone w laboratorium hello za pośrednictwem hello laboratorium **wszystkich maszyn wirtualnych** bloku. Jednak użytkowników w roli DevTest Labs hello nie otrzymują automatycznie zasobów tooVM dostęp do odczytu, utworzonych przez innych użytkowników. W związku z tym te maszyny wirtualne nie są wyświetlane w hello **maszyn wirtualnych** bloku.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Jaka jest różnica hello niestandardowych obrazów i formuły?
Obraz niestandardowy jest wirtualnego dysku twardego (wirtualny dysk twardy), formułę jest obraz, który można skonfigurować dodatkowe ustawienia, które można zapisywać i można odtworzyć. Obraz niestandardowy może być tooquickly utworzyć kilku środowiskach z hello takiego samego obrazu podstawowego, modyfikować. Formuła może być lepsze, jeśli konfiguracja hello tooreproduce hello najnowsze usługi bits, wirtualnej podsieci lub określonego rozmiaru maszyny wirtualnej. Aby uzyskać szczegółowe informacje, zobacz artykuł hello, [porównanie niestandardowych obrazów i formuły w usłudze DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Jak utworzyć wiele maszyn wirtualnych z hello jednocześnie tego samego szablonu?
Można użyć hello [VSTS zadań rozszerzenia](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) lub [Generowanie szablonu usługi Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) podczas tworzenia maszyny Wirtualnej i [wdrażanie szablonu usługi Azure Resource Manager hello ze środowiska Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Jak przenieść Mój istniejący maszynach wirtualnych platformy Azure do Moje laboratorium w usłudze Azure DevTest Labs?
Wykonaj kroki hello poniżej toocopy istniejących tooAzure maszyn wirtualnych DevTest Labs:

1. Plik VHD hello kopię istniejącej maszyny wirtualnej za pomocą tej [skrypt programu Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Tworzenie niestandardowego obrazu hello](devtest-lab-create-template.md) w usłudze Azure DevTest Labs laboratorium.
3. Utwórz maszynę Wirtualną w laboratorium hello z niestandardowego obrazu

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>Czy można podłączyć wiele dysków toomy maszyn wirtualnych?
Dołączenie wielu dysków tooVMs jest obsługiwana.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Czy Moje testowania toouse obrazu systemu operacyjnego Windows, czy jest konieczne toopurchase subskrypcję MSDN?
Jeśli potrzebujesz obrazów systemu operacyjnego klienta toouse systemu Windows (z systemem Windows 7 lub nowszy) dla programowania i testowania na platformie Azure, tak, musisz najpierw albo:

- [Kup subskrypcję MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Jeśli masz umowy Enterprise Agreement, Utwórz subskrypcję platformy Azure z hello [oferta przedsiębiorstwa i testowania](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Aby uzyskać więcej informacji na temat hello kredytów systemu Azure dla każdego oferty MSDN, zobacz [Azure miesięczne środki dla subskrybentów programu Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Jak zautomatyzować proces hello przesyłania plików VHD toocreate niestandardowych obrazów?
Dostępne są dwie opcje:

* [Azure AzCopy](../storage/common/storage-use-azcopy.md#blob-upload) można toocopy używane lub przekazywanie wirtualnego dysku twardego pliki toohello konta magazynu skojarzone z hello laboratorium.
* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która działa w systemach Windows, OS x i Linux.   

toofind hello docelowego konta magazynu skojarzone z laboratorium, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Wybierz **grup zasobów** z hello lewego panelu.
3. Znajdź i wybierz grupę zasobów hello skojarzone z laboratorium.
4. Na powitania **omówienie** bloku, wybierz jedną z hello kont magazynu.
5. Wybierz **obiekty BLOB**.
6. Poszukaj przekazywania na liście hello. Jeśli żaden nie istnieje, zwracany tooStep #4 i spróbuj innego konta magazynu.
7. Użyj hello **adres URL** jako lokalizacja docelowa polecenia AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Jak można zautomatyzować proces usuwania wszystkich hello maszyn wirtualnych w laboratorium Moje hello?
Ponadto toodeleting maszyn wirtualnych z laboratorium w hello portalu Azure, możesz usunąć wszystkich hello maszyn wirtualnych w laboratorium, za pomocą skryptu programu PowerShell. Witaj poniższy przykład, zmodyfikuj hello wartości parametrów w obszarze hello **toochange wartości** komentarza. Możesz pobrać hello `subscriptionId`, `labResourceGroup`, i `labName` wartości z bloku laboratorium hello w hello portalu Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Artefakty**
## <a name="what-are-artifacts"></a>Co to są artefakty?
Artefakty są elementy dostosowywalne, które mogą być używane toodeploy Twojego najnowsze bitów lub użytkownika standardowego narzędzia na maszynie Wirtualnej. Są one dołączone tooyour maszyny Wirtualnej podczas tworzenia za pomocą kilku kliknięć proste, a po zainicjowaniu obsługi maszyny Wirtualnej hello artefakty hello wdrażanie i konfigurowanie maszyny Wirtualnej. Istnieją różne artefakty istniejące w naszym [publicznego repozytorium GitHub](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), ale możesz też łatwo [tworzyć własne artefakty](devtest-lab-artifact-author.md).


**Konfiguracja laboratorium**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Jak utworzyć laboratorium z szablonem usługi Azure Resource Manager?
Firma Microsoft umieściła [repozytorium GitHub szablonów usługi Azure Resource Manager laboratorium](https://aka.ms/dtlquickstarttemplate) wdrażanego jako- lub zmodyfikować toocreate szablony niestandardowe w laboratoriach użytkownika. Każdy z tych szablonów ma łącze, które można kliknąć laboratorium hello toodeploy jako — znajduje się w ramach własnej subskrypcji platformy Azure, lub możesz dostosować szablon hello i [wdrażanie przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Dlaczego moja maszyny wirtualne są tworzone w różnych grupach zasobów z dowolnych nazw Można zmienić nazwy lub zmodyfikować te grupy zasobów?
Grupy zasobów są tworzone w ten sposób, aby Azure DevTest Labs toomanage hello użytkownikowi uprawnień i dostępu toovirtual maszyny. Podczas gdy można przenieść grupy zasobów tooanother wirtualna hello z żądaną nazwą, to nie jest to zalecane. Pracujemy nad poprawy tooallow to środowisko większą elastyczność.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Ile labs można utworzyć w obszarze hello tej samej subskrypcji?
Nie ma żadnego określonego limitu liczby hello labs, które mogą być tworzone na subskrypcję. Jednak hello zasoby używane są ograniczone na subskrypcję. Informacje o hello [limity i przydziały narzucone subskrypcji platformy Azure](../azure-subscription-service-limits.md) i [jak tooincrease te limity](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Jak wiele maszyn wirtualnych można utworzyć dla laboratorium?
Nie ma żadnego określonego limitu hello liczby maszyn wirtualnych, które mogą być tworzone dla laboratorium. Jednak hello zasoby używane są ograniczone dla subskrypcji (np. maszyna wirtualna rdzeni, publiczne adresy IP, itp.). Informacje o hello [limity i przydziały narzucone subskrypcji platformy Azure](../azure-subscription-service-limits.md) i [jak tooincrease te limity](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Jak udostępnić laboratorium toomy bezpośrednie połączenie?
bezpośrednie połączenie tooshare tooyour laboratorium użytkownicy, można wykonywać hello następujące procedury:

1. Przeglądaj laboratorium toohello w hello portalu Azure.
2. Skopiuj adres URL laboratorium hello z przeglądarki i udostępniać użytkownikom laboratorium.

> [!NOTE]
> Jeśli użytkownicy laboratorium użytkowników zewnętrznych z [konta Microsoft](#what-is-a-microsoft-account) i nie należą one firmy tooyour usługi Active directory, mogą otrzymywać wystąpił błąd podczas nawigowania toohello podane łącze. Jeżeli one komunikat o błędzie, poinstruuj ich tooclick hello nazwy na powitania prawym górnym rogu portalu Azure i hello wybierz katalog, gdy laboratorium hello istnieje z hello **katalogu** część hello menu.
>
>

## <a name="what-is-a-microsoft-account"></a>Co to jest konto Microsoft?
Konto Microsoft, które jest używane dla prawie wszystko, co zrobić z Microsoft urządzeń i usług. Jest to adres e-mail i hasło, użyj toosign w tooSkype, Outlook.com, OneDrive, Windows Phone i Xbox LIVE — i oznacza Twoje pliki, zdjęć, kontakty i ustawienia można wykonać tooany urządzenia.

> [!NOTE]
> Konto Microsoft używane toobe o nazwie "Windows Live ID".
>
>


**Rozwiązywanie problemów**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Moje artefaktu nie powiodło się podczas tworzenia maszyny Wirtualnej. Jak rozwiązać go
Odwołuje się zbyt[jak toodiagnose artefaktu błędów w usłudze DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn sposób rejestrowania tooobtain dotyczące Twojej artefaktów nie powiodło się.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Dlaczego nie jest Mój istniejący wirtualny sieci zapisywanie prawidłowo?
Jedną z możliwości to, że nazwy sieci wirtualnej zawiera kropki. Jeśli tak, spróbuj usunąć hello okresy lub zastępowania ich łączników, a następnie spróbuj zapisywania Witaj ponownie sieci wirtualnej.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Dlaczego uzyskać komunikat o błędzie "Nie znaleziono zasobu nadrzędnego", podczas inicjowania obsługi administracyjnej maszyny Wirtualnej z programu PowerShell?
Gdy jeden zasób jest zasobem nadrzędnej tooanother, zasobu nadrzędnego hello musi istnieć przed utworzeniem hello zasobu podrzędnego. Jeśli nie istnieje, zostanie wyświetlony **ParentResourceNotFound** błędu. Jeśli nie określisz zależność od zasobu nadrzędnego hello, zasobu podrzędnego hello może wdrożyć przed hello nadrzędnej.

Maszyny wirtualne są zasoby podrzędne w laboratorium w grupie zasobów. Gdy używasz toodeploy szablonów usługi Azure Resource Manager za pomocą programu PowerShell, nazwa grupy zasobów hello w hello skrypt programu PowerShell powinna być nazwa grupy zasobów hello hello laboratorium. Aby uzyskać więcej informacji, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Gdzie można znaleźć więcej informacji o błędzie w przypadku wdrożenia maszyny Wirtualnej nie powiedzie się?
Błędy wdrożenia maszyny Wirtualnej są przechwytywane hello Dzienniki aktywności. Możesz znaleźć laboratorium Dzienniki aktywności maszyn wirtualnych za pośrednictwem hello **dzienniki inspekcji** lub **diagnostyki maszyny wirtualnej** menu zasobów hello w bloku maszyny Wirtualnej laboratorium hello (bloku hello wyświetla po wybraniu hello maszyny Wirtualnej z **Moje maszyny wirtualne** listy).

Czasami hello wdrożenia błędu przed rozpoczęciem powitalne wdrożenia maszyny Wirtualnej — np. po przekroczeniu limitu subskrypcji hello zasobu utworzone za pomocą hello maszyny Wirtualnej. W takim przypadku szczegóły błędu hello są przechwytywane hello laboratorium poziom **Dzienniki aktywności** którego można znaleźć u dołu hello hello **konfiguracji i zasadach** ustawienia. Aby uzyskać więcej informacji na temat używania działania logowania na platformie Azure, zobacz [widoku działania rejestruje akcje tooaudit zasobów](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
