---
title: "aaaCreate i udostępniać pulpity nawigacyjne portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate i edytowanie pulpitów nawigacyjnych w hello portalu Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Tworzenie i udostępnianie pulpitów nawigacyjnych w hello portalu Azure
Można tworzyć wiele pulpitów nawigacyjnych i udostępniać innym użytkownikom, którzy mają dostęp tooyour Azure subskrypcji.  W tym artykule przechodzi przez hello podstawy tworzenia, edytowania, publikowanie i zarządzanie toodashboards dostępu.

## <a name="create-a-dashboard"></a>Utwórz pulpit nawigacyjny
toocreate pulpitu nawigacyjnego, wybierz hello **nowego pulpitu nawigacyjnego** przycisku Dalej toohello bieżącego jego nazwę.  

![Utwórz pulpit nawigacyjny](./media/azure-portal-dashboards/new-dashboard.png)

Ta akcja tworzy nowy, pusty, prywatne pulpitu nawigacyjnego i umieszcza Tryb dostosowywania, w którym można nazwa pulpitu nawigacyjnego i dodać lub zmienić Kafelki.  W tym trybie hello zwijanej kafelka przyjmuje Galerii za pośrednictwem menu nawigacji po lewej stronie powitania.  Witaj galerii kafelka pozwala znaleźć kafelków dla zasobów platformy Azure na różne sposoby: można przeglądać [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups), przez przez typ zasobu [tag](../azure-resource-manager/resource-group-using-tags.md), lub przez wyszukiwanie według nazwy zasobu.  

![Dostosowanie pulpitu nawigacyjnego](./media/azure-portal-dashboards/customize-dashboard.png)

Dodaj Kafelki przez przeciąganie i upuszczanie je na powierzchnię pulpitu nawigacyjnego hello wszędzie tam, gdzie ma.

Brak nową kategorię o nazwie **ogólne** dla kafelków, które nie są skojarzone z określonego zasobu.  W tym przykładzie mamy przypiąć hello Markdown kafelka.  Korzystając z tego pulpitu nawigacyjnego kafelka tooadd niestandardowych tooyour zawartości.  Witaj Kafelek obsługuje zwykłego tekstu, [składni języka Markdown](https://daringfireball.net/projects/markdown/syntax)oraz ograniczony zestaw HTML.  (Dla bezpieczeństwa, nie może wykonać czynności, takie jak wstrzyknąć `<script>` znaczniki lub używać niektórych elementu Style CSS, która może zakłócać hello portalu.) 

![Dodawanie znaczników markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Edytuj pulpit nawigacyjny
Po utworzeniu pulpitu nawigacyjnego, można przypiąć Kafelki z galerii kafelka hello lub hello kafelka reprezentację bloków. Załóżmy przypiąć hello reprezentację naszej grupy zasobów. Podczas przeglądania hello elementu lub bloku grupy zasobów hello albo można przypiąć. W obu przypadkach efekt spowodować przypinanie kafelka hello reprezentację hello grupy zasobów.

![Toodashboard numeru PIN](./media/azure-portal-dashboards/pin-to-dashboard.png)

Po przypięciu elementu hello, wygląda na to, na pulpicie nawigacyjnym.

![widok pulpitu nawigacyjnego](./media/azure-portal-dashboards/view-dashboard.png)

Teraz, gdy mamy kafelków Markdown i pulpit nawigacyjny przypiętych toohello grupy zasobów, firma Microsoft można zmieniać rozmiar i rozmieszczanie Kafelki hello do odpowiedniego układu.

Kursora myszy i wybierając "..." lub klikając Kafelek można wyświetlić wszystkie polecenia kontekstowe powitania dla tego kafelka. Domyślnie istnieją dwie pozycje:

1. **Odepnij z pulpitu nawigacyjnego** — usuwa hello fragment hello pulpitu nawigacyjnego
2. **Dostosowywanie** — wprowadza trybu dostosowania

![Dostosowywanie kafelka](./media/azure-portal-dashboards/customize-tile.png)

Wybierając dostosować, można zmieniać rozmiar i zmienić kolejność kafelków. tooresize kafelka, wybierz hello nowy rozmiar menu kontekstowe hello, jak pokazano w powitania po obrazu.

![Zmień rozmiar kafelka](./media/azure-portal-dashboards/resize-tile.png)

Lub, jeśli kafelka hello obsługuje dowolnej wielkości, możesz przeciągać hello dolnej prawym rogu toohello żądany rozmiar.

![Zmień rozmiar kafelka](./media/azure-portal-dashboards/resize-corner.png)

Po zmianie rozmiaru kafelków, Wyświetl hello pulpitu nawigacyjnego.

![Widok kafelków](./media/azure-portal-dashboards/view-tile.png)

Po zakończeniu dostosowanie pulpitu nawigacyjnego po prostu wybierz hello **gotowe dostosowywanie** tooexit trybu dostosowania, lub kliknij prawym przyciskiem myszy i wybierz polecenie **gotowe dostosowywanie** z menu kontekstowego hello.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Publikowanie pulpitu nawigacyjnego i zarządzanie kontrolą dostępu
Podczas tworzenia pulpitu nawigacyjnego jest prywatna domyślnie, co oznacza, że jesteś hello jedyną osobą, która to sprawdzić.  toomake on widoczny tooothers, użyj hello **udziału** przycisku, który jest wyświetlany obok hello innych poleceń pulpitu nawigacyjnego.

![Udostępnij pulpit nawigacyjny](./media/azure-portal-dashboards/share-dashboard.png)

Zostanie wyświetlona prośba toochoose subskrypcji i zasobu grupy dla użytkownika pulpitu nawigacyjnego toobe publikowane do. tooseamlessly zintegrować ekosystemu hello pulpity nawigacyjne, wdrożyliśmy udostępnionych pulpitów nawigacyjnych jako zasobów platformy Azure (tak, aby nie można udostępnić, wpisując adres e-mail).  Uzyskiwanie dostępu do informacji toohello wyświetlanych przez większość hello Kafelki w portalu hello są regulowane przez [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md). Z punktu widzenia kontroli dostępu do udostępnionych pulpitów nawigacyjnych nie różnią się od maszyny wirtualnej lub konto magazynu.  

Załóżmy, że masz subskrypcję platformy Azure i członkowie zespołu są przypisane role hello **właściciela**, **współautora**, lub **czytnika** hello subskrypcji.  Użytkownicy, którzy są właściciele i Współautorzy są możliwe toolist, widok, Utwórz, modyfikować lub usuwać pulpitów nawigacyjnych w ramach danej subskrypcji.  Użytkownicy, którzy są czytników są możliwe toolist i wyświetlanie pulpitów nawigacyjnych, ale nie można je modyfikować lub usuwać.  Użytkownicy z dostępem czytnika są toomake stanie edycje lokalne tooa udostępnionego pulpitu nawigacyjnego, ale są toopublish nie jest w stanie serwera zapasowego toohello tych zmian.  Jednak mogą one ułatwić prywatnej kopii pulpitu nawigacyjnego hello na własny użytek.  Jak zawsze poszczególnych Kafelki na pulpicie nawigacyjnym hello wymuszanie własnych regułami kontroli dostępu na podstawie hello zasobów, które są zgodne.  

Dla wygody hello portalu do publikowania przewodniki środowisko możesz kierunku wzorzec, gdzie umieścić pulpitów nawigacyjnych w grupie zasobów o nazwie **pulpity nawigacyjne**.  

![Publikowanie pulpitu nawigacyjnego](./media/azure-portal-dashboards/publish-dashboard.png)

Możesz również toopublish pulpitu nawigacyjnego tooa określonej grupy zasobów.  Witaj kontroli dostępu do tego pulpitu nawigacyjnego odpowiada hello kontroli dostępu dla grupy zasobów hello.  Użytkownicy, którzy mogą zarządzać zasobami hello w danej grupie zasobów ma również pulpity nawigacyjne toohello dostępu.

![Publikowanie pulpitu nawigacyjnego tooresource grupy](./media/azure-portal-dashboards/publish-to-resource-group.png)

Po opublikowaniu pulpitu nawigacyjnego hello **udostępniania + dostępu** Panelu sterowania zostanie odświeżania i wyświetlić informacje o opublikowanych pulpitu nawigacyjnego hello, w tym pulpit nawigacyjny toohello dostępu użytkownika toomanage łącza.  To łącze powoduje uruchomienie hello standardowe kontroli dostępu opartej na rolach bloku używane toomanage dostępu do żadnych zasobów platformy Azure.  Możesz zawsze wrócić widoku toothis wybierając **udziału**.

![Zarządzanie kontrolą dostępu](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Następne kroki
* Zobacz zasoby toomanage [zasobów Azure zarządzania za pośrednictwem portalu](../azure-resource-manager/resource-group-portal.md).
* Zobacz zasoby toodeploy [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

