---
title: aaaGet pracy z szablonami prywatnymi | Dokumentacja firmy Microsoft
description: "Dodawanie, zarządzanie i udostępnianie szablonów prywatnych przy użyciu hello portalu Azure, hello wiersza polecenia platformy Azure lub programu PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Rozpoczynanie pracy z szablonami prywatnymi w portalu Azure hello
[Usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) szablon to deklaracyjny szablon używany toodefine wdrożenia. Można zdefiniować hello toodeploy zasobów dla rozwiązania i określić parametry i zmienne, które pozwalają tooinput wartości dla różnych środowisk. Witaj szablon składa się z kodu JSON i wyrażeń, których można użyć wartości tooconstruct na potrzeby wdrożenia.

Można użyć nowego hello **szablony** możliwości w hello [Azure Portal](https://portal.azure.com) wraz z hello **Microsoft.Gallery** dostawcy zasobów jako rozszerzenie hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate użytkowników, zarządzanie i wdrażanie szablonów prywatnych z poziomu biblioteki osobistej.

Ten dokument przeprowadzi Cię przez dodawanie, zarządzanie i udostępnianie prywatnej **szablonu** przy użyciu hello portalu Azure.

## <a name="guidance"></a>Wskazówki
Witaj poniższe sugestie pomogą Ci w pełni korzystać z **szablony** podczas pracy z rozwiązaniami:

* **Szablon** to hermetyzowany zasób, który zawiera szablon usługi Resource Manager i dodatkowe metadane. Zachowuje się bardzo podobnie tooan elementu hello Marketplace. Hello klucza różnica polega na tym, że jest to element prywatny jako min. toohello publicznych elementów Marketplace.
* Witaj **szablony** biblioteki działa dobrze w przypadku użytkowników, którzy potrzebują toocustomize ich wdrożenia.
* **Szablony** są dobrym rozwiązaniem dla użytkowników, którzy potrzebują prostego repozytorium na platformie Azure.
* Rozpocznij pracę z istniejącym szablonem usługi Resource Manager. Wyszukaj szablony w witrynie [github](https://github.com/Azure/azure-quickstart-templates) lub [wyeksportuj szablon](../azure-resource-manager/resource-manager-export-template.md) z istniejącej grupy zasobów.
* **Szablony** wiązanej toohello użytkowników, którzy je opublikował. Nazwa wydawcy Hello jest widoczne tooeveryone, kto ma dostęp do odczytu tooit.
* **Szablony** to zasoby usługi Resource Manager. Po opublikowaniu nie można zmienić ich nazwy.

## <a name="add-a-template-resource"></a>Dodawanie zasobu Szablon
Istnieją dwa sposoby toocreate **szablonu** zasobu w hello portalu Azure.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Metoda 1. Tworzenie nowego zasobu Szablon z poziomu uruchomionej grupy zasobów
1. Przejdź tooan istniejącej grupy zasobów na powitania portalu Azure. Wybierz pozycję **Eksportuj szablon** w obszarze **Ustawienia**.
2. Po wyeksportowaniu szablonu usługi Resource Manager hello, użyj hello **Zapisz szablon** toosave przycisk go toohello **szablony** repozytorium. Wszystkie szczegóły eksportowania szablonu możesz znaleźć [tutaj](../azure-resource-manager/resource-manager-export-template.md).
   <br /><br />
   ![Eksportowanie grupy zasobów](media/rg-export-portal1.PNG)  <br />
3. Wybierz hello **zapisać tooTemplate** przycisku polecenia.
   <br /><br />
4. Wprowadź hello następujących informacji:
   
   * Nazwa — Nazwa obiektu szablonu hello (Uwaga: to jest nazwa usługi Azure Resource Manager, na podstawie. Obowiązują wszystkie ograniczenia związane z nazewnictwem, a utworzonej nazwy nie można zmienić).
   * Opis — krótkie podsumowanie dotyczące szablonu hello.
     
     ![Zapisywanie szablonu](media/save-template-portal1.PNG)  <br />
5. Kliknij pozycję **Zapisz**.
   
   > [!NOTE]
   > Hello bloku eksportowania szablonu zostaną wyświetlone powiadomienia podczas hello wyeksportowanego szablonu usługi Resource Manager zawiera błędy, ale nadal będzie można toosave tego toohello szablonu usługi Resource Manager szablonów. Upewnij się, sprawdź, a następnie napraw wszystkie problemy dotyczące szablonu przed ponownego wdrażania hello wyeksportowanego szablonu usługi Resource Manager.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Metoda 2. Dodawanie nowego szablonu przy użyciu funkcji przeglądania
Można również dodać nowy **szablonu** od początku, używając Witaj + przycisk polecenia Dodaj w **Przeglądaj > Szablony**. Konieczne będzie tooprovide nazwę, opis i hello JSON szablonu usługi Resource Manager.

![Dodawanie szablonu](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery to oparty na dzierżawie dostawca zasobów platformy Azure. Witaj zasobu szablon jest wiązana toohello użytkownika, który go utworzył. Nie jest związany tooany określonej subskrypcji. Subskrypcję należy wybrać tylko w przypadku wdrażania szablonu toobe.
> 
> 

## <a name="view-template-resources"></a>Wyświetlanie zasobów Szablon
Wszystkie **szablony** tooyou dostępne są widoczne w **Przeglądaj > Szablony**. Będą to **szablony** utworzone przez Ciebie, a także te, które zostały Ci udostępnione z różnymi poziomami uprawnień. Więcej szczegółów w hello [kontrola dostępu](#access-control-for-a-tenant-resource-provider) poniższej sekcji.

![Wyświetlanie szablonu](media/view-template-portal1.PNG)  <br />

Można wyświetlić szczegóły hello **szablonu** , kliknij element na liście hello.

![Wyświetlanie szablonu](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Edytowanie zasobu Szablon
Możesz zainicjować przepływ edycji hello **szablonu** przez kliknięcie prawym przyciskiem myszy element hello na powitania listy przeglądania lub wybierając przycisk polecenia edycji hello.

![Edytowanie szablonu](media/edit-template-portal1a.PNG)  <br />

Można edytować hello opis lub tekst szablonu usługi Resource Manager. Nie można edytować nazwy hello, ponieważ jest to nazwa zasobu usługi Resource Manager. Podczas edytowania szablonu usługi Resource Manager hello JSON sprawdzamy, czy tooensure jest poprawne dane JSON. Wybierz **OK** , a następnie **zapisać** toosave zaktualizowany szablon.

![Edytowanie szablonu](media/edit-template-portal2a.PNG)  <br />

Raz hello **szablonu** zapisaniu zostanie wyświetlone powiadomienie o potwierdzenie.

![Edytowanie szablonu](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Wdrażanie zasobu Szablon
Możesz wdrożyć dowolny **szablon**, do którego masz uprawnienia do **odczytu**. Witaj przepływ wdrożenia powoduje uruchomienie standardowego bloku wdrożenia szablonu Azure hello. Należy wprowadzić wartości hello hello Menedżera zasobów szablonu parametrów tooproceed hello wdrożenia.

![Wdrażanie szablonu](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Udostępnianie zasobu Szablon
Zasób **Szablon** można udostępniać innym użytkownikom. Udostępnianie działa podobnie zbyt[przypisania roli dla dowolnego zasobu na platformie Azure](../active-directory/role-based-access-control-configure.md). Witaj **szablonu** właściciela zapewnia uprawnienia tooother użytkowników, którzy mogą współdziałać z zasobem szablon. Witaj osoba lub grupa osób udostępnianie hello **szablonu** z będą szablonu usługi Resource Manager hello stanie toosee i galerię jego właściwości.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Kontrola dostępu do zasobów Microsoft.Gallery hello
| Rola | Uprawnienia |
| --- | --- |
| Właściciel |Umożliwia pełną kontrolę zasobu szablon hello tym udostępnianie. |
| Czytelnik |Umożliwia odczyt i wykonywanie (wdrażanie) na powitania zasobu szablon |
| Współautor |Umożliwia edytowanie i usuwanie hello zasobu szablon. Użytkownik nie może udostępnić hello szablonu |

Wybierz **udziału** hello przeglądania elementu przez kliknięcie prawym przyciskiem myszy lub na powitania bloku przeglądania określonego elementu. Spowoduje to uruchomienie środowiska udostępniania.

![Udostępnianie szablonu](media/share-template-portal1a.png)  <br />

 Teraz możesz wybrać rolę i użytkownika lub grupę tooprovide dostępu tooa określonego **szablonu**. Witaj dostępne role to właściciel, Czytelnik i współautor. Więcej szczegółów w hello [kontrola dostępu](#access-control-for-a-tenant-resource-provider) powyższej sekcji.

![Udostępnianie szablonu](media/share-template-portal2b.png)  <br />

![Udostępnianie szablonu](media/share-template-portal3b.png)  <br />

Kliknij pozycję **Wybierz**, a następnie przycisk **OK**. Możesz teraz przeglądać hello użytkowników lub grupy dodane toohello zasobów.

![Udostępnianie szablonu](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Szablon tylko może być udostępniane innym użytkownikom i grupom w hello tej samej dzierżawy usługi Azure Active Directory. Jeśli szablon jest udostępniany adres e-mail, który nie jest w dzierżawie, zostaną wysłane zaproszenie pytaniem hello użytkownika toojoin hello dzierżawy jako Gość.
> 
> 

## <a name="next-steps"></a>Następne kroki
* toolearn o tworzeniu szablonów usługi Resource Manager, zobacz [tworzenia szablonów](../azure-resource-manager/resource-group-authoring-templates.md)
* Funkcje hello toounderstand można użyć w szablonie usługi Resource Manager, zobacz [funkcje szablonów](../azure-resource-manager/resource-group-template-functions.md)
* Aby uzyskać wskazówki dotyczące projektowania szablonów, zobacz artykuł [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md) (Najlepsze rozwiązania dotyczące projektowania szablonów usługi Azure Resource Manager).

