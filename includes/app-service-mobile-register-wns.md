
1. W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows hello, a następnie kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepu hello**.

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. W Kreatorze powitania kliknij **dalej**i zaloguj się przy użyciu konta Microsoft. Wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, a następnie kliknij przycisk **rezerwy**.
3. Po rejestracji aplikacji hello jest hello został pomyślnie utworzony, wybierz nową nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**. Spowoduje to dodanie manifest aplikacji toohello informacji o rejestracji Sklepu Windows hello wymagane.
4. Powtórz kroki 1 i 3 dla projektu aplikacji ze Sklepu Windows Phone hello przy użyciu hello samą rejestrację, wcześniej utworzone dla aplikacji ze Sklepu Windows hello.  
5. Przeglądaj toohello [Centrum deweloperów systemu Windows](https://dev.windows.com/en-us/overview)i zaloguj się przy użyciu konta Microsoft. Kliknij przycisk hello nowej rejestracji aplikacji w **Moje aplikacje**, a następnie rozwiń węzeł **usług** > **powiadomienia wypychane**.
6. Na powitania **powiadomienia wypychane** kliknij przycisk **witryna usług Live** w obszarze **Push powiadomienia usługi WNS (Windows) i Microsoft Azure Mobile Apps**. Zanotuj wartości hello hello **identyfikatora SID pakietu** i hello *bieżącego* wartość w **klucz tajny aplikacji**. 

    ![Ustawienie aplikacji w Centrum deweloperów hello](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > klucz tajny aplikacji Hello i identyfikatora SID pakietu są ważnymi poświadczeniami zabezpieczeń. Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją.
   >
   >
