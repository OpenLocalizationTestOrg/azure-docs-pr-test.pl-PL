---
title: Tworzenie aplikacji sieci Web z poziomu portalu Azure Marketplace | Microsoft Docs
description: "Dowiedz się, jak utworzyć nową aplikację sieci Web WordPress z poziomu portalu Azure Marketplace przy użyciu Portalu Azure."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 16951ac0fcc350b7176747a7ad4e0bc8e186ab17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-from-the-azure-marketplace"></a>Tworzenie aplikacji sieci Web z poziomu portalu Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

W portalu Azure Marketplace udostępnia szeroką gamę popularnych aplikacji sieci web opracowanych przez Wspólnot oprogramowania typu open source, na przykład WordPress i Umbraco CMS. Z tego samouczka dowiesz się tworzenie aplikacji WordPress z portalu Azure marketplace.
które tworzy bazę danych aplikacji sieci Web platformy Azure i MySQL. 

![Przykład pulpitu nawigacyjnego aplikacji sieci web dla WordPress](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="deploy-from-azure-marketplace"></a>Wdrażanie z portalu Azure Marketplace
Wykonaj poniższe kroki, aby wdrożyć WordPress z portalu Azure Marketplace.

### <a name="sign-in-to-azure"></a>Logowanie do platformy Azure
Zaloguj się do witryny [Azure Portal](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Wdrażanie szablonu WordPress
W portalu Azure Marketplace zawiera szablony do konfigurowania zasobów, należy skonfigurować [WordPress](https://portal.azure.com/#create/WordPress.WordPress) szablonu, aby rozpocząć pracę.
   
Wprowadź następujące informacje do wdrażania aplikacji WordPress i jego zasoby.

  ![WordPress Tworzenie przepływu](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Pole         | Sugerowana wartość           | Opis  |
| ------------- |-------------------------|-------------|
| Nazwa aplikacji      | mywordpressapp          | Wprowadź nazwę aplikacji unikatowy dla użytkownika **Nazwa aplikacji sieci Web**. Ta nazwa jest używana jako część domyślną nazwę DNS dla aplikacji `<app_name>.azurewebsites.net`, więc musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure. Można później zamapować niestandardową nazwę domeny na aplikacji przed udostępnieniem użytkownikom |
| Subskrypcja  | Płatność zgodnie z rzeczywistym użyciem             | Wybierz pozycję **Subskrypcja**. Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję. |
| Grupa zasobów| mywordpressappgroup                 |    Wprowadź **grupy zasobów**. Grupa zasobów jest kontenerem logicznym, do których zasobów platformy Azure, takich jak aplikacje sieci web, baz danych, które jest wdrożone i zarządzane. Można utworzyć grupy zasobów lub użyć istniejącego |
| Plan usługi App Service | myappplan          | Plany usług aplikacji reprezentują kolekcji zasobów fizycznych używana do hostowania aplikacji. Wybierz **lokalizacji** i **warstwa cenowa**. Aby uzyskać więcej informacji o cenach, zobacz [usługi aplikacji — warstwa cenowa](https://azure.microsoft.com/pricing/details/app-service/) |
| Database (Baza danych)      | mywordpressapp          | Wybierz dostawcę odpowiednią bazę danych MySQL. Sieci Web obsługuje aplikacje **ClearDB**, **bazy danych Azure dla programu MySQL** i **MySQL w aplikacji**. Aby uzyskać więcej informacji, zobacz [bazy danych konfiguracji](#database-config) poniższej sekcji. |
| Application Insights | ON lub OFF          | Jest to opcjonalne. [Usługa Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) umożliwia monitorowanie aplikacji sieci web, klikając **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Konfiguracja bazy danych
Wykonaj poniższe kroki do wybranych dostawcy bazy danych MySQL.  Zaleca się, że baza danych zarówno aplikacji sieci Web i MySQL, być w tej samej lokalizacji.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) to rozwiązanie innej firmy w pełni zintegrowane usługi MySQL na platformie Azure. Aby można było używać bazy danych ClearDB, konieczne będzie skojarzenia karty kredytowej z [konta Azure](http://account.windowsazure.com/subscriptions). W przypadku wybrania dostawcy bazy danych ClearDB można wyświetlić listę istniejących baz danych, aby wybrać, lub kliknij przycisk **Utwórz nowy** przycisk, aby utworzyć bazę danych.

![Utwórz ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)
[Bazy danych platformy Azure dla programu MySQL](https://azure.microsoft.com/en-us/services/mysql) zapewnia zarządzana usługa bazy danych dla rozwoju aplikacji i wdrożenia, które umożliwia wstanie bazę danych MySQL w minutach i skalowanie na bieżąco w chmurze większość zaufania. Przy użyciu modeli cenową włącznie, Pobierz wszystkie możliwości mają takie jak wysoka dostępność, bezpieczeństwo i odzyskiwanie — wbudowane, bez dodatkowych kosztów. Kliknij przycisk **warstwa cenowa** wybrać inną [warstwy cenowej](https://azure.microsoft.com/pricing/details/mysql). Aby użyć istniejącej bazy danych lub istniejącego serwera MySQL, użyj istniejącej grupy zasobów, w której znajduje się serwer. 

![Konfigurowanie ustawień bazy danych dla aplikacji sieci Web](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure bazy danych MySQL (wersja zapoznawcza) i aplikacji sieci Web w systemie Linux (wersja zapoznawcza) nie są dostępne we wszystkich regionach. Aby dowiedzieć się więcej o [bazy danych Azure dla programu MySQL (wersja zapoznawcza)](https://docs.microsoft.com/en-us/azure/mysql) i [aplikacji sieci Web w systemie Linux](./app-service-linux-intro.md) ograniczenia. 

#### <a name="mysql-in-app"></a>MySQL w aplikacji
[MySQL w aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) to funkcja usługi App Service, dzięki czemu natywnie systemem MySql na platformie. Podstawowe funkcje obsługiwane w wersji funkcji:

- Serwer MySQL uruchomiona na tym samym wystąpieniu obok siebie z serwerem sieci web hosta witryny. Zwiększa to wydajność aplikacji.
- Magazyn jest udostępniana między zarówno MySQL i pliki aplikacji sieci web. Uwaga z planami wolnego i udostępnione, które można napotkać naszych limity przydziału po użyciu lokacji na podstawie akcje można wykonać. Zapoznaj się z [limity przydziału](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) dla planów wolnego i udostępnione.
- Należy włączyć rejestrowanie powolne zapytań i ogólne rejestrowania dla programu MySQL. Zauważ, że to może wpłynąć na wydajność witryny i powinna nie zawsze jest włączona. Funkcja rejestrowania pomaga w badaniu problemów z aplikacjami. 

Aby uzyskać więcej informacji, zapoznaj się z tym [artykułu](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![Zarządzanie w aplikacji MySQL](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Możesz obserwować postęp, klikając ikonę dzwonka w górnej części strony portalu podczas wdrażania aplikacji WordPress.    
![Wskaźnik postępu](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Zarządzanie nową aplikacją sieci Web platformy Azure

Przejdź do witryny Azure Portal, aby przyjrzeć się właśnie utworzonej aplikacji sieci Web.

W tym celu zaloguj się do witryny [https://portal.azure.com](https://portal.azure.com).

W lewym menu kliknij pozycję **App Services**, a następnie kliknij nazwę swojej aplikacji sieci Web platformy Azure.

![Nawigacja w portalu do aplikacji sieci Web platformy Azure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Jesteś teraz w _bloku_ aplikacji sieci Web (stronie portalu, która jest otwierana w poziomie).

Domyślnie blok aplikacji sieci Web wyświetla stronę **Przegląd**. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Karty po lewej stronie bloku pokazują różne strony konfiguracji, które można otworzyć.

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Te karty w bloku pokazują wiele doskonałych funkcji, które możesz dodać do aplikacji sieci Web. Poniższa lista zawiera tylko kilka możliwości:

* Mapowanie niestandardowej nazwy DNS
* Tworzenie powiązania niestandardowego certyfikatu SSL
* Konfigurowanie ciągłego wdrażania
* Skalowanie w górę i w dół
* Dodawanie uwierzytelniania użytkownika

Ukończ pracę Kreatora instalacji WordPress 5 minut do pracy z aplikacjami WordPress. Zapoznaj się z [dokumentacji Wordpress](https://codex.WordPress.org/) umożliwiające tworzenie aplikacji sieci web.

![Kreator instalacji WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Konfigurowanie aplikacji 
Istnieje wiele kroków zarządzania aplikacji WordPress, aby była gotowa do użycia w środowisku produkcyjnym. Wykonaj następujące kroki, aby skonfigurować i zarządzać nimi aplikacji WordPress:

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Przekazywanie lub przechowywania dużych plików** |[Wtyczki WordPress dla przy użyciu magazynu obiektów Blob](https://wordpress.org/plugins/windows-azure-storage/)|
| **Wyślij wiadomość e-mail** |Zakupu [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) poczty e-mail usługi i użyj [wtyczki WordPress dla przy użyciu SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) ją skonfigurować|
| **Niestandardowa nazwa domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md) |
| **PROTOKÓŁ HTTPS** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Sprawdzanie poprawności produkcji wstępnej** |[Konfigurowanie środowisk przemieszczania i deweloperów aplikacji sieci web w usłudze Azure App Service](web-sites-staged-publishing.md)|
| **Monitorowanie i rozwiązywanie problemów** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md) i [monitorowanie aplikacji sieci Web w usłudze Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Wdrażanie witryny** |[Wdrażanie aplikacji sieci web w usłudze Azure App Service](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Zabezpieczanie aplikacji 
Istnieje wiele kroków zarządzania aplikacji WordPress, aby była gotowa do użycia w środowisku produkcyjnym. Wykonaj następujące kroki, aby skonfigurować i zarządzać nimi aplikacji WordPress:

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Silne nazwy użytkownika i hasła**|  Często Zmień hasło. Czy nie nazw użytkowników użyj powszechnie używane, takich jak *admin* lub *wordpress* itp. Wymusić unikatowe nazwy użytkownika i silne hasła wszystkich użytkowników WordPress. |
| **Aktualności** | Aktualizowanie programu WordPress core, kompozycje, wtyczek. Użyj najnowszej środowiska wykonawczego PHP, dostępne w usłudze Azure App service |
| **Aktualizowanie kluczy zabezpieczeń WordPress** | Aktualizacja [klucz zabezpieczeń WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) zwiększające szyfrowania przechowywane w plikach cookie|

## <a name="improve-performance"></a>Poprawianie wydajności
Wydajność w chmurze jest osiągana, przede wszystkim dzięki buforowaniu oraz skalowalnych w poziomie. Jednak należy rozważyć pamięć, przepustowości i inne atrybuty hosting aplikacji sieci Web.

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Zrozumieć możliwości wystąpienia usługi aplikacji** |[Informacje o cenach, łącznie z możliwości warstwy usług aplikacji](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Zasoby pamięci podręcznej** |Użyj [pamięci podręcznej Azure Redis](https://azure.microsoft.com/en-us/services/cache/), lub jeden z buforowania oferty w [magazynu Azure](https://azuremarketplace.microsoft.com) |
| **Skalowanie aplikacji** |Musi przebiegać proces skalowania [aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md) i/lub baza danych MySQL. MySQL w aplikacji nie obsługuje skalowania w poziomie, dlatego należy wybierać ClearDB bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza). [Skalowanie bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/pricing/details/mysql/) lub jeśli za pomocą [ClearDB wysokiej dostępności routingu](http://w2.cleardb.net/faqs/) można skalować bazy danych |

## <a name="availability-and-disaster-recovery"></a>Dostępność i odzyskiwanie po awarii
Wysoka dostępność obejmuje aspekt odzyskiwania po awarii, aby utrzymać ciągłość prowadzenia działalności biznesowej. Planowanie błędów i awarii w chmurze wymaga szybko rozpoznać niepowodzenia. Te rozwiązania pomagają, zaimplementować strategię wysokiej dostępności.

| Aby wykonać tę czynność... | Użyj polecenia... |
| --- | --- |
| **Lokacje Równoważenie obciążenia** lub **geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Tworzenie kopii zapasowej i przywracanie** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md) i [Przywracanie aplikacji sieci web w usłudze Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat różnych funkcji usługi [usługi aplikacji na tworzenie i](/app-service-web/).