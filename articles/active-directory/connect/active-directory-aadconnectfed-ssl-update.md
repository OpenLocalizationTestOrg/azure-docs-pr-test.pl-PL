---
title: "Azure AD Connect: Certyfikat SSL hello aktualizacji dla farmę serwerów usługi Active Directory Federation Services (AD FS) | Dokumentacja firmy Microsoft"
description: "Ten dokument szczegóły hello kroki tooupdate hello certyfikat SSL farmy usług AD FS przy użyciu usługi Azure AD Connect."
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
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="3d51c-104">Aktualizuj hello certyfikat protokołu SSL dla farmę serwerów usługi Active Directory Federation Services (AD FS)</span><span class="sxs-lookup"><span data-stu-id="3d51c-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="3d51c-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3d51c-105">Overview</span></span>
<span data-ttu-id="3d51c-106">W tym artykule opisano, jak można użyć certyfikatu SSL hello tooupdate Azure AD Connect dla farmę serwerów usługi Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="3d51c-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="3d51c-107">Można użyć certyfikatu SSL hello aktualizacji tooeasily hello Azure AD Connect narzędzia hello AD FS farmy programu, nawet jeśli wybrano metodę logowania dla użytkownika hello nie usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="3d51c-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="3d51c-108">Można wykonywać hello całej operacji aktualizowania certyfikat SSL dla hello AD FS farmy we wszystkich federacyjnych i serwerach Proxy aplikacji sieci Web (WAP) w trzy proste kroki:</span><span class="sxs-lookup"><span data-stu-id="3d51c-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Trzy kroki](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="3d51c-110">toolearn więcej informacji na temat certyfikatów, które są używane przez usługi AD FS, zobacz [Opis certyfikatów używane przez usługi AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d51c-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d51c-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3d51c-111">Prerequisites</span></span>

* <span data-ttu-id="3d51c-112">**Farmy usług AD FS**: Upewnij się, że farmę usług AD FS jest systemem Windows Server 2012 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="3d51c-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="3d51c-113">**Azure AD Connect**: Upewnij się, że hello wersji programu Azure AD Connect jest 1.1.443.0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="3d51c-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="3d51c-114">Użyjesz zadań hello **aktualizacja AD FS certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="3d51c-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Zadanie aktualizacji protokołu SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="3d51c-116">Krok 1: Podaj informacje farmy usług AD FS</span><span class="sxs-lookup"><span data-stu-id="3d51c-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="3d51c-117">Azure AD Connect podejmuje automatycznie przez tooobtain informacji na temat hello AD FS farmy:</span><span class="sxs-lookup"><span data-stu-id="3d51c-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="3d51c-118">Kwerenda hello farmy informacji z usług AD FS (Windows Server 2016 lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="3d51c-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="3d51c-119">Odwołuje się do hello informacje z poprzedniego przebiegi, które są przechowywane lokalnie z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3d51c-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="3d51c-120">Można zmodyfikować hello listy serwerów, które są wyświetlane przez dodanie lub usunięcie hello serwerów tooreflect hello bieżącej konfiguracji hello AD FS farmy.</span><span class="sxs-lookup"><span data-stu-id="3d51c-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="3d51c-121">Jak podano informacje o serwerze hello, Azure AD Connect Wyświetla hello łączności i bieżący stan certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="3d51c-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Informacje o serwerze programu AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="3d51c-123">Jeśli lista hello zawiera serwer, który nie jest już częścią hello AD FS farmy, kliknij przycisk **Usuń** toodelete powitania serwera z hello listę serwerów w farmie serwerów usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="3d51c-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![W trybie offline serwer na liście](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="3d51c-125">Usuwanie serwera z listy hello serwerów usług AD FS farmy w programie Azure AD Connect jest operacją lokalnych i aktualizacje hello informacje dotyczące hello farmy usług AD FS, zawierającą lokalnie Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3d51c-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="3d51c-126">Azure AD Connect nie modyfikuje hello konfiguracji usług AD FS tooreflect hello zmian.</span><span class="sxs-lookup"><span data-stu-id="3d51c-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="3d51c-127">Krok 2: Podaj nowy certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="3d51c-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="3d51c-128">Po potwierdzeniu hello informacji na temat serwerów w kolektywie serwerów usług AD FS, Azure AD Connect monituje o podanie hello nowy certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="3d51c-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="3d51c-129">Podaj chroniony hasłem PFX toocontinue hello instalacji certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="3d51c-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![Certyfikat SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="3d51c-131">Po podaniu certyfikatu hello Azure AD Connect przechodzi przez szereg wymagań wstępnych.</span><span class="sxs-lookup"><span data-stu-id="3d51c-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="3d51c-132">Sprawdź, czy hello tooensure certyfikatu, który hello certyfikat jest poprawny dla farmy usług AD FS hello:</span><span class="sxs-lookup"><span data-stu-id="3d51c-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="3d51c-133">Witaj podmiotu nazwy/alternatywny nazwa podmiotu certyfikatu hello jest hello takie same jak nazwa usługi federacyjnej hello albo jest certyfikat wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="3d51c-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="3d51c-134">Witaj certyfikat jest ważny przez dłużej niż 30 dni.</span><span class="sxs-lookup"><span data-stu-id="3d51c-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="3d51c-135">łańcuch zaufania certyfikatów Hello jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="3d51c-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="3d51c-136">Witaj certyfikat jest chroniony hasłem.</span><span class="sxs-lookup"><span data-stu-id="3d51c-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="3d51c-137">Krok 3: Wybierz serwery hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="3d51c-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="3d51c-138">W następnym kroku hello wybierz serwery hello, wymagające certyfikatów SSL hello toohave zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="3d51c-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="3d51c-139">Nie można wybrać serwery, które są w trybie offline hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3d51c-139">Servers that are offline can't be selected for hello update.</span></span>

![Wybierz serwery tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="3d51c-141">Po zakończeniu konfiguracji hello Azure AD Connect wyświetla wiadomość hello wskazuje stan hello hello aktualizacji i udostępnia opcję tooverify hello usług AD FS logowania.</span><span class="sxs-lookup"><span data-stu-id="3d51c-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Kończenie konfiguracji](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="3d51c-143">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="3d51c-143">FAQs</span></span>

* <span data-ttu-id="3d51c-144">**Jakie powinny być hello nazwa podmiotu certyfikatu hello uzyskać nowy certyfikat SSL usług AD FS hello?**</span><span class="sxs-lookup"><span data-stu-id="3d51c-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="3d51c-145">Azure AD Connect sprawdza, czy nazwa podmiotu nazwy/alternatywny podmiotu hello hello certyfikatu zawiera nazwy usługi federacyjnej hello.</span><span class="sxs-lookup"><span data-stu-id="3d51c-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="3d51c-146">Na przykład jeśli nazwa usługi federacyjnej jest fs.contoso.com, nazwa podmiotu nazwy/alternatywny podmiotu hello musi być fs.contoso.com.  Certyfikatów z symbolami wieloznacznymi również są akceptowane.</span><span class="sxs-lookup"><span data-stu-id="3d51c-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="3d51c-147">**Dlaczego pojawia się pytanie o poświadczenia ponownie na stronie serwer proxy hello?**</span><span class="sxs-lookup"><span data-stu-id="3d51c-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="3d51c-148">Jeśli poświadczenia hello, które zapewniają połączenia tooAD FS serwerów również nie ma serwerów proxy hello toomanage uprawnień hello, Azure AD Connect zapyta o poświadczenia, które mają uprawnienia administracyjne na powitania serwerów proxy.</span><span class="sxs-lookup"><span data-stu-id="3d51c-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="3d51c-149">**Serwer Hello jest wyświetlany w trybie offline. Co zrobić?**</span><span class="sxs-lookup"><span data-stu-id="3d51c-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="3d51c-150">Azure AD Connect nie może wykonać żadnej operacji, jeśli serwer hello jest w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="3d51c-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="3d51c-151">Jeżeli serwer hello jest częścią hello farmy usług AD FS, sprawdź hello łączności toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="3d51c-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="3d51c-152">Po hello problem został rozwiązany, naciśnij klawisz hello odświeżania ikona tooupdate hello stan hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="3d51c-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="3d51c-153">Jeśli serwer hello jest częścią programu hello farmy wcześniej, ale teraz już nie istnieje, kliknij pozycję **Usuń** toodelete przechowuje go z listy hello serwerów, które programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="3d51c-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="3d51c-154">Usuwanie serwera hello z listy hello w programie Azure AD Connect nie powoduje zmian hello konfiguracji usług AD FS, sama.</span><span class="sxs-lookup"><span data-stu-id="3d51c-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="3d51c-155">Jeśli korzystasz z usług AD FS w systemie Windows Server 2016 lub nowszym powitania serwera pozostaje w ustawieniach konfiguracji hello i pojawi się ponownie hello następnym hello zadanie zostanie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="3d51c-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="3d51c-156">**Można aktualizować podzbiór serwerów w kolektywie serwerów z hello nowy certyfikat SSL?**</span><span class="sxs-lookup"><span data-stu-id="3d51c-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="3d51c-157">Tak.</span><span class="sxs-lookup"><span data-stu-id="3d51c-157">Yes.</span></span> <span data-ttu-id="3d51c-158">Będzie można uruchamiać zadania hello **certyfikat SSL aktualizacji** ponownie hello tooupdate pozostałych serwerów.</span><span class="sxs-lookup"><span data-stu-id="3d51c-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="3d51c-159">Na powitania **wybierz serwery protokołu SSL certyfikatów aktualizacji** strony, można sortować hello listę serwerów na **datę wygaśnięcia SSL** tooeasily dostępu hello serwerów, które nie są jeszcze zaktualizowana.</span><span class="sxs-lookup"><span data-stu-id="3d51c-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="3d51c-160">**Po usunięciu serwera hello w poprzednim hello uruchomiony, ale jego jest nadal wyświetlane jako w trybie offline i listy na stronie serwery FS hello AD. Dlaczego jest hello nadal istnieje serwer w trybie offline, nawet po usunięciu go?**</span><span class="sxs-lookup"><span data-stu-id="3d51c-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="3d51c-161">Usuwanie serwera hello z listy hello w programie Azure AD Connect nie powoduje jego usunięcia w hello konfiguracji usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="3d51c-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="3d51c-162">Azure AD Connect odwołuje się do usług AD FS (Windows Server 2016 lub nowszego) żadnych informacji o hello farmy.</span><span class="sxs-lookup"><span data-stu-id="3d51c-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="3d51c-163">Jeśli serwer hello jest nadal znajdują się na powitania konfiguracji usług AD FS, będzie wyświetlane w hello listy.</span><span class="sxs-lookup"><span data-stu-id="3d51c-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="3d51c-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3d51c-164">Next steps</span></span>

- [<span data-ttu-id="3d51c-165">Program Azure AD Connect a federacja</span><span class="sxs-lookup"><span data-stu-id="3d51c-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="3d51c-166">Dostosowywanie z programem Azure AD Connect i zarządzania w usłudze Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="3d51c-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
