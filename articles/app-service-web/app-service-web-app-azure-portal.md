---
title: "Odwołanie do nawigowania portalu Azure"
description: "Dowiedz się więcej możliwości różnych użytkowników dla aplikacji sieci Web usługi między portalu zarządzania i portalu Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a>Odwołanie do nawigowania portalu Azure
Witryn sieci Web Azure są teraz nazywane [aplikacji usługi sieci Web aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714). Aktualizujemy wszystkie naszej dokumentacji w celu odzwierciedlenia tej zmiany nazwy i zapewniające instrukcje dotyczące portalu Azure. Dopóki ten proces odbywa się, można użyć tego dokumentu jako wskazówki dotyczące pracy z aplikacjami sieci Web w portalu Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a>Przyszłość klasycznego portalu Azure
Gdy zauważysz zmiany znakowania w portalu klasycznym Azure tego portalu trwa zastępowane przez Azure Portal. Zgodnie z klasycznego portalu są obecnie wycofywane, fokus dla nowych aplikacji jest zmieni się do portalu Azure. Wszystkie nowe funkcje nadchodzących dla aplikacji sieci Web rozpocznie się w portalu Azure. Uruchom przy użyciu portalu Azure, aby móc korzystać z najnowszej i najlepszej, że aplikacje sieci Web mają do zaoferowania.

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a>Układ różnice między klasycznego portalu Azure i portalu Azure
W klasycznym portalu usług Azure znajduje się na lewą stronę. Nawigacja w klasycznym portalu następuje struktury drzewa, gdzie uruchomić z usługi i przejdź do każdego elementu. Ta struktura działa dobrze w przypadku, gdy zarządzanie składnikami niezależne. Jednak aplikacje utworzone na platformie Azure są kolekcja połączonych usług i ta struktura drzewa nie jest idealne rozwiązanie w przypadku pracy z kolekcji usług. 

Azure portal ułatwia tworzenie aplikacji end-to-end ze składnikami z wielu usług. Portalu są organizowane jako *podróże*. A *podróży* jest szereg *bloków*, które są kontenerami dla różnych składników. Na przykład ustawienie automatyczne skalowanie aplikacji sieci web jest *podróży* który przejście kilku bloków jak pokazano w poniższym przykładzie: **witryny sieci web** bloku (czy Tytuł bloku ma jeszcze nie zostały zaktualizowane do używania nowych terminologia) **ustawienia** bloku i **skalowanie** bloku. W tym przykładzie automatyczne skalowanie jest konfigurowany do są zależne od użycia procesora CPU, więc jest również **procent użycia procesora CPU** bloku. Składniki w ramach *bloków* są nazywane *części*, który wygląda jak kafelki. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Przykład nawigacji: tworzenie aplikacji sieci web
Tworzenie nowej aplikacji sieci web jest nadal tak proste, jak 1, 2, 3. Na poniższej ilustracji przedstawiono portalu klasycznego i portalu side-by-side aby zademonstrować znacznie nie została zmieniona w liczbie kroki potrzebne do uruchomienia aplikacji sieci web i systemem. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

W portalu można wybrać z najbardziej typowych aplikacji sieci web, w tym galerii popularnych aplikacji, takich jak WordPress. Aby uzyskać pełną listę dostępnych aplikacji, odwiedź stronę [portalu Azure Marketplace].

Podczas tworzenia aplikacji sieci web, określ adres URL, plan usługi aplikacji i lokalizację w portalu tak samo jak to zrobić w klasycznym portalu. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Ponadto portalu pozwala zdefiniować inne typowe ustawienia. Na przykład [grup zasobów](../azure-resource-manager/resource-group-overview.md) ułatwiają wyświetlanie i zarządzanie nimi powiązanych zasobów systemu Azure. 

## <a name="navigation-example-settings-and-features"></a>Przykład nawigacji: ustawienia i funkcje
Wszystkie ustawienia i funkcje teraz są logicznie pogrupowane w jednej bloku, w którym można nawigować.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Na przykład można utworzyć domeny niestandardowe, klikając **domen niestandardowych i SSL** w **ustawienia** bloku.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

Aby skonfigurować alert monitorowania, kliknij przycisk **żądań i błędów** , a następnie **dodać Alert**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Aby włączyć diagnostykę, kliknij **dzienników diagnostycznych** w **ustawienia** bloku.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Kliknij, aby skonfigurować ustawienia aplikacji **ustawienia aplikacji** w **ustawienia** bloku. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Inna niż nazwa marki zostały zmieniona lub pogrupowane inaczej, aby ułatwić ich wyszukiwanie kilka czynności w portalu. Na przykład poniżej przedstawiono zrzut ekranu strony odpowiednie dla ustawienia aplikacji (**Konfiguruj**) w klasycznym portalu.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Więcej zasobów
[Azure Portal]: https://portal.azure.com
[portalu Azure Marketplace]: /marketplace/

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

