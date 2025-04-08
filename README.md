# Caldera_practice
Caldera 是一個由 MITRE 開發的自動化紅隊（Red Team）和藍隊（Blue Team）對抗模擬平台。它主要用來測試、驗證和改善企業或機構的網路防禦能力。Caldera 是開源的，基於 MITRE 的 ATT&CK 框架，模擬真實攻擊者的行為。


利用資訊安全課，累積caldera實戰經驗，以下為幾個使用過的ability

## 1. Pipe Creation - PsExec Tool Execution From Suspicious Locations
### 1.1 Background and Use Cases of the Command
  PsExec 是一款 windows 遠程命令工具，可讓使用者在本地或遠端電腦上執行程式，他不需要在目標機器上安裝 Agent，而是透過 Windows 管理服務來執行命令。PsExec 的特點是能夠遠端系統上用系統權限執行命令。然而正是因為它能在未提示使用者的情況下執行高權限命令，他也被攻擊者濫用。
  	在紅隊演練中和真實攻擊中，PsExec 常被用於

   
  + 橫向移動 : 從一台已被控制的主機向其他主機部署惡意程式

  
  + 權限升級 : 藉由系統權限執行程式已取得更高存取權

  
  + 後門 : 在目標系統上執行後門或安裝其他攻擊工具。
### 1.2 Environment Configuration and Requirements
攻擊端 : 使用wsl執行caldera

目標機器 : VMware建立的windows10

攻擊條件 : 目標機器運行PsExec.exe在指定目錄下(ex:/Temp)，確保端口(135, 139, 445) 開啟

執行command : cd C:\Users\Public\Temp\ ; .\PsExec.exe -i -s cmd /c "echo This machine was hacked. > C:\Users\99053\Desktop\hack.txt"
