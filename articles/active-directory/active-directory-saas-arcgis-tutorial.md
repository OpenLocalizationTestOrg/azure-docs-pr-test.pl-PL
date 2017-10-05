---
title: "Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ArcGIS Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="88204-103">Samouczek: Integracja usługi Azure Active Directory z usługą ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="88204-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="88204-104">Z tego samouczka dowiesz się integrowanie ArcGIS Online z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="88204-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="88204-105">Integrowanie ArcGIS Online z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="88204-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="88204-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="88204-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="88204-107">Umożliwia użytkownikom automatycznie pobrać zalogowane ArcGIS online (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88204-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="88204-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="88204-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="88204-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="88204-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="88204-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88204-110">Prerequisites</span></span>

<span data-ttu-id="88204-111">Aby skonfigurować integrację usługi Azure AD z ArcGIS Online, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="88204-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="88204-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88204-112">An Azure AD subscription</span></span>
- <span data-ttu-id="88204-113">ArcGIS Online jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="88204-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="88204-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="88204-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="88204-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="88204-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="88204-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="88204-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="88204-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88204-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="88204-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="88204-118">Scenario description</span></span>
<span data-ttu-id="88204-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="88204-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="88204-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="88204-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="88204-121">Dodawanie ArcGIS Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="88204-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="88204-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="88204-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="88204-123">Dodawanie ArcGIS Online z poziomu galerii</span><span class="sxs-lookup"><span data-stu-id="88204-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="88204-124">Aby skonfigurować integrację ArcGIS online z usługą Azure AD, należy dodać do listy zarządzanych aplikacji SaaS ArcGIS Online z poziomu galerii.</span><span class="sxs-lookup"><span data-stu-id="88204-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="88204-125">**Aby dodać ArcGIS Online z poziomu galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="88204-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="88204-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="88204-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="88204-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="88204-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="88204-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="88204-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="88204-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego, aby dodać nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="88204-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="88204-133">W polu wyszukiwania wpisz **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="88204-133">In the search box, type **ArcGIS Online**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="88204-135">W panelu wyników wybierz **ArcGIS Online**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="88204-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="88204-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="88204-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="88204-138">W tej sekcji można skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ArcGIS Online na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="88204-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="88204-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ArcGIS w trybie Online jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="88204-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="88204-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w trybie Online ArcGIS musi określone.</span><span class="sxs-lookup"><span data-stu-id="88204-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="88204-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w ArcGIS w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="88204-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="88204-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ArcGIS Online, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="88204-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="88204-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="88204-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="88204-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="88204-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="88204-145">**[Tworzenie użytkownika testowego ArcGIS Online](#creating-an-arcgis-online-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ArcGIS Online, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88204-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="88204-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="88204-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="88204-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="88204-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="88204-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="88204-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="88204-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w trybie Online ArcGIS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="88204-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="88204-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ArcGIS Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="88204-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="88204-151">W portalu Azure na **ArcGIS Online** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="88204-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="88204-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="88204-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="88204-155">Na **ArcGIS Online domeny i adres URL** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="88204-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="88204-157">W **adres URL logowania** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="88204-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="88204-158">Ta wartość nie jest rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="88204-158">This value is not the real.</span></span> <span data-ttu-id="88204-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="88204-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="88204-160">Skontaktuj się z [zespołem pomocy technicznej Online klienta ArcGIS](http://support.esri.com/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="88204-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="88204-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="88204-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="88204-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88204-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="88204-165">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ArcGIS jako administrator.</span><span class="sxs-lookup"><span data-stu-id="88204-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="88204-166">Kliknij przycisk **Edytuj ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="88204-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="88204-167">![Edytuj ustawienia](./media/active-directory-saas-arcgis-tutorial/ic784742.png "edytować ustawienia")</span><span class="sxs-lookup"><span data-stu-id="88204-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="88204-168">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="88204-168">Click **Security**.</span></span>

    <span data-ttu-id="88204-169">![Zabezpieczenia](./media/active-directory-saas-arcgis-tutorial/ic784743.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="88204-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="88204-170">W obszarze **logowania do organizacji**, kliknij przycisk **USTAWIĆ dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="88204-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="88204-171">![Logowania do organizacji](./media/active-directory-saas-arcgis-tutorial/ic784744.png "logowania do organizacji")</span><span class="sxs-lookup"><span data-stu-id="88204-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="88204-172">Na **ustawić dostawcy tożsamości** konfiguracji wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="88204-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="88204-173">![Ustawienie dostawcy tożsamości](./media/active-directory-saas-arcgis-tutorial/ic784745.png "ustawienie dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="88204-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="88204-174">a.</span><span class="sxs-lookup"><span data-stu-id="88204-174">a.</span></span> <span data-ttu-id="88204-175">W **nazwa** tekstowym, wpisz nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="88204-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="88204-176">b.</span><span class="sxs-lookup"><span data-stu-id="88204-176">b.</span></span> <span data-ttu-id="88204-177">Aby uzyskać **metadanych dla dostawcy tożsamości organizacji dostarczane za pomocą**, wybierz pozycję **plik**.</span><span class="sxs-lookup"><span data-stu-id="88204-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="88204-178">c.</span><span class="sxs-lookup"><span data-stu-id="88204-178">c.</span></span> <span data-ttu-id="88204-179">Aby przekazać plik metadanych pobranych, kliknij przycisk **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="88204-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="88204-180">d.</span><span class="sxs-lookup"><span data-stu-id="88204-180">d.</span></span> <span data-ttu-id="88204-181">Kliknij przycisk **dostawcy tożsamości zestawu**.</span><span class="sxs-lookup"><span data-stu-id="88204-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="88204-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="88204-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="88204-183">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="88204-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="88204-184">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="88204-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="88204-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88204-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="88204-186">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="88204-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="88204-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="88204-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="88204-189">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="88204-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="88204-191">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="88204-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="88204-193">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88204-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="88204-195">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="88204-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="88204-197">a.</span><span class="sxs-lookup"><span data-stu-id="88204-197">a.</span></span> <span data-ttu-id="88204-198">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="88204-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="88204-199">b.</span><span class="sxs-lookup"><span data-stu-id="88204-199">b.</span></span> <span data-ttu-id="88204-200">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="88204-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="88204-201">c.</span><span class="sxs-lookup"><span data-stu-id="88204-201">c.</span></span> <span data-ttu-id="88204-202">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="88204-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="88204-203">d.</span><span class="sxs-lookup"><span data-stu-id="88204-203">d.</span></span> <span data-ttu-id="88204-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="88204-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="88204-205">Tworzenie użytkownika testowego ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="88204-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="88204-206">Aby włączyć użytkowników usługi Azure AD zalogować się do ArcGIS Online, muszą mieć przydzielone do ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="88204-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="88204-207">W przypadku ArcGIS Online Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="88204-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="88204-208">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="88204-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="88204-209">Zaloguj się do Twojego **ArcGIS** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="88204-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="88204-210">Kliknij przycisk **członków zaproszenia**.</span><span class="sxs-lookup"><span data-stu-id="88204-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="88204-211">![Zaprosić](./media/active-directory-saas-arcgis-tutorial/ic784747.png "zaprosić")</span><span class="sxs-lookup"><span data-stu-id="88204-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="88204-212">Wybierz **automatycznie dodawać członków bez wysyłania wiadomości e-mail**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="88204-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="88204-213">![Automatyczne dodawanie członków](./media/active-directory-saas-arcgis-tutorial/ic784748.png "automatycznie dodawać członków")</span><span class="sxs-lookup"><span data-stu-id="88204-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="88204-214">Na **członków** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="88204-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="88204-215">![Dodaj i przejrzyj](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Dodaj i przejrzyj")</span><span class="sxs-lookup"><span data-stu-id="88204-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="88204-216">a.</span><span class="sxs-lookup"><span data-stu-id="88204-216">a.</span></span> <span data-ttu-id="88204-217">Wprowadź **E-mail**, **imię**, i **nazwisko** chcesz udostępnić poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="88204-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="88204-218">b.</span><span class="sxs-lookup"><span data-stu-id="88204-218">b.</span></span> <span data-ttu-id="88204-219">Kliknij przycisk **Dodaj i przejrzyj**.</span><span class="sxs-lookup"><span data-stu-id="88204-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="88204-220">Przejrzyj dane zostały wprowadzone, a następnie kliknij przycisk **Dodaj członków**.</span><span class="sxs-lookup"><span data-stu-id="88204-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="88204-221">![Dodaj element członkowski](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Dodaj element członkowski")</span><span class="sxs-lookup"><span data-stu-id="88204-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="88204-222">Właścicielem konta usługi Azure Active Directory otrzymasz wiadomość e-mail, a następnie kliknij łącze, aby potwierdzić swoje konto, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="88204-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="88204-223">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="88204-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="88204-224">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="88204-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="88204-226">**Aby przypisać Simona Britta ArcGIS Online, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="88204-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="88204-227">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="88204-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="88204-229">Na liście aplikacji zaznacz **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="88204-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="88204-231">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="88204-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="88204-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="88204-233">Click **Add** button.</span></span> <span data-ttu-id="88204-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88204-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="88204-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="88204-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="88204-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88204-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="88204-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="88204-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="88204-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="88204-239">Testing single sign-on</span></span>

<span data-ttu-id="88204-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="88204-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="88204-241">Po kliknięciu kafelka ArcGIS Online w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji ArcGIS w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="88204-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="88204-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="88204-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="88204-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="88204-243">Additional resources</span></span>

* [<span data-ttu-id="88204-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88204-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="88204-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="88204-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

