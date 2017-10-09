
Każdy punkt końcowy ma *port publiczny* i *port prywatny*:

* port publiczny Hello jest używany przez toolisten usługi równoważenia obciążenia Azure hello maszyny wirtualnej toohello ruchu przychodzącego z hello Internet.
* port prywatny Hello jest używany przez hello toolisten maszyny wirtualnej dla przychodzącego ruchu, zwykle kierowana tooan aplikacji lub usługa jest uruchomiona na maszynie wirtualnej hello.

Wartości domyślne dla hello protokołu IP i portów TCP lub UDP dla dobrze znanych protokołów sieciowych są udostępniane po utworzeniu punktów końcowych z hello portalu Azure. Niestandardowe punkty końcowe konieczne będzie, toospecify hello poprawne protokołu IP (TCP lub UDP) i hello publicznych i prywatnych portów. ruch przychodzący toodistribute losowo między wieloma maszynami wirtualnymi, będziesz potrzebować toocreate zestaw z równoważeniem obciążenia składające się z wielu punktów końcowych.

Po utworzeniu punktu końcowego, można użyć zasad kontroli dostępu do listę kontroli dostępu (ACL) toodefine które akceptowanie lub odrzucanie hello ruch przychodzący port publiczny toohello hello punktu końcowego na podstawie jego adresu IP źródłowego. Jednak jeśli hello maszyny wirtualnej znajduje się w sieci wirtualnej platformy Azure, należy zamiast tego użyć grup zabezpieczeń sieci. Aby uzyskać więcej informacji, zobacz [dotyczące grup zabezpieczeń sieci](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> Konfiguracja zapory dla maszyn wirtualnych platformy Azure odbywa się automatycznie dla portów skojarzonych z punktami końcowymi połączenia zdalnego, które Azure konfiguruje się automatycznie. Porty określone dla innych punktów końcowych konfiguracja nie odbywa się automatycznie zapory toohello hello maszyny wirtualnej. Po utworzeniu punktu końcowego dla maszyny wirtualnej hello należy tooensure, który hello zapory hello maszyny wirtualnej umożliwia również hello ruchu protokołu hello i konfiguracji punktu końcowego toohello odpowiedni port prywatny. tooconfigure hello zapory można znaleźć w dokumentacji hello lub Pomoc online dla hello systemu operacyjnego na maszynie wirtualnej hello.
>
>

## <a name="create-an-endpoint"></a>Tworzenie punktu końcowego
1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **maszyn wirtualnych**, a następnie kliknij nazwę hello hello maszyny wirtualnej, które mają tooconfigure.
3. Kliknij przycisk **punkty końcowe** w hello **ustawienia** grupy. Witaj **punkty końcowe** strona zawiera listę wszystkich hello bieżące punkty końcowe hello maszyny wirtualnej. (W tym przykładzie jest Maszynę wirtualną systemu Windows. Linux VM domyślnie wyświetli punkt końcowy SSH.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Punkty końcowe](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Na pasku poleceń hello powyżej hello wpisy punktów końcowych, kliknij przycisk **Dodaj**.
5. Na powitania **dodać punkt końcowy** wpisz nazwę dla punktu końcowego hello w **nazwa**.
6. W **protokołu**, albo wybierz **TCP** lub **UDP**.
7. W **Port publiczny**, wpisz numer portu hello hello ruch przychodzący z hello Internet. W **Port prywatny**, wpisz numer portu hello, na które hello nasłuchuje maszyny wirtualnej. Numery portów mogą być różne. Upewnij się, że hello zapora na maszynie wirtualnej hello została skonfigurowana tooallow hello ruchu odpowiedniego toohello protokołu (w kroku 6) i port prywatny.
10. Kliknij przycisk **OK**.

nowy punkt końcowy Hello zostaną wyświetlone na powitania **punkty końcowe** strony.

![Pomyślne utworzenie punktu końcowego](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Zarządzanie hello listy ACL punktu końcowego
toodefine hello zestaw komputerów, które mogą przesyłać, hello listy ACL punktu końcowego można ograniczyć ruch ustalane na podstawie źródłowego adresu IP. Wykonaj te kroki tooadd, zmodyfikować lub usunąć listy ACL punktu końcowego.

> [!NOTE]
> Jeśli hello punkt końcowy jest częścią zestawu o zrównoważonym obciążeniu, wszystkie wprowadzone zmiany listy ACL punktu końcowego są toohello tooall zastosowanych punktów końcowych w zestawie hello.
>
>

Jeśli hello maszyny wirtualnej znajduje się w sieci wirtualnej platformy Azure, zalecamy sieciowe grupy zabezpieczeń zamiast listy kontroli dostępu. Aby uzyskać więcej informacji, zobacz [dotyczące grup zabezpieczeń sieci](../articles/virtual-network/virtual-networks-nsg.md).

1. Jeśli jeszcze tego nie zrobiono, zaloguj się toohello portalu Azure.
2. Kliknij przycisk **maszyn wirtualnych**, a następnie kliknij nazwę hello hello maszyny wirtualnej, które mają tooconfigure.
3. Kliknij przycisk **Punkty końcowe**. Z listy hello wybierz odpowiednie punktu końcowego hello. listy ACL Hello jest u dołu hello hello strony.

   ![Określ szczegóły list kontroli dostępu](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Użyj wierszy w tooadd listy hello, usuń lub Edytuj reguły dla listy ACL i ich kolejność. Witaj **podsieci zdalnej** wartość jest zakres adresów IP dla ruchu przychodzącego z hello Internet hello toopermit używa modułu równoważenia obciążenia Azure lub odrzucające hello ruchu na podstawie jego adresu IP źródłowego. Należy się toospecify hello zakres adresów IP w formacie CIDR, znanej także jako formacie prefiksu adresu. Na przykład `10.1.0.0/8`.

 ![Nowy wpis listy kontroli dostępu](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Można użyć tylko ruch tooallow reguły z określonych komputerów odpowiadającego tooyour komputerów na ruch do Internetu lub toodeny hello z zakresów adresów określone, znane.

Witaj reguły są sprawdzane w kolejności, zaczynając od pierwszej reguły hello i kończąc hello ostatnia reguła. Oznacza to, że reguły powinna być wyświetlana z najmniej restrykcyjny toomost restrykcyjne. Aby uzyskać więcej informacji, zobacz [co to jest lista kontroli dostępu do sieci](../articles/virtual-network/virtual-networks-acl.md).
