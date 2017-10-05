---
title: Lista kont magazynu Azure
description: "Zarządzanie ustawieniami konta magazynu przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Lista kont magazynu Azure
Konta magazynu platformy Azure umożliwiają lokalizacji pobierania do użycia dla JDK, serwera aplikacji i składników dowolnego, a także na potrzeby przechowywania stanu, korzystając z buforowania. Eclipse przechowuje listę kont magazynu znane, które są dostępne dla projektów w obszarze roboczym Eclipse. Aby otworzyć **kont magazynu** okno dialogowe, które jest używane do zarządzania tym listy w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure**, a następnie kliknij przycisk **kont magazynu**.

Poniżej przedstawiono **kont magazynu** okna dialogowego.

![][ic719496]

Można również otworzyć to okno dialogowe z **kont** łącza w oknach dialogowych, korzystających z konta magazynu, takich jak następujące:

* **JDK** karcie **konfiguracji serwera** okna dialogowego.
* **Serwera** karcie **konfiguracji serwera** okna dialogowego.
* **Dodaj składnik** okna dialogowego.
* **Buforowanie** okna dialogowego właściwości.

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>Aby zaimportować kont magazynu używany plik ustawień publikowania
1. W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Import z pliku ustawień publikowania**.

2. (Pomiń ten krok, jeśli został już zapisany plik ustawień publikowania na komputer lokalny). W **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**. Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, pojawi się zalogować. Następnie zostanie wyświetlony monit, aby zapisać Azure pliku ustawień publikowania. (Możesz zignorować wynikowy instrukcje wyświetlane na stronach logowania — one znajdują się w portalu Azure i są przeznaczone dla użytkowników programu Visual Studio) Zapisz go na komputerze lokalnym.

3. Nadal **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Przeglądaj** przycisku, wybierz plik ustawień publikowania, który został wcześniej zapisany w lokalnie, a następnie kliknij przycisk **Otwórz**.

4. Kliknij przycisk **OK** zamknąć **importu informacji o subskrypcji** okna dialogowego.

## <a name="to-create-a-new-storage-account"></a>Aby utworzyć nowe konto magazynu
1. W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.

2. W ramach **Dodawanie konta magazynu** okna dialogowego, kliknij przycisk **nowy**.

3. W ramach **nowe konto magazynu** okna dialogowego, określ wartości dla następujących:

   * Nazwa konta magazynu.

   * Lokalizacja konta magazynu.

   * Opis konta magazynu.

   * Subskrypcja, do której należy konto magazynu.

4. Kliknij przycisk **OK** zamknąć **nowe konto magazynu** okna dialogowego.

Może upłynąć kilka minut dla konta magazynu do utworzenia. Po utworzeniu, kliknij przycisk **OK** zamknąć **Dodawanie konta magazynu** okno dialogowe i nowe konto magazynu zostanie dodany do listy kont dostępny magazyn.

## <a name="to-add-an-existing-storage-account-to-the-list"></a>Aby dodać istniejące konto magazynu do listy
1. Jeśli nie masz już konto magazynu Azure, utworzyć, wykonując czynności opisane w **do utworzenia nowej sekcji konta magazynu** powyżej. (Można również utworzyć nowe konto magazynu w [portalu zarządzania Azure][Azure Management Portal].)

2. W ramach **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.

3. W ramach **Dodawanie konta magazynu** okna dialogowego, wprowadź wartości w polach **nazwa** i **klucz dostępu**. Konto nazwy i klucza dostępu musi być dla istniejącego konta magazynu platformy Azure. Użyj **magazynu** sekcji [portalu zarządzania Azure] [ Azure Management Portal] wyświetlanie Twoich nazwy konta magazynu i klucze. Twoje **Dodawanie konta magazynu** okno dialogowe będzie wyglądać podobnie do następującego.
   
   ![][ic719497]

4. Kliknij przycisk **OK** zamknąć **Dodawanie konta magazynu** okna dialogowego.

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>Aby zmodyfikować konto magazynu, aby użyć klucza dostępu
1. W ramach **kont magazynu** okno dialogowe, kliknij przycisk Magazyn konta chcesz edytować, a następnie kliknij przycisk **Edytuj**.

2. W ramach **Edytuj klucz dostępu do konta magazynu** okna dialogowego, zmodyfikuj **klucz dostępu** wartość.

3. Kliknij przycisk **OK** zamknąć **Edytuj klucz dostępu do konta magazynu** okna dialogowego.

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>Aby usunąć konto magazynu z listy w programie Eclipse
1. W ramach **kont magazynu** okno dialogowe, kliknij przycisk Magazyn konta chcesz edytować, a następnie kliknij przycisk **Usuń**.

2. Kliknij przycisk **OK** po wyświetleniu monitu, aby usunąć konto magazynu.

> [!NOTE]
> Usuwanie konta magazynu za pośrednictwem **kont magazynu** okna dialogowego tylko usunięcie go z listy kont magazynu, widocznego w środowisku Eclipse. Nie powoduje usunięcia konta magazynu z subskrypcją platformy Azure. Ponadto konto magazynu może ponownie wyświetlone na liście po Eclipse ponowne ładowanie szczegółów subskrypcji.
> 
> 

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse] 

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
