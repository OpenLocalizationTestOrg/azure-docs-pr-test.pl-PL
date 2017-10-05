---
title: "Co to jest panel dostępu w usłudze Azure Active Directory? | Microsoft Docs"
description: "Dowiedz się, jak używać różnych wersji panelu dostępu (przeglądarki sieci web, aplikacji systemu Android, aplikacji iPhone i iPad) dostępu do aplikacji SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd9066c251188c0f18fe1a9403baa2beaeeb987c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-access-panel"></a><span data-ttu-id="da850-104">Co to jest panel dostępu?</span><span class="sxs-lookup"><span data-stu-id="da850-104">What is the access panel?</span></span>

<span data-ttu-id="da850-105">Panel dostępu jest portalem sieci web.</span><span class="sxs-lookup"><span data-stu-id="da850-105">The access panel is a web-based portal.</span></span> <span data-ttu-id="da850-106">Umożliwia użytkownikowi służbowy lub konto służbowe w usłudze Azure Active Directory do wyświetlania i uruchamiania aplikacji opartej na chmurze administrator usługi Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="da850-106">It enables a user with a work or school account in Azure Active Directory to view and start cloud-based applications an Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="da850-107">Można również użyć grupami samoobsługi i funkcje zarządzania aplikacjami za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="da850-107">You can also use self-service group and app management capabilities through the access panel.</span></span>

<span data-ttu-id="da850-108">Panel dostępu jest oddzielony od portalu Azure i nie może być subskrypcji platformy Azure jest.</span><span class="sxs-lookup"><span data-stu-id="da850-108">The access panel is separate from the Azure portal and does not you to have an Azure subscription.</span></span>

![Panel dostępu][1]

<span data-ttu-id="da850-110">Panel dostępu umożliwia edytowanie niektórych ustawień profilu, umożliwiając między innymi:</span><span class="sxs-lookup"><span data-stu-id="da850-110">The access panel enables you to edit some of your profile settings, including the ability to:</span></span>

- <span data-ttu-id="da850-111">Zmień hasło skojarzone z konta służbowego</span><span class="sxs-lookup"><span data-stu-id="da850-111">Change the password associated with a work or school account</span></span>

- <span data-ttu-id="da850-112">Edytuj ustawienia resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="da850-112">Edit password reset settings</span></span>

- <span data-ttu-id="da850-113">Edytuj ustawienia kontaktowe i preferencje dotyczące uwierzytelniania wieloskładnikowego (dla kont, które są wymagane do używania go przez administratora)</span><span class="sxs-lookup"><span data-stu-id="da850-113">Edit contact and preference settings related to multi-factor authentication (for accounts that have been required to use it by an administrator)</span></span>

- <span data-ttu-id="da850-114">Wyświetl konta alternatywne szczegóły, takie jak nazwa użytkownika, poczty e-mail oraz mobile i office numery telefonów i urządzeń</span><span class="sxs-lookup"><span data-stu-id="da850-114">View account details, such as user ID, alternate email, and mobile and office phone numbers, and devices</span></span>

- <span data-ttu-id="da850-115">Wyświetl i uruchamiania aplikacji opartej na chmurze, które administrator usługi Azure AD udzielił im dostępu do.</span><span class="sxs-lookup"><span data-stu-id="da850-115">View and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="da850-116">Aby uzyskać więcej informacji na temat panelu dostępu z punktu widzenia użytkownika Zobacz Korzystanie z panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="da850-116">For more information about the access panel from the users’ perspective, see Using the access panel.</span></span> 

- <span data-ttu-id="da850-117">Własnym Zarządzanie grupami.</span><span class="sxs-lookup"><span data-stu-id="da850-117">Self-manage groups.</span></span> <span data-ttu-id="da850-118">W szczególności administrator można tworzyć i Zarządzaj grupami zabezpieczeń i żądania członkostwa w grupach zabezpieczeń w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-118">More specifically, the administrator can create and manage security groups and request security group memberships in Azure AD.</span></span> <span data-ttu-id="da850-119">Aby uzyskać więcej informacji, zobacz [Samoobsługowe zarządzanie grupami użytkowników w usłudze Azure AD](active-directory-accessmanagement-self-service-group-management.md) i [Zarządzanie grupami](active-directory-manage-groups.md).</span><span class="sxs-lookup"><span data-stu-id="da850-119">For more information, see [Self-service group management for users in Azure AD](active-directory-accessmanagement-self-service-group-management.md) and [Manage your groups](active-directory-manage-groups.md).</span></span>




## <a name="accessing-the-access-panel"></a><span data-ttu-id="da850-120">Uzyskiwanie dostępu do panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="da850-120">Accessing the access panel</span></span>

<span data-ttu-id="da850-121">Aby dostęp do panelu dostępu, przechodząc na stronę następujący adres URL w przeglądarce sieci web:`http://myapps.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="da850-121">You can access the access panel by visiting the following URL in a web browser: `http://myapps.microsoft.com`</span></span>

<span data-ttu-id="da850-122">Jeśli masz niestandardowe znakowanie skonfigurowana dla strony logowania, należy załadować tego znakowania przez dołączenie domeny organizacji na końcu adresu URL:`http://myapps.microsoft.com/<your domain>.com`</span><span class="sxs-lookup"><span data-stu-id="da850-122">If you have custom branding configured for your sign-in page, you can load this branding by appending your organization’s domain to the end of the URL: `http://myapps.microsoft.com/<your domain>.com`</span></span>

<span data-ttu-id="da850-123">W takim przypadku można użyć dowolnej nazwy aktywnych lub zweryfikowanej domeny, skonfigurowanego w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="da850-123">In this case, you can use any active or verified domain name that has been configured in your Azure portal.</span></span>

![Nazwa domeny Wingtip Toys][2]  

<span data-ttu-id="da850-125">Należy rozpowszechniać adres URL dla wszystkich użytkowników, którzy będą Zaloguj się do aplikacji, które są zintegrowane z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-125">You need to distribute the URL to all users who will sign in to applications that are integrated with Azure AD.</span></span>

## <a name="authentication"></a><span data-ttu-id="da850-126">Authentication</span><span class="sxs-lookup"><span data-stu-id="da850-126">Authentication</span></span>

<span data-ttu-id="da850-127">Aby uzyskać dostęp do panelu dostępu, użytkownik musi zostać uwierzytelniony przy użyciu konta służbowego w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-127">To reach the access panel, you must be authenticated through a work or school account in Azure AD.</span></span> <span data-ttu-id="da850-128">Użytkownik może zostać uwierzytelniony do usługi Azure AD bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="da850-128">You can be authenticated to Azure AD directly.</span></span> <span data-ttu-id="da850-129">Alternatywnie Jeśli organizacji skonfigurował Federacji przy użyciu usługi Active Directory Federation Services (AD FS) ani innych technologii, możesz mogą być uwierzytelniane przez usługę Active Directory systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="da850-129">Alternatively, if an organization has configured federation by using Active Directory Federation Services (AD FS) or other technologies, you can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="da850-130">Jeśli masz subskrypcji Azure lub usługi Office 365 i był używany portalu Azure lub aplikacji pakietu Office 365, widać na liście aplikacji bez logowanie się ponownie.</span><span class="sxs-lookup"><span data-stu-id="da850-130">If you have a subscription for Azure or Office 365 and you have been using the Azure portal or an Office 365 application, you can see the list of applications without signing-in again.</span></span> <span data-ttu-id="da850-131">Jeśli nie są uwierzytelniane zostanie wyświetlony monit logowania przy użyciu nazwy użytkownika i hasło dla swojego konta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-131">If you are are not authenticated you are prompted to sign in by using the username and password for your account in Azure AD.</span></span> <span data-ttu-id="da850-132">Jeśli organizacji skonfigurował federacyjnych, wpisując nazwę użytkownika jest wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="da850-132">If your organization has configured federation, typing the username is sufficient.</span></span>

<span data-ttu-id="da850-133">Gdy użytkownik jest uwierzytelniony, mogą współdziałać z aplikacjami, które administrator ma zintegrowane z katalogiem.</span><span class="sxs-lookup"><span data-stu-id="da850-133">When you are authenticated, you can interact with the applications that your administrator has integrated with the directory.</span></span> <span data-ttu-id="da850-134">Aby dowiedzieć się, jak integrować aplikacje z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da850-134">To learn how to integrate applications with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="web-browser-requirements"></a><span data-ttu-id="da850-135">Wymagania dotyczące przeglądarki sieci Web</span><span class="sxs-lookup"><span data-stu-id="da850-135">Web browser requirements</span></span>

<span data-ttu-id="da850-136">Co najmniej panelu dostępu wymaga przeglądarki obsługującej JavaScript i włączył CSS.</span><span class="sxs-lookup"><span data-stu-id="da850-136">At a minimum, the access panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="da850-137">Aby użytkownik mógł zalogowani do aplikacji za pomocą opartego na hasłach rejestracji jednokrotnej (SSO) rozszerzenie panelu dostępu musi być zainstalowany w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="da850-137">For the user to be signed in to applications through password-based single sign-on (SSO), the access panel extension must be installed in your browser.</span></span> <span data-ttu-id="da850-138">Rozszerzenie jest pobierany automatycznie po wybraniu aplikacji, która jest skonfigurowana do opartego na hasłach logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="da850-138">The extension is downloaded automatically when you select an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="da850-139">Rozszerzenie panelu dostępu jest obecnie dostępny dla programu Internet Explorer 8 lub nowszy, krawędzi i Chrome, Firefox przeglądarek.</span><span class="sxs-lookup"><span data-stu-id="da850-139">The access panel extension is currently available for Internet Explorer 8 and later, Edge, Chrome, and Firefox browsers.</span></span>

## <a name="mobile-app-support"></a><span data-ttu-id="da850-140">Obsługa aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="da850-140">Mobile app support</span></span>

<span data-ttu-id="da850-141">Zespół usługi Azure Active Directory publikuje mojej aplikacji mobilnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-141">The Azure Active Directory team publishes the my apps mobile app.</span></span> <span data-ttu-id="da850-142">Po zainstalowaniu aplikacji można logowania się do aplikacji opartych na hasło logowania jednokrotnego w systemach iOS i urządzeniach z systemem Android.</span><span class="sxs-lookup"><span data-stu-id="da850-142">When you install the app, you can sign in to password-based SSO applications on iOS and Android devices.</span></span>

> [!NOTE]
> <span data-ttu-id="da850-143">Można logowania się do aplikacji, które obsługują federacji z usługą Azure AD (w tym Salesforce, usługi Google Apps, Dropbox, pole, Concur, produktu Workday, usługi Office 365 i więcej niż 70 innych użytkowników) w praktycznie dowolnej przeglądarki sieci web, na dowolnym urządzeniu, bez konieczności wtyczki lub przenośnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-143">You can sign in to applications that support federation with Azure AD (including Salesforce, Google Apps, Dropbox, Box, Concur, Workday, Office 365, and more than 70 others) on virtually any web browser, on any device, without needing a plug-in or mobile app.</span></span> <span data-ttu-id="da850-144">Wszystkie inne [dostęp do środowiska panelu](https://myapps.microsoft.com/) również nie wymagają mojej aplikacji mobilnej aplikacji do użycia na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="da850-144">All other [access panel experiences](https://myapps.microsoft.com/) do also not require the my apps mobile app to be used on a mobile device.</span></span>
>
>

### <a name="my-apps-for-android"></a><span data-ttu-id="da850-145">Moje aplikacje dla systemu Android</span><span class="sxs-lookup"><span data-stu-id="da850-145">My apps for Android</span></span>

<span data-ttu-id="da850-146">Moje aplikacje dla systemu Android jest obsługiwana na dowolnym urządzeniu z systemem Android, którym jest uruchomiona wersja systemu Android 4.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="da850-146">My apps for Android is supported on any Android device that is running Android version 4.1 and later.</span></span>  
<span data-ttu-id="da850-147">Jest on dostępny w [sklepu Google Play](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span><span class="sxs-lookup"><span data-stu-id="da850-147">It is available in the [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.myapps).</span></span>

![Moje aplikacje dla systemu Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a><span data-ttu-id="da850-149">Moje aplikacje dla urządzenia iPhone i iPad</span><span class="sxs-lookup"><span data-stu-id="da850-149">My apps for iPhone and iPad</span></span>

<span data-ttu-id="da850-150">Moje aplikacje dla systemu iOS jest obsługiwana na wszystkie urządzenia iPhone lub iPad z systemem iOS w wersji 7 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="da850-150">My apps for iOS is supported on any iPhone or iPad that is running iOS version 7 and later.</span></span>  
<span data-ttu-id="da850-151">Jest on dostępny w [sklepu Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span><span class="sxs-lookup"><span data-stu-id="da850-151">It is available in the [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).</span></span>

![Moje aplikacje dla systemu iOS][4]    



## <a name="managed-browser-for-my-apps"></a><span data-ttu-id="da850-153">Zarządzane przeglądarki pod kątem Moje aplikacje</span><span class="sxs-lookup"><span data-stu-id="da850-153">Managed browser for my apps</span></span>

<span data-ttu-id="da850-154">Moje aplikacje są również zintegrowane w programie Intune Managed Browser.</span><span class="sxs-lookup"><span data-stu-id="da850-154">My apps is also integrated in the Intune Managed Browser.</span></span> <span data-ttu-id="da850-155">Intune Managed Browser dla urządzeń iOS i Android odgrywa kluczową rolę w zapewnieniu, że dane na urządzeniach przenośnych jest bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="da850-155">The Intune Managed Browser for iOS and Android devices plays a key role in ensuring that data on mobile devices stays secure.</span></span> <span data-ttu-id="da850-156">Umożliwia ona bezpiecznie przeglądać i przejdź do strony sieci web, które mogą zawierać informacje o firmie i zapewnia bezpieczne przeglądanie sieci web.</span><span class="sxs-lookup"><span data-stu-id="da850-156">It lets you safely view and navigate web pages that might contain company information, and provides a secure web-browsing experience.</span></span>  
<span data-ttu-id="da850-157">Możesz znaleźć szybki dostęp do mojej aplikacji na stronie głównej Managed Browser oraz w zakładki, umożliwiając mniejszej liczby kliknięć do dowolnej aplikacji, którego chcesz uzyskać dostęp.</span><span class="sxs-lookup"><span data-stu-id="da850-157">You find quick access to my apps on your Managed Browser homepage and in your bookmarks, giving you fewer clicks to reach any application you want to access.</span></span>

<span data-ttu-id="da850-158">Jest on dostępny w [sklepu Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) i [sklepu Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span><span class="sxs-lookup"><span data-stu-id="da850-158">It is available in the [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) and [Google Play Store](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).</span></span>

![Przeglądarka Mananged Moje aplikacje][5]    





## <a name="tips-for-testing-the-user-experience"></a><span data-ttu-id="da850-160">Porady dotyczące testowania czynności użytkownika</span><span class="sxs-lookup"><span data-stu-id="da850-160">Tips for testing the user experience</span></span>

<span data-ttu-id="da850-161">Jeśli jesteś administratorem systemu Azure i użytkownik jest zalogowany do portalu Azure przy użyciu konta w katalogu, użytkownik zostanie automatycznie zarejestrowany do panelu dostępu jako swoim aktualnym kontem.</span><span class="sxs-lookup"><span data-stu-id="da850-161">If you are an Azure administrator and you are signed in to the Azure portal by using an account in the directory, you are automatically signed in to the access panel as your current account.</span></span> <span data-ttu-id="da850-162">W takim przypadku widoczne wszystkie aplikacje, które zostały przypisane do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="da850-162">In this case, you can see all applications that have been assigned to you.</span></span>

<span data-ttu-id="da850-163">**Aby przetestować jako *różnych* konta użytkownika:**</span><span class="sxs-lookup"><span data-stu-id="da850-163">**To test as a *different* user account:**</span></span>

1. <span data-ttu-id="da850-164">Kliknij menu użytkownika w prawym górnym rogu portalu Azure lub panel dostępu, a następnie wybierz **Wyloguj**.</span><span class="sxs-lookup"><span data-stu-id="da850-164">Click the user menu in the upper-right corner of the Azure portal or the access panel, and then select **Sign Out**.</span></span> 
2. <span data-ttu-id="da850-165">Przejdź do [panelu dostępu](http://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="da850-165">Go to the [access panel](http://myapps.microsoft.com).</span></span>
3. <span data-ttu-id="da850-166">Na stronie logowania wpisz nazwę użytkownika i hasło dla konta w katalogu, który ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="da850-166">On the sign-in page, type the username and password for the account in your directory you want to test.</span></span>


## <a name="starting-applications"></a><span data-ttu-id="da850-167">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="da850-167">Starting applications</span></span>

<span data-ttu-id="da850-168">Kilka typów aplikacji może występować w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="da850-168">Several types of applications can appear on the access panel.</span></span>

### <a name="office-365-applications"></a><span data-ttu-id="da850-169">Aplikacje pakietu Office 365</span><span class="sxs-lookup"><span data-stu-id="da850-169">Office 365 applications</span></span>

<span data-ttu-id="da850-170">Jeśli organizacja korzysta z aplikacji usługi Office 365, jest udzielana dla nich aplikacje pakietu Office 365 pojawiają się na Twoje panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="da850-170">If your organization is using Office 365 applications and you are licensed for them, the Office 365 applications appear on your access panel.</span></span>

<span data-ttu-id="da850-171">Po kliknięciu kafelka aplikacji dla aplikacji usługi Office 365 są przekierowywane do aplikacji i zostanie automatycznie zalogowany.</span><span class="sxs-lookup"><span data-stu-id="da850-171">When you click an application tile for an Office 365 application, you are redirected to the application and automatically signed in.</span></span>

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a><span data-ttu-id="da850-172">Aplikacje firmy Microsoft i innych firm skonfigurowaną na podstawie federacyjnego logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="da850-172">Microsoft and third-party applications configured with federation-based SSO</span></span>

<span data-ttu-id="da850-173">Administrator może dodać aplikacje w sekcji usługi Active Directory w portalu Azure w trybie logowania jednokrotnego ustawioną **Azure AD rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="da850-173">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Azure AD Single Sign-On**.</span></span> <span data-ttu-id="da850-174">Te aplikacje może zobaczyć tylko, jeśli administrator ma jawnie przyznane uprawnienia dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-174">You can only see these applications if your administrator has explicitly granted you access to the applications.</span></span>

<span data-ttu-id="da850-175">Po kliknięciu kafelka dla jednej z tych aplikacji, są przekierowywane i zostanie automatycznie zalogowany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-175">When you click a tile for one of these applications, you are redirected and automatically signed in to the application.</span></span>

### <a name="password-based-sso-without-identity-provisioning"></a><span data-ttu-id="da850-176">Na podstawie hasła logowania jednokrotnego bez obsługi tożsamości</span><span class="sxs-lookup"><span data-stu-id="da850-176">Password-based SSO without identity provisioning</span></span>

<span data-ttu-id="da850-177">Administrator może dodać aplikacje w sekcji usługi Active Directory w portalu Azure w trybie logowania jednokrotnego ustawioną **opartego na hasłach rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="da850-177">Your administrator can add applications in the Active Directory section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**.</span></span> <span data-ttu-id="da850-178">Wszyscy użytkownicy w katalogu widzą wszystkie aplikacje, które zostały skonfigurowane w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="da850-178">All users in the directory can see all applications that have been configured in this mode.</span></span>

<span data-ttu-id="da850-179">Po raz pierwszy, kliknięciu kafelka dla jednej z tych aplikacji, zostanie wyświetlony monit zainstalować wtyczkę logowania jednokrotnego hasła dla programu Internet Explorer lub przeglądarki Chrome.</span><span class="sxs-lookup"><span data-stu-id="da850-179">The first time, you click a tile for one of these applications, you are prompted to install the Password SSO plug-in for Internet Explorer or Chrome.</span></span> <span data-ttu-id="da850-180">Instalacja może wymagać ponownego uruchomienia przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="da850-180">The installation might require you to restart your web browser.</span></span> <span data-ttu-id="da850-181">Po powrocie do panelu dostępu i ponownie kliknij Kafelek aplikacji, monit o nazwę użytkownika i hasło dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-181">When you return to the access panel and click the application tile again, you are prompted for a username and password for the application.</span></span> <span data-ttu-id="da850-182">Po wprowadzeniu nazwy użytkownika i hasła, te poświadczenia są bezpiecznie przechowywane i połączony z kontem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-182">When you have entered your username and password, these credentials are securely stored and linked to your account in Azure AD.</span></span>

<span data-ttu-id="da850-183">Przy następnym kliknięciu kafelka aplikacji, użytkownik zostanie automatycznie zarejestrowany aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-183">The next time you click the application tile, you are automatically signed in to the application.</span></span>  
<span data-ttu-id="da850-184">Nie trzeba ponownie wprowadź swoje poświadczenia i/lub Zainstaluj wtyczkę logowania jednokrotnego hasła.</span><span class="sxs-lookup"><span data-stu-id="da850-184">You don't have to enter your credentials again and or install the Password SSO plug-in.</span></span>

<span data-ttu-id="da850-185">Jeśli poświadczenia zostały zmienione w aplikacji docelowej innych firm, należy również zaktualizować swoje poświadczenia, które są przechowywane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-185">If your credentials have changed in the target third-party application, you must also update your credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="da850-186">**Aby zaktualizować poświadczenia:**</span><span class="sxs-lookup"><span data-stu-id="da850-186">**To update credentials:**</span></span>

1. <span data-ttu-id="da850-187">Wybierz ikonę na kafelku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-187">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="da850-188">Wybierz **zaktualizować poświadczenia** ponownie wprowadzić nazwę użytkownika i hasło dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-188">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="password-based-sso-with-identity-provisioning"></a><span data-ttu-id="da850-189">Oparte na hasłach rejestracji Jednokrotnej z inicjowaniem obsługi administracyjnej tożsamości</span><span class="sxs-lookup"><span data-stu-id="da850-189">Password-based SSO with identity provisioning</span></span>

<span data-ttu-id="da850-190">Administrator może dodawać aplikacje w **usługi Active Directory** części portalu Azure w trybie logowania jednokrotnego ustawioną **opartego na hasłach rejestracji jednokrotnej**, oraz inicjowanie obsługi tożsamości.</span><span class="sxs-lookup"><span data-stu-id="da850-190">Your administrator can add applications in the **Active Directory** section of the Azure portal with the SSO mode set to **Password-based Single Sign-On**, along with identity provisioning.</span></span>

<span data-ttu-id="da850-191">Po raz pierwszy, kliknij Kafelek aplikacji, dla jednego z tych aplikacji, monit o zainstalowanie **logowania jednokrotnego hasła dodatek dla programu Internet Explorer lub przeglądarki Chrome**.</span><span class="sxs-lookup"><span data-stu-id="da850-191">The first time, you click an application tile for one of these applications, you are prompted to install the **Password SSO plug-in for Internet Explorer or Chrome**.</span></span> <span data-ttu-id="da850-192">Instalacja może wymagać ponownego uruchomienia przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="da850-192">The installation might require you to restart your web browser.</span></span>  
<span data-ttu-id="da850-193">Po powrocie do panelu dostępu i ponownie kliknij Kafelek aplikacji, użytkownik zostanie automatycznie zarejestrowany aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-193">When you return to the access panel and click the application tile again, you are automatically signed in to the application.</span></span>

<span data-ttu-id="da850-194">Niektóre aplikacje mogą wymagać można zmienić hasło przy pierwszym logowaniu.</span><span class="sxs-lookup"><span data-stu-id="da850-194">Some applications might require you to change your password on the first sign-in.</span></span> <span data-ttu-id="da850-195">Jeśli poświadczenia zostały zmienione w aplikacji docelowej innych firm, należy również zaktualizować poświadczenia, które są przechowywane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da850-195">If your credentials have changed in the target third-party application, you must also update the credentials that are stored in Azure AD.</span></span> 

<span data-ttu-id="da850-196">**Aby zaktualizować poświadczenia:**</span><span class="sxs-lookup"><span data-stu-id="da850-196">**To update credentials:**</span></span>

1. <span data-ttu-id="da850-197">Wybierz ikonę na kafelku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-197">Select the icon on the application tile.</span></span>
2. <span data-ttu-id="da850-198">Wybierz **zaktualizować poświadczenia** ponownie wprowadzić nazwę użytkownika i hasło dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="da850-198">Select **update credentials** to reenter the username and password for the application.</span></span>


### <a name="application-with-existing-sso-solutions"></a><span data-ttu-id="da850-199">Aplikacja z istniejącymi rozwiązaniami do logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="da850-199">Application with existing SSO solutions</span></span>

<span data-ttu-id="da850-200">Aby skonfigurować logowanie Jednokrotne dla aplikacji, Azure portal udostępnia trzecia opcja o nazwie **istniejących rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="da850-200">To configure SSO for an application, the Azure portal provides a third option called **Existing Single Sign-On**.</span></span> <span data-ttu-id="da850-201">Ta opcja umożliwia administratorem, aby utworzyć łącze do aplikacji i umieść ją na panel dostępu dla wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="da850-201">This option enables your administrator to create a link to an application and place it on the access panel for selected users.</span></span>

<span data-ttu-id="da850-202">Na przykład jeśli aplikacja jest skonfigurowana do uwierzytelniania użytkowników za pomocą usług AD FS 2.0, administrator może użyć **istniejących rejestracji jednokrotnej** opcję, aby utworzyć łącze do niego w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="da850-202">For example, if an application is configured to authenticate users by using AD FS 2.0, your administrator can use the **Existing Single Sign-On** option to create a link to it on the access panel.</span></span> <span data-ttu-id="da850-203">Gdy uzyskujesz dostęp do łącza, są uwierzytelniane za pośrednictwem usług AD FS 2.0 lub niezależnie od istniejącej rejestracji Jednokrotnej rozwiązania przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="da850-203">When you access the link, you are authenticated through AD FS 2.0 or whatever existing SSO solution the application provides.</span></span>


## <a name="next-steps"></a><span data-ttu-id="da850-204">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da850-204">Next steps</span></span>

- <span data-ttu-id="da850-205">Aby wyświetlić listę wszystkich tematów, które są powiązane z zarządzaniem aplikacjami, zobacz [indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md).</span><span class="sxs-lookup"><span data-stu-id="da850-205">To see a list of all topics that are related to application management, see the [article index for application management in Azure Active Directory](active-directory-apps-index.md).</span></span>
 
- <span data-ttu-id="da850-206">Aby uzyskać informacje o integracji aplikacji SaaS w usłudze Azure AD, zobacz [lista samouczków dotyczących sposobów integracji aplikacji SaaS](active-directory-saas-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="da850-206">To learn how to integrate a SaaS app into Azure AD, see the [list of tutorials on how to integrate SaaS apps](active-directory-saas-tutorial-list.md).</span></span>
 
- <span data-ttu-id="da850-207">Aby dowiedzieć się więcej o zarządzaniu aplikacjami za pomocą usługi Azure AD, zobacz [wprowadzenie do uzyskania dostępu do pojedynczego aplikacji logowania jednokrotnego i zarządzanie nimi w usłudze Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="da850-207">To learn more about managing apps with Azure AD, see the [introduction to single sign-on and managing app access with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>
 
- <span data-ttu-id="da850-208">Aby dowiedzieć się więcej na temat Inicjowanie obsługi użytkowników, zobacz [zautomatyzować użytkownika alokowania i anulowania alokowania do aplikacji SaaS](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="da850-208">To learn more about user provisioning, see [automate user provisioning and deprovisioning to SaaS applications](active-directory-saas-app-provisioning.md).</span></span>

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
