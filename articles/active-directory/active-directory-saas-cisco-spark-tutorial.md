---
title: 'Samouczek: Integracji Azure Active Directory z Cisco Spark | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: a0a221622afe1c801a331e2319f3a7ace3111dad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="5c9fa-103">Samouczek: Integracji Azure Active Directory z Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="5c9fa-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="5c9fa-104">Z tego samouczka dowiesz się integrowanie Cisco Spark w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c9fa-104">In this tutorial, you learn how to integrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c9fa-105">Integracja z usługą Azure AD Cisco Spark zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-105">Integrating Cisco Spark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c9fa-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="5c9fa-106">You can control in Azure AD who has access to Cisco Spark</span></span>
- <span data-ttu-id="5c9fa-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Cisco Spark (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c9fa-107">You can enable your users to automatically get signed-on to Cisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c9fa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5c9fa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c9fa-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c9fa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c9fa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5c9fa-110">Prerequisites</span></span>

<span data-ttu-id="5c9fa-111">Aby skonfigurować integrację usługi Azure AD z Cisco Spark, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-111">To configure Azure AD integration with Cisco Spark, you need the following items:</span></span>

- <span data-ttu-id="5c9fa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c9fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c9fa-113">Cisco Spark logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5c9fa-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c9fa-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c9fa-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c9fa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c9fa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c9fa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c9fa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5c9fa-118">Scenario description</span></span>
<span data-ttu-id="5c9fa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c9fa-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c9fa-121">Dodawanie Cisco Spark z galerii</span><span class="sxs-lookup"><span data-stu-id="5c9fa-121">Adding Cisco Spark from the gallery</span></span>
2. <span data-ttu-id="5c9fa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5c9fa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-the-gallery"></a><span data-ttu-id="5c9fa-123">Dodawanie Cisco Spark z galerii</span><span class="sxs-lookup"><span data-stu-id="5c9fa-123">Adding Cisco Spark from the gallery</span></span>
<span data-ttu-id="5c9fa-124">Aby skonfigurować integrację Cisco Spark w usłudze Azure Active Directory, należy dodać Cisco Spark z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-124">To configure the integration of Cisco Spark into Azure AD, you need to add Cisco Spark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c9fa-125">**Aby dodać Cisco Spark z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c9fa-125">**To add Cisco Spark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c9fa-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5c9fa-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c9fa-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5c9fa-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5c9fa-133">W polu wyszukiwania wpisz **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-133">In the search box, type **Cisco Spark**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="5c9fa-135">W panelu wyników wybierz **Cisco Spark**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-135">In the results panel, select **Cisco Spark**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c9fa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5c9fa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c9fa-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Cisco Spark oparty na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5c9fa-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c9fa-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Cisco Spark jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cisco Spark is to a user in Azure AD.</span></span> <span data-ttu-id="5c9fa-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w łączniku Spark Cisco.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-140">In other words, a link relationship between an Azure AD user and the related user in Cisco Spark needs to be established.</span></span>

<span data-ttu-id="5c9fa-141">W łączniku Spark Cisco, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-141">In Cisco Spark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c9fa-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Cisco Spark, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-142">To configure and test Azure AD single sign-on with Cisco Spark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c9fa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c9fa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c9fa-145">**[Tworzenie użytkownika testowego Cisco Spark](#creating-a-cisco-spark-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Spark Cisco, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - to have a counterpart of Britta Simon in Cisco Spark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c9fa-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c9fa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c9fa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5c9fa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c9fa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="5c9fa-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Cisco Spark, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c9fa-150">**To configure Azure AD single sign-on with Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="5c9fa-151">W portalu Azure na **Cisco Spark** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-151">In the Azure portal, on the **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5c9fa-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="5c9fa-155">Na **Cisco Spark domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-155">On the **Cisco Spark Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="5c9fa-157">a.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-157">a.</span></span> <span data-ttu-id="5c9fa-158">W **adres URL logowania** tekstowym, wpisz adres URL jako:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="5c9fa-158">In the **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="5c9fa-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-159">b.</span></span> <span data-ttu-id="5c9fa-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5c9fa-160">In the **Identifier** textbox, type a URL using the following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5c9fa-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-161">This value is not real.</span></span> <span data-ttu-id="5c9fa-162">Zaktualizuj tę wartość z rzeczywistego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-162">Update this value with the actual Identifier.</span></span> <span data-ttu-id="5c9fa-163">Skontaktuj się z [zespołem pomocy technicznej klienta Spark Cisco](https://support.ciscospark.com/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) to get this value.</span></span> 
 
4. <span data-ttu-id="5c9fa-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="5c9fa-166">Aplikacji Spark Cisco oczekuje potwierdzenia SAML w celu uwzględnienia określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-166">Cisco Spark application expects the SAML assertions to contain specific attributes.</span></span> <span data-ttu-id="5c9fa-167">Skonfiguruj następujące atrybuty dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-167">Configure the following attributes  for this application.</span></span> <span data-ttu-id="5c9fa-168">Możesz zarządzać wartości tych atrybutów z **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-168">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="5c9fa-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-169">The following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="5c9fa-171">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-171">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="5c9fa-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="5c9fa-172">Attribute Name</span></span>  | <span data-ttu-id="5c9fa-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="5c9fa-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="5c9fa-174">Identyfikator UID</span><span class="sxs-lookup"><span data-stu-id="5c9fa-174">uid</span></span>    | <span data-ttu-id="5c9fa-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5c9fa-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="5c9fa-176">a.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-176">a.</span></span> <span data-ttu-id="5c9fa-177">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-177">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5c9fa-180">b.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-180">b.</span></span> <span data-ttu-id="5c9fa-181">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-181">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5c9fa-182">c.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-182">c.</span></span> <span data-ttu-id="5c9fa-183">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-183">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5c9fa-184">d.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-184">d.</span></span> <span data-ttu-id="5c9fa-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-185">Click **Ok**.</span></span>

7. <span data-ttu-id="5c9fa-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5c9fa-188">Zaloguj się do [zarządzania współpracy chmury Cisco](https://admin.ciscospark.com/) przy użyciu poświadczeń administratora pełnego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-188">Sign in to [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="5c9fa-189">Wybierz **ustawienia** i w obszarze **uwierzytelniania** kliknij **Modyfikuj**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-189">Select **Settings** and under the **Authentication** section, click **Modify**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="5c9fa-191">Wybierz **dostawcy tożsamości firm 3rd integracji. (Zaawansowane)**  i przejdź do następnego ekranu.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go to the next screen.</span></span>

11. <span data-ttu-id="5c9fa-192">Na **Importowanie metadanych Idp** strony albo przeciągania i upuszczania pliku metadanych usługi Azure AD na stronę lub użyj opcji przeglądarki plików do lokalizowania i przekazać plik metadanych usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-192">On the **Import Idp Metadata** page, either drag and drop the Azure AD metadata file onto the page or use the file browser option to locate and upload the Azure AD metadata file.</span></span> <span data-ttu-id="5c9fa-193">Następnie wybierz opcję **wymagają certyfikatu podpisanego przez urząd certyfikacji w metadanych (bardziej bezpieczny)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="5c9fa-195">Wybierz **Test rejestracji Jednokrotnej połączenia**i po otwarciu nowej karty przeglądarki uwierzytelniania za pomocą usługi Azure AD logując się.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="5c9fa-196">Wróć do **zarządzania współpracy chmury Cisco** karty przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-196">Return to the **Cisco Cloud Collaboration Management** browser tab.</span></span> <span data-ttu-id="5c9fa-197">Jeśli test zakończyło się pomyślnie, wybierz **ten test zakończyła się pomyślnie. Włącz opcję logowania jednokrotnego** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-197">If the test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="5c9fa-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5c9fa-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c9fa-199">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c9fa-200">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5c9fa-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c9fa-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c9fa-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c9fa-202">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5c9fa-204">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c9fa-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c9fa-205">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c9fa-207">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c9fa-209">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c9fa-211">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c9fa-213">a.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-213">a.</span></span> <span data-ttu-id="5c9fa-214">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c9fa-215">b.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-215">b.</span></span> <span data-ttu-id="5c9fa-216">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c9fa-217">c.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-217">c.</span></span> <span data-ttu-id="5c9fa-218">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c9fa-219">d.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-219">d.</span></span> <span data-ttu-id="5c9fa-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-220">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="5c9fa-221">Tworzenie użytkownika testowego Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="5c9fa-221">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="5c9fa-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="5c9fa-223">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-223">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="5c9fa-224">Przejdź do [zarządzania współpracy chmury Cisco](https://admin.ciscospark.com/) przy użyciu poświadczeń administratora pełnego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-224">Go to the [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="5c9fa-225">Kliknij przycisk **użytkowników** , a następnie **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-225">Click **Users** and then **Manage Users**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="5c9fa-227">W **zarządzania użytkownika** wybierz **ręcznego dodawania lub modyfikowania użytkowników** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-227">In the **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="5c9fa-228">Wybierz **nazwy i adresu E-mail**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-228">Select **Names and Email address**.</span></span> <span data-ttu-id="5c9fa-229">Następnie należy wypełnić pole tekstowe w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5c9fa-229">Then, fill out the textbox as follows:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="5c9fa-231">a.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-231">a.</span></span> <span data-ttu-id="5c9fa-232">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-232">In the **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="5c9fa-233">b.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-233">b.</span></span> <span data-ttu-id="5c9fa-234">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-234">In the **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="5c9fa-235">c.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-235">c.</span></span> <span data-ttu-id="5c9fa-236">W **adres E-mail** pole tekstowe, typ  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5c9fa-236">In the **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="5c9fa-237">Kliknij znak plus, aby dodać Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-237">Click the plus sign to add Britta Simon.</span></span> <span data-ttu-id="5c9fa-238">Następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-238">Then, click **Next**.</span></span>

6. <span data-ttu-id="5c9fa-239">W **Dodaj usługi dla użytkowników** okna, kliknij przycisk **zapisać** , a następnie **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-239">In the **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c9fa-240">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c9fa-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c9fa-241">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cisco Spark.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5c9fa-243">**Aby przypisać Simona Britta Cisco Spark, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5c9fa-243">**To assign Britta Simon to Cisco Spark, perform the following steps:**</span></span>

1. <span data-ttu-id="5c9fa-244">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5c9fa-246">Na liście aplikacji zaznacz **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-246">In the applications list, select **Cisco Spark**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="5c9fa-248">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5c9fa-250">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-250">Click **Add** button.</span></span> <span data-ttu-id="5c9fa-251">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5c9fa-253">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c9fa-254">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c9fa-255">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c9fa-256">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5c9fa-256">Testing single sign-on</span></span>

<span data-ttu-id="5c9fa-257">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-257">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5c9fa-258">Po kliknięciu kafelka Cisco Spark w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5c9fa-258">When you click the Cisco Spark tile in the Access Panel, you should get automatically signed-on to your Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c9fa-259">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5c9fa-259">Additional resources</span></span>

* [<span data-ttu-id="5c9fa-260">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c9fa-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c9fa-261">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c9fa-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

