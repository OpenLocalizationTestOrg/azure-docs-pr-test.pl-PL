---
title: "pojęcia Labs aaaDevTest | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących DevTest Labs i jak może być łatwo toocreate, zarządzanie i monitorowanie maszyn wirtualnych platformy Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a>DevTest Labs — pojęcia
## <a name="overview"></a>Omówienie
Witaj, następujące listy zawiera kluczowe założenia DevTest Labs i definicje:

## <a name="labs"></a>Laboratoria
Laboratorium jest hello infrastruktury, który obejmuje grupy zasobów, takich jak maszyn wirtualnych (VM), które umożliwiają lepsze zarządzanie tych zasobów, określając ograniczenia i limity przydziału.

## <a name="virtual-machine"></a>Maszyna wirtualna
Maszyny Wirtualnej platformy Azure jest jednym z kilku typów [na żądanie, skalowalnych zasobów obliczeniowych](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) udostępniającej Azure. Azure maszyn wirtualnych zapewnia hello swobodne korzystanie z wirtualizacji bez konieczności toobuy i obsługa hello sprzętem fizycznym, który uruchamia go, mimo że nadal potrzebujesz toomaintain hello maszyny Wirtualnej przez wykonywania określonych zadań, takich jak konfigurowanie, poprawki i instalowanie oprogramowania hello który uruchamia na nim.

[Omówienie maszyn wirtualnych systemu Windows na platformie Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) zapewnia informacje o kwestiach należy rozważyć przed Utwórz Maszynę wirtualną, jak utworzyć i jak zarządzać.

## <a name="claimable-vm"></a>Claimable maszyny Wirtualnej
Claimable maszyny Wirtualnej platformy Azure jest maszyny wirtualnej, która jest dostępna do użycia przez każdy laboratorium użytkownik z uprawnieniami. Administrator laboratorium można przygotować maszyn wirtualnych z określonych obrazów podstawowej i artefakty i je zapisać puli tooa udostępnionych. Użytkownik laboratorium następnie mogą rezerwować pracy maszyny Wirtualnej z puli hello, jeśli wymagany jest jeden z tej konkretnej konfiguracji.

Maszynę Wirtualną, która jest claimable nie przypisano początkowo tooany określonego użytkownika, ale będą widoczne w obszarze "Claimable maszyny wirtualnej" na liście każdego użytkownika. Po maszyny Wirtualnej jest określona przez użytkownika, należy przenieść w górę tootheir obszarze "Moje maszyny wirtualne" i nie jest już claimable przez innego użytkownika.

## <a name="environment"></a>Środowisko
W usłudze DevTest Labs w środowisku odwołuje się tooa kolekcja zasobów platformy Azure w laboratorium. [Ten wpis w blogu](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) omówiono sposób toocreate wielu maszyn wirtualnych środowisk z szablonów usługi Azure Resource Manager.

## <a name="base-images"></a>Obrazy podstawowe
Podstawowy obrazy są obrazy maszyny Wirtualnej ze wszystkimi hello narzędzia i ustawienia preinstalowany i skonfigurowany tooquickly tworzenie maszyny Wirtualnej. Maszyny Wirtualnej można udostępnić pobrania istniejących podstawowej i dodając tooinstall artefaktu agenta testowego. Można następnie zapisz hello aprowizowanej maszyny Wirtualnej jako podstawowej, tak aby hello base można używać bez agenta testowego hello tooreinstall dla każdego Inicjowanie obsługi administracyjnej hello maszyny Wirtualnej.

## <a name="artifacts"></a>Artefakty
Artefakty są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej. Artefaktami mogą być:

* Narzędzia, które mają tooinstall na powitania maszyny Wirtualnej — np. agenci, program Fiddler i program Visual Studio.
* Akcje, które mają toorun na powitania maszyny Wirtualnej — np. klonowanie repozytorium.
* Aplikacje, które mają tootest.

Artefakty [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) pliki JSON, które zawierają instrukcje tooperform wdrożenia i zastosować konfigurację.

## <a name="artifact-repositories"></a>Repozytoria artefaktów
Repozytoria artefaktu są repozytoria git, gdzie artefakty są sprawdzane w. Repozytoria artefaktu można dodać toomultiple laboratoriów w Twojej organizacji, udostępniania i włączanie ponownego użycia.

## <a name="formulas"></a>Formuły
Formuły w przypadku dodawania toobase obrazów mechanizm umożliwiający szybkiej obsługi maszyny Wirtualnej. Formuły w usłudze DevTest Labs znajduje się lista domyślnej właściwości wartości używane toocreate laboratorium maszyny Wirtualnej.
Mogą być tworzone z formułami, maszyn wirtualnych o hello sam zestaw właściwości — takie jak podstawowy obraz, rozmiar maszyny Wirtualnej, sieci wirtualnej i artefakty — bez konieczności toospecify te właściwości zawsze. Podczas tworzenia maszyny Wirtualnej z formuły, wartości domyślne hello może służyć jako- lub zmodyfikowany.

## <a name="policies"></a>Zasady
Pomoc dotycząca zasad kontrolowania kosztów w laboratorium. Na przykład można utworzyć tooautomatically zasad, zamknij maszyn wirtualnych na podstawie zdefiniowanego harmonogramu.

## <a name="caps"></a>Cap
Włączony klawisz Caps jest mechanizm odpady toominimize w laboratorium. Na przykład można ustawić liczbę hello toorestrict zakończenia maszyn wirtualnych, które mogą być tworzone dla poszczególnych użytkowników lub w laboratorium.

## <a name="security-levels"></a>Poziomy zabezpieczeń
Dostęp zabezpieczeń jest określany przez based kontroli dostępu (RBAC). toounderstand sposób uzyskiwania dostępu do działania, ale toounderstand hello różnice między uprawnienia roli i zakres zgodnie z definicją RBAC.

* Uprawnienie - uprawnienie jest określoną akcję tooa zdefiniowanych dostępu (np. dostęp do odczytu tooall maszyn wirtualnych).
* Rola: Rola to zestaw uprawnień, które mogą być grupowane i przypisany użytkownik tooa. Na przykład Witaj *właściciel subskrypcji* rola ma dostęp do zasobów tooall w ramach subskrypcji.
* Zakres - zakres jest poziom w hierarchii hello zasobów platformy Azure, takich jak grupy zasobów, pojedynczy laboratorium lub hello całej subskrypcji.

W zakresie hello DevTest Labs, istnieją dwa typy uprawnień użytkownika toodefine ról: laboratorium właściciela i użytkownika laboratorium.

* Właściciel laboratorium - właściciela laboratorium ma dostęp do zasobów tooany w laboratorium hello. W związku z tym właściciela laboratorium można modyfikować zasady, zapisywania i odczytywania żadnej maszyny wirtualnej, zmień hello sieci wirtualnej, a itd.
* Użytkownik laboratorium —, użytkownik laboratorium mogą wyświetlać wszystkie zasoby laboratorium, takich jak maszyny wirtualne, zasady i sieci wirtualne, ale nie można zmodyfikować zasady lub żadnych maszyn wirtualnych utworzonych przez innych użytkowników.

toosee jak toocreate role niestandardowe w usłudze DevTest Labs można znaleźć w artykule toohello [przyznawanie uprawnień użytkownikom zasad laboratorium toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Ponieważ zakresy są hierarchiczne, jeśli użytkownik ma uprawnienia w zakresie niektórych, automatycznie otrzymują tych uprawnień w zakresie niższego poziomu, co razem. Na przykład jeśli użytkownik jest przypisany toohello roli właściciela subskrypcji, następnie mają dostęp do tooall zasobów w ramach subskrypcji, które obejmują wszystkie maszyny wirtualne, wszystkie sieci wirtualne i laboratoriów wszystkie. W związku z tym właściciela subskrypcji automatycznie dziedziczy hello roli właściciela laboratorium. Jednak hello przeciwną nie jest prawdziwe. Właściciela laboratorium ma laboratorium tooa dostępu, które jest zakresem niższym niż poziom subskrypcji hello. W związku z tym właściciela laboratorium nie będą mogli toosee maszyny wirtualne lub sieci wirtualne lub wszystkie zasoby, które znajdują się poza laboratorium hello.

## <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager
Wszystkie hello omówione w tym artykule można skonfigurować przy użyciu szablonów usługi Azure Resource Manager, które umożliwiają definiowanie hello infrastruktury/konfiguracji rozwiązania Azure i wielokrotnie wdrażać w spójnym stanie.

[Struktura hello i składni szablonów usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) opisuje strukturę hello Azure Resource Manager szablon i hello właściwości, które są dostępne w innych sekcjach hello szablonu.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Następne kroki
[Tworzenie laboratorium w usłudze DevTest Labs](devtest-lab-create-lab.md)
