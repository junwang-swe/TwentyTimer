# TwentyTimer 專案筆記

## 雙平台同步提醒
本專案同時維護 `mac/`（Swift + SwiftUI）與 `windows/`（C# + WinForms）兩個原生版本，功能刻意保持對等。

- 當使用者要求修改 `mac/` 下的程式碼時，修改完成後主動詢問：「windows 版要不要一起加上這個改動？」
- 當使用者要求修改 `windows/` 下的程式碼時，修改完成後主動詢問：「mac 版要不要一起加上這個改動？」
- 只在對方平台**確實存在對應功能/畫面**、且改動有意義移植時才問；純平台特定的實作細節（例如 WinForms 的 `WS_EX_NOACTIVATE` vs. SwiftUI 的視窗行為）不必問。
- 使用者說不用同步時，這次就不用再追問。

## 建置
- Windows 版改完程式碼後，記得重新 `dotnet build`，否則 `windows/build/TwentyTimer.exe` 會是舊版，執行起來看不到新功能。

## 待辦
- **重新打包 Windows 版**：`windows/build/TwentyTimer.exe` 目前是舊版，不含「閒置多久重設計時」（`IdleResetMinutes`）與勿擾「60 分＋自訂分鐘」。這些改動（commit `47890fd`）只在 macOS 上用 `dotnet build -p:EnableWindowsTargeting=true` 確認過編譯，沒在 Windows 上實測。
  - 需要在 Windows 機器上執行 `windows/build.ps1` 重新打包，並實測：設定頁的新 Stepper、系統匣面板的自訂勿擾輸入框與 ✓ 按鈕。
  - 若目前不是在 Windows 環境，不要假裝已驗證；完成後把這一條刪掉。
