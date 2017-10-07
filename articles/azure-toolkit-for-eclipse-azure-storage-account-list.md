---
title: aaaAzure lista kont magazynu
description: "Zarządzanie ustawieniami konta magazynu przy użyciu hello Azure zestawu narzędzi dla programu Eclipse"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Lista kont magazynu Azure
Włącz konta magazynu platformy Azure Pobierz toobe lokalizacje używane dla JDK, serwera aplikacji i składników dowolnego, a także na potrzeby przechowywania stanu, korzystając z buforowania. Eclipse przechowuje listę kont magazynu znane, projekty tooyour dostępne w obszarze roboczym Eclipse. Witaj tooopen **kont magazynu** okno dialogowe, które jest używane toomanage, który listy w programie Eclipse kliknij **okna**, kliknij przycisk **preferencje**, rozwiń węzeł **Azure **, a następnie kliknij przycisk **kont magazynu**.

Witaj poniżej pokazano hello **kont magazynu** okna dialogowego.

![][ic719496]

Można również otworzyć to okno dialogowe z **kont** łącza w oknach dialogowych, korzystających z konta magazynu, takich jak następujące hello:

* Witaj **JDK** kartę hello **konfiguracji serwera** okna dialogowego.
* Witaj **serwera** kartę hello **konfiguracji serwera** okna dialogowego.
* Witaj **Dodaj składnik** okna dialogowego.
* Witaj **buforowanie** okna dialogowego właściwości.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>Magazyn kont przy użyciu narzędzia tooimport plik ustawień publikowania
1. W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Import z pliku ustawień publikowania**.

2. (Pomiń ten krok, jeśli został już zapisany publikowania ustawienia pliku tooyour komputer lokalny). W hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk **Pobierz plik ustawień publikowania**. Jeśli użytkownik nie jest jeszcze zalogowany do konta platformy Azure, będzie zostanie wyświetlony monit o toolog w. Następnie zostanie wyświetlony monit pliku ustawień publikowania toosave platformy Azure. (Możesz zignorować hello instrukcje wynikowy wyświetlane na stronach logowania hello - one są dostarczane przez hello portalu Azure i są przeznaczone dla użytkowników programu Visual Studio) Zapisz tooyour komputera lokalnego.

3. Nadal w hello **importu informacji o subskrypcji** okna dialogowego, kliknij przycisk hello **Przeglądaj** przycisku, wybierz hello lokalnie zapisany wcześniej plik ustawień publikowania, a następnie kliknij przycisk **Otwórz**.

4. Kliknij przycisk **OK** tooclose hello **importu informacji o subskrypcji** okna dialogowego.

## <a name="toocreate-a-new-storage-account"></a>toocreate nowe konto magazynu
1. W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.

2. W ramach hello **Dodawanie konta magazynu** okna dialogowego, kliknij przycisk **nowy**.

3. W ramach hello **nowe konto magazynu** okna dialogowego, określ wartości dla następujących hello:

   * Nazwa konta magazynu.

   * Lokalizacja konta magazynu hello.

   * Opis hello konta magazynu.

   * Konto magazynu hello Hello subskrypcji toowhich należy.

4. Kliknij przycisk **OK** tooclose hello **nowe konto magazynu** okna dialogowego.

Może upłynąć kilka minut dla Twojego toobe konta magazynu utworzone. Po utworzeniu, kliknij przycisk **OK** tooclose hello **Dodawanie konta magazynu** okno dialogowe i nowe konto magazynu zostanie dodany toohello listę kont magazynu dostępne.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd istniejącej listy toohello konta magazynu
1. Jeśli nie masz już usługi Azure storage account, utwórz ją za następujące kroki hello liście hello **toocreate nowej sekcji konta magazynu** powyżej. (Można również utworzyć nowe konto magazynu na powitania [portalu zarządzania Azure][Azure Management Portal].)

2. W ramach hello **kont magazynu** okna dialogowego, kliknij przycisk **Dodaj**.

3. W ramach hello **Dodawanie konta magazynu** okna dialogowego, wprowadź wartości w polach **nazwa** i **klucz dostępu**. Witaj konta nazwy i klucza dostępu musi być dla istniejącego konta magazynu platformy Azure. Użyj hello **magazynu** sekcji hello [portalu zarządzania Azure] [ Azure Management Portal] tooview nazwy konta magazynu i klucze. Twoje **Dodawanie konta magazynu** okno dialogowe będzie wyglądać podobnie następujące toohello.
   
   ![][ic719497]

4. Kliknij przycisk **OK** tooclose hello **Dodawanie konta magazynu** okna dialogowego.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify toouse konta magazynu klucza dostępu
1. W ramach hello **kont magazynu** okna dialogowego, kliknij konto magazynu hello mają tooedit, a następnie kliknij przycisk **Edytuj**.

2. W ramach hello **Edytuj klucz dostępu do konta magazynu** okna dialogowego, zmodyfikuj hello **klucz dostępu** wartość.

3. Kliknij przycisk **OK** tooclose hello **Edytuj klucz dostępu do konta magazynu** okna dialogowego.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove konto magazynu z listy hello w środowisku Eclipse
1. W ramach hello **kont magazynu** okna dialogowego, kliknij konto magazynu hello mają tooedit, a następnie kliknij przycisk **Usuń**.

2. Kliknij przycisk **OK** gdy zostanie wyświetlony monit o tooremove hello konta magazynu.

> [!NOTE]
> Usuwanie konta magazynu hello za pośrednictwem hello **kont magazynu** okna dialogowego tylko spowoduje usunięcie jej z listy hello możliwych do wyświetlenia w programie Eclipse kont magazynu. Nie powoduje usunięcia konta magazynu hello z subskrypcją platformy Azure. Ponadto hello konta magazynu można ponownie wyświetlone na liście po Eclipse ładuje hello Szczegóły subskrypcji.
> 
> 

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
