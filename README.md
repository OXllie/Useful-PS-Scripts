# Useful-PS-Scripts
Assortment of commands

<details>
  <summary> <b> Hash contents of folder </b> </summary>
  ```powershell
  Get-ChildItem | ForEach-Object {Get-FileHash $_.FullName -Algorithm MD5}
  ```
</details>

<details>
  <summary> <b> Force change desktop wallpaper </b> </summary>
  ```powershell
  H:;
  cd H:\Downloads;
  $file = Read-Host -Prompt "Filename";
  $file = "/" + $file;
  $path = "C:\Users\16crossol\AppData\Roaming\Microsoft\Windows\Themes";
  cp .\$file $path ; rm $path\TranscodedWallpaper -ErrorAction SilentlyContinue;
  rni ($path + $file) $path\TranscodedWallpaper;
  rundll32.exe USER32.DLL,UpdatePerUserSystemParameters 1, True;
  ```
</details>

<details>
  <summary> <b> Powershell Autoclicker </b> </summary>
  ```powershell

  Add-Type -TypeDefinition @'

  using System;
  using System.Runtime.InteropServices;

  public class Clicker{

      [StructLayout(LayoutKind.Sequential)]
      struct INPUT{
          public int type;

          public MOUSEINPUT mi;
      }

      [StructLayout(LayoutKind.Sequential)]
      struct MOUSEINPUT{
         public int dx;
         public int dy;
         public int mouseData;
         public int dwFlags;
         public int time;
         public IntPtr dwExtraInfo; 
      }

      const int MOUSEEVENTF_MOVED      = 0x0001 ;
      const int MOUSEEVENTF_LEFTDOWN   = 0x0002 ;
      const int MOUSEEVENTF_LEFTUP     = 0x0004 ;
      const int MOUSEEVENTF_RIGHTDOWN  = 0x0008 ;
      const int MOUSEEVENTF_RIGHTUP    = 0x0010 ;
      const int MOUSEEVENTF_MIDDLEDOWN = 0x0020 ;
      const int MOUSEEVENTF_MIDDLEUP   = 0x0040 ;
      const int MOUSEEVENTF_WHEEL      = 0x0080 ;
      const int MOUSEEVENTF_XDOWN      = 0x0100 ;
      const int MOUSEEVENTF_XUP        = 0x0200 ;
      const int MOUSEEVENTF_ABSOLUTE   = 0x8000 ;

      [DllImport("User32.dll")]
      extern static uint SendInput(uint nInputs, INPUT[] pInputs, int cbSize);

      public static void Click() {
          INPUT[] input = new INPUT[2];
          input[0].mi.dwFlags = MOUSEEVENTF_LEFTDOWN;
          input[1].mi.dwFlags = MOUSEEVENTF_LEFTUP;
          SendInput(2,input,Marshal.SizeOf(input[0]));
      }
  }


  '@

  while (1 -eq 1) { start-sleep -m 5; [Clicker]::Click() }
  ```
</details>
