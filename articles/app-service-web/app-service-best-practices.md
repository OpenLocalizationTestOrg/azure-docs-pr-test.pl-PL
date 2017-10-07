---
title: "aaaBest wskazówki dotyczące usługi Azure App Service"
description: "Dowiedz się, najlepsze rozwiązania i rozwiązywanie problemów dotyczących usługi Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Najlepsze rozwiązania dotyczące usługi Azure App Service
W tym artykule przedstawiono najlepsze rozwiązania dotyczące używania [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Wspólnej lokalizacji
Podczas tworzenia rozwiązania, takie jak aplikacji sieci web i bazy danych zasobów platformy Azure znajdują się w różnych regionach hello efekty może obejmować następujące hello:

* Większe opóźnienia w łączności między zasobami
* Opłaty finansowe dla danych wychodzących transferu między regionu wspomnianego na powitania [Azure cennikiem](https://azure.microsoft.com/pricing/details/data-transfers).

Kolokacji hello tym samym regionie jest najlepsze w przypadku tworzenia rozwiązania, takie jak aplikacja sieci web zasobów platformy Azure i konto bazy danych lub magazyn używany toohold zawartości lub danych. Podczas tworzenia zasobów, które należy upewnić się, że są one hello tego samego regionu Azure, chyba że masz firmy lub projektowania ich nie toobe przyczyna. Można przenieść toohello aplikację usługi aplikacji — tym samym regionie co baza danych dzięki wykorzystaniu hello [usługi aplikacji — funkcja klonowania](app-service-web-app-cloning-portal.md) obecnie dostępne dla aplikacji Plan usługi aplikacji — warstwa Premium.   

## <a name="memoryresources"></a>Gdy aplikacje korzystać z większej ilości pamięci, niż oczekiwano
Gdy zauważysz aplikacji wymaga więcej pamięci niż oczekiwano wskazywany przez monitorowanie lub usługi zalecenia należy wziąć pod uwagę hello [aplikacji usługi automatyczne naprawianie funkcji](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Jedną z opcji hello funkcji Automatyczne naprawianie hello trwa akcje niestandardowe w oparciu próg pamięci. Akcje span spektrum hello z tooinvestigation powiadomienia e-mail za pośrednictwem ograniczenie tooon miejscu zrzutu pamięci przez proces roboczy hello odtwarzania. Automatyczne naprawianie można skonfigurować za pomocą pliku web.config i za pośrednictwem interfejsu użytkownika przyjazną zgodnie z opisem w w tym blogu dla hello [aplikacji usługi pomocy technicznej witryny rozszerzenia](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Gdy aplikacje korzystać więcej procesorów niż oczekiwano
Jeśli widać, że aplikacja wykorzystuje więcej procesorów niż oczekiwano lub napotyka powtarzany nagłego Procesora wskazywany przez monitorowanie lub usługi zalecenia należy wziąć pod uwagę skalowanie w i skalowania hello planu usługi aplikacji. Jeśli aplikacja jest statefull, skalowaniu jest jedyną opcją hello, natomiast w przypadku aplikacji bezstanowych, skalowania w poziomie zapewni większą elastyczność i wyższe możliwości skalowania. 

Aby uzyskać więcej informacji o aplikacjach "bezstanowych", "statefull" vs można Obejrzyj ten film: [planowanie skalowalności End-to-End wielowarstwowej aplikacji w aplikacji sieci Web platformy Microsoft Azure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid). Aby uzyskać więcej informacji na temat opcji skalowania i skalowanie automatyczne usługi aplikacji przeczytaj: [skalowanie aplikacji sieci Web w usłudze Azure App Service](web-sites-scale.md).  

## <a name="socketresources"></a>Gdy wyczerpania zasobów gniazda
Typową przyczyną wyczerpuje wychodzące połączenia TCP jest Użyj hello bibliotek klienta, które nie są zaimplementowaną tooreuse połączeń TCP, lub w przypadku hello protokół poziomu wyższej takich jak HTTP - Keep-Alive nie wykorzystywane. Przejrzyj dokumentację hello na każdej z bibliotek hello odwołuje się aplikacji hello w tooensure Twojego planu usługi App Service są skonfigurowane lub dostępne w kodzie wydajne ponowne połączeń wychodzących. Wykonaj również hello biblioteka dokumentacji wskazówki dotyczące tworzenia odpowiednich i wersji lub czyszczenia tooavoid przeciek połączenia. W czasie dochodzenia takie biblioteki klienta wpływ postępu mogą skorygowane przez skalowanie w poziomie toomultiple wystąpień.  

## <a name="appbackup"></a>Gdy aplikacja kopii zapasowej uruchamia się niepowodzeniem
Witaj dwie najbardziej typowe przyczyny niepowodzenia tworzenia kopii zapasowej aplikacji są: nieprawidłowy miejsca do magazynowania i nieprawidłowa konfiguracja bazy danych. Takie błędy zazwyczaj się tak zdarzyć przy istnieją zmiany toostorage lub bazy danych zasobów lub zmiany dotyczące tooaccess tych zasobów (np. poświadczenia zaktualizowane hello bazy danych, w menu ustawienia kopii zapasowej hello). Tworzenie kopii zapasowych zwykle uruchamiane zgodnie z harmonogramem i wymagają toostorage dostępu (dla wyprowadzania hello kopię zapasową plików) i baz danych (kopiowanie i odczytywania zawartości toobe uwzględnione w kopii zapasowej hello). Witaj wynik niepowodzenie tooaccess albo te zasoby będą zgodne niepowodzenia wykonywania kopii zapasowej. 

Gdy wystąpi niepowodzenie wykonywania kopii zapasowej, zapoznaj się z tematem najnowszych toounderstand wyniki typu błędu jest wykonywane. W przypadku hello niepowodzenia dostępu do magazynu Przejrzyj i zaktualizowanie ustawień magazynu hello używane w konfiguracji kopii zapasowej hello. W przypadku hello niepowodzenia dostępu do bazy danych Przejrzyj i zaktualizuj Twojej parametry połączenia w ustawieniach aplikacji; Aby kontynuować tooupdate Twojego tooproperly konfiguracji kopii zapasowej to hello wymagane bazy danych. Aby uzyskać więcej informacji na temat tworzenia kopii zapasowej aplikacji Zobacz hello [kopii zapasowej aplikacji sieci web w usłudze Azure App Service](web-sites-backup.md) dokumentacji.

## <a name="nodejs"></a>Kiedy nowych aplikacji Node.js są wdrożone tooAzure usługi aplikacji
Usługi aplikacji Azure domyślnej konfiguracji dla aplikacji Node.js jest zamierzone toobest koloru hello potrzeby najbardziej typowych aplikacji. Jeśli Konfiguracja aplikacji Node.js będzie korzystać ze spersonalizowanego dostrajania wydajności tooimprove lub optymalizować wykorzystanie zasobów dla zasobów Procesora i pamięci/sieci, można przejrzeć naszych najlepszych rozwiązań i kroki rozwiązywania problemów. W tym artykule dokumentacji opisano ustawienia programu iisnode hello może być konieczne tooconfigure dla aplikacji Node.js, w tym artykule opisano hello różnych scenariuszy lub problemy, które mogą miała dostęp do aplikacji i przedstawia sposób tooaddress te problemy: [najlepsze rozwiązania i Przewodnik rozwiązywania problemów dla węzła aplikacji w usłudze Azure App Service](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

