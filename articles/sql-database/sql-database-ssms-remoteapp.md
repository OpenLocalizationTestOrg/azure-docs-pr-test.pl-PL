---
title: "tooSQL aaaConnect bazy danych przy użyciu programu SQL Server Management Studio w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Jak korzystać z tego samouczka toolearn toouse programu SQL Server Management Studio w usłudze Azure RemoteApp zabezpieczeń i wydajności podczas łączenia tooSQL bazy danych"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a><span data-ttu-id="aebb3-103">Użyj programu SQL Server Management Studio w usłudze Azure RemoteApp tooconnect tooSQL bazy danych</span><span class="sxs-lookup"><span data-stu-id="aebb3-103">Use SQL Server Management Studio in Azure RemoteApp tooconnect tooSQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aebb3-104">Usługa Azure RemoteApp nie jest już obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="aebb3-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="aebb3-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="aebb3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="aebb3-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="aebb3-106">Introduction</span></span>
<span data-ttu-id="aebb3-107">W tym samouczku przedstawiono sposób toouse programu SQL Server Management Studio (SSMS) w usłudze Azure RemoteApp tooconnect tooSQL bazy danych.</span><span class="sxs-lookup"><span data-stu-id="aebb3-107">This tutorial shows you how toouse SQL Server Management Studio (SSMS) in Azure RemoteApp tooconnect tooSQL Database.</span></span> <span data-ttu-id="aebb3-108">Go przeprowadzi Cię przez proces hello konfigurowania programu SQL Server Management Studio w usłudze Azure RemoteApp, opisano hello korzyści i zawiera funkcje zabezpieczeń, które są dostępne w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aebb3-108">It walks you through hello process of setting up SQL Server Management Studio in Azure RemoteApp, explains hello benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="aebb3-109">**Szacowany czas toocomplete:** 45 minut</span><span class="sxs-lookup"><span data-stu-id="aebb3-109">**Estimated time toocomplete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="aebb3-110">SSMS w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="aebb3-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="aebb3-111">Usługa Azure RemoteApp jest usługą usług pulpitu zdalnego na platformie Azure, który zawiera aplikacje.</span><span class="sxs-lookup"><span data-stu-id="aebb3-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="aebb3-112">Można uzyskać więcej informacji na ten temat tutaj: [co to jest RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="aebb3-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="aebb3-113">SSMS uruchomionych w usłudze Azure RemoteApp daje hello tego samego środowiska jako SSMS uruchomionej na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="aebb3-113">SSMS running in Azure RemoteApp gives you hello same experience as running SSMS locally.</span></span>

![Zrzut ekranu przedstawiający SSMS uruchomionych w usłudze Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="aebb3-115">Korzyści</span><span class="sxs-lookup"><span data-stu-id="aebb3-115">Benefits</span></span>
<span data-ttu-id="aebb3-116">Istnieje wiele korzyści toousing SSMS w usłudze Azure RemoteApp w tym:</span><span class="sxs-lookup"><span data-stu-id="aebb3-116">There are many benefits toousing SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="aebb3-117">Port 1433 na serwerze Azure SQL nie ma toobe widoczne na zewnątrz (poza platformą Azure).</span><span class="sxs-lookup"><span data-stu-id="aebb3-117">Port 1433 on Azure SQL server does not have toobe exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="aebb3-118">Nie konieczności tookeep Dodawanie i usuwanie adresów IP w zapory serwera Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="aebb3-118">No need tookeep adding and removing IP addresses in hello Azure SQL server firewall.</span></span>
* <span data-ttu-id="aebb3-119">Wszystkie połączenia z usługą Azure RemoteApp odbywa się za pośrednictwem protokołu HTTPS przy użyciu portu 443 szyfrowane protokołu Remote Desktop protocol</span><span class="sxs-lookup"><span data-stu-id="aebb3-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="aebb3-120">Jest wielu użytkowników i mogą być skalowane.</span><span class="sxs-lookup"><span data-stu-id="aebb3-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="aebb3-121">Jest z konieczności SSMS w hello są bardziej wydajne tego samego regionu hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="aebb3-121">There is a performance gain from having SSMS in hello same region as hello SQL Database.</span></span>
* <span data-ttu-id="aebb3-122">Można przeprowadzić inspekcję korzystanie z usługi Azure RemoteApp z wersji Premium hello Azure Active Directory, która ma raporty aktywności użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aebb3-122">You can audit use of Azure RemoteApp with hello Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="aebb3-123">Można włączyć uwierzytelnianie wieloskładnikowe (MFA).</span><span class="sxs-lookup"><span data-stu-id="aebb3-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="aebb3-124">Dostęp SSMS dowolne miejsce w przypadku, gdy przy użyciu dowolnego hello obsługiwani klienci usługi Azure RemoteApp, w tym z systemem iOS, Android, Mac, Windows Phone i komputerach z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="aebb3-124">Access SSMS anywhere when using any of hello supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-hello-azure-remoteapp-collection"></a><span data-ttu-id="aebb3-125">Utwórz kolekcję usługi Azure RemoteApp hello</span><span class="sxs-lookup"><span data-stu-id="aebb3-125">Create hello Azure RemoteApp collection</span></span>
<span data-ttu-id="aebb3-126">Oto toocreate kroki hello kolekcji usługi Azure RemoteApp z SSMS:</span><span class="sxs-lookup"><span data-stu-id="aebb3-126">Here are hello steps toocreate your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="aebb3-127">1. Utwórz nową maszynę Wirtualną systemu Windows na podstawie obrazu</span><span class="sxs-lookup"><span data-stu-id="aebb3-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="aebb3-128">Użyj hello obrazu "Systemu Windows serwera zdalnego pulpitu sesji hosta systemu Windows Server 2012 R2" z toomake galerii hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aebb3-128">Use hello "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from hello Gallery toomake your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="aebb3-129">2. Zainstaluj narzędzia SSMS z SQL Express</span><span class="sxs-lookup"><span data-stu-id="aebb3-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="aebb3-130">Przejdź na hello nowej maszyny Wirtualnej, a następnie przejdź do strony pobierania toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="aebb3-130">Go onto hello new VM and navigate toothis download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="aebb3-131">Istnieje opcja pobierania tooonly SSMS.</span><span class="sxs-lookup"><span data-stu-id="aebb3-131">There is an option tooonly download SSMS.</span></span> <span data-ttu-id="aebb3-132">Po pobraniu przejdź do katalogu instalacyjnego hello i uruchom Instalator tooinstall SSMS.</span><span class="sxs-lookup"><span data-stu-id="aebb3-132">After download, go into hello install directory and run Setup tooinstall SSMS.</span></span>

<span data-ttu-id="aebb3-133">Należy również tooinstall dodatku Service Pack 1 dla programu SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="aebb3-133">You also need tooinstall SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="aebb3-134">Można go pobrać tutaj: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="aebb3-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="aebb3-135">Dodatek Service Pack 1 dla programu SQL Server 2014 r. obejmuje funkcje niezbędne do pracy z bazą danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="aebb3-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="aebb3-136">3. Uruchom skrypt weryfikacji i programu Sysprep</span><span class="sxs-lookup"><span data-stu-id="aebb3-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="aebb3-137">Na powitania pulpitu hello maszyny Wirtualnej jest skrypt programu PowerShell o nazwie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="aebb3-137">On hello desktop of hello VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="aebb3-138">Uruchom tego klikając dwukrotnie.</span><span class="sxs-lookup"><span data-stu-id="aebb3-138">Run this by double-clicking.</span></span> <span data-ttu-id="aebb3-139">Zweryfikuje hello, że maszyna wirtualna jest gotowa toobe używany do zdalnego hostowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aebb3-139">It will verify that hello VM is ready toobe used for remote hosting of applications.</span></span> <span data-ttu-id="aebb3-140">Po zakończeniu weryfikacji poprosi sysprep toorun — wybierz toorun go.</span><span class="sxs-lookup"><span data-stu-id="aebb3-140">When verification is complete, it will ask toorun sysprep - choose toorun it.</span></span>

<span data-ttu-id="aebb3-141">Po zakończeniu działania programu sysprep, wyłączy hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="aebb3-141">When sysprep completes, it will shut down hello VM.</span></span>

<span data-ttu-id="aebb3-142">toolearn więcej informacji o tworzeniu obrazu usługi Azure RemoteApp, zobacz: [jak toocreate szablonu usługi RemoteApp obrazu na platformie Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="aebb3-142">toolearn more about creating a Azure RemoteApp image, see: [How toocreate a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="aebb3-143">4. Przechwycenie obrazu</span><span class="sxs-lookup"><span data-stu-id="aebb3-143">4. Capture image</span></span>
<span data-ttu-id="aebb3-144">Gdy powitalne wirtualna przestała działać, znajdź go w bieżącym portalu hello i przechwyceniem go.</span><span class="sxs-lookup"><span data-stu-id="aebb3-144">When hello VM has stopped running, find it in hello current portal and capture it.</span></span>

<span data-ttu-id="aebb3-145">toolearn więcej informacji na temat przechwytywania obrazu, zobacz [przechwytywania obrazu systemu Windows Azure maszyny wirtualnej utworzone za pomocą hello klasycznego modelu wdrażania](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="aebb3-145">toolearn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with hello classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-tooazure-remoteapp-template-images"></a><span data-ttu-id="aebb3-146">5. Dodaj tooAzure obrazy szablonów usługi RemoteApp</span><span class="sxs-lookup"><span data-stu-id="aebb3-146">5. Add tooAzure RemoteApp Template images</span></span>
<span data-ttu-id="aebb3-147">W hello sekcji hello bieżącym portalu usługi Azure RemoteApp przejdź na kartę obrazy szablonów toohello, a następnie kliknij przycisk Dodaj.</span><span class="sxs-lookup"><span data-stu-id="aebb3-147">In hello Azure RemoteApp section of hello current portal, go toohello Template Images tab and click Add.</span></span> <span data-ttu-id="aebb3-148">W oknie podręcznym hello wybierz "Import obrazów z biblioteki maszyn wirtualnych", a następnie wybierz hello obrazu, który został właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="aebb3-148">In hello pop-up box, select "Import an image from your Virtual Machines library" and then choose hello Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="aebb3-149">6. Tworzenie kolekcji w chmurze</span><span class="sxs-lookup"><span data-stu-id="aebb3-149">6. Create cloud collection</span></span>
<span data-ttu-id="aebb3-150">W bieżącym portalu hello Utwórz nową kolekcję chmury Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="aebb3-150">In hello current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="aebb3-151">Wybierz hello obrazu szablonu, który właśnie zaimportowany z SSMS na nim zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="aebb3-151">Choose hello Template Image that you just imported with SSMS installed on it.</span></span>

![Utwórz nową kolekcję w chmurze][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="aebb3-153">7. Publikowanie programu SSMS</span><span class="sxs-lookup"><span data-stu-id="aebb3-153">7. Publish SSMS</span></span>
<span data-ttu-id="aebb3-154">Na powitania publikowania kartę nowej kolekcji chmury, wybierz opcję publikowania aplikacji za pomocą hello Start Menu, a następnie wybierz pozycję Narzędzia SSMS z listy hello.</span><span class="sxs-lookup"><span data-stu-id="aebb3-154">On hello Publishing tab of your new cloud collection, select Publish an application from hello Start Menu and then choose SSMS from hello list.</span></span>

![Publikowanie aplikacji][5]

### <a name="8-add-users"></a><span data-ttu-id="aebb3-156">8. Dodawanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="aebb3-156">8. Add users</span></span>
<span data-ttu-id="aebb3-157">Na karcie dostęp użytkownika hello można wybrać hello użytkowników, którzy będą miały dostępu toothis usługi Azure RemoteApp kolekcję, która zawiera tylko SSMS.</span><span class="sxs-lookup"><span data-stu-id="aebb3-157">On hello User Access tab you can select hello users that will have access toothis Azure RemoteApp collection which only includes SSMS.</span></span>

![Dodaj użytkownika][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a><span data-ttu-id="aebb3-159">9. Zainstaluj aplikację kliencką hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="aebb3-159">9. Install hello Azure RemoteApp client application</span></span>
<span data-ttu-id="aebb3-160">Możesz pobrać i zainstalować klienta usługi Azure RemoteApp w tym miejscu: [Pobierz | Usługa Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="aebb3-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="aebb3-161">Konfigurowanie serwera Azure SQL</span><span class="sxs-lookup"><span data-stu-id="aebb3-161">Configure Azure SQL server</span></span>
<span data-ttu-id="aebb3-162">Hello zapory hello jest włączona tylko konfiguracji potrzebne jest tooensure, czy usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="aebb3-162">hello only configuration needed is tooensure that Azure Services is enabled for hello firewall.</span></span> <span data-ttu-id="aebb3-163">Jeśli używasz tego rozwiązania, następnie nie trzeba tooadd dowolnego adresu IP adresów tooopen hello zapory.</span><span class="sxs-lookup"><span data-stu-id="aebb3-163">If you use this solution, then you do not need tooadd any IP addresses tooopen hello firewall.</span></span> <span data-ttu-id="aebb3-164">Witaj ruchu sieciowego, który jest dozwolony toohello programu SQL Server jest z innymi usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="aebb3-164">hello network traffic that is allowed toohello SQL Server is from other Azure services.</span></span>

![Zezwalaj na platformie Azure][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="aebb3-166">Uwierzytelnianie wieloskładnikowe (MFA)</span><span class="sxs-lookup"><span data-stu-id="aebb3-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="aebb3-167">Uwierzytelnianie wieloskładnikowe można włączyć specjalnie dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aebb3-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="aebb3-168">Przejdź na kartę aplikacje toohello usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aebb3-168">Go toohello Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="aebb3-169">Wpis będą dostępne do funkcji RemoteApp systemu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="aebb3-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="aebb3-170">Jeśli klikniesz tej aplikacji, a następnie skonfiguruj, zostanie wyświetlona strona hello poniżej której można włączyć usługę MFA dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="aebb3-170">If you click that application and then configure, you will see hello page below where you can enable MFA for this application.</span></span>

![Włączenie uwierzytelniania MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="aebb3-172">Inspekcja aktywności użytkownika za pomocą usługi Azure Active Directory — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="aebb3-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="aebb3-173">Jeśli nie masz usługi Azure AD Premium, a następnie masz tooturn go na hello licencji części katalogu.</span><span class="sxs-lookup"><span data-stu-id="aebb3-173">If you do not have Azure AD Premium, then you have tooturn it on in hello Licenses section of your directory.</span></span> <span data-ttu-id="aebb3-174">Z Premium włączone można przypisywać użytkowników toohello poziom Premium.</span><span class="sxs-lookup"><span data-stu-id="aebb3-174">With Premium enabled, you can assign users toohello Premium level.</span></span>

<span data-ttu-id="aebb3-175">Po przejściu tooa użytkownika w usłudze Azure Active Directory, możesz przejść toohello działania kartę toosee logowania informacji tooAzure programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="aebb3-175">When you go tooa user in your Azure Active Directory, you can then go toohello Activity tab toosee login information tooAzure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aebb3-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aebb3-176">Next steps</span></span>
<span data-ttu-id="aebb3-177">Po zakończeniu wszystkich hello powyżej kroki, użytkownik zostanie klienta usługi Azure RemoteApp hello stanie toorun i dziennika za pomocą przypisany użytkownik.</span><span class="sxs-lookup"><span data-stu-id="aebb3-177">After completing all hello above steps, you will be able toorun hello Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="aebb3-178">Użytkownik zobaczy SSMS jako jedna z aplikacji i można go uruchomić, jak w przypadku, jeśli zostały zainstalowane na komputerze z serwerem SQL tooAzure dostępu.</span><span class="sxs-lookup"><span data-stu-id="aebb3-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access tooAzure SQL server.</span></span>

<span data-ttu-id="aebb3-179">Aby uzyskać więcej informacji dotyczących sposobu toomake hello tooSQL połączenia bazy danych, zobacz [uzyskuj tooSQL bazy danych programu SQL Server Management Studio i wykonywanie przykładowego zapytania T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="aebb3-179">For more information on how toomake hello connection tooSQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="aebb3-180">To wszystko jest teraz.</span><span class="sxs-lookup"><span data-stu-id="aebb3-180">That's everything for now.</span></span> <span data-ttu-id="aebb3-181">Owocnej pracy.</span><span class="sxs-lookup"><span data-stu-id="aebb3-181">Enjoy!</span></span>

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png