# 00 - Install VMs


1. Installed Windows Server 2022 as a Virtual machine in VMWare workstaion pro
2. Installed Windows 11 pro as a Virtual machine in VMWare workstaion pro
    - Had to modify the registry utilizing regedit before installation:
        - `SHIFT` + `F10` to access cmd. pre `install now`
        - Type **regedit** and press **Enter**
        - Navigate to **HKEY_LOCAL_MACHINE \ SYSTEM \ Setup** to create a new key called **LabConfig**
        - Under the **LabConfig** key. Create 3 new **DWORD (32-bit) value** with the following names:
            - **BypassTPMCheck** (Value = 1)
            - **BypassRAMCheck** (Value = 1)
            - **BypassSecureBootCheck** (Value = 1)
        - close regedit and begin install