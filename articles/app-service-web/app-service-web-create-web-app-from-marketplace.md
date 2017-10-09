---
title: aaaCreate aplikacji sieci web z hello Azure Marketplace | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate nowej aplikacji sieci web WordPress z hello Azure Marketplace przy użyciu hello portalu Azure."
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
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Tworzenie aplikacji sieci web z hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Hello Azure Marketplace udostępnia szeroką gamę popularnych aplikacji sieci web opracowanych przez Wspólnot oprogramowania typu open source, na przykład WordPress i Umbraco CMS. Z tego samouczka, dowiesz się, jak toocreate aplikacji WordPress z portalu Azure marketplace.
które tworzy bazę danych aplikacji sieci Web platformy Azure i MySQL. 

![Przykład pulpitu nawigacyjnego aplikacji sieci web dla WordPress](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Przed rozpoczęciem 

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="deploy-from-azure-marketplace"></a>Wdrażanie z portalu Azure Marketplace
Wykonaj kroki hello poniżej toodeploy WordPress z portalu Azure Marketplace.

### <a name="sign-in-tooazure"></a>Zaloguj się tooAzure
Zaloguj się za toohello [portalu Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Wdrażanie szablonu WordPress
Hello Azure Marketplace zawiera szablony tworzenia zasobów, Instalator hello [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget szablonu uruchomiona.
   
Wprowadź poniżej hello aplikacji WordPress hello toodeploy informacji i zasobów.

  ![WordPress Tworzenie przepływu](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Pole         | Sugerowana wartość           | Opis  |
| ------------- |-------------------------|-------------|
| Nazwa aplikacji      | mywordpressapp          | Wprowadź nazwę aplikacji unikatowy dla użytkownika **Nazwa aplikacji sieci Web**. Ta nazwa jest używana jako część nazwy DNS domyślne hello aplikacji `<app_name>.azurewebsites.net`, a więc musi toobe unikatowy przez wszystkie aplikacje na platformie Azure. Później można mapować aplikacji tooyour nazwy domeny niestandardowej przed udostępnieniem jej tooyour użytkowników |
| Subskrypcja  | Płatność zgodnie z rzeczywistym użyciem             | Wybierz pozycję **Subskrypcja**. Jeśli masz wiele subskrypcji, wybierz odpowiednią subskrypcję hello. |
| Grupa zasobów| mywordpressappgroup                 |    Wprowadź **grupy zasobów**. Grupa zasobów jest kontenerem logicznym, do których zasobów platformy Azure, takich jak aplikacje sieci web, baz danych, które jest wdrożone i zarządzane. Można utworzyć grupy zasobów lub użyć istniejącego |
| Plan usługi App Service | myappplan          | Plany usług aplikacji reprezentują hello zbiór toohost fizyczne zasoby używane aplikacje. Wybierz hello **lokalizacji** i hello **warstwa cenowa**. Aby uzyskać więcej informacji o cenach, zobacz [usługi aplikacji — warstwa cenowa](https://azure.microsoft.com/pricing/details/app-service/) |
| Database (Baza danych)      | mywordpressapp          | Wybierz hello dostawcy odpowiednie bazy danych dla programu MySQL. Sieci Web obsługuje aplikacje **ClearDB**, **bazy danych Azure dla programu MySQL** i **MySQL w aplikacji**. Aby uzyskać więcej informacji, zobacz [bazy danych konfiguracji](#database-config) poniższej sekcji. |
| Application Insights | ON lub OFF          | Jest to opcjonalne. [Usługa Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) umożliwia monitorowanie aplikacji sieci web, klikając **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Konfiguracja bazy danych
Wykonaj kroki hello poniżej do wybranych dostawcy bazy danych MySQL.  Zaleca się hello należeć do tej bazy danych zarówno aplikacji sieci Web i MySQL tej samej lokalizacji.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) to rozwiązanie innej firmy w pełni zintegrowane usługi MySQL na platformie Azure. W bazach danych ClearDB toouse kolejności, konieczne będzie tooassociate tooyour karty kredytowej [konta Azure](http://account.windowsazure.com/subscriptions). W przypadku wybrania dostawcy bazy danych ClearDB możesz wyświetlić listę istniejących toochoose baz danych z lub kliknąć przycisk **Utwórz nowy** toocreate przycisk bazy danych.

![Utwórz ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)
[Bazy danych platformy Azure dla programu MySQL](https://azure.microsoft.com/en-us/services/mysql) zapewnia tworzenia aplikacji i wdrożenia, które umożliwia toostand bazę danych MySQL w protokole i skali na powitania udać w chmurze hello ufasz najbardziej zarządzana usługa bazy danych. Przy użyciu modeli cenową włącznie, Pobierz wszystkie funkcje hello mają takie jak wysoka dostępność, bezpieczeństwo i odzyskiwanie — wbudowane, bez dodatkowych kosztów. Kliknij przycisk **warstwa cenowa** toochoose inną [warstwy cenowej](https://azure.microsoft.com/pricing/details/mysql). toouse istniejącej bazy danych lub istniejący serwer MySQL, użyj istniejącej grupy zasobów, w których hello znajduje się serwer. 

![Konfigurowanie ustawień bazy danych hello hello aplikacji sieci web](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Azure bazy danych MySQL (wersja zapoznawcza) i aplikacji sieci Web w systemie Linux (wersja zapoznawcza) nie są dostępne we wszystkich regionach. więcej informacji na temat toolearn [bazy danych Azure dla programu MySQL (wersja zapoznawcza)](https://docs.microsoft.com/en-us/azure/mysql) i [aplikacji sieci Web w systemie Linux](./app-service-linux-intro.md) ograniczenia. 

#### <a name="mysql-in-app"></a>MySQL w aplikacji
[MySQL w aplikacji](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) to funkcja usługi aplikacji, co umożliwia uruchomienie MySql natywnie na platformie hello. Witaj podstawowe funkcje obsługiwane w wersji hello hello funkcji:

- MySQL na serwerze działa na powitania takie same wystąpienia równolegle z witryny sieci web serwera hostingu hello. Zwiększa to wydajność aplikacji.
- Magazyn jest udostępniana między zarówno MySQL i pliki aplikacji sieci web. Uwaga z planami wolnego i udostępnione, które można napotkać naszych limity przydziału, gdy za pomocą witryny hello oparte na powitania akcje wykonać. Zapoznaj się z [limity przydziału](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) dla planów wolnego i udostępnione.
- Należy włączyć rejestrowanie powolne zapytań i ogólne rejestrowania dla programu MySQL. Warto zauważyć, że to może wpłynąć na wydajność lokacji hello powinien nie zawsze jest włączona. Funkcja rejestrowania Hello pomaga w badaniu problemów z aplikacjami. 

Aby uzyskać więcej informacji, zapoznaj się z tym [artykułu](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![Zarządzanie w aplikacji MySQL](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Możesz obserwować postęp hello, klikając ikonę dzwonka hello u góry strony portalu hello podczas wdrażania aplikacji WordPress powitalne hello.    
![Wskaźnik postępu](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Zarządzanie nową aplikacją sieci Web platformy Azure

Przejdź toohello tootake portalu Azure przyjrzeć się hello aplikacji sieci web, który został utworzony.

toodo, zaloguj się za[https://portal.azure.com](https://portal.azure.com).

W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Jesteś teraz w _bloku_ aplikacji sieci Web (stronie portalu, która jest otwierana w poziomie).

Domyślnie bloku aplikacji sieci web zawiera hello **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. Tutaj możesz również wykonywać podstawowe zadania zarządzania, takie jak przeglądanie, zatrzymywanie, uruchamianie, ponowne uruchamianie i usuwanie. Hello karty po lewej stronie powitania bloku hello pokazuje hello innej konfiguracji stron, które można otworzyć.

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Te karty w bloku hello zawierają hello wiele aplikacji sieci web tooyour można dodać funkcje. powitania po liście oferuje kilka możliwości hello:

* Mapowanie niestandardowej nazwy DNS
* Tworzenie powiązania niestandardowego certyfikatu SSL
* Konfigurowanie ciągłego wdrażania
* Skalowanie w górę i w dół
* Dodawanie uwierzytelniania użytkownika

Ukończyć powitalnych 5-minutowy WordPress instalacji Kreator toohave aplikacji WordPress do pracy. Zapoznaj się z [dokumentacji Wordpress](https://codex.WordPress.org/) toodevelop aplikacji sieci web.

![Kreator instalacji WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Konfigurowanie aplikacji 
Istnieje wiele kroków zarządzania aplikacji WordPress, aby była gotowa do użycia w środowisku produkcyjnym. Wykonaj te kroki tooconfigure aplikacji i zarządzanie nią WordPress:

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Przekazywanie lub przechowywania dużych plików** |[Wtyczki WordPress dla przy użyciu magazynu obiektów Blob](https://wordpress.org/plugins/windows-azure-storage/)|
| **Wyślij wiadomość e-mail** |Zakupu [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) poczty e-mail usługi i użyj hello [wtyczki WordPress dla przy użyciu SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure go|
| **Niestandardowa nazwa domeny** |[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](app-service-web-tutorial-custom-domain.md) |
| **PROTOKÓŁ HTTPS** |[Włącz protokół HTTPS dla aplikacji sieci web w usłudze Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Sprawdzanie poprawności produkcji wstępnej** |[Konfigurowanie środowisk przemieszczania i deweloperów aplikacji sieci web w usłudze Azure App Service](web-sites-staged-publishing.md)|
| **Monitorowanie i rozwiązywanie problemów** |[Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](web-sites-enable-diagnostic-log.md) i [monitorowanie aplikacji sieci Web w usłudze Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Wdrażanie witryny** |[Wdrażanie aplikacji sieci web w usłudze Azure App Service](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Zabezpieczanie aplikacji 
Istnieje wiele kroków zarządzania aplikacji WordPress, aby była gotowa do użycia w środowisku produkcyjnym. Wykonaj te kroki tooconfigure aplikacji i zarządzanie nią WordPress:

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Silne nazwy użytkownika i hasła**|  Często Zmień hasło. Czy nie nazw użytkowników użyj powszechnie używane, takich jak *admin* lub *wordpress* itp. Wymuś wszystkich WordPress użytkowników toouse unikatowych nazw użytkowników i silne hasła. |
| **Aktualności** | Zachowaj programu WordPress core, kompozycje, wtyczek się toodate. Użyj hello najnowsze środowiska uruchomieniowego języka PHP dostępnych w usłudze Azure App service |
| **Aktualizowanie kluczy zabezpieczeń WordPress** | Aktualizacja [klucz zabezpieczeń WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) szyfrowania tooimprove przechowywane w plikach cookie|

## <a name="improve-performance"></a>Poprawianie wydajności
Wydajność w chmurze hello jest osiągana, przede wszystkim dzięki buforowaniu oraz skalowalnych w poziomie. Jednak należy rozważyć hello pamięci, przepustowości i inne atrybuty hosting aplikacji sieci Web.

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Zrozumieć możliwości wystąpienia usługi aplikacji** |[Informacje o cenach, łącznie z możliwości warstwy usług aplikacji](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Zasoby pamięci podręcznej** |Użyj [pamięci podręcznej Azure Redis](https://azure.microsoft.com/en-us/services/cache/), lub jeden z innych buforowania oferty w hello hello [magazynu Azure](https://azuremarketplace.microsoft.com) |
| **Skalowanie aplikacji** |Należy tooscale [hello aplikacji sieci web w usłudze Azure App Service](web-sites-scale.md) i/lub baza danych MySQL. MySQL w aplikacji nie obsługuje skalowania w poziomie, dlatego należy wybierać ClearDB bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza). [Skalowanie bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza)](https://azure.microsoft.com/en-us/pricing/details/mysql/) lub jeśli za pomocą [ClearDB wysokiej dostępności routingu](http://w2.cleardb.net/faqs/) tooscale zapasową bazy danych |

## <a name="availability-and-disaster-recovery"></a>Dostępność i odzyskiwanie po awarii
Wysoka dostępność obejmuje hello aspekt ciągłość działania toomaintain odzyskiwania po awarii. Planowanie błędów i awarii w chmurze hello wymaga błędów hello toorecognize szybko. Te rozwiązania pomagają, zaimplementować strategię wysokiej dostępności.

| toodo to... | Użyj polecenia... |
| --- | --- |
| **Lokacje Równoważenie obciążenia** lub **geograficznie-dystrybucji lokacji** |[Kierować ruchem z usługi Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Tworzenie kopii zapasowej i przywracanie** |[Tworzenie kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md) i [Przywracanie aplikacji sieci web w usłudze Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat różnych funkcji usługi [toodevelop usługi aplikacji i skali](/app-service-web/).
