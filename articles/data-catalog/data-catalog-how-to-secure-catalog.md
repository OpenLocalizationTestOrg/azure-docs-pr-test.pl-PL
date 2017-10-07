---
title: "aaaHow toosecure dostępu tooAzure Data Catalog | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toosecure usługi data catalog i jej zasobów danych."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a>Jak toosecure uzyskują dostęp do zasobów katalogu i danych toodata
> [!IMPORTANT]
> Ta funkcja jest dostępna tylko w wersji standard hello usługi Azure Data Catalog.

Wykaz danych Azure umożliwia toospecify, kto ma dostęp do wykazu danych hello i jakie operacje (rejestrowanie, dodawanie adnotacji, przejąć na własność) mogą dotyczyć metadanych w katalogu hello. 

## <a name="catalog-users-and-permissions"></a>Katalogu użytkowników i uprawnień
toogive przez użytkownika lub hello grupy dostępu usługi data catalog tooa i ustawić uprawnienia:

1. Na powitania [strony głównej wykazu danych](http://www.azuredatacatalog.com), kliknij przycisk **ustawienia** na powitania narzędzi.

    ![Data catalog — ustawienia](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. Na stronie ustawień hello, rozwiń węzeł hello **użytkownicy wykazu** sekcji.
    ![W katalogu użytkowników — Dodaj](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)
3. Kliknij pozycję **Dodaj**.
4. Wprowadź w pełni kwalifikowana hello **nazwy użytkownika** lub nazwa hello **grupy zabezpieczeń** w hello Azure Active Directory (AAD) skojarzone z hello katalogu. Użyj przecinka (",") jako separatora, dodając więcej niż jednego użytkownika lub grupę.
    ![Użytkownicy wykazu - użytkowników lub grup](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)
5. Naciśnij klawisz **ENTER** lub **kartę** poza hello pola tekstowego. 
6.  Upewnij się, że wszystkie uprawnienia (**Adnotuj**, **zarejestrować**, i **Przejmij na własność**) domyślnie przypisane toothese użytkowników lub grup. Oznacza to, że hello użytkownik lub grupa może [zarejestrować zasobów danych]( data-catalog-how-to-register.md), [adnotacji zasobów danych]( data-catalog-how-to-annotate.md), i [przejąć na własność zasobów danych]( data-catalog-how-to-manage.md). 
    ![Użytkownicy wykazu - domyślnych uprawnień](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)
7.  toogive użytkownikowi lub grupie tylko hello katalogu toohello dostęp, wyczyść hello **adnotacji** opcji dla tego użytkownika lub grupy. Po wykonaniu tej hello użytkownika lub grupy nie można adnotować zasobów danych w katalogu hello, ale mogą je wyświetlać. 
8.  toodeny użytkownika lub grupy z rejestrowania zasobów danych, wyczyść hello **zarejestrować** opcji dla tego użytkownika lub grupy.
9.  toodeny użytkownika z przejmowania własności zasobów danych, wyczyść hello **przejąć na własność** opcji dla tego użytkownika lub grupy. 
10. toodelete użytkownika/grupy użytkowników z katalogu, kliknij przycisk **x** hello użytkownika/grupy u dołu hello hello listy. 
    ![Użytkownicy w katalogu — Usuń użytkownika](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)

    > [!IMPORTANT]
    > Zalecamy bezpośrednio dodać użytkowników toocatalog grup zabezpieczeń, zamiast dodawania użytkowników, a następnie przypisz uprawnienia. Następnie należy dodać grupy zabezpieczeń toohello użytkowników odpowiadających im role i ich katalogu toohello wymaganego dostępu.

## <a name="special-considerations"></a>Uwagi

- grupy toosecurity przypisane uprawnienia Hello są dodatku. Użytkownik jest w dwóch grupach. Jedna grupa ma adnotacji uprawnienia i nie mają adnotacje do innej grupy uprawnień. Następnie użytkownik ma adnotacji uprawnienia. 
- jawnie hello zastąpienie użytkownika tooa przypisane uprawnienia toogroups toowhich hello użytkownika należy przypisać uprawnienia Hello. W poprzednim przykładzie hello powiedzieć jawnie dodać hello użytkownika toocatalog użytkowników i nie należy przypisywać uprawnienia adnotacji. Użytkownik Hello nie adnotacji zasobów danych, mimo że hello użytkownik jest członkiem grupy, która ma adnotacji uprawnienia.

## <a name="next-steps"></a>Następne kroki
- [Rozpoczynanie pracy z usługą Azure Data Catalog](data-catalog-get-started.md)

