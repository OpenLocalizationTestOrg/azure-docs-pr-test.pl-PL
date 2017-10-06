---
title: "tooconfigure aaaHow usługi w chmurze (klasyczny portal) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze tooconfigure na platformie Azure. Dowiedz się, konfiguracji usługi w chmurze hello tooupdate i skonfiguruj wystąpień toorole dostępu zdalnego."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>W jaki sposób tooConfigure usług w chmurze
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-configure-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-configure.md)
> 
> 

Usługi w chmurze hello najczęściej używane ustawienia można skonfigurować w hello klasycznego portalu Azure. Lub, jeśli chcesz tooupdate plikach konfiguracyjnych bezpośrednio, Pobierz tooupdate pliku konfiguracji usługi, a następnie przekaż hello zaktualizowany plik i aktualizacji hello usługi w chmurze hello zmian konfiguracji. W obu przypadkach aktualizacji konfiguracji hello są wypychani tooall wystąpień roli.

Witaj klasycznego portalu Azure można też zbyt[włączyć Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)

Azure można tylko zapewnienia dostępności usług 99,95% podczas hello aktualizacji konfiguracji Jeśli masz co najmniej dwóch wystąpień roli dla każdej roli. Umożliwiająca jednego żądania klientów tooprocess maszyny wirtualnej podczas aktualizowania hello innych. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Zmiana usługi w chmurze
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **Konfiguruj**.
   
    ![Na stronie konfiguracji](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Na powitania **Konfiguruj** strony, można skonfigurować monitorowanie ustawień roli aktualizacji i wybierz system operacyjny gościa hello i rodziny wystąpień roli. 
2. W **monitorowania**, monitorowania poziomu tooVerbose hello zestawu lub minimalnym i skonfigurować parametry połączenia diagnostyki hello, które są wymagane do pełnego monitorowania.
3. Usługi ról (pogrupowane według roli) można zaktualizować hello następujące ustawienia:
   
    * **Ustawienia** zmodyfikuj wartości hello konfiguracji dodatkowych ustawień, które są określone w hello *appSettings* elementy pliku konfiguracji (cscfg) hello usługi.

    * **Certyfikaty**  
        Zmień hello odcisk palca certyfikatu, który jest używany w przypadku szyfrowania SSL dla roli. toochange certyfikatu, należy najpierw przekazać nowy certyfikat hello (na powitania **certyfikaty** strony). Następnie zaktualizuj odcisk palca hello w hello certyfikatu ciąg wyświetlany w hello ustawienia roli.
4. W **systemu operacyjnego**, można zmienić hello rodziny systemów operacyjnych lub wersja dla wystąpień roli, lub wybierz **automatyczne** tooenable automatyczne aktualizacje hello bieżącą wersję systemu operacyjnego. Ustawienia systemu operacyjnego Hello stosowane tooweb ról i proces roboczy, ale nie wpływają na maszynach wirtualnych.
   
    Podczas wdrażania hello najnowszej wersji systemu operacyjnego jest zainstalowany we wszystkich wystąpieniach ról i systemy operacyjne hello są automatycznie aktualizowane domyślnie. 
   
    Jeśli potrzebujesz dla Twojego toorun usługi chmury w innej wersji systemu operacyjnego ze względu na wymagania zgodności w kodzie, można wybrać rodziny systemów operacyjnych i wersji. W przypadku konkretnej wersji systemu operacyjnego, aktualizacje automatyczne systemu operacyjnego dla usługi w chmurze hello są wstrzymane. Konieczne będzie tooensure systemów operacyjnych hello otrzymywać aktualizacje.
   
    Jeśli należy rozwiązać wszystkie problemy ze zgodnością aplikacji mających z hello najnowszej wersji systemu operacyjnego, można włączyć Aktualizacje automatyczne systemu operacyjnego przez ustawienie wersji systemu operacyjnego hello zbyt**automatyczne**. 
   
    ![Ustawienia systemu operacyjnego](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave ustawień konfiguracji i wypychanie ich toohello wystąpienia roli, kliknij przycisk **zapisać**. (Kliknij **odrzucić** zmiany hello toocancel.) **Zapisz** i **odrzucić** po zmianie ustawienia zostaną dodane toohello paska poleceń.

## <a name="update-a-cloud-service-configuration-file"></a>Aktualizuj plik konfiguracji usługi w chmurze
1. Pobierz chmury pliku konfiguracji usługi (cscfg) hello bieżącej konfiguracji. Na powitania **Konfiguruj** dla usługi w chmurze powitania kliknij pozycję **Pobierz**. Następnie kliknij przycisk **zapisać**, lub kliknij przycisk **Zapisz jako** toosave hello pliku.
2. Po zaktualizowaniu pliku konfiguracji usługi hello, przekazywanie i stosowania aktualizacji konfiguracji hello:
   
   1. Na powitania **Konfiguruj** kliknij przycisk **przekazać**.
      
       ![Przekazywanie konfiguracji](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. W **pliku konfiguracyjnego**, użyj **Przeglądaj** tooselect hello zaktualizować pliku .cscfg.
   3. Jeśli usługi w chmurze zawiera wszystkie role, które mają tylko jedno wystąpienie, wybierz hello **zastosowanie konfiguracji, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** aktualizacji konfiguracji hello tooenable pole wyboru dla hello tooproceed ról.
      
       Jeśli nie możesz zdefiniować co najmniej dwa wystąpienia każdej roli, Azure nie może zagwarantować co najmniej 99,95% dostępności usługi w chmurze podczas aktualizacji konfiguracji usługi. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).
   4. Kliknij przycisk **OK** (znacznikiem wyboru). 

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).
* [Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure](cloud-services-role-enable-remote-desktop.md)
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).

