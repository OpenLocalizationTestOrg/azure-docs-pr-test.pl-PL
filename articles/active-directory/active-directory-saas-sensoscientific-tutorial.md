---
title: 'Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między SensoScientific bezprzewodowej temperatury monitorowania systemu i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: fa6242cf7f9559ca394ffde2e5e734cb935b03dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="2f788-103">Samouczek: Integracji Azure Active Directory z SensoScientific bezprzewodowej temperatury monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="2f788-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="2f788-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-104">In this tutorial, you learn how to integrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f788-105">Integrowanie SensoScientific bezprzewodowej temperatury monitorowania systemu z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2f788-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f788-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do monitorowania systemu SensoScientific bezprzewodowej temperatury</span><span class="sxs-lookup"><span data-stu-id="2f788-106">You can control in Azure AD who has access to SensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="2f788-107">Umożliwia użytkownikom automatycznie pobrać zalogowane SensoScientific bezprzewodowej temperatury monitorowania systemu (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f788-107">You can enable your users to automatically get signed-on to SensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f788-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2f788-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f788-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f788-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f788-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f788-110">Prerequisites</span></span>

<span data-ttu-id="2f788-111">Aby skonfigurować integrację usługi Azure AD z SensoScientific bezprzewodowej temperatury monitorowania systemu, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2f788-111">To configure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need the following items:</span></span>

- <span data-ttu-id="2f788-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f788-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f788-113">SensoScientific bezprzewodowej temperatury monitorowania systemu jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2f788-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f788-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2f788-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f788-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2f788-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f788-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2f788-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f788-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f788-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f788-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2f788-118">Scenario description</span></span>
<span data-ttu-id="2f788-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2f788-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f788-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2f788-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f788-121">Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii</span><span class="sxs-lookup"><span data-stu-id="2f788-121">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
2. <span data-ttu-id="2f788-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2f788-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-the-gallery"></a><span data-ttu-id="2f788-123">Dodawanie SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii</span><span class="sxs-lookup"><span data-stu-id="2f788-123">Adding SensoScientific Wireless Temperature Monitoring System from the gallery</span></span>
<span data-ttu-id="2f788-124">Aby skonfigurować integrację usługi Azure AD SensoScientific bezprzewodowej temperatury monitorowania systemu, należy dodać SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2f788-124">To configure the integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need to add SensoScientific Wireless Temperature Monitoring System from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f788-125">**Aby dodać SensoScientific bezprzewodowej temperatury monitorowania systemu z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2f788-125">**To add SensoScientific Wireless Temperature Monitoring System from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f788-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2f788-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2f788-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2f788-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f788-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2f788-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2f788-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2f788-133">W polu wyszukiwania wpisz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.</span><span class="sxs-lookup"><span data-stu-id="2f788-133">In the search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="2f788-135">W panelu wyników wybierz **SensoScientific bezprzewodowej temperatury monitorowania systemu**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2f788-135">In the results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2f788-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2f788-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2f788-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej SensoScientific bezprzewodowej temperatury monitorowania systemu, na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2f788-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2f788-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem SensoScientific bezprzewodowej temperatury monitorowania systemu jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f788-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SensoScientific Wireless Temperature Monitoring System is to a user in Azure AD.</span></span> <span data-ttu-id="2f788-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-140">In other words, a link relationship between an Azure AD user and the related user in SensoScientific Wireless Temperature Monitoring System needs to be established.</span></span>

<span data-ttu-id="2f788-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="2f788-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2f788-142">To configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f788-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2f788-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f788-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2f788-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f788-145">**[Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SensoScientific bezprzewodowej temperatury monitorowania systemu, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2f788-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - to have a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f788-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2f788-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f788-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2f788-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2f788-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2f788-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2f788-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="2f788-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SensoScientific bezprzewodowej temperatury monitorowania systemu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2f788-150">**To configure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="2f788-151">W portalu Azure na **SensoScientific bezprzewodowej temperatury monitorowania systemu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2f788-151">In the Azure portal, on the **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2f788-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="2f788-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="2f788-155">Na **adresy URL i monitorowania domeny systemu SensoScientific bezprzewodowej temperatury** sekcji, nie trzeba wykonywać żadnych czynności jako aplikacja jest już wstępnie zintegrowanych z platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2f788-155">On the **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need to perform any steps as the app is already pre-integrated with Azure:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="2f788-157">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2f788-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="2f788-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2f788-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f788-161">Na **monitorowania konfiguracji systemu SensoScientific bezprzewodowej temperatury** kliknij **Konfiguruj SensoScientific bezprzewodowej temperatury monitorowania System** otworzyć **Konfiguruj Zaloguj się na** okna.</span><span class="sxs-lookup"><span data-stu-id="2f788-161">On the **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f788-162">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML** i **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2f788-162">Copy the **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="2f788-164">Zaloguj się do aplikacji SensoScientific bezprzewodowej temperatury monitorowania systemu jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2f788-164">Sign on to your SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="2f788-165">W menu nawigacji u góry kliknij **konfiguracji** i przejdź do **Konfiguruj** w obszarze **rejestracji jednokrotnej** otworzyć pojedynczy znak na ustawienia.</span><span class="sxs-lookup"><span data-stu-id="2f788-165">In the navigation menu on the top, click **Configuration** and goto **Configure** under **Single Sign On** to open the Single Sign On Settings.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="2f788-167">W **pojedynczy znak na ustawienia** formularza należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f788-167">In **Single Sign On Settings** form perform the following steps:</span></span>
 
    <span data-ttu-id="2f788-168">a.</span><span class="sxs-lookup"><span data-stu-id="2f788-168">a.</span></span> <span data-ttu-id="2f788-169">Wybierz **Nazwa wystawcy** jako usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f788-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="2f788-170">b.</span><span class="sxs-lookup"><span data-stu-id="2f788-170">b.</span></span> <span data-ttu-id="2f788-171">Wklej **identyfikator jednostki SAML** którego została skopiowana z portalu Azure w tekstowym adres URL wystawcy.</span><span class="sxs-lookup"><span data-stu-id="2f788-171">Paste the **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="2f788-172">c.</span><span class="sxs-lookup"><span data-stu-id="2f788-172">c.</span></span> <span data-ttu-id="2f788-173">Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure w pole tekstowe pojedynczy znak na adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="2f788-173">Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="2f788-174">d.</span><span class="sxs-lookup"><span data-stu-id="2f788-174">d.</span></span> <span data-ttu-id="2f788-175">Wklej **Sign-Out URL** którego została skopiowana z portalu Azure do pojedynczego adresu URL usługi Sign-Out pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-175">Paste the **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="2f788-176">e.</span><span class="sxs-lookup"><span data-stu-id="2f788-176">e.</span></span> <span data-ttu-id="2f788-177">Przeglądaj certyfikatu, który został pobrany z portalu Azure i przekaż go tutaj.</span><span class="sxs-lookup"><span data-stu-id="2f788-177">Browse the certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="2f788-178">f.</span><span class="sxs-lookup"><span data-stu-id="2f788-178">f.</span></span> <span data-ttu-id="2f788-179">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="2f788-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="2f788-180">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="2f788-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f788-181">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="2f788-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f788-182">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f788-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2f788-183">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f788-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="2f788-184">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2f788-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2f788-186">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2f788-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f788-187">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2f788-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f788-189">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2f788-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f788-191">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f788-193">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2f788-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f788-195">a.</span><span class="sxs-lookup"><span data-stu-id="2f788-195">a.</span></span> <span data-ttu-id="2f788-196">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f788-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f788-197">b.</span><span class="sxs-lookup"><span data-stu-id="2f788-197">b.</span></span> <span data-ttu-id="2f788-198">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2f788-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f788-199">c.</span><span class="sxs-lookup"><span data-stu-id="2f788-199">c.</span></span> <span data-ttu-id="2f788-200">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2f788-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f788-201">d.</span><span class="sxs-lookup"><span data-stu-id="2f788-201">d.</span></span> <span data-ttu-id="2f788-202">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2f788-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="2f788-203">Tworzenie użytkownika testowego SensoScientific bezprzewodowej temperatury monitorowania systemu</span><span class="sxs-lookup"><span data-stu-id="2f788-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="2f788-204">Aby umożliwić użytkownikom usługi Azure AD zalogować się do SensoScientific bezprzewodowej temperatury monitorowania systemu, muszą mieć przydzielone do SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-204">To enable Azure AD users to log in to SensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="2f788-205">Praca z [zespołem pomocy technicznej SensoScientific bezprzewodowej temperatury monitorowania systemu](https://www.sensoscientific.com/contact-us/) Aby dodać użytkowników na platformie SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add the users in the SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="2f788-206">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2f788-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2f788-207">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f788-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2f788-208">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do monitorowania systemu SensoScientific bezprzewodowej temperatury.</span><span class="sxs-lookup"><span data-stu-id="2f788-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SensoScientific Wireless Temperature Monitoring System.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2f788-210">**Aby przypisać Simona Britta SensoScientific bezprzewodowej temperatury monitorowania systemu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2f788-210">**To assign Britta Simon to SensoScientific Wireless Temperature Monitoring System, perform the following steps:**</span></span>

1. <span data-ttu-id="2f788-211">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2f788-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2f788-213">Na liście aplikacji zaznacz **SensoScientific bezprzewodowej temperatury monitorowania systemu**.</span><span class="sxs-lookup"><span data-stu-id="2f788-213">In the applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="2f788-215">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2f788-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2f788-217">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2f788-217">Click **Add** button.</span></span> <span data-ttu-id="2f788-218">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2f788-220">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2f788-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f788-221">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f788-222">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2f788-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2f788-223">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2f788-223">Testing single sign-on</span></span>

<span data-ttu-id="2f788-224">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2f788-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> <span data-ttu-id="2f788-225">Kliknij Kafelek SensoScientific bezprzewodowej temperatury monitorowania System w panelu dostępu, użytkownik będzie można automatycznie zalogowane do aplikacji SensoScientific bezprzewodowej temperatury monitorowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2f788-225">Click the SensoScientific Wireless Temperature Monitoring System tile in the Access Panel, you will be automatically signed-on to your SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="2f788-226">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="2f788-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f788-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2f788-227">Additional resources</span></span>

* [<span data-ttu-id="2f788-228">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f788-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f788-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2f788-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

