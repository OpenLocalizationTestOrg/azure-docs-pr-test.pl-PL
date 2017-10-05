---
title: "Jak skonfigurować hasło rejestracji jednokrotnej dla applicationn z systemem innym niż galerii | Dokumentacja firmy Microsoft"
description: "Konfigurowanie niestandardowych aplikacji z systemem innym niż galerii dla bezpiecznej opartego na hasłach rejestracji jednokrotnej, gdy nie znajduje się w galerii aplikacji usługi Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="242b1-103">Jak skonfigurować hasła logowanie jednokrotne dla aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="242b1-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="242b1-104">Oprócz opcji znaleziony w galerii aplikacji usługi Azure AD, masz również możliwość dodania **aplikacji z systemem innym niż galerii** gdy aplikacja ma nie ma na liście istnieje.</span><span class="sxs-lookup"><span data-stu-id="242b1-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="242b1-105">Przy użyciu tej możliwości, możesz dodać dowolnej aplikacji, która już istnieje w danej organizacji lub dowolnej aplikacji innych firm, z którego można korzystać z dostawcy, który nie jest już częścią [galerii aplikacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="242b1-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="242b1-106">Po dodaniu aplikacji z systemem innym niż galerii, następnie można skonfigurować pojedynczy metodę logowania jednokrotnego korzysta z tej aplikacji, wybierając **rejestracji jednokrotnej** element nawigacji w aplikacji przedsiębiorstwa w [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="242b1-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="242b1-107">Dostępne metod rejestracji jednokrotnej jest [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) opcji.</span><span class="sxs-lookup"><span data-stu-id="242b1-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="242b1-108">Z **dodania aplikacji z systemem innym niż galerii** doświadczenia, można je zintegrować w dowolnej aplikacji, która renderuje oparty na języku HTML nazwy użytkownika i hasła, wprowadź pola, nawet jeśli nie jest w naszym zestawie wstępnie zintegrowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="242b1-109">Jest to działania przez stronę oskrobaniu technologii, która jest częścią rozszerzenia Panelu dostępu, które pozwala na automatyczne wykrywanie pól wejściowych użytkownika i hasło, bezpieczne przechowywanie dla swojego wystąpienia określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="242b1-110">Bezpiecznie powtarzania nazwy użytkownika i hasła do tych pól, gdy użytkownik przechodzi do tej aplikacji na panelu dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="242b1-111">Jest to dobry sposób, aby rozpocząć integrowanie dowolnego rodzaju aplikacji usługi Azure AD szybko i umożliwia:</span><span class="sxs-lookup"><span data-stu-id="242b1-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="242b1-112">Integracja **aplikacje w świecie** z dzierżawy usługi Azure AD, ile renderowania HTML nazwy użytkownika i hasła pola wejściowego</span><span class="sxs-lookup"><span data-stu-id="242b1-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="242b1-113">Włącz **rejestracji jednokrotnej dla użytkowników** bezpieczne przechowywanie i odtwarzanie nazwy użytkowników i hasła dla aplikacji zostały zintegrowane z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="242b1-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="242b1-114">**Autowykrywanie wprowadzania** pól dla każdej aplikacji i umożliwiają ręcznie wykryć tych pól przy użyciu rozszerzenia przeglądarki panelu dostępu, w przypadku automatycznego wykrywania ich nie znajdzie</span><span class="sxs-lookup"><span data-stu-id="242b1-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="242b1-115">**Obsługuje aplikacje, które wymagają wielu pól logowania** dla aplikacji, które wymagają więcej niż tylko pola Nazwa użytkownika i hasło do logowania się w</span><span class="sxs-lookup"><span data-stu-id="242b1-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="242b1-116">**Dostosowywanie etykiet** pól wprowadzania nazwy użytkownika i hasła użytkownicy zobaczą na [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) po oni wprowadzić swoje poświadczenia</span><span class="sxs-lookup"><span data-stu-id="242b1-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="242b1-117">Zezwalaj na Twojej **użytkowników** zapewnienie własne nazwy użytkowników i hasła dla wszystkich istniejących kont aplikacji wpisywania w ręcznie na [Panel dostępu do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="242b1-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="242b1-118">Zezwalaj na **grupy biznesowej** do określenia nazwy użytkowników i hasła przypisana do użytkownika za pomocą [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) funkcji</span><span class="sxs-lookup"><span data-stu-id="242b1-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="242b1-119">Zezwalaj na **administratora** do określenia nazwy użytkowników i hasła przypisana do użytkownika przy użyciu poświadczeń aktualizacji funkcji podczas [przypisanie użytkownika do aplikacji](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="242b1-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="242b1-120">Zezwalaj na **administratora** do określenia udostępnionego nazwy użytkownika i hasło używane przez grupy osób przy użyciu poświadczeń aktualizacji funkcji podczas [przypisanie grupy do aplikacji](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="242b1-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="242b1-121">Poniżej opisano, jak można włączyć [opartego na hasłach rejestracji jednokrotnej](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) do dowolnej aplikacji, które można dodać przy użyciu **dodania aplikacji z systemem innym niż galerii** wystąpić.</span><span class="sxs-lookup"><span data-stu-id="242b1-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="242b1-122">Omówienie kroków wymaganych</span><span class="sxs-lookup"><span data-stu-id="242b1-122">Overview of steps required</span></span>

<span data-ttu-id="242b1-123">Aby skonfigurować aplikację z galerii Azure AD, która ma być:</span><span class="sxs-lookup"><span data-stu-id="242b1-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="242b1-124">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="242b1-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="242b1-125">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="242b1-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="242b1-126">Przypisywanie aplikacji do użytkownika lub grupy</span><span class="sxs-lookup"><span data-stu-id="242b1-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="242b1-127">Bezpośrednio przypisać użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="242b1-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="242b1-128">Bezpośrednie przypisywanie aplikacji do grupy</span><span class="sxs-lookup"><span data-stu-id="242b1-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="242b1-129">Dodawanie aplikacji z systemem innym niż galerii</span><span class="sxs-lookup"><span data-stu-id="242b1-129">Add a non-gallery application</span></span>

<span data-ttu-id="242b1-130">Aby dodać aplikację z poziomu galerii Azure AD, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="242b1-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="242b1-131">Otwórz [Azure Portal](https://portal.azure.com) i zaloguj się jako **administratora globalnego** lub **współadministratora**</span><span class="sxs-lookup"><span data-stu-id="242b1-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="242b1-132">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="242b1-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="242b1-133">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="242b1-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="242b1-134">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="242b1-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="242b1-135">Kliknij przycisk **Dodaj** znajdującego się w prawym górnym rogu na **aplikacje dla przedsiębiorstw** bloku</span><span class="sxs-lookup"><span data-stu-id="242b1-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="242b1-136">Kliknij przycisk **Non galerii aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="242b1-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="242b1-137">Wprowadź nazwę aplikacji w **nazwa** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="242b1-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="242b1-138">Wybierz **dodać.**</span><span class="sxs-lookup"><span data-stu-id="242b1-138">Select **Add.**</span></span>

<span data-ttu-id="242b1-139">Po krótkim czasie można zobaczyć blok konfiguracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="242b1-140">Skonfiguruj aplikację dla hasła logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="242b1-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="242b1-141">Aby skonfigurować logowanie jednokrotne dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="242b1-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="242b1-142">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**</span><span class="sxs-lookup"><span data-stu-id="242b1-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="242b1-143">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="242b1-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="242b1-144">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="242b1-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="242b1-145">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="242b1-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="242b1-146">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="242b1-147">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="242b1-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="242b1-148">Wybierz aplikację, aby skonfigurować logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="242b1-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="242b1-149">Po załadowaniu aplikacji, kliknij przycisk **logowanie jednokrotne** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="242b1-150">Wybierz tryb **opartego na hasłach logowania jednokrotnego.**</span><span class="sxs-lookup"><span data-stu-id="242b1-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="242b1-151">Wprowadź **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="242b1-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="242b1-152">Jest to adres URL, których użytkownicy wprowadzić swoją nazwę i hasło do logowania się na.</span><span class="sxs-lookup"><span data-stu-id="242b1-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="242b1-153">Upewnij się, że logowanie pola są widoczne pod adresem URL.</span><span class="sxs-lookup"><span data-stu-id="242b1-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="242b1-154">Przypisywanie użytkowników do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-154">Assign users to the application.</span></span>

11. <span data-ttu-id="242b1-155">Ponadto można też podać poświadczenia w imieniu użytkownika, wybierając wierszy użytkowników i kliknięcie **poświadczenia aktualizacji** i wprowadzić nazwę użytkownika i hasło w imieniu użytkowników.</span><span class="sxs-lookup"><span data-stu-id="242b1-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="242b1-156">W przeciwnym razie użytkownicy monit o podanie poświadczeń się po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="242b1-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="242b1-157">Bezpośrednio przypisać użytkownika do aplikacji</span><span class="sxs-lookup"><span data-stu-id="242b1-157">Assign a user to an application directly</span></span>

<span data-ttu-id="242b1-158">Aby przypisać bezpośrednio co najmniej jednego użytkownika do aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="242b1-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="242b1-159">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="242b1-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="242b1-160">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="242b1-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="242b1-161">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="242b1-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="242b1-162">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="242b1-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="242b1-163">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="242b1-164">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="242b1-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="242b1-165">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="242b1-166">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="242b1-167">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="242b1-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="242b1-168">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="242b1-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="242b1-169">Wpisz w **Pełna nazwa** lub **adres e-mail** użytkownika planuje się przypisanie do **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="242b1-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="242b1-170">Umieść kursor nad **użytkownika** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="242b1-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="242b1-171">Zaznacz pole wyboru obok zdjęcia profilu użytkownika lub logo, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="242b1-172">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać użytkownika do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="242b1-173">Po zakończeniu wybierania użytkowników, kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="242b1-174">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do użytkowników po wybraniu.</span><span class="sxs-lookup"><span data-stu-id="242b1-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="242b1-175">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="242b1-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="242b1-176">Bezpośrednie przypisywanie aplikacji do grupy</span><span class="sxs-lookup"><span data-stu-id="242b1-176">Assign an application to a group directly</span></span>

<span data-ttu-id="242b1-177">Aby przypisać co najmniej jedną grupę aplikacji bezpośrednio, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="242b1-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="242b1-178">Otwórz [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**</span><span class="sxs-lookup"><span data-stu-id="242b1-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="242b1-179">Otwórz **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="242b1-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="242b1-180">Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr a wybierz **usługi Azure Active Directory** elementu.</span><span class="sxs-lookup"><span data-stu-id="242b1-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="242b1-181">Kliknij przycisk **aplikacje dla przedsiębiorstw** w menu nawigacji po lewej stronie usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="242b1-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="242b1-182">Kliknij przycisk **wszystkie aplikacje** Aby wyświetlić listę wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="242b1-183">Jeśli nie ma aplikacji ma tutaj będą wyświetlane, użyj **filtru** kontroli nad **listę wszystkich aplikacji** i ustaw **Pokaż** opcji w celu **wszystkich aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="242b1-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="242b1-184">Wybierz aplikacji, którą chcesz przypisać do użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="242b1-185">Po załadowaniu aplikacji, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="242b1-186">Kliknij przycisk **Dodaj** przycisk nad **użytkowników i grup** listy, aby otworzyć **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="242b1-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="242b1-187">Kliknij przycisk **użytkowników i grup** selektora z **Dodaj przydziału** bloku.</span><span class="sxs-lookup"><span data-stu-id="242b1-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="242b1-188">Wpisz w **grupy Pełna nazwa** planuje się przypisanie do grupy **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="242b1-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="242b1-189">Umieść kursor nad **grupy** na liście, aby wyświetlić **wyboru**.</span><span class="sxs-lookup"><span data-stu-id="242b1-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="242b1-190">Kliknij pole wyboru obok profilu zdjęcie lub logo, aby dodać użytkownika do grupy **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="242b1-191">**Opcjonalnie:** Jeśli chcesz **dodać więcej niż jedną grupę**, typu w innym **grupy Pełna nazwa** do **wyszukiwanie według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk wyboru, aby dodać tę grupę do **wybrane** listy.</span><span class="sxs-lookup"><span data-stu-id="242b1-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="242b1-192">Po wybraniu grup kliknij przycisk **wybierz** przycisk, aby dodać je do listy użytkowników i grup, które ma być przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="242b1-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="242b1-193">**Opcjonalnie:** kliknij **wybierz rolę** selektora w **Dodaj przydziału** bloku, aby wybrać rolę można przypisać do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="242b1-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="242b1-194">Kliknij przycisk **przypisać** przycisk, aby przypisać aplikację do wybranych grup.</span><span class="sxs-lookup"><span data-stu-id="242b1-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="242b1-195">Po krótkim czasie użytkowników, dla których wybrano mieć możliwość uruchamiania tych aplikacji w panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="242b1-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="242b1-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="242b1-196">Next steps</span></span>
[<span data-ttu-id="242b1-197">Podaj logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="242b1-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
