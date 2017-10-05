---
title: "What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, co jest nowego w zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: asteen
ms.reviewer: asteen
ms.openlocfilehash: 0c32a6719292aa903aa32dfdc4a31114e7a28346
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="whats-new-in-enterprise-application-management-in-azure-active-directory"></a><span data-ttu-id="2c9f5-103">What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c9f5-103">What's new in Enterprise Application management in Azure Active Directory</span></span> 

<span data-ttu-id="2c9f5-104">Azure Active Directory (Azure AD) rozszerzona enterprise narzędzia do zarządzania aplikacjami, z nowych funkcji i możliwości, aby prostszy i wydajne zarządzanie aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-104">Azure Active Directory (Azure AD) has enhanced enterprise application management tools, with new features and capabilities to make managing apps simpler and efficient.</span></span>

<span data-ttu-id="2c9f5-105">Oto niektóre ulepszenia dla usługi Azure AD w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c9f5-105">Following are some of the enhancements for Azure AD in the [Azure portal](https://portal.azure.com).</span></span>

- <span data-ttu-id="2c9f5-106">Galerii aplikacji ulepszone wystąpić z modelem tworzenia aplikacji uproszczone i obsługę wszystkich typów aplikacji, których użyto do.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-106">An improved application gallery experience, with a simplified application creation model and support for all the application types that you’re used to.</span></span> 
- <span data-ttu-id="2c9f5-107">Środowisko całkowicie nowy szybki start, które mogą pomóc rozpocząć korzystanie z pilotażu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-107">A brand-new quick start experience that can help you get going with a pilot of your application.</span></span> 
- <span data-ttu-id="2c9f5-108">Konfigurowanie zasad samoobsługi za pomocą kilku kliknięć.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-108">Configure self-service policies with just a few clicks.</span></span> 
- <span data-ttu-id="2c9f5-109">Ulepszenia serwera proxy aplikacji, z jednym konfiguracji logowania jednokrotnego, a następnie przełącz własnego środowiska aplikacji, umożliwiające uzyskanie bardziej gotowe niż przed.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-109">Improvements to application proxy, single sign-on configuration, and bring your own application experiences, allowing you to get more done than before.</span></span>

## <a name="improvements-to-the-azure-active-directory-application-gallery"></a><span data-ttu-id="2c9f5-110">Ulepszenia dotyczące galerii aplikacji Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c9f5-110">Improvements to the Azure Active Directory Application Gallery</span></span>

<span data-ttu-id="2c9f5-111">Dodawanie ulubionych aplikacji, czy są one z [galerii aplikacji](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), niestandardowych aplikacji, jest rozszerzenie w chmurze lub nowe aplikacje projektujesz.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-111">Add your favorite applications whether they are from the [application gallery](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), custom applications you’re extending to the cloud, or new applications you’re developing.</span></span>  <span data-ttu-id="2c9f5-112">Możesz rozpocząć pracę z nowe środowisko, klikając **Dodaj** na **aplikacje dla przedsiębiorstw** omówienie lub **wszystkie aplikacje** bloków.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-112">You can get started with this new experience by clicking **Add** on the **Enterprise Applications** overview or **All applications** blades.</span></span>
 
  ![Dodawanie aplikacji](./media/active-directory-enterprise-apps-whats-new-azure-portal/01.png)

<span data-ttu-id="2c9f5-114">Raz w galerii, zobaczysz, których obsługę użytkowników naszego polecanych aplikacji wyświetlane przodu Centrum.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-114">Once in the gallery, you’ll see all our featured applications which support user provisioning displayed front-and-center.</span></span>  <span data-ttu-id="2c9f5-115">Możesz przeglądać szerokiej gamy różne kategorie, aby przejść do aplikacji, które są dla Ciebie ważne lub można szybko znaleźć aplikacji, którą chcesz zintegrować wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-115">You can browse all sorts of different categories to drill into the applications you care about, or you can use the search experience to rapidly find the applications you want to integrate.</span></span>

  ![Galerii aplikacji](./media/active-directory-enterprise-apps-whats-new-azure-portal/02.png)

## <a name="add-custom-applications-from-one-place"></a><span data-ttu-id="2c9f5-117">Dodawanie niestandardowych aplikacji w jednym miejscu</span><span class="sxs-lookup"><span data-stu-id="2c9f5-117">Add custom applications from one place</span></span>

<span data-ttu-id="2c9f5-118">Oprócz dodania wstępnie zintegrowanych aplikacji z poziomu galerii, konfiguracji niestandardowej aplikacji napotyka, aby były używane do w portalu klasycznym zarządzania się teraz w nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-118">In addition to adding pre-integrated applications from the gallery, all the custom application configuration experiences that you were used to in the classic management portal are now possible in the new portal.</span></span> <span data-ttu-id="2c9f5-119">Czy to rozszerzenie aplikacji lokalnych przy użyciu serwera proxy aplikacji, integrowanie własnego hasła lub aplikacji federacyjnej logowania jednokrotnego, lub tworzenia zupełnie nowym aplikacji za pomocą rejestru aplikacji, można uzyskać do niego z tym jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-119">Whether you are extending an application from on-premises using the application proxy, integrating your own password or federated SSO application, or creating a brand-new application using the application registry, you can get to it all from this one single place.</span></span>

  ![Dodawanie aplikacji](./media/active-directory-enterprise-apps-whats-new-azure-portal/03.png)

 
<span data-ttu-id="2c9f5-121">**Aby rozpocząć dodawanie własnych aplikacji**:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-121">**To get started adding your own application**:</span></span>

1. <span data-ttu-id="2c9f5-122">Kliknij przycisk **dodać własne łącze** w górnej części galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-122">Click the **add your own link** at the top of the application gallery.</span></span> 
2. <span data-ttu-id="2c9f5-123">Zostaną wyświetlone dwie opcje przed możesz: **wdrażania istniejącej aplikacji** lub **Tworzenie nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-123">You’ll see two options in front of you: **deploy an existing application** or **develop a new application**.</span></span> <span data-ttu-id="2c9f5-124">W dalszej różnice między dwóch opcji i sposobu ich używania.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-124">Read on to learn the difference between the two options and how to use them.</span></span>

### <a name="deploying-existing-applications"></a><span data-ttu-id="2c9f5-125">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c9f5-125">Deploying existing applications</span></span>

1. <span data-ttu-id="2c9f5-126">Jeśli otrzymasz aplikacji już uruchomiona i po prostu chcesz zintegrować ją z usługą Azure AD, jednokrotnego na lub inicjowania obsługi administracyjnej, wybierz **wdrażania istniejącej aplikacji** opcji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-126">If you’ve got an application running already and just want to integrate it into Azure AD for single-sign on or provisioning, choose the **Deploy an existing application** option.</span></span> <span data-ttu-id="2c9f5-127">Wybierz nazwę dla aplikacji, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-127">Pick a name for your application, click **Add**.</span></span>
2. <span data-ttu-id="2c9f5-128">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-128">That's it!</span></span> <span data-ttu-id="2c9f5-129">Zamiast konieczności poznać wszystkie szczegóły dotyczące Twojej aplikacji na początku, można teraz skonfigurować działanie nowej aplikacji przechodząc za pośrednictwem menu po lewej stronie i konfigurowanie aplikacji do potrzeb użytkownika w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-129">Instead of needing to know all the details about your application up front, you can now set up how your new application works by navigating through the left menu and configuring the application to your liking at any time.</span></span>

  ![Dodawanie istniejącej aplikacji jednym kliknięciem](./media/active-directory-enterprise-apps-whats-new-azure-portal/04.png)
 
### <a name="developing-new-applications"></a><span data-ttu-id="2c9f5-131">Tworzenie nowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="2c9f5-131">Developing new applications</span></span>

1. <span data-ttu-id="2c9f5-132">W przypadku tworzenia nowej aplikacji, istnieje łatwy sposób na uzyskanie dostępu do rejestru aplikacji prawo z poziomu galerii:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-132">If you’re developing a new application, there's an easy way for you to get to the Application Registry right from the gallery:</span></span>
2. <span data-ttu-id="2c9f5-133">Polecenie **dodać własną** opcję z galerii aplikacji, wybierz **opracowanie istniejącej aplikacji** wyboru, aby zobaczyć szybkie łącze prawo do obsługi Dodaj aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-133">Click on the **add your own** option from the Application Gallery, select the **develop an existing application** choice, and you’ll see a quick link right to the application add experience.</span></span>

  ![Dodawanie do aplikacji nowo utworzonych za pomocą kilku kliknięć](./media/active-directory-enterprise-apps-whats-new-azure-portal/05.png)


>[!NOTE]
><span data-ttu-id="2c9f5-135">Po dodaniu aplikacji za pomocą rejestru aplikacji, zobaczysz je na liście aplikacji przedsiębiorstwa, w której będziesz mieć możliwość konfigurowania rejestracji jednokrotnej i zarządzania zasady dostępu dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-135">Once you add an application using the Application Registry, you’ll see it show up in the list of Enterprise Applications where you’ll be able to configure single sign-on and manage access policies for your new application.</span></span>

  ![Zarządzanie dostępem do nowych aplikacji w aplikacjach dla przedsiębiorstw](./media/active-directory-enterprise-apps-whats-new-azure-portal/06.png)


## <a name="quick-start-get-going-with-your-new-application-right-away"></a><span data-ttu-id="2c9f5-137">Szybki start: rozpocząć korzystanie z nowej aplikacji natychmiast</span><span class="sxs-lookup"><span data-stu-id="2c9f5-137">Quick start: Get going with your new application right away</span></span> 

<span data-ttu-id="2c9f5-138">Po dodaniu aplikacji, czy też być wstępnie zintegrowanych lub własną aplikację, utworzyliśmy dostosowane środowisko szybki start, umożliwiające szybkie uziemione w nowym środowisku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-138">After you’ve added an application, whether it be pre-integrated or your own app, we’ve created a tailored quick-start experience to get you grounded in the new applications experience quickly.</span></span> <span data-ttu-id="2c9f5-139">Jeśli wykonujesz systematycznie poszczególnych opcji, firma Microsoft będzie przeprowadzenie interfejsu użytkownika i opisano, jak rozpocząć korzystanie z pilotażu nowej aplikacji tak szybko jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-139">If you follow each option systematically, we’ll walk you through the UI and show you how to get going with a pilot of your new application as quickly as possible.</span></span> 
 
  ![Nowe aplikacje szybki start środowisko](./media/active-directory-enterprise-apps-whats-new-azure-portal/07.png)

 <span data-ttu-id="2c9f5-141">Nowe środowisko szybki start w dowolnym momencie, a dla dowolnej aplikacji, mogą odwiedzać, klikając **szybki start** w menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-141">You can visit this new quick start experience at any time, and for any application, by clicking on **Quick start** from the application left navigation menu.</span></span>


## <a name="updated-application-proxy-configuration"></a><span data-ttu-id="2c9f5-142">Konfiguracja serwera proxy aplikacji zaktualizowane</span><span class="sxs-lookup"><span data-stu-id="2c9f5-142">Updated application proxy configuration</span></span>
<span data-ttu-id="2c9f5-143">Teraz załóżmy powiedzieć jedną z nowych aplikacji, dodane jest uruchomiony w środowisku lokalnym i chcesz zintegrować ją z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-143">Now, let’s say one of the new applications you added is running in your on-premises environment and you want to integrate it with Azure AD.</span></span>  <span data-ttu-id="2c9f5-144">Jeden z chłodnych nowe obiekty o nowe środowisko konfiguracji aplikacji w nowej usłudze Azure AD portalu jest, że dzielenie aplikacji logowania w trybie z jego konfigurację serwera proxy aplikacji, mogą teraz łatwo naraża hasło logowania jednokrotnego lub aplikacje, które są uruchomione w sieci firmowej bezpośrednio do chmury, bez konieczności tworzenia wielu wystąpień aplikacji federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-144">One of the cool new things about the new application configuration experience in the new Azure AD portal is that by splitting the application’s sign-on mode from its application proxy configuration, you can now easily expose password SSO or federated applications that are running in your corporate network right to the cloud, without having to create multiple instances of the application.</span></span>

<span data-ttu-id="2c9f5-145">Oprócz tego można teraz również skonfigurować wszelkie nowe aplikacje, które zostały dodane do użycia z prawej strony serwera Proxy aplikacji usługi Azure AD z nowego portalu, w tym aplikacji, które obsługują macierzysty środowiska uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-145">In addition to this, you can now also configure any of the new applications you’ve added for use with the Azure AD Application Proxy right from the new portal, including applications which support native Windows authentication experiences.</span></span>

  ![Konfigurowanie aplikacji do korzystania z opcji logowania jednokrotnego zintegrowane uwierzytelnianie systemu Windows](./media/active-directory-enterprise-apps-whats-new-azure-portal/08.png)
 

<span data-ttu-id="2c9f5-147">Aby rozpocząć konfigurowanie aplikacji natywnej uwierzytelniania systemu Windows przy użyciu serwera Proxy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-147">To get started configuring a native Windows authentication application with the Application Proxy:</span></span>
1. <span data-ttu-id="2c9f5-148">Kliknij element nawigacji rejestracji jednokrotnej i wybierz polecenie **zintegrowane uwierzytelnianie systemu Windows** w bloku ustawienia logowania jednokrotnego i skonfiguruj ustawienia do swoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-148">Click on the Single sign-on navigation item and choose **Integrated Windows Authentication** from the sign-on settings blade and configure the settings to your liking.</span></span>
2. <span data-ttu-id="2c9f5-149">U góry obsługi tych nowych tryby uwierzytelniania, możesz teraz również przekazać certyfikatów z niestandardowych domen do obsługi aplikacji działających na bezpieczne punkty końcowe w ramach danej organizacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-149">On top of supporting these new authentication modes, you can now also upload certificates from custom domains to support applications running on secure endpoints within your organization.</span></span>  
 
   ![Przekazywanie certyfikatu do użycia z serwera Proxy aplikacji](./media/active-directory-enterprise-apps-whats-new-azure-portal/09.png)

3. <span data-ttu-id="2c9f5-151">Aby przekazać nowy certyfikat dla aplikacji lokalnych Ulubione, kliknij **serwera proxy aplikacji** opcję w menu nawigacji po lewej stronie, kliknij przycisk **certyfikatu** selektor i przekazywanie pliku certyfikatu, możemy użyć do zaszyfrowania żądania z naszych punktu końcowego w chmurze do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-151">To upload a new certificate for your favorite on-premises application, click on the **Application proxy** option from the left navigation menu, click the **Certificate** selector, and upload a certificate file we can use to encrypt requests from our cloud endpoint to your application.</span></span>

## <a name="advanced-federated-single-sign-on-configuration"></a><span data-ttu-id="2c9f5-152">Federacyjnych pojedynczego logowania jednokrotnego Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="2c9f5-152">Advanced federated single sign-on configuration</span></span>

<span data-ttu-id="2c9f5-153">Dla osób, które obecnie za pomocą aplikacji federacyjnych istnieje wiele nowych funkcji w bloku konfiguracji opartej na SAML logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-153">For those of you using federated applications today, there are many new features in the SAML-based sign-on configuration blade.</span></span> <span data-ttu-id="2c9f5-154">Do uruchomienia z teraz możesz można całkowicie dostosować, dodawania, usuwania i mapowanie istniejących atrybutów użytkownika wystawione jako oświadczenia w tokenach SAML.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-154">To start with, now you can fully customize, add, remove, and map the existing user attributes issued as claims in SAML tokens.</span></span>
 
  ![Dostosowywanie atrybutów użytkownika tokenu SAML przekazane do aplikacji federacyjnych](./media/active-directory-enterprise-apps-whats-new-azure-portal/10.png)


<span data-ttu-id="2c9f5-156">Aby sprawdzić się z nowym Federacyjna usługa rejestracji Jednokrotnej w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-156">To check that out the new federated SSO configuration:</span></span>
1. <span data-ttu-id="2c9f5-157">Otwórz aplikacji federacyjnych **logowanie jednokrotne** bloku z menu nawigacji po lewej stronie i upewnij się, że "*na języku SAML logowania jednokrotnego** wybrany tryb.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-157">Open a federated application’s **single sign-on** blade from the left navigation menu and make sure the ‘*SAML-based Sign-on** mode is selected.</span></span> 
2. <span data-ttu-id="2c9f5-158">Raz istnieje, włączyć pole wyboru w obszarze **atrybuty użytkownika** nagłówek, aby zmodyfikować wszystkie atrybuty uwzględnione w tokenie SAML przekazany do tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-158">Once there, enable the checkbox under the **User Attributes** heading to modify all of the attributes included in the SAML token passed to that application.</span></span>

<span data-ttu-id="2c9f5-159">Możesz można również utworzyć, przerzucania i zarządzanie certyfikatami używanymi do federacyjnego logowania jednokrotnego, a także edytować, który pobiera powiadamiani się wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-159">You can also create, rollover, and manage certificates used for federated single sign-on, as well as edit who gets notified when your certificate is about to expire.</span></span> <span data-ttu-id="2c9f5-160">Zobaczysz tych nowych opcji w obszarze **certyfikaty** nagłówek w tym samym pojedynczego logowania jednokrotnego bloku.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-160">You’ll see these new options under the **Certificates** heading on the same Single sign-on blade.</span></span>
 
  ![Tworzenie nowego świadectwa, dostosowywanie wygaśnięcia powiadomienia e-mail i opcje podpisywania certyfikatu](./media/active-directory-enterprise-apps-whats-new-azure-portal/11.png)

### <a name="relay-state-paramenter"></a><span data-ttu-id="2c9f5-162">Stan przekazywania paramenter</span><span class="sxs-lookup"><span data-stu-id="2c9f5-162">Relay State paramenter</span></span>
<span data-ttu-id="2c9f5-163">Na koniec możemy zostały również rozszerzony zestaw parametrów, adres URL SAML obsługujemy obejmują **parametr Stan przekazywania**, czyli strony użytkownicy przeniesie na wewnątrz aplikacji federacyjnych po przy logowaniu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-163">Finally, we’ve also extended the set of SAML URL parameters we support to include the **Relay State parameter**, which is the page your users will land on inside of a federated application once the sign-in is completed.</span></span> <span data-ttu-id="2c9f5-164">Jest to bardzo przydatne ustawienie umożliwia skonfigurowanie, jeśli chcesz wysłać użytkowników do określonego miejsca w aplikacji, aby udostępnić je szybko przerywaj.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-164">This is very useful setting to configure if you want to send your users to a specific place within the application to get them going quickly.</span></span>

  ![Ustawienie parametru stan przekazywania SAML](./media/active-directory-enterprise-apps-whats-new-azure-portal/12.png)
 
<span data-ttu-id="2c9f5-166">**Aby ustawić parametr Stan przekazywania**:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-166">**To set the relay state parameter**:</span></span>

1. <span data-ttu-id="2c9f5-167">Włącz **Pokaż zaawansowane ustawienia adresu URL** pole wyboru w obszarze **domeny i adres URL** nagłówek jednokrotnego blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-167">Enable the **Show advanced URL settings** check-box under the **Domain and URLs** heading on the single-sign on configuration blade.</span></span> 
2. <span data-ttu-id="2c9f5-168">Po wykonaniu tej czynności zobaczysz wprowadzenia danych przez zestaw nowy adres URL, który umożliwi to i inne ustawienia adresu URL SAML okien dialogowych.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-168">Once you do this, you’ll see a set of new URL input boxes appear which will allow you to set this, and other, SAML URL settings.</span></span>

## <a name="bring-your-own-password-sso-applications"></a><span data-ttu-id="2c9f5-169">Przenoszenie własnego hasła aplikacji rejestracji Jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2c9f5-169">Bring your own password SSO applications</span></span>

<span data-ttu-id="2c9f5-170">Wiemy, że nie każda aplikacja obsługuje federacyjnego dodatkowych zabiegów.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-170">We know that not every application supports federation right out of the box.</span></span> <span data-ttu-id="2c9f5-171">Na przykład może być jedną z nowych aplikacji, dodane ma ekran logowania niestandardowe, w której korzystają użytkownicy nazwy użytkownika i hasła do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-171">For example, maybe one of the new applications you added has a custom login screen that your users use a username and password to sign in to.</span></span> <span data-ttu-id="2c9f5-172">Aplikacje tego typu nadal można zintegrować z usługą Azure AD za pomocą naszych **Przenoszenie własnych aplikacji** funkcji, która jest teraz dostępna do skonfigurowania w nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-172">You can still integrate these types of applications with Azure AD using our **Bring your own applications** feature, which is now available for you to configure in the new portal.</span></span>
 
  ![Integrowanie niestandardowych hasła vaulting aplikacji za pomocą usługi Azure AD](./media/active-directory-enterprise-apps-whats-new-azure-portal/13.png)

<span data-ttu-id="2c9f5-174">**Aby zapoznać się z funkcji "Przynieś własne aplikacje"**:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-174">**To check out the 'Bring your own applications' feature**:</span></span>

1. <span data-ttu-id="2c9f5-175">Po ustawieniu jeden tryb logowania jednokrotnego dla nowej aplikacji niestandardowych, które zostały dodane do **opartego na hasłach logowania jednokrotnego**, wprowadź adres URL, w którym aplikacja renderuje jego ekran logowania i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-175">After you set the single sign-on mode for a new custom application that you’ve added to **Password-based Sign-on**, enter the URL where the application renders its login screen and click **Save**.</span></span>  
2. <span data-ttu-id="2c9f5-176">Po wykonaniu tej czynności, firma Microsoft będzie automatycznie scrape tego adresu URL dla nazwy użytkownika i hasło pole wprowadzania i umożliwiają używanie usługi Azure AD do bezpiecznego przesyłania hasła do tej aplikacji przy użyciu rozszerzenia przeglądarki panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-176">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="configure-self-service-application-access"></a><span data-ttu-id="2c9f5-177">Konfigurowanie dostępu do aplikacji Sklep internetowy</span><span class="sxs-lookup"><span data-stu-id="2c9f5-177">Configure self-service application access</span></span>

<span data-ttu-id="2c9f5-178">Po dodaniu wiele nowych aplikacji może być chcesz zezwolić użytkownikom przeglądać i dodać te aplikacje do ich własnych paneli dostępu, bez konieczności odblokowane jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-178">After you’ve added lots of new applications, maybe you want to allow your users to browse and add those applications to their own access panels, without needing to bother you as an administrator.</span></span> <span data-ttu-id="2c9f5-179">Teraz w tej najnowszej wersji, można skonfigurować i zarządzanie dostępem do aplikacji Sklep internetowy z nowego portalu.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-179">Now, with this latest release, you can configure and manage self-service application access right from the new portal.</span></span>

  ![Konfigurowanie dostępu do aplikacji Sklep internetowy hasła aplikacji rejestracji Jednokrotnej](./media/active-directory-enterprise-apps-whats-new-azure-portal/14.png)
 
<span data-ttu-id="2c9f5-181">**Aby skonfigurować i zarządzać dostępem do aplikacji Sklep internetowy**:</span><span class="sxs-lookup"><span data-stu-id="2c9f5-181">**To configure and manage self-service application access**:</span></span>

1. <span data-ttu-id="2c9f5-182">Aby rozpocząć pracę, możesz zaznaczyć **samoobsługi** menu nawigacji w lewo i ustaw opcję z aplikacji **Zezwalaj użytkownikom na żądanie dostępu do tej aplikacji?** opcje "**tak**".</span><span class="sxs-lookup"><span data-stu-id="2c9f5-182">To get started, you can select the **Self-service** option from the application’s left navigation menu and set the **Allow users to request access to this application?** option to ‘**Yes**’.</span></span> 
2. <span data-ttu-id="2c9f5-183">Można konfigurować, kto może zatwierdzić dostęp do tej aplikacji i grup samoobsługi użytkowników, którzy zostaną dodane zostaną włączone.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-183">This will enable you to configure who is allowed to approve access to this application, and which group self-service users will be added.</span></span> <span data-ttu-id="2c9f5-184">Ponadto jeśli aplikacja jest skonfigurowana pod kątem hasła jednokrotnego, również zobaczysz inną opcją, co umożliwia opcjonalnie zezwolić tych osób zatwierdzających do zarządzania hasłami przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-184">In addition, if the application is configured for password single-sign on, you’ll also see another option which lets you optionally allow those approvers to manage the passwords assigned to the application.</span></span>

##<a name="feedback"></a><span data-ttu-id="2c9f5-185">Opinia</span><span class="sxs-lookup"><span data-stu-id="2c9f5-185">Feedback</span></span>

<span data-ttu-id="2c9f5-186">Mamy nadzieję przy użyciu udoskonalone środowisko usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-186">We hope you like using the improved Azure AD experience.</span></span> <span data-ttu-id="2c9f5-187">Pamiętaj o opinie przesyłanych!</span><span class="sxs-lookup"><span data-stu-id="2c9f5-187">Please keep the feedback coming!</span></span> <span data-ttu-id="2c9f5-188">Opinie i pomysły dotyczące poprawy **portalu administracyjnego** sekcji naszych [forum opinii](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span><span class="sxs-lookup"><span data-stu-id="2c9f5-188">Post your feedback and ideas for improvement in the **Admin Portal** section of our [feedback forum](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).</span></span>  <span data-ttu-id="2c9f5-189">Firma Microsoft jest podekscytowani, informacje o kompilowaniu chłodnych nowości codziennie i użyj wskazówek z kształtem i zdefiniować, co mamy utworzyć w następnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="2c9f5-189">We’re excited about building cool new stuff every day, and use your guidance to shape and define what we build next.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c9f5-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c9f5-190">Next steps</span></span>

<span data-ttu-id="2c9f5-191">Aby uzyskać więcej informacji, zobacz [Zarządzanie aplikacjami w usłudze Azure Active Directory](active-directory-enable-sso-scenario.md).</span><span class="sxs-lookup"><span data-stu-id="2c9f5-191">For more details, see [Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md).</span></span>



