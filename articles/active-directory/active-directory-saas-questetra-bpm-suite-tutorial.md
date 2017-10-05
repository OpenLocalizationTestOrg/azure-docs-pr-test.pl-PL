---
title: 'Samouczek: Azure Active Directory integracji z pakietem BPM Questetra | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="a19ec-103">Samouczek: Azure Active Directory integracji z pakietem BPM Questetra</span><span class="sxs-lookup"><span data-stu-id="a19ec-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="a19ec-104">Celem tego samouczka jest pokazanie sposobu integracji Questetra BPM pakietu z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a19ec-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="a19ec-105">Integracja z usługą Azure AD Questetra BPM Suite zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a19ec-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="a19ec-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zestawu BPM Questetra</span><span class="sxs-lookup"><span data-stu-id="a19ec-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="a19ec-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Questetra BPM pakietu (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a19ec-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a19ec-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a19ec-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="a19ec-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a19ec-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a19ec-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a19ec-110">Prerequisites</span></span>
<span data-ttu-id="a19ec-111">Aby skonfigurować integrację usługi Azure AD z pakietem BPM Questetra, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a19ec-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="a19ec-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a19ec-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a19ec-113">[Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a19ec-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a19ec-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a19ec-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a19ec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a19ec-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a19ec-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a19ec-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a19ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="a19ec-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a19ec-118">Scenario Description</span></span>
<span data-ttu-id="a19ec-119">Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a19ec-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="a19ec-120">Scenariusz opisany w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="a19ec-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="a19ec-121">Dodawanie pakietu BPM Questetra z galerii</span><span class="sxs-lookup"><span data-stu-id="a19ec-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="a19ec-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a19ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="a19ec-123">Dodawanie pakietu BPM Questetra z galerii</span><span class="sxs-lookup"><span data-stu-id="a19ec-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="a19ec-124">Aby skonfigurować integrację usługi Azure AD Questetra BPM pakietu, należy dodać pakiet BPM Questetra z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a19ec-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a19ec-125">**Aby dodać pakiet BPM Questetra z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a19ec-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a19ec-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="a19ec-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a19ec-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="a19ec-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="a19ec-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="a19ec-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="a19ec-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="a19ec-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="a19ec-135">W polu wyszukiwania wpisz **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="a19ec-137">W okienku wyników wybierz **Questetra BPM Suite**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a19ec-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a19ec-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a19ec-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a19ec-139">Jest celem tej sekcji opisano, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a19ec-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi pakietu BPM Questetra użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a19ec-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="a19ec-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi pakietu BPM Questetra musi określone.</span><span class="sxs-lookup"><span data-stu-id="a19ec-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="a19ec-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** Questetra BPM pakietu.</span><span class="sxs-lookup"><span data-stu-id="a19ec-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="a19ec-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a19ec-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a19ec-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a19ec-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a19ec-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a19ec-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a19ec-146">**[Tworzenie użytkownika testowego zestawu BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Questetra BPM pakiet, który jest połączony z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a19ec-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a19ec-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a19ec-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a19ec-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a19ec-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a19ec-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a19ec-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="a19ec-150">Celem tej sekcji jest można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu Azure i skonfigurować logowanie jednokrotne w Questetra BPM pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a19ec-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="a19ec-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a19ec-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="a19ec-152">W klasycznym portalu Azure na **Questetra BPM Suite** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. <span data-ttu-id="a19ec-154">Na **jak chcesz użytkownikom zalogować się do zestawu BPM Questetra** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]

3. <span data-ttu-id="a19ec-156">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Questetra BPM Suite** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a19ec-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="a19ec-157">W menu u góry kliknij **ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][10]

5. <span data-ttu-id="a19ec-159">Aby otworzyć **SingleSignOnSAML** kliknij przycisk **logowania jednokrotnego (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][11]

6. <span data-ttu-id="a19ec-161">W klasycznym portalu Azure na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][13]
   
    <span data-ttu-id="a19ec-163">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-163">a.</span></span> <span data-ttu-id="a19ec-164">W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP kopii **adres URL usługi ACS**i wklej go do **na adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="a19ec-165">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-165">b.</span></span> <span data-ttu-id="a19ec-166">W przypadku **Questetra BPM pakiet** witryna firmy, w sekcji informacji SP kopii **identyfikator jednostki**, a następnie wklej go do **adres URL wystawcy** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="a19ec-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="a19ec-167">c.</span><span class="sxs-lookup"><span data-stu-id="a19ec-167">c.</span></span> <span data-ttu-id="a19ec-168">W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP kopii **adres URL usługi ACS**i wklej go do **adres URL odpowiedzi służący** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="a19ec-169">d.</span><span class="sxs-lookup"><span data-stu-id="a19ec-169">d.</span></span> <span data-ttu-id="a19ec-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-170">Click **Next**.</span></span>

7. <span data-ttu-id="a19ec-171">Na **skonfigurować logowanie jednokrotne w pakiet BPM Questetra** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a19ec-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

8. <span data-ttu-id="a19ec-173">W przypadku **Questetra BPM Suite** firmy, witryny, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][15]
   
    <span data-ttu-id="a19ec-175">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-175">a.</span></span> <span data-ttu-id="a19ec-176">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="a19ec-177">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-177">b.</span></span> <span data-ttu-id="a19ec-178">W klasycznym portalu Azure, skopiuj **adres URL wystawcy** wartość, a następnie wklej ją do **identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="a19ec-179">c.</span><span class="sxs-lookup"><span data-stu-id="a19ec-179">c.</span></span> <span data-ttu-id="a19ec-180">W klasycznym portalu Azure, skopiuj **pojedynczy znak na adres URL usługi** wartość, a następnie wklej ją do **adres URL logowania strony** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="a19ec-181">d.</span><span class="sxs-lookup"><span data-stu-id="a19ec-181">d.</span></span> <span data-ttu-id="a19ec-182">W klasycznym portalu Azure, skopiuj **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej ją do **adres URL strony wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="a19ec-183">e.</span><span class="sxs-lookup"><span data-stu-id="a19ec-183">e.</span></span> <span data-ttu-id="a19ec-184">W **NameID format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="a19ec-185">f.</span><span class="sxs-lookup"><span data-stu-id="a19ec-185">f.</span></span> <span data-ttu-id="a19ec-186">Utwórz plik zakodowany base-64 z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a19ec-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="a19ec-187">Aby uzyskać więcej informacji, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a19ec-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="a19ec-188">g.</span><span class="sxs-lookup"><span data-stu-id="a19ec-188">g.</span></span> <span data-ttu-id="a19ec-189">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu weryfikacji** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a19ec-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="a19ec-190">h.</span><span class="sxs-lookup"><span data-stu-id="a19ec-190">h.</span></span> <span data-ttu-id="a19ec-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-191">Click **Save**.</span></span>

1. <span data-ttu-id="a19ec-192">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Co to jest program Azure AD Connect][17]

2. <span data-ttu-id="a19ec-194">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Co to jest program Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a19ec-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a19ec-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a19ec-197">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a19ec-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="a19ec-198">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a19ec-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a19ec-199">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][100] 

2. <span data-ttu-id="a19ec-201">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a19ec-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="a19ec-202">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][101] 

4. <span data-ttu-id="a19ec-204">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][102] 

5. <span data-ttu-id="a19ec-206">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][103]
   
    <span data-ttu-id="a19ec-208">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-208">a.</span></span> <span data-ttu-id="a19ec-209">Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="a19ec-210">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-210">b.</span></span> <span data-ttu-id="a19ec-211">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a19ec-212">c.</span><span class="sxs-lookup"><span data-stu-id="a19ec-212">c.</span></span> <span data-ttu-id="a19ec-213">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="a19ec-213">Click Next.</span></span>

6. <span data-ttu-id="a19ec-214">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][104] 
   
    <span data-ttu-id="a19ec-216">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-216">a.</span></span> <span data-ttu-id="a19ec-217">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="a19ec-218">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-218">b.</span></span> <span data-ttu-id="a19ec-219">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="a19ec-220">c.</span><span class="sxs-lookup"><span data-stu-id="a19ec-220">c.</span></span> <span data-ttu-id="a19ec-221">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="a19ec-222">d.</span><span class="sxs-lookup"><span data-stu-id="a19ec-222">d.</span></span> <span data-ttu-id="a19ec-223">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="a19ec-224">e.</span><span class="sxs-lookup"><span data-stu-id="a19ec-224">e.</span></span> <span data-ttu-id="a19ec-225">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-225">Click **Next**.</span></span>

7. <span data-ttu-id="a19ec-226">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][105]  

8. <span data-ttu-id="a19ec-228">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][106]   
   
    <span data-ttu-id="a19ec-230">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-230">a.</span></span> <span data-ttu-id="a19ec-231">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="a19ec-232">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-232">b.</span></span> <span data-ttu-id="a19ec-233">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="a19ec-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="a19ec-234">Tworzenie użytkownika testowego Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="a19ec-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="a19ec-235">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta Questetra BPM pakietu.</span><span class="sxs-lookup"><span data-stu-id="a19ec-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="a19ec-236">**Aby utworzyć użytkownika o nazwie Simona Britta pakietu BPM Questetra, wykonaj następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a19ec-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="a19ec-237">Logowanie do witryny firmy Questetra BPM Suite jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a19ec-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="a19ec-238">Przejdź do **ustawienia systemu > listy użytkowników > Nowy użytkownik**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="a19ec-239">W oknie dialogowym Nowy użytkownik wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a19ec-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego][300] 
   
    <span data-ttu-id="a19ec-241">a.</span><span class="sxs-lookup"><span data-stu-id="a19ec-241">a.</span></span> <span data-ttu-id="a19ec-242">W **nazwa** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a19ec-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a19ec-243">b.</span><span class="sxs-lookup"><span data-stu-id="a19ec-243">b.</span></span> <span data-ttu-id="a19ec-244">W **E-mail** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a19ec-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a19ec-245">c.</span><span class="sxs-lookup"><span data-stu-id="a19ec-245">c.</span></span> <span data-ttu-id="a19ec-246">W **hasło** tekstowym, wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="a19ec-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="a19ec-247">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a19ec-248">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a19ec-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="a19ec-249">Celem tej sekcji jest włączenie Simona Britta na udostępnienie jej do zestawu BPM Questetra za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a19ec-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Co to jest program Azure AD Connect][200]

<span data-ttu-id="a19ec-251">**Aby przypisać Simona Britta Questetra BPM pakietu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a19ec-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="a19ec-252">W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="a19ec-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Co to jest program Azure AD Connect][201]
2. <span data-ttu-id="a19ec-254">Na liście aplikacji zaznacz **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Co to jest program Azure AD Connect][205]
3. <span data-ttu-id="a19ec-256">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-256">In the menu on the top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][202]
4. <span data-ttu-id="a19ec-258">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Co to jest program Azure AD Connect][203]
5. <span data-ttu-id="a19ec-260">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="a19ec-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Co to jest program Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a19ec-262">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a19ec-262">Testing Single Sign-On</span></span>
<span data-ttu-id="a19ec-263">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a19ec-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a19ec-264">Po kliknięciu kafelka Questetra BPM Suite w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane Questetra BPM pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a19ec-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a19ec-265">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a19ec-265">Additional Resources</span></span>
* [<span data-ttu-id="a19ec-266">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a19ec-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a19ec-267">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a19ec-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
