---
title: "Azure AD Connect: Zaktualizuj certyfikat SSL do farmę serwerów usługi Active Directory Federation Services (AD FS) | Dokumentacja firmy Microsoft"
description: "Szczegóły tego dokumentu kroki, aby zaktualizować certyfikat SSL farmy usług AD FS przy użyciu usługi Azure AD Connect."
services: active-directory
keywords: "programu Azure ad connect, aktualizacji ssl usług AD FS, aktualizacja certyfikatu usług AD FS, zmienianie certyfikatu usług AD FS, nowego certyfikatu usług AD FS, certyfikat usług AD FS aktualizacji usług AD FS certyfikat ssl, aktualizacja AD FS certyfikat ssl, skonfigurować certyfikat ssl usług AD FS, usługi AD FS, ssl, certyfikatu, certyfikat komunikacji usługi AD FS, federation aktualizacji, konfigurowanie Federacji, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="253f7-104">Aktualizuj certyfikat protokołu SSL dla farmę serwerów usługi Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="253f7-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="253f7-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="253f7-105">Overview</span></span>
<span data-ttu-id="253f7-106">W tym artykule opisano, jak Azure AD Connect umożliwia zaktualizowanie certyfikatu SSL dla farmę serwerów usługi Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="253f7-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="253f7-107">Narzędzie Azure AD Connect pozwalają łatwo aktualizować certyfikat SSL do farmy usług AD FS, nawet jeśli nie jest użytkownik logowania wybrano metodę usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="253f7-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="253f7-108">Można wykonać całą operację aktualizowania certyfikat protokołu SSL dla farmy usług AD FS we wszystkich federacyjnych i serwerach Proxy aplikacji sieci Web (WAP) w trzy proste kroki:</span><span class="sxs-lookup"><span data-stu-id="253f7-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Trzy kroki](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="253f7-110">Aby dowiedzieć się więcej o certyfikatach, które są używane przez usługi AD FS, zobacz [Opis certyfikatów używane przez usługi AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="253f7-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="253f7-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="253f7-111">Prerequisites</span></span>

* <span data-ttu-id="253f7-112">**Farmy usług AD FS**: Upewnij się, że farmę usług AD FS jest systemem Windows Server 2012 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="253f7-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="253f7-113">**Azure AD Connect**: Upewnij się, że wersja programu Azure AD Connect jest 1.1.443.0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="253f7-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="253f7-114">Użyjesz zadania **aktualizacja AD FS certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="253f7-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Zadanie aktualizacji protokołu SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="253f7-116">Krok 1: Podaj informacje farmy usług AD FS</span><span class="sxs-lookup"><span data-stu-id="253f7-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="253f7-117">Azure AD Connect podejmuje próbę automatycznie przez Uzyskaj informacje na temat farmy usług AD FS:</span><span class="sxs-lookup"><span data-stu-id="253f7-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="253f7-118">Podczas badania informacji farmy z usług AD FS (Windows Server 2016 lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="253f7-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="253f7-119">Odwołanie do informacje z poprzedniego działa, które są przechowywane lokalnie z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="253f7-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="253f7-120">Umożliwia zmodyfikowanie listy serwerów, które są wyświetlane przez dodawanie lub usuwanie serwerów w celu odzwierciedlenia bieżącej konfiguracji farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="253f7-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="253f7-121">Jak podano informacje o serwerze, Azure AD Connect Wyświetla łączności i bieżący stan certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="253f7-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![Informacje o serwerze programu AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="253f7-123">Jeśli lista zawiera serwer, który nie jest już częścią farmy usług AD FS, kliknij przycisk **Usuń** można usunąć serwera na liście serwerów w farmie serwerów usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="253f7-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![W trybie offline serwer na liście](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="253f7-125">Usuwanie serwera z listy serwerów dla farmy usług AD FS w programie Azure AD Connect jest operacją lokalnego i aktualizuje informacje o farmy usług AD FS, które Azure AD Connect obsługuje lokalnie.</span><span class="sxs-lookup"><span data-stu-id="253f7-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="253f7-126">Azure AD Connect nie modyfikuje konfiguracji w usługach AD FS w celu odzwierciedlenia zmian.</span><span class="sxs-lookup"><span data-stu-id="253f7-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="253f7-127">Krok 2: Podaj nowy certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="253f7-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="253f7-128">Po potwierdzeniu informacji na temat usług AD FS farmy serwerów usługi Azure AD Connect monituje o podanie nowego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="253f7-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="253f7-129">Podaj certyfikat PFX chroniony hasłem, aby kontynuować instalację.</span><span class="sxs-lookup"><span data-stu-id="253f7-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![Certyfikat SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="253f7-131">Po podaniu certyfikatu Azure AD Connect przechodzi przez szereg wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="253f7-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="253f7-132">Sprawdź certyfikat, aby upewnić się, że certyfikat jest poprawny dla farmy usług AD FS:</span><span class="sxs-lookup"><span data-stu-id="253f7-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="253f7-133">Nazwa podmiotu nazwy/alternatywny podmiotu certyfikatu jest ona taka sama jak nazwa usługi federacyjnej lub jest certyfikat uniwersalny.</span><span class="sxs-lookup"><span data-stu-id="253f7-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="253f7-134">Certyfikat jest ważny przez dłużej niż 30 dni.</span><span class="sxs-lookup"><span data-stu-id="253f7-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="253f7-135">Łańcuch zaufania certyfikatów jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="253f7-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="253f7-136">Certyfikat jest chroniony hasłem.</span><span class="sxs-lookup"><span data-stu-id="253f7-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="253f7-137">Krok 3: Wybierz serwery aktualizacji</span><span class="sxs-lookup"><span data-stu-id="253f7-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="253f7-138">W następnym kroku wybierz serwery, które wymagają certyfikatów SSL, zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="253f7-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="253f7-139">Nie można wybrać serwery, które są w trybie offline dla aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="253f7-139">Servers that are offline can't be selected for the update.</span></span>

![Wybierz serwery, aby zaktualizować](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="253f7-141">Po zakończeniu konfigurowania Azure AD Connect wyświetla komunikat, który wskazuje stan aktualizacji i udostępnia opcję, aby sprawdzić logowanie usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="253f7-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Kończenie konfiguracji](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="253f7-143">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="253f7-143">FAQs</span></span>

* <span data-ttu-id="253f7-144">**Co powinna być nazwą podmiotu certyfikatu dla nowego certyfikatu SSL usług AD FS?**</span><span class="sxs-lookup"><span data-stu-id="253f7-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="253f7-145">Azure AD Connect sprawdza, czy nazwa podmiotu nazwy/alternatywny podmiotu certyfikatu zawiera nazwę usługi federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="253f7-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="253f7-146">Na przykład jeśli nazwa usługi federacyjnej jest fs.contoso.com, nazwa podmiotu nazwy/alternatywny podmiotu musi być fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="253f7-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="253f7-147">Certyfikatów z symbolami wieloznacznymi również są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="253f7-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="253f7-148">**Dlaczego pojawia się pytanie o poświadczenia ponownie na stronie serwer proxy?**</span><span class="sxs-lookup"><span data-stu-id="253f7-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="253f7-149">Jeśli poświadczenia podane w celu nawiązania serwerów usług AD FS również nie ma uprawnień do zarządzania serwerami proxy, Azure AD Connect zapyta o poświadczenia, które mają uprawnienia administracyjne na serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="253f7-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="253f7-150">**Serwer jest wyświetlany w trybie offline. Co zrobić?**</span><span class="sxs-lookup"><span data-stu-id="253f7-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="253f7-151">Azure AD Connect nie może wykonać żadnej operacji, jeśli serwer jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="253f7-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="253f7-152">Jeżeli serwer jest częścią farmy usług AD FS, sprawdź łączność z serwerem.</span><span class="sxs-lookup"><span data-stu-id="253f7-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="253f7-153">Po problem został rozwiązany, naciśnij ikonę odświeżania, aby zaktualizować stan w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="253f7-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="253f7-154">Jeśli serwer był częścią farmy wcześniej, ale teraz już nie istnieje, kliknij przycisk **Usuń** go usunąć z listy serwerów, że Azure AD Connect obsługuje.</span><span class="sxs-lookup"><span data-stu-id="253f7-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="253f7-155">Usuwanie serwera z listy w programie Azure AD Connect nie zmieni konfigurację usług AD FS samej siebie.</span><span class="sxs-lookup"><span data-stu-id="253f7-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="253f7-156">Jeśli korzystasz z usług AD FS w systemie Windows Server 2016 lub nowszym, pozostaje serwera w ustawieniach konfiguracji i pojawi się ponownie przy następnym uruchomieniu zadania.</span><span class="sxs-lookup"><span data-stu-id="253f7-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="253f7-157">**Można aktualizować podzbiór serwerów w kolektywie serwerów przy użyciu nowego certyfikatu SSL?**</span><span class="sxs-lookup"><span data-stu-id="253f7-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="253f7-158">Tak.</span><span class="sxs-lookup"><span data-stu-id="253f7-158">Yes.</span></span> <span data-ttu-id="253f7-159">Będzie można uruchamiać zadania **zaktualizuj certyfikat SSL** ponownie, aby zaktualizować pozostałych serwerów.</span><span class="sxs-lookup"><span data-stu-id="253f7-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="253f7-160">Na **wybierz serwery protokołu SSL certyfikatów aktualizacji** strony, można sortować listę serwerów na **datę wygaśnięcia SSL** aby łatwo uzyskiwać dostęp do serwerów, które nie są jeszcze zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="253f7-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="253f7-161">**Po usunięciu serwera w poprzedniego działania, ale jego jest nadal wyświetlane jako w trybie offline i listy na stronie serwery usług AD FS. Dlaczego jest w trybie offline serwer nadal istnieje, nawet po usunięciu go?**</span><span class="sxs-lookup"><span data-stu-id="253f7-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="253f7-162">Usuwanie serwera z listy w programie Azure AD Connect nie powoduje usunięcia w konfiguracji usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="253f7-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="253f7-163">Azure AD Connect odwołuje się do usług AD FS (Windows Server 2016 lub nowszego) żadnych informacji o farmy.</span><span class="sxs-lookup"><span data-stu-id="253f7-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="253f7-164">Jeśli serwer jest nadal znajdują się w konfiguracji usług AD FS, będzie wyświetlane w liście.</span><span class="sxs-lookup"><span data-stu-id="253f7-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="253f7-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="253f7-165">Next steps</span></span>

- [<span data-ttu-id="253f7-166">Program Azure AD Connect a federacja</span><span class="sxs-lookup"><span data-stu-id="253f7-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="253f7-167">Dostosowywanie z programem Azure AD Connect i zarządzania w usłudze Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="253f7-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
