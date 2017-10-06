---
title: "aaaManage usług Azure Analysis Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage usług Analysis Services serwera na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Zarządzanie usług Analysis Services
Po utworzeniu serwerem usług Analysis Services na platformie Azure, mogą występować niektórych zadań administracji i zarządzania należy tooperform od razu lub jakimś dół hello drogowej. Na przykład uruchom toohello odświeżanie danych, kontrolowania, kto może uzyskać dostępu modeli hello na serwerze lub monitorowania kondycji serwera przetwarzania. Niektóre zadania zarządzania można wykonać tylko w portalu Azure, inne osoby w programu SQL Server Management Studio (SSMS), a niektóre zadania można to zrobić na dwa.

## <a name="azure-portal"></a>Azure Portal
[Azure portal](http://portal.azure.com/) pozwala można tworzyć i usuwać serwery, monitorowanie zasobów serwera, Zmień rozmiar, i zarządzanie, kto ma dostęp do serwerów tooyour.  Jeśli występują problemy, możesz również przekazywać żądania pomocy technicznej.

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Połączenie serwera tooyour na platformie Azure to podobnie jak łączenie tooa wystąpienie serwera w organizacji. Z programu SSMS można wykonywać wiele hello same zadania, takie jak przetwarzania danych lub utworzyć skrypt przetwarzania, Zarządzanie rolami i przy użyciu programu PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Pobierz i zainstaluj narzędzia SSMS
tooget hello wszystkie najnowsze funkcje i czynności daje płynne hello podczas łączenia z serwerem usług Azure Analysis Services tooyour, upewnij się, że używasz najnowszej wersji programu SSMS hello. 

[Pobieranie programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect za pomocą narzędzia SSMS
 Korzystając z narzędzia SSMS, przed łączącego tooyour powitania serwera po raz pierwszy, upewnij się, że nazwa użytkownika jest uwzględniona w grupie Administratorzy usług analizy hello. toolearn więcej, zobacz [administratorom serwerów](#server-administrators) dalszej części tego artykułu.

1. Przed nawiązaniem połączenia należy nazwę serwera na powitania tooget. W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwę serwera na powitania kopiowania.
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. W programie SSMS > **Eksplorator obiektów**, kliknij przycisk **Connect** > **usług Analysis Services**.
3. W hello **połączyć tooServer** okno dialogowe, Wklej w hello nazwę serwera, a następnie w **uwierzytelniania**, wybierz jedną z hello następujące typy uwierzytelniania:
   
    **Uwierzytelnianie systemu Windows** toouse poświadczeń domena azwa_użytkownika i hasło systemu Windows.

    **Uwierzytelnianie hasłem usługi Active Directory** toouse konta organizacyjnego. Na przykład podczas nawiązywania połączenia ze spoza domeny przyłączone do komputera.

    **Uwierzytelnianie usługi Active Directory uniwersalnych** toouse [nieinterakcyjnym lub usługi Multi-Factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Połącz w programie SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Administratorzy serwera i bazy danych użytkowników
W usłudze Azure Analysis Services istnieją dwa typy użytkowników, administratorów serwera i bazy danych użytkowników. Użytkownicy obu typów musi znajdować się w usłudze Azure Active Directory i musi być określona za pomocą adresu e-mail organizacji lub nazwy UPN. toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Rozwiązywanie problemów z połączeniem
Podczas nawiązywania połączenia przy użyciu narzędzia SSMS, jeśli wystąpią problemy, może być konieczne tooclear hello logowania w pamięci podręcznej. Nic nie toodisc pamięci podręcznej. tooclear hello pamięci podręcznej, zamknij i ponowne uruchomienie hello łączą procesu. 

## <a name="next-steps"></a>Następne kroki
Jeśli nie zostało już wdrożony nowy serwer tooyour modelu tabelarycznego, teraz jest odpowiedni moment. toolearn więcej, zobacz [wdrażanie usług Analysis Services tooAzure](analysis-services-deploy.md).

Po wdrożeniu serwera tooyour modelu, możesz za pomocą klienta lub przeglądarki tooit tooconnect gotowe. toolearn więcej, zobacz [Pobierz dane z serwera usług Azure Analysis Services](analysis-services-connect.md).

