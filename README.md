# EGFR_Hunter-Automated-Virtual-Screening-Engine-for-C797S-Mutants:
EGFR_Hunter 是一套專為對抗 EGFR C797S 耐藥突變設計的開源 CADD/AIDD 自動化流水線
# Key Features:
/AI-Powered Fast Screening: 整合 2054 維 ECFP4 特徵工程與 XGBoost QSAR 模型，數秒內預測活性標度 (pIC50)。  

/Physics-Based 3D Validation: 自動調用 OpenBabel & AutoDock Vina，針對 C797S 晶體口袋 (6LUD) 進行結合能預測 (Delta G)。 

/Zero-Setup & Robust: 內建自癒式依賴套件安裝與結構 Sanitize 機制，完全不懼環境重置。 

/In-Browser 3D Viewer: 整合 py3Dmol，免安裝桌面版 PyMOL 即可查看分子打靶姿勢。  

# [目前基礎：v1.0 乾實驗引擎]
       │
       ├─── 1. 動態物理模擬 (MD & MM/PBSA) ───> 補足靜態對接的假陽性
       ├─── 2. 生成式 AI (De Novo Design) ───> 擺脫已知分子庫限制
       ├─── 3. 藥物成藥性 (ADMET & SA Score) ─> 避免設計出「無法合成/毒性爆表」的分子
       ├─── 4. 專利查重 (Patent Novelty) ────> 確保智慧財產權 (IP) 完全原創
       └─── 5. 濕實驗轉譯語文 (In Vitro) ─────> 建立與生化/細胞實驗室對接的 Protocol
