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
# <a name="manage-analysis-services"></a><span data-ttu-id="3078b-103">Zarządzanie usług Analysis Services</span><span class="sxs-lookup"><span data-stu-id="3078b-103">Manage Analysis Services</span></span>
<span data-ttu-id="3078b-104">Po utworzeniu serwerem usług Analysis Services na platformie Azure, mogą występować niektórych zadań administracji i zarządzania należy tooperform od razu lub jakimś dół hello drogowej.</span><span class="sxs-lookup"><span data-stu-id="3078b-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="3078b-105">Na przykład uruchom toohello odświeżanie danych, kontrolowania, kto może uzyskać dostępu modeli hello na serwerze lub monitorowania kondycji serwera przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="3078b-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="3078b-106">Niektóre zadania zarządzania można wykonać tylko w portalu Azure, inne osoby w programu SQL Server Management Studio (SSMS), a niektóre zadania można to zrobić na dwa.</span><span class="sxs-lookup"><span data-stu-id="3078b-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="3078b-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3078b-107">Azure portal</span></span>
<span data-ttu-id="3078b-108">[Azure portal](http://portal.azure.com/) pozwala można tworzyć i usuwać serwery, monitorowanie zasobów serwera, Zmień rozmiar, i zarządzanie, kto ma dostęp do serwerów tooyour.</span><span class="sxs-lookup"><span data-stu-id="3078b-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="3078b-109">Jeśli występują problemy, możesz również przekazywać żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="3078b-109">If you're having some problems, you can also submit a support request.</span></span>

![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="3078b-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3078b-111">SQL Server Management Studio</span></span>
<span data-ttu-id="3078b-112">Połączenie serwera tooyour na platformie Azure to podobnie jak łączenie tooa wystąpienie serwera w organizacji.</span><span class="sxs-lookup"><span data-stu-id="3078b-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="3078b-113">Z programu SSMS można wykonywać wiele hello same zadania, takie jak przetwarzania danych lub utworzyć skrypt przetwarzania, Zarządzanie rolami i przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3078b-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="3078b-115">Pobierz i zainstaluj narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="3078b-115">Download and install SSMS</span></span>
<span data-ttu-id="3078b-116">tooget hello wszystkie najnowsze funkcje i czynności daje płynne hello podczas łączenia z serwerem usług Azure Analysis Services tooyour, upewnij się, że używasz najnowszej wersji programu SSMS hello.</span><span class="sxs-lookup"><span data-stu-id="3078b-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="3078b-117">[Pobieranie programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="3078b-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="3078b-118">tooconnect za pomocą narzędzia SSMS</span><span class="sxs-lookup"><span data-stu-id="3078b-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="3078b-119">Korzystając z narzędzia SSMS, przed łączącego tooyour powitania serwera po raz pierwszy, upewnij się, że nazwa użytkownika jest uwzględniona w grupie Administratorzy usług analizy hello.</span><span class="sxs-lookup"><span data-stu-id="3078b-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="3078b-120">toolearn więcej, zobacz [administratorom serwerów](#server-administrators) dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="3078b-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="3078b-121">Przed nawiązaniem połączenia należy nazwę serwera na powitania tooget.</span><span class="sxs-lookup"><span data-stu-id="3078b-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="3078b-122">W **portalu Azure** > serwera > **omówienie** > **nazwy serwera**, nazwę serwera na powitania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="3078b-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Pobieranie nazwy serwera z systemu Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="3078b-124">W programie SSMS > **Eksplorator obiektów**, kliknij przycisk **Connect** > **usług Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="3078b-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="3078b-125">W hello **połączyć tooServer** okno dialogowe, Wklej w hello nazwę serwera, a następnie w **uwierzytelniania**, wybierz jedną z hello następujące typy uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="3078b-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="3078b-126">**Uwierzytelnianie systemu Windows** toouse poświadczeń domena azwa_użytkownika i hasło systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3078b-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="3078b-127">**Uwierzytelnianie hasłem usługi Active Directory** toouse konta organizacyjnego.</span><span class="sxs-lookup"><span data-stu-id="3078b-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="3078b-128">Na przykład podczas nawiązywania połączenia ze spoza domeny przyłączone do komputera.</span><span class="sxs-lookup"><span data-stu-id="3078b-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="3078b-129">**Uwierzytelnianie usługi Active Directory uniwersalnych** toouse [nieinterakcyjnym lub usługi Multi-Factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3078b-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Połącz w programie SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="3078b-131">Administratorzy serwera i bazy danych użytkowników</span><span class="sxs-lookup"><span data-stu-id="3078b-131">Server administrators and database users</span></span>
<span data-ttu-id="3078b-132">W usłudze Azure Analysis Services istnieją dwa typy użytkowników, administratorów serwera i bazy danych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3078b-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="3078b-133">Użytkownicy obu typów musi znajdować się w usłudze Azure Active Directory i musi być określona za pomocą adresu e-mail organizacji lub nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="3078b-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="3078b-134">toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="3078b-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="3078b-135">Rozwiązywanie problemów z połączeniem</span><span class="sxs-lookup"><span data-stu-id="3078b-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="3078b-136">Podczas nawiązywania połączenia przy użyciu narzędzia SSMS, jeśli wystąpią problemy, może być konieczne tooclear hello logowania w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3078b-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="3078b-137">Nic nie toodisc pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="3078b-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="3078b-138">tooclear hello pamięci podręcznej, zamknij i ponowne uruchomienie hello łączą procesu.</span><span class="sxs-lookup"><span data-stu-id="3078b-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3078b-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3078b-139">Next steps</span></span>
<span data-ttu-id="3078b-140">Jeśli nie zostało już wdrożony nowy serwer tooyour modelu tabelarycznego, teraz jest odpowiedni moment.</span><span class="sxs-lookup"><span data-stu-id="3078b-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="3078b-141">toolearn więcej, zobacz [wdrażanie usług Analysis Services tooAzure](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3078b-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="3078b-142">Po wdrożeniu serwera tooyour modelu, możesz za pomocą klienta lub przeglądarki tooit tooconnect gotowe.</span><span class="sxs-lookup"><span data-stu-id="3078b-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="3078b-143">toolearn więcej, zobacz [Pobierz dane z serwera usług Azure Analysis Services](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3078b-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

