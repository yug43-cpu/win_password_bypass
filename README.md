# Documentation: Windows Local Password Reset Bypass (Utilman Method)

## Overview
This document outlines a local privilege escalation technique used to bypass the Windows lock screen and reset a local user account password. This method works by replacing the Windows Accessibility feature executable (`Utilman.exe`) with the Command Prompt (`cmd.exe`) via the Windows Recovery Environment (WinRE). 

*Note: This technique requires physical access to the device and relies on the system drive being unencrypted (e.g., no BitLocker enabled).*

---

## Execution Procedure

### Phase 1: Accessing the Recovery Environment
1. **Trigger Advanced Startup:** On the Windows lock screen, press and hold the **Left Shift** key. While holding it, click the Power icon and select **Restart**.
2. **Open Command Prompt:** Once the Advanced Startup menu loads, navigate to `Troubleshoot` > `Advanced options` > `Command Prompt`.

### Phase 2: Swapping the Executables
3. **Target the OS Drive:** Select or type the drive letter where Windows is installed. (In the recovery environment, this is usually `C:` or `D:`).
   ```cmd
   c:
   ```
4. **Navigate to System32:** Change the directory to the core Windows system folder:
   ```cmd
   cd windows\system32
   ```
5. **Backup Utilman:** Rename the original Utility Manager executable so it is not permanently lost:
   ```cmd
   ren Utilman.exe Utilman1.exe
   ```
6. **Replace Utilman with CMD:** Rename the Command Prompt executable to trick the system into launching it from the lock screen:
   ```cmd
   ren cmd.exe Utilman.exe
   ```

### Phase 3: Bypassing and Resetting
7. **Reboot System:** Close the command prompt and select the option to continue booting into Windows normally.
8. **Trigger the Bypass:** Once at the lock screen, click the **Accessibility** icon (typically located in the bottom-right corner). Because of the file swap, a Command Prompt window running with `SYSTEM` privileges will open instead of the accessibility menu.
9. **Reset the Password:** In the elevated Command Prompt, type either of the following commands to open the User Accounts control panel and reset your password:
   ```cmd
   control userpasswords2
   ```
   *or*
   ```cmd
   netplwiz
   ```

---

## Reference Tutorials

For visual demonstrations of this technique, refer to the following resources:

### Quick Walkthrough
* **Forgot Your Windows 11 Password? Reset it EASY!** (YouTube Short)
  * *Description:* A 60-second summary walking through the advanced options, accessing the command prompt, swapping the executable files, and resetting the password from the lock screen.
  * *Link:* [Watch on YouTube](http://www.youtube.com/watch?v=TTN9aTuo8ck)

### Detailed Tutorials
* **Reset Forgotten Windows 11/10 password in 3 minutes**
  * *Description:* A straight-to-the-point demonstration of using the command prompt from the recovery environment to swap the `Utilman.exe` file.
  * *Link:* [Watch on YouTube](http://www.youtube.com/watch?v=ZK5mzXPlEHc)

* **How to Reset Windows 10/11 Password (No USB or Format Needed)**
  * *Description:* Covers the full process of interrupting the boot cycle to reach the Advanced Startup menu, renaming the `cmd.exe`, and utilizing the user account commands to regain access.
  * *Link:* [Watch on YouTube](http://www.youtube.com/watch?v=hX0VquFGM4I)

```cmd
1. Press and hold "Left shift" key then restart the pc/lapi on lock screen.

2. Go to advance option and go to cmd option.

3. "Select drive" where u install windows in my case its C: Type c:  enter.

4. Go to system 32 folder cd windows/system32.

5. ren Utilman.exe Utilman1.exe

6. ren cmd.exe Utilman.exe

7. Boot window, then click on accessibility option on lock screen.

8. Cmd will open then type "control userpasswords2." Or "netplwiz"
```
