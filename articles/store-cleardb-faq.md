---
title: "aaaFAQ w przypadku baz danych ClearDB MySql w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na pytania toocommon dotyczące korzystania z usługi aplikacji Azure baz danych ClearDB MySQL."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Często zadawane pytania dotyczące baz danych ClearDB MySQL w usłudze Azure App Service
Często zadawane pytania odpowiedzi na często zadawane pytania dotyczące przy użyciu i zakup ClearDB MySQL baz danych na potrzeby aplikacji sieci Web Azure.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Jakie opcje są dostępne dla programu MySQL na platformie Azure?
Istnieje kilka opcji:

* [Baza danych ClearDB MySQL udostępnionych](/marketplace/partners/cleardb/databases/)
* [Klastry ClearDB MySQL — wersja Premium](/marketplace/partners/cleardb-clusters/cluster/)
* [Klaster programu MySQL uruchomionych na maszynie Wirtualnej platformy Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Pojedyncze wystąpienie MySQL uruchomionych na maszynie Wirtualnej platformy Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB MySQL, usługi hostingu jest i zarządza hello MySQL infrastruktury. Po uruchomieniu własnych klaster programu MySQL lub bazy danych na maszynie wirtualnej platformy Azure, masz tooset hello MySQL serwera i aktualizacji poprawki.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>Należy karty kredytowej dla aplikacji sieci Web hello + MySQL szablonu w hello Azure Marketplace?
To zależy od typu hello subskrypcji, którego używasz. Poniżej przedstawiono niektóre typy typowe subskrypcji:

* [Płatność zgodnie z rzeczywistym](/offers/ms-azr-0003p/): wymaga kart kredytowych, oraz gdy kupić płatną bazy danych MySQL rozliczany karty kredytowej.
* [Bezpłatna wersja próbna](https://azure.microsoft.com/pricing/free-trial/): zawiera środków dla usługi użycia z Microsoft Azure, ale nie zezwala na zakup zasobów innych firm. toopurchase usług innych firm lub płatną bazy danych MySQL należy toouse karty kredytowej włączone subskrypcji. Dla aplikacji sieci Web można utworzyć bezpłatne ClearDB MySQL bazy danych.
* [Subskrypcja MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) i **MSDN: tworzenie testowanie płatności zgodnie z rzeczywistym**: podobne tooFree wersji próbnej subskrypcji MSDN wymaga toohave toopurchase karty kredytowej płatną rozwiązania MySQL z ClearDB.
* [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/): EA klienci są rozliczane przed ich EA co kwartał dla wszystkich swoich zakupów (niezależny) Azure Marketplace na fakturze oddzielne, skonsolidowanego. Rozliczenie jest poza hello zobowiązaniom pieniężnym na zakupy w witrynie marketplace. Należy pamiętać, że w tej chwili magazynu Azure nie jest dostępne toocustomers zarejestrowane w Azerbejdżanu, Chorwacji, Norwegia i Portoryko. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): można utworzyć tylko baza danych ClearDB wolnego dla aplikacji sieci Web. Nie ma żadnego limitu liczby hello wolnego ClearDB MySQL baz danych, które można utworzyć. Należy pamiętać, że bezpłatnych baz danych nie mogą toobe używane dla aplikacji sieci web w środowisku produkcyjnym, ponieważ ta usługa jest przeznaczona tylko dla wersji próbnej.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Dlaczego naliczono daną opłatę 3.50 $ dla aplikacji sieci Web + MySQL z hello Azure Marketplace?
opcja bazy danych domyślne Hello jest Titan, czyli 3.50 $. Firma Microsoft nie pokazuj koszt hello podczas tworzenia bazy danych, a przez pomyłkę zakupie bazy danych, które nie mają być. Próbujemy toofind w sposób tooimprove hello środowisku, ale do tego czasu musi sprawdzić wszystkie Twoje wybranych warstw cenowych dla aplikacji sieci web i bazy danych, przed kliknięciem przycisku **Utwórz** i rozpoczęciu wdrażania hello hello zasobów.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>Używam MySQL na własną maszyny wirtualnej platformy Azure. Czy można połączyć bazy danych toomy aplikacji sieci web platformy Azure?
Tak. Bazy danych tooyour aplikacji sieci web można łączyć z maszyną Wirtualną Azure została podana aplikacji sieci web tooyour dostępu zdalnego. Aby uzyskać więcej informacji, zobacz [zainstalować bazy danych MySQL na maszynie wirtualnej](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>W których krajach są klastry ClearDB MySQL — wersja Premium, obsługiwane?
[Klastry ClearDB MySQL — wersja Premium](/marketplace/partners/cleardb-clusters/cluster/) są dostępne we wszystkich regionach platformy Azure na całym świecie z wyjątkiem hello Indie, Australia Brazylia Południowa i Chinach.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>Można utworzyć nowego klastra przed toocreating bazy danych z rozwiązań klastrowych premium ClearDB?
Nie, tworzenia klastrów ClearDB pusty nie jest obsługiwany. Witaj portalu Azure pozwala toocreate baz danych w klastrze, może utworzyć nowego klastra w hello tym samym czasie.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>Będzie I wyświetlane ostrzeżenie I spróbuj toodelete bazę danych ClearDB MySQL, która jest używana przez jedną z mojej aplikacji?
Nie, Azure zostanie nie ostrzega użytkownika, jeśli usuniesz zakupu marketplace, która zależy od aplikacji.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>Regiony można utworzyć bazy danych ClearDB w?
Azure Marketplace nie jest dostępne toocustomers zarejestrowane w Azerbejdżanu, Chorwacji, Norwegia lub Portoryko. ClearDB nie jest dostępny w tych obszarach.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Jakie warstwy cenowej należy wybrać dla aplikacji sieci web w środowisku produkcyjnym i bazy danych?
Użyj podstawowego lub wyższej warstwy cenowej dla aplikacji sieci Web. ClearDB zalecamy Saturn albo Jupiter planu. Przejrzyj funkcje hello & ograniczenia każdej warstwy cenowej dla obu [aplikacje sieci Web](https://azure.microsoft.com/pricing/details/app-service/) i [baz danych ClearDB MySQL](/marketplace/partners/cleardb/databases/) hello toochoose, który potrzebom użytkownika.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Jak uaktualnić bazy danych ClearDB z jednego tooanother planu?
W hello [portalu Azure](https://portal.azure.com), można zwiększać ClearDB udostępnionej hostingu bazy danych. Przeczytaj [artykułu](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn więcej. Obecnie nie obsługujemy uaktualnienia ClearDB Premium klastrów w hello portalu Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Nie widzę mojego baza danych ClearDB w portalu Azure?
Jeśli utworzony ClearDB bazy danych przy użyciu usługi Azure Resource Manager lub [nowego portalu Azure](https://portal.azure.com), nie będą widoczne w hello [starego portalu Azure](https://manage.windowsazure.com). toowork-obejścia tego problemu jest toolink bazę danych ręcznie toohello aplikacji sieci web. Podobnie jeśli utworzyć bazę danych ClearDB w hello [starego portalu](https://manage.windowsazure.com) nie będzie można toosee stanie bazy danych w hello [nowego portalu Azure](https://portal.azure.com). Nie ma żadnych obejścia dla scenariusza ostatnie hello.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Kto I skontaktuj się z pomocy technicznej, gdy baza danych działa?
Skontaktuj się z [Obsługa ClearDB](https://www.cleardb.com/developers/help/support) dla dowolnej bazy danych problemy związane z. Można przygotować tooprovide je z informacjami o subskrypcji platformy Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>Moje rozwiązanie klastra bazy danych ClearDB MySQL można utworzyć dodatkowych użytkowników?
Nie. Nie można utworzyć dodatkowych użytkowników, ale można utworzyć dodatkowych baz danych w klastrze usługi ClearDB bazy danych.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Bazy danych serii Basic/Pro może być uaktualniony w miejscu podobne tooPlanetary planów dzisiaj w portalu ClearDB?
Tak, podstawowe serii, baz danych może być uaktualniony (60 podstawowych za pośrednictwem podstawowych 500) w miejscu. Seria Pro mogą być uaktualnienia w miejscu (125 Pro za pośrednictwem Pro 1000) z wyjątkiem Pro 60. Obecnie uaktualnienie bazy danych Pro 60 nie jest obsługiwana. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Jeśli zasoby przeprowadzić migrację z jednego tooanother subskrypcji, baza danych ClearDB MySQL uzyskać migracji także?
Po wykonaniu migracji zasobów w subskrypcjach, niektóre [ograniczenia](app-service-web/app-service-move-resources.md) zastosowania. Bazę danych ClearDB MySQL jest usługi innej firmy i dlatego nie pobrać migracji podczas migracji subskrypcji platformy Azure. Jeśli nie zarządzasz hello migracji programu MySQL bazy danych poprzednich toomigrating Azure zasobów, Twoje ClearDB MySQL baz danych można wyłączyć. Najpierw ręcznej migracji baz danych, a następnie dokonaj migracji subskrypcji platformy Azure dla aplikacji sieci web. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>Witaj limit wydatków na subskrypcję I odwołań. Po usunięciu hello limit i Moje usługi aplikacji jest w trybie online, jednak hello bazy danych nie jest dostępny. Jak ponownie włączyć bazę danych ClearDB hello?
Skontaktuj się z [Obsługa ClearDB](https://www.cleardb.com/developers/help/support) toore Włącz hello w bazie danych. Podaj je z Twojej subskrypcji platformy Azure informacji i nazwa bazy danych.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Czy można przenieść bazę danych ClearDB, z karty kredytowej subskrypcja tooan EA subskrypcji?
Istniejące bazy danych ClearDB Użyj hello karta kredytowa skojarzona z hello istniejące subskrypcje. toouse subskrypcję EA należy toomigrate danych tooa nowej bazy danych:

* Zakup nową bazę danych ClearDB z subskrypcją EA.
* Migracja danych tooyour nową bazę danych.
* Aktualizowanie aplikacji toouse hello nową bazę danych.
* Usuń stare bazy danych ClearDB.

Podczas tworzenia nowej aplikacji sieci web z obsługą MySQL (ClearDB) lub Utwórz bazę danych MySQL (ClearDB), wskazanej subskrypcji hello Określa, jak chcesz zapłacić za hello usługi. W ramach subskrypcji EA firma Microsoft nie blokuje hello nabywania usług innych firm hello takich jak ClearDB w hello portalu Azure. Umowa EA subskrypcji są rozliczane poza zobowiązania pieniężnego i są rozliczane co kwartał i zaległości. powitania klienta EA musi tooset się formę płatności, takich jak toopay karty kredytowej dla wszystkich usług innych firm w witrynie marketplace.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Gdzie można zobaczyć hello opłat za ClearDB zasobów w subskrypcji EA?
Dla klientów bezpośrednich EA opłat w witrynie Azure Marketplace są widoczne na powitania Enterprise Portal. Zauważ, że wszystkie zakupy w witrynie marketplace oraz zużycie są rozliczane poza zobowiązań i są rozliczane co kwartał i zaległości. EA klienci mają toopay bezpośrednio toohello dostawców usług innych firm oraz mogą więc przez włączenie formę płatności, takich jak karty kredytowej z ich EA konta.

Pośrednie EA klientów można znaleźć subskrypcji Azure Marketplace na powitania **Zarządzaj subskrypcjami** strony hello Enterprise Portal, ale cennik jest ukryty. Klienci powinni skontaktować się ich LSP, aby uzyskać informacje dotyczące opłat w witrynie marketplace.

Administratorzy rejestracji EA Azure można zarządzać dostępu tooAzure Marketplace usług innych firm. One wyłączone lub ponownie włączyć dostęp too3rd strona zakupach hello magazynu w zarządzanie kontami i subskrypcje w sekcji konta hello w hello Enterprise Portal.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Kto I skontaktuj się z pytaniami o płatności usługi ClearDB w mojej subskrypcji EA?
Skontaktuj się z [technicznej Enterprise](http://aka.ms/AzureEntSupport) o zakresie toobilling w ich EA rejestracji. Hello zespołem pomocy technicznej EA portalu będzie odpowiedź na Twoje pytanie lub pomóc w rozwiązaniu problemu.

## <a name="more-information"></a>Więcej informacji
[Często zadawane pytania dotyczące portalu Azure Marketplace](/marketplace/faq/)

